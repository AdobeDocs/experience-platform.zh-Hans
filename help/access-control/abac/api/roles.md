---
keywords: Experience Platform；首頁；熱門主題；API；屬性型存取控制；屬性型存取控制
solution: Experience Platform
title: 角色API端點
description: 屬性式存取控制API中的/roles端點可讓您以程式設計方式管理Adobe Experience Platform中的角色。
exl-id: 049f7a18-7d06-437b-8ce9-25d7090ba782
source-git-commit: 16d85a2a4ee8967fc701a3fe631c9daaba9c9d70
workflow-type: tm+mt
source-wordcount: '1606'
ht-degree: 5%

---

# 角色端點

>[!NOTE]
>
>如果傳遞的是使用者權杖，則權杖的使用者必須具有請求組織的「組織管理員」角色。

角色定義管理員、專家或一般使用者對貴組織資源的存取權。 在基於角色的存取控制環境中，使用者存取布建是透過共同責任和需求進行分組。 一个角色具有一组给定的权限，可将您组织的成员分配给一个或多个角色，具体取决于他们需要的查看或写入访问权限的范围。

此 `/roles` 屬性型存取控制API中的端點可讓您以程式設計方式管理組織中的角色。

## 快速入门

本指南中使用的API端點是以屬性為基礎的存取控制API的一部分。 在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的閱讀指南，以及有關成功呼叫任何Experience PlatformAPI所需必要標題的重要資訊。

## 擷取角色清單 {#list}

您可以透過向以下人員發出GET請求，列出屬於您組織的所有現有角色： `/roles` 端點。

**API格式**

```http
GET /roles/
```

**请求**

下列請求會擷取屬於您組織的角色清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的回應會傳回組織中的角色清單，包括有關其各自角色型別、許可權集和主體屬性的資訊。

