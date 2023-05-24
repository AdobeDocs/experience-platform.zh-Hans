---
title: 使用結構描述登入API新增特定欄位到結構描述
description: 瞭解如何使用結構描述登入API，將現有欄位群組中的個別欄位新增到體驗資料模型(XDM)結構描述。
exl-id: 696cce2b-bbde-416a-9f52-12ab4da9c2c6
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 2%

---

# 使用結構描述登入API將特定欄位新增到結構描述

Experience Data Model (XDM)結構描述由基底類別組成，並使用由Adobe定義的標準欄位群組和您的組織定義的自訂欄位群組來包含其他欄位。

在建置結構描述時，您可能要使用指定欄位群組中的某些欄位，同時排除相同群組中您不需要的其他欄位。 本教學課程說明如何使用Schema Registry API將欄位群組中的個別欄位新增到結構描述。

>[!NOTE]
>
>如需如何在Adobe Experience Platform UI中新增和移除個別結構描述欄位的詳細資訊，請參閱以下指南： [欄位式工作流程](../ui/field-based-workflows.md) （目前為測試版）。

## 先决条件

本教學課程涉及對 [結構描述登入API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). 開始之前，請檢閱 [開發人員指南](../api/getting-started.md) 如需成功呼叫API所需的重要資訊，包括 `{TENANT_ID}`、容器的概念，以及發出請求所需的標頭。

## 瞭解 `meta:refProperty` 欄位

對於任何指定的結構描述，組成其結構的類別和欄位群組會在下列專案底下參考： `allOf` 陣列。 每個元件都表示為一個物件，其中包含一個 `$ref` 參考元件URI的屬性 `$id`.

以下JSON代表使用單一類別(`experienceevent`)和欄位群組(`experienceevent-all`)：

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all"
    }
  ]
}
```

對於中的任何物件 `allOf` 參照欄位群組的陣列，您可以新增同層級 `meta:refProperty` 欄位，指定群組中的哪些欄位應包含在結構描述中。

>[!NOTE]
>
>每個欄位都使用JSON指標字串指定，該字串代表其各自欄位群組中的欄位路徑。 字串必須以前導斜線(`/`)且不應包含任何 `properties` 名稱空間。 例如：`/_experience/campaign/message/id`。

當以字串形式包含時， `meta:refProperty` 可參照群組中的單一欄位。 來自相同群組的其他欄位可使用相同來包含 `$ref` 另一個物件中具有不同值的值 `meta:refProperty` 值。

```json
{
  "title": "My Sample Schema",
  "description": "An example schema that uses the XDM ExperienceEvent class.",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": "/_experience/campaign/message/id"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": "/_experience/campaign/message/size"
    }
  ]
}
```

或者， `meta:refProperty` 可作為陣列提供，讓您指定在單一群組中要包含來自指定群組的多個欄位 `allOf` 清單專案：

```json
{
  "title": "My Sample Schema",
  "description": "An example schema that uses the XDM ExperienceEvent class.",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ]
}
```

## 使用PUT操作新增欄位

您可以使用PUT請求來重寫整個結構描述，並設定您要包含的欄位 `allOf`.

**API格式**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 此 `meta:altId` 或URL編碼 `$id` 要重寫的結構描述中。 |

**请求**

以下請求會更新底下欄位群組包含的特定欄位 `allOf` 陣列。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "title": "My Sample Schema",
        "description": "My Sample Description",
        "type": "object",
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
          },
          {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
            "meta:refProperty": [
              "/_experience/campaign/message/id",
              "/_experience/campaign/message/size",
              "/_experience/campaign/message/variant"
            ]
          }
        ]
      }'
```

**响应**

成功的回應會傳回更新後之結構的詳細資訊。

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ],
  "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
  "meta:abstract": false,
  "meta:extensible": false,
  "meta:extends": [
      "https://ns.adobe.com/xdm/context/experienceevent",
      "https://ns.adobe.com/xdm/data/time-series"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
  "version": "1.0",
  "meta:resourceType": "schemas",
  "meta:registryMetadata": {
      "repo:createDate": 1552088461236,
      "repo:lastModifiedDate": 1552088470592,
      "xdm:createdClientId": "{CREATED_CLIENT}",
      "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

>[!NOTE]
>
>如需結構描述之PUT請求的詳細資訊，請參閱 [結構描述端點指南](../api/schemas.md#put).

## 使用PATCH操作新增欄位

您可以使用PATCH請求將個別欄位新增到結構描述而不覆寫其他欄位。 Schema Registry支援所有標準JSON修補程式操作，包括 `add`， `remove`、和 `replace`. 如需JSON修補程式的詳細資訊，請參閱 [API基礎指南](../../landing/api-fundamentals.md#json-patch).

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 此 `meta:altId` 或URL編碼 `$id` 要重寫的結構描述中。 |

**请求**

以下請求會將新物件新增至結構描述的 `allOf` 陣列，指定要新增的欄位。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
            "meta:refProperty": [
              "/_experience/campaign/message/id",
              "/_experience/campaign/message/size",
              "/_experience/campaign/message/variant"
            ]
          }
        }
      ]'
```

**响应**

成功的回應會傳回更新後之結構的詳細資訊。

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ],
  "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
  "meta:abstract": false,
  "meta:extensible": false,
  "meta:extends": [
      "https://ns.adobe.com/xdm/context/experienceevent",
      "https://ns.adobe.com/xdm/data/time-series"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
  "version": "1.0",
  "meta:resourceType": "schemas",
  "meta:registryMetadata": {
      "repo:createDate": 1552088461236,
      "repo:lastModifiedDate": 1552088470592,
      "xdm:createdClientId": "{CREATED_CLIENT}",
      "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

>[!NOTE]
>
>如需結構描述之PATCH請求的詳細資訊，請參閱 [結構描述端點指南](../api/schemas.md#patch).

## 后续步骤

本指南說明如何使用API呼叫，將現有欄位群組中的個別欄位新增至結構描述。 如需如何在Platform UI中執行類似的欄位式工作的詳細資訊，請參閱以下指南： [欄位式工作流程](../ui/field-based-workflows.md).

如需Schema Registry API功能的詳細資訊，請參閱 [API概觀](../api/overview.md) 以取得完整的端點與程式清單。
