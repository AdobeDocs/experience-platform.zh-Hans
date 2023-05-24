---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；體驗資料模型；體驗資料模型；資料模型；資料模型；結構描述登入；結構描述登入；行為；行為；
solution: Experience Platform
title: 行為API端點
description: Schema Registry API中的/behaviors端點可讓您擷取全域容器中的所有可用行為。
exl-id: 3b45431f-1d55-4279-8b62-9b27863885ec
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 2%

---

# 行為端點

在Experience Data Model (XDM)中，行為會定義結構描述之資料的性質。 每個XDM類別都必須參考特定行為，而使用該類別的所有結構描述都會繼承該行為。 在Platform的幾乎所有使用案例中，有兩個可用的行為：

* **[!UICONTROL 記錄]**：提供主旨屬性的相關資訊。 主體可以是組織或個人。
* **[!UICONTROL 時間序列]**：提供記錄主體直接或間接執行動作時的系統快照。

>[!NOTE]
>
>Platform中有些使用案例需要使用未採用上述任一行為的結構描述。 對於這些情況，可以使用第三個「臨機」行為。 請參閱教學課程，位置如下： [建立臨時結構描述](../tutorials/ad-hoc.md) 以取得詳細資訊。
>
>如需資料行為如何影響結構描述構成的詳細一般資訊，請參閱 [結構描述組合基本概念](../schema/composition.md).

此 `/behaviors` 中的端點 [!DNL Schema Registry] API可讓您檢視以下專案中的可用行為： `global` 容器。

## 快速入门

本指南中使用的端點是 [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml). 在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的閱讀指南，以及有關成功呼叫任何Experience PlatformAPI所需必要標題的重要資訊。

## 擷取行為清單 {#list}

您可以透過向以下專案發出GET請求，擷取所有可用行為的清單： `/behaviors` 端點。

**API格式**

```http
GET /global/behaviors
```

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

**响应**

```json
{
    "results": [
        {
            "$id": "https://ns.adobe.com/xdm/data/record",
            "meta:altId": "_xdm.data.record",
            "version": "1.16.4",
            "title": "Record Schema"
        },
        {
            "$id": "https://ns.adobe.com/xdm/data/adhoc",
            "meta:altId": "_xdm.data.adhoc",
            "version": "1.16.4",
            "title": "Ad Hoc Schema"
        },
        {
            "$id": "https://ns.adobe.com/xdm/data/time-series",
            "meta:altId": "_xdm.data.time-series",
            "version": "1.16.4",
            "title": "Time-series Schema"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 3
    },
    "_links": {
        "next": null
    }
}
```

## 查詢行為 {#lookup}

您可以在GET請求的路徑中提供特定行為的ID，以查詢特定行為。 `/behaviors` 端點。

**API格式**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{BEHAVIOR_ID}` | 此 `meta:altId` 或URL編碼 `$id` 您想查詢之行為的詳細資訊。 |

{style="table-layout:auto"}

**请求**

以下請求會提供下列內容，以擷取記錄行為的詳細資料： `meta:altId` 在請求路徑中。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors/_xdm.data.record \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json;version=1'
```

**响应**

成功的回應會傳回行為的詳細資訊，包括其版本、說明，以及行為提供給使用它的類別的屬性。

```json
{
    "$id": "https://ns.adobe.com/xdm/data/record",
    "meta:altId": "_xdm.data.record",
    "meta:resourceType": "behaviors",
    "version": "1.16.4",
    "title": "Record Schema",
    "type": "object",
    "description": "Used to indicate the behavior of record data semantic when composed into data schemas.",
    "definitions": {
        "record": {
            "properties": {
                "_id": {
                    "title": "Identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "A unique identifier for the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "@id"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/record",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:xdmType": "object",
    "meta:status": "stable",
    "$schema": "http://json-schema.org/draft-06/schema#",
    "meta:registryMetadata": {
        "repo:createdDate": 1606266789446,
        "repo:lastModifiedDate": 1606266789446,
        "eTag": "2cc114a54949a9668fe2ad046ccece59192e1bfa28f14e5ac7c893acb7820ba2",
        "meta:globalLibVersion": "1.16.4"
    }
}
```

## 后续步骤

本指南涵蓋 `/behaviors` 中的端點 [!DNL Schema Registry] API。 若要瞭解如何使用API將行為指派給類別，請參閱 [類別端點指南](./classes.md).