```json
{
  "roles": [
    {
      "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "name": "Administrator Role",
      "description": "Role for administrator type of responsibilities and access",
      "roleType": "user-defined",
      "permissionSets": [
        "manage-datasets",
        "manage-schemas"
      ],
      "sandboxes": [
        "prod"
      ],
      "subjectAttributes": {
        "labels": [
          "core/S1"
        ]
      },
      "createdBy": "{CREATED_BY}",
      "createdAt": 1648153201825,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1648153201825,
      "etag": null
    }
  ],
  "_page": {
    "limit": 1,
    "count": 1
  },
  "_links": {
    "next": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    },
    "page": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    },
    "subjects": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    }
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 與角色相對應的ID。 此ID會自動產生。 |
| `name` | 您的角色名稱。 |
| `description` | description屬性提供有關您角色的其他資訊。 |
| `roleType` | 角色的指定型別。 角色型別的可能值包括： `user-defined` 和 `system-defined`. |
| `permissionSets` | 許可權集代表管理員可套用至角色的一組許可權。 管理員可以將許可權集指派給角色，而不是指派個別許可權。 這可讓您從包含一組許可權的預定義角色建立自訂角色。 |
| `sandboxes` | 此屬性會顯示貴組織內為特定角色布建的沙箱。 |
| `subjectAttributes` | 指出主體與其有權存取的Platform資源之間關聯的屬性。 |
| `subjectAttributes.labels` | 顯示套用至查詢角色的資料使用標籤。 |

## 查詢角色 {#lookup}

您可以透過提出包含對應角色的GET請求來查詢個別角色 `roleId` 在請求路徑中。

**API格式**

```http
GET /roles/{ROLE_ID}
```

| 参数 | 描述 |
| --- | --- |
| {ROLE_ID} | 您要查閱的角色的ID。 |

**请求**

以下請求會擷取以下專案的資訊： `{ROLE_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的回應會傳回查詢角色ID的詳細資料，包括其角色型別、許可權集和主體屬性的資訊。

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role for administrator type of responsibilities and access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 與角色相對應的ID。 此ID會自動產生。 |
| `name` | 您的角色名稱。 |
| `description` | description屬性提供有關您角色的其他資訊。 |
| `roleType` | 角色的指定型別。 角色型別的可能值包括： `user-defined` 和 `system-defined`. |
| `permissionSets` | 許可權集代表管理員可套用至角色的一組許可權。 管理員可以將許可權集指派給角色，而不是指派個別許可權。 這可讓您從包含一組許可權的預定義角色建立自訂角色。 |
| `sandboxes` | 此屬性會顯示貴組織內為特定角色布建的沙箱。 |
| `subjectAttributes` | 指出主體與其有權存取的Platform資源之間關聯的屬性。 |
| `subjectAttributes.labels` | 顯示套用至查詢角色的資料使用標籤。 |

## 依角色ID查詢主題

您也可以向以下網址發出GET要求，以擷取主題： `/roles` 提供{ROLE_ID}時的端點。

**API格式**

```http
GET /roles/{ROLE_ID}/subjects
```

| 参数 | 描述 |
| --- | --- |
| {ROLE_ID} | 與您要查閱的主體相關聯的角色識別碼。 |

**请求**

以下請求會擷取與關聯的主題 `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809/subjects \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功回應會傳回與查詢的角色ID相關聯的主題，包括對應的主題ID和主題型別。

```json
{
  "items": [
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "03Z07HFQCCUF3TUHAX274206@AdobeID"
      },
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "PIRJ7WE5T3QT9Z4TCLVH86DE@AdobeID"
      },
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "WHPWE00MC26SHZ7AKBFG403D@AdobeID"
      },
  ]
  "_page": {
    "limit": 0,
    "count": 0
  },
  "_links": {
      "self": {
          "href": "/roles/{ROLE_ID}/subjects",
          "templated": false,
          "type": null,
          "method": null
      },
      "page": {
          "href": "/roles/{ROLE_ID}/subjects?limit={limit}&start={start}&orderBy={orderBy}&property={property}",
          "templated": true,
          "type": null,
          "method": null
      }
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `roleId` | 與查詢主體相關聯的角色ID。 |
| `subjectType` | 查詢的主旨型別。 |
| `subjectId` | 與查詢的主體相對應的ID。 |

## 建立角色 {#create}

POST若要建立新角色，請向 `/roles` 端點，同時提供角色名稱、說明和角色型別的值。

**API格式**

```http
POST /roles/
```

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "name": "Administrator Role",
    "description": "Role for administrator type of responsibilities and access",
    "roleType": "user-defined"
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 您的角色名稱。 確保您的角色名稱是描述性的，因為您可以使用此名稱來查閱有關您角色的資訊。 |
| `description` | （選擇性）您可以納入的描述性值，以提供角色的相關詳細資訊。 |
| `roleType` | 角色的指定型別。 角色型別的可能值包括： `user-defined` 和 `system-defined`. |

**响应**

成功的回應會傳回您新建立的角色，以及其對應的角色ID，以及其角色型別、許可權集和主體屬性的資訊。

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role for administrator type of responsibilities and access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 與角色相對應的ID。 此ID會自動產生。 |
| `name` | 您的角色名稱。 |
| `description` | description屬性提供有關您角色的其他資訊。 |
| `roleType` | 角色的指定型別。 角色型別的可能值包括： `user-defined` 和 `system-defined`. |
| `permissionSets` | 許可權集代表管理員可套用至角色的一組許可權。 管理員可以將許可權集指派給角色，而不是指派個別許可權。 這可讓您從包含一組許可權的預定義角色建立自訂角色。 |
| `sandboxes` | 此屬性會顯示貴組織內為特定角色布建的沙箱。 |
| `subjectAttributes` | 指出主體與其有權存取的Platform資源之間關聯的屬性。 |
| `subjectAttributes.labels` | 顯示套用至查詢角色的資料使用標籤。 |

## 更新角色 {#patch}

您可以透過向以下專案發出PATCH請求來更新角色的屬性： `/roles` 端點，並為您要套用的作業提供對應的角色ID和值。

**API格式**

```http
PATCH /roles/{ROLE_ID}
```

| 参数 | 描述 |
| --- | --- |
| {ROLE_ID} | 您要更新的角色ID。 |

**请求**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "add",
        "path": "/description",
        "value": "Role with permission sets for admin type of access"
      }
    ]
  }'
```

| 操作 | 描述 |
| --- | --- |
| `op` | 用於定義更新角色所需動作的操作呼叫。 作業包括： `add`， `replace`、和 `remove`. |
| `path` | 要更新的引數路徑。 |
| `value` | 您想要用來更新引數的新值。 |

**响应**

成功的回應會傳回更新的角色，包括您選擇更新的屬性的新值。

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role with permission sets for admin type of access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 與角色相對應的ID。 此ID會自動產生。 |
| `name` | 您的角色名稱。 |
| `description` | description屬性提供有關您角色的其他資訊。 |
| `roleType` | 角色的指定型別。 角色型別的可能值包括： `user-defined` 和 `system-defined`. |
| `permissionSets` | 許可權集代表管理員可套用至角色的一組許可權。 管理員可以將許可權集指派給角色，而不是指派個別許可權。 這可讓您從包含一組許可權的預定義角色建立自訂角色。 |
| `sandboxes` | 此屬性會顯示貴組織內為特定角色布建的沙箱。 |
| `subjectAttributes` | 指出主體與其有權存取的Platform資源之間關聯的屬性。 |
| `subjectAttributes.labels` | 顯示套用至查詢角色的資料使用標籤。 |

## 依角色ID更新角色 {#put}

您可以透過向以下專案發出PUT請求來更新角色： `/roles` 端點，並指定與您要更新的角色對應的角色ID。

**API格式**

```http
PUT /roles/{ROLE_ID}
```

**请求**

以下請求會更新角色ID的名稱、說明和角色型別： `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "name": "Administrator role for ACME",
    "description": "New administrator role for ACME",
    "roleType": "user-defined"
  }'
```

| 参数 | 描述 |
| --- | --- |
| `name` | 角色的更新名稱。 |
| `description` | 角色的更新說明。 |
| `roleType` | 角色的指定型別。 角色型別的可能值包括： `user-defined` 和 `system-defined`. |

**响应**

成功會傳回您更新的角色，包括其名稱、說明和角色型別的新值。

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role with permission sets for admin type of access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 與角色相對應的ID。 此ID會自動產生。 |
| `name` | 您的角色名稱。 |
| `description` | description屬性提供有關您角色的其他資訊。 |
| `roleType` | 角色的指定型別。 角色型別的可能值包括： `user-defined` 和 `system-defined`. |
| `permissionSets` | 許可權集代表管理員可套用至角色的一組許可權。 管理員可以將許可權集指派給角色，而不是指派個別許可權。 這可讓您從包含一組許可權的預定義角色建立自訂角色。 |
| `sandboxes` | 此屬性會顯示貴組織內為特定角色布建的沙箱。 |
| `subjectAttributes` | 指出主體與其有權存取的Platform資源之間關聯的屬性。 |
| `subjectAttributes.labels` | 顯示套用至查詢角色的資料使用標籤。 |

## 依角色ID更新主旨

PATCH若要更新與角色相關聯的主體，請向 `/roles` 端點，並提供您要更新之主體的角色ID。

**API格式**

```http
PATCH /roles/{ROLE_ID}
```

| 参数 | 描述 |
| --- | --- |
| {ROLE_ID} | 與您要更新之主體相關聯的角色ID。 |

**请求**

以下請求會更新與關聯的主題 `{ROLE_ID}`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "add",
        "path": "/subjects",
        "value": "New subjects"
      }
    ]
  }'
```

| 操作 | 描述 |
| --- | --- |
| `op` | 用於定義更新角色所需動作的操作呼叫。 作業包括： `add`， `replace`、和 `remove`. |
| `path` | 要更新的引數路徑。 |
| `value` | 您想要用來更新引數的新值。 |

**响应**

成功回應會傳回與查詢的角色ID相關聯的更新主題。

```json
{
  "subjects": [
    {
      "subjectId": "string",
      "subjectType": "user"
    }
  ],
  "_page": {
    "limit": 0,
    "count": 0
  },
  "_links": {
    "next": {
      "href": "string",
      "templated": true
    },
    "page": {
      "href": "string",
      "templated": true
    }
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `subjectId` | 主旨的ID。 |
| `subjectType` | 主旨的型別。 |

## 刪除角色 {#delete}

若要刪除角色，請向以下專案發出DELETE請求： `/roles` 端點，同時指定您要刪除的角色的ID。

**API格式**

```http
DELETE /roles/{ROLE_ID}
```

| 参数 | 描述 |
| --- | --- |
| {ROLE_ID} | 您要刪除的角色的ID。 |

**请求**

以下請求會刪除ID為的角色 `{ROLE_ID}`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的回應會傳回HTTP狀態204 （無內容）和空白內文。

您可以嘗試向角色查詢(GET)請求以確認刪除。 您會收到HTTP狀態404 （找不到），因為角色已從管理中移除。
