---
keywords: Experience Platform；首頁；熱門主題；API；屬性型存取控制；屬性型存取控制
solution: Experience Platform
title: 存取控制原則API端點
description: 屬性式存取控制API中的/policies端點可讓您以程式設計方式管理Adobe Experience Platform中的原則。
exl-id: 07690f43-fdd9-4254-9324-84e6bd226743
source-git-commit: 16d85a2a4ee8967fc701a3fe631c9daaba9c9d70
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 2%

---

# 存取控制原則端點

>[!NOTE]
>
>如果傳遞的是使用者權杖，則權杖的使用者必須具有請求組織的「組織管理員」角色。

存取控制原則是將屬性集合在一起以建立允許和不允許動作的宣告。 這些原則可以是本機或全域，並且可以覆寫其他原則。 此 `/policies` 屬性型存取控制API中的端點可讓您以程式設計方式管理原則，包括管理原則的規則相關資訊及其各自的主題條件。

>[!IMPORTANT]
>
>此端點不可與 `/policies` 中的端點 [原則服務API](../../../data-governance/api/policies.md)，用來管理資料使用原則。

## 快速入门

本指南中使用的API端點是以屬性為基礎的存取控制API的一部分。 在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的閱讀指南，以及有關成功呼叫任何Experience PlatformAPI所需必要標題的重要資訊。

## 擷取原則清單 {#list}

向發出GET要求 `/policies` 端點可列出組織中的所有現有原則。

**API格式**

```http
GET /policies
```

**请求**

以下請求會擷取現有原則的清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的回應會傳回現有原則的清單。

```json
{
  {
      "id": "7019068e-a3a0-48ce-b56b-008109470592",
      "imsOrgId": "{IMS_ORG}",
      "createdBy": "{CREATED_BY}",
      "createdAt": 1652892767559,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1652895736367,
      "name": "schema-field",
      "description": "schema-field",
      "status": "inactive",
      "subjectCondition": null,
      "rules": [
          {
              "effect": "Deny",
              "resource": "/orgs/{IMS_ORG}/sandboxes/xql/schemas/*/schema-fields/*",
              "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
              "actions": [
                  "com.adobe.action.read",
                  "com.adobe.action.write",
                  "com.adobe.action.view"
              ]
          },
          {
              "effect": "Permit",
              "resource": "/orgs/{IMS_ORG}/sandboxes/*/schemas/*/schema-fields/*",
              "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
              "actions": [
                  "com.adobe.action.delete"
              ]
          },
          {
              "effect": "Deny",
              "resource": "/orgs/{IMS_ORG}/sandboxes/delete-sandbox-adfengine-test-8/segments/*",
              "condition": "{\"!\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}",
              "actions": [
                  "com.adobe.action.write"
              ]
          }
      ],
      "_etag": "\"0300593f-0000-0200-0000-62852ff80000\""
  },
  {
      "id": "13138ef6-c007-495d-837f-0a248867e219",
      "imsOrgId": "{IMS_ORG}",
      "createdBy": "{CREATED_BY}",
      "createdAt": 1652859368555,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1652890780206,
      "name": "Documentation-Copy",
      "description": "xyz",
      "status": "active",
      "subjectCondition": null,
      "rules": [
          {
              "effect": "Permit",
              "resource": "orgs/{IMS_ORG}/sandboxes/ro-sand/schemas/*/schema-fields/*",
              "condition": "{\"!\":[{\"or\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"and\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}]}]}",
              "actions": [
                  "com.adobe.action.read"
              ]
          },
          {
              "effect": "Deny",
              "resource": "orgs/{IMS_ORG}/sandboxes/*/segments/*",
              "condition": "{\"!\":[{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}]}",
              "actions": [
                  "com.adobe.action.read"
              ]
          }
      ],
      "_etag": "\"0300d43c-0000-0200-0000-62851c9c0000\""
  },
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 與原則相對應的ID。 此識別碼是自動產生的，可用於查詢、更新和刪除原則。 |
| `imsOrgId` | 可存取查詢之原則的組織。 |
| `createdBy` | 建立原則的使用者ID。 |
| `createdAt` | 建立原則的時間。 此 `createdAt` 屬性會顯示在unix epoch時間戳記中。 |
| `modifiedBy` | 上次更新原則的使用者ID。 |
| `modifiedAt` | 上次更新原則的時間。 此 `modifiedAt` 屬性會顯示在unix epoch時間戳記中。 |
| `name` | 原則的名稱。 |
| `description` | （選用）可新增的屬性，以提供特定原則的進一步資訊。 |
| `status` | 原則的目前狀態。 此屬性定義原則目前是否為 `active` 或 `inactive`. |
| `subjectCondition` | 套用至主旨的條件。 主體是具有特定屬性的使用者，會請求存取資源以執行動作。 在這種情況下， `subjectCondition` 是套用至主旨屬性的類似查詢條件。 |
| `rules` | 定義原則的規則集。 規則定義哪些屬性組合已獲授權，主體才能成功對資源執行動作。 |
| `rules.effect` | 考量以下專案的值後所產生的影響： `action`， `condition` 和 `resource`. 可能的值包括： `permit`， `deny`，或 `indeterminate`. |
| `rules.resource` | 主體可以或無法存取的資產或物件。  資源可以是檔案、應用程式、伺服器，甚至API。 |
| `rules.condition` | 套用至資源的條件。 例如，如果資源是結構描述，則結構描述可以套用某些標籤，這有助於決定針對該結構描述的操作是允許還是不允許的。 |
| `rules.action` | 允許主體對查詢的資源執行的動作。 可能的值包括： `read`， `create`， `edit`、和 `delete`. |

## 依ID查詢原則詳細資料 {#lookup}

向發出GET要求 `/policies` 端點時，在請求路徑中提供原則ID以擷取有關該個別原則的資訊。

**API格式**

```http
GET /policies/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| {POLICY_ID} | 您要擷取之原則的ID。 |

**请求**

下列要求會擷取個別原則的相關資訊。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/13138ef6-c007-495d-837f-0a248867e219 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的要求會傳回有關查詢的原則ID的資訊。

```json
{
    "id": "13138ef6-c007-495d-837f-0a248867e219",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652859368555,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652890780206,
    "name": "Documentation-Copy",
    "description": "xyz",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "orgs/{IMS_ORG}/sandboxes/ro-sand/schemas/*/schema-fields/*",
            "condition": "{\"!\":[{\"or\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"and\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        },
        {
            "effect": "Deny",
            "resource": "orgs/{IMS_ORG}/sandboxes/*/segments/*",
            "condition": "{\"!\":[{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        }
    ],
    "_etag": "\"0300d43c-0000-0200-0000-62851c9c0000\""
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 與原則相對應的ID。 此識別碼是自動產生的，可用於查詢、更新和刪除原則。 |
| `imsOrgId` | 可存取查詢之原則的組織。 |
| `createdBy` | 建立原則的使用者ID。 |
| `createdAt` | 建立原則的時間。 此 `createdAt` 屬性會顯示在unix epoch時間戳記中。 |
| `modifiedBy` | 上次更新原則的使用者ID。 |
| `modifiedAt` | 上次更新原則的時間。 此 `modifiedAt` 屬性會顯示在unix epoch時間戳記中。 |
| `name` | 原則的名稱。 |
| `description` | （選用）可新增的屬性，以提供特定原則的進一步資訊。 |
| `status` | 原則的目前狀態。 此屬性定義原則目前是否為 `active` 或 `inactive`. |
| `subjectCondition` | 套用至主旨的條件。 主體是具有特定屬性的使用者，會請求存取資源以執行動作。 在這種情況下， `subjectCondition` 是套用至主旨屬性的類似查詢條件。 |
| `rules` | 定義原則的規則集。 規則定義哪些屬性組合已獲授權，主體才能成功對資源執行動作。 |
| `rules.effect` | 考量以下專案的值後所產生的影響： `action`， `condition` 和 `resource`. 可能的值包括： `permit`， `deny`，或 `indeterminate`. |
| `rules.resource` | 主體可以或無法存取的資產或物件。  資源可以是檔案、應用程式、伺服器，甚至API。 |
| `rules.condition` | 套用至資源的條件。 例如，如果資源是結構描述，則結構描述可以套用某些標籤，這有助於決定針對該結構描述的操作是允許還是不允許的。 |
| `rules.action` | 允許主體對查詢的資源執行的動作。 可能的值包括： `read`， `create`， `edit`、和 `delete`. |


## 创建策略 {#create}

POST若要建立新原則，請向 `/policies` 端點。

**API格式**

```http
POST /policies
```

**请求**

下列要求會建立名為的新原則： `acme-integration-policy`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
      "name": "acme-integration-policy",
      "description": "Policy for ACME",
      "imsOrgId": "{IMS_ORG}",
      "rules": [
        {
          "effect": "Permit",
          "resource": "/orgs/{IMS_ORG}/sandboxes/*",
          "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
          "actions": [
            "read"
          ]
        }
      ]
    }'
```

| 参数 | 描述 |
| --- | --- |
| `name` | 原則的名稱。 |
| `description` | （選用）可新增的屬性，以提供特定原則的進一步資訊。 |
| `imsOrgId` | 包含原則的組織。 |
| `rules` | 定義原則的規則集。 規則定義哪些屬性組合已獲授權，主體才能成功對資源執行動作。 |
| `rules.effect` | 考量以下專案的值後所產生的影響： `action`， `condition` 和 `resource`. 可能的值包括： `permit`， `deny`，或 `indeterminate`. |
| `rules.resource` | 主體可以或無法存取的資產或物件。  資源可以是檔案、應用程式、伺服器，甚至API。 |
| `rules.condition` | 套用至資源的條件。 例如，如果資源是結構描述，則結構描述可以套用某些標籤，這有助於決定針對該結構描述的操作是允許還是不允許的。 |
| `rules.action` | 允許主體對查詢的資源執行的動作。 可能的值包括： `read`， `create`， `edit`、和 `delete`. |

**响应**

成功的請求會傳回新建立的原則，包括其唯一的原則ID和相關聯的規則。

```json
{
    "id": "c3863937-5d40-448d-a7be-416e538f955e",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652988384458,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652988384458,
    "name": "acme-integration-policy",
    "description": "Policy for ACME",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "read"
            ]
        }
    ],
    "_etag": null
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 與原則相對應的ID。 此識別碼是自動產生的，可用於查詢、更新和刪除原則。 |
| `name` | 原則的名稱。 |
| `rules` | 定義原則的規則集。 規則定義哪些屬性組合已獲授權，主體才能成功對資源執行動作。 |
| `rules.effect` | 考量以下專案的值後所產生的影響： `action`， `condition` 和 `resource`. 可能的值包括： `permit`， `deny`，或 `indeterminate`. |
| `rules.resource` | 主體可以或無法存取的資產或物件。  資源可以是檔案、應用程式、伺服器，甚至API。 |
| `rules.condition` | 套用至資源的條件。 例如，如果資源是結構描述，則結構描述可以套用某些標籤，這有助於決定針對該結構描述的操作是允許還是不允許的。 |
| `rules.action` | 允許主體對查詢的資源執行的動作。 可能的值包括： `read`， `create`， `edit`、和 `delete`. |


## 依原則ID更新原則 {#put}

PUT若要更新個別原則的規則，請向 `/policies` 端點，同時在請求路徑中提供您要更新之原則的ID。

**API格式**

```http
PUT /policies/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| {POLICY_ID} | 您要更新的原則ID。 |

**请求**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/8cf487d7-3642-4243-a8ea-213d72f694b9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
      "id": "8cf487d7-3642-4243-a8ea-213d72f694b9",
      "imsOrgId": "{IMS_ORG}",
      "name": "test-2",
      "rules": [
      {
        "effect": "Deny",
        "resource": "/orgs/{IMS_ORG}/sandboxes/*",
        "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
        "actions": [
          "read"
        ]
      }
    ]
  }'
```

**响应**

成功的回應會傳回更新的原則。

```json
{
    "id": "8cf487d7-3642-4243-a8ea-213d72f694b9",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652988866647,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652989297287,
    "name": "test-2",
    "description": null,
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Deny",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "read"
            ]
        }
    ],
    "_etag": null
}
```

## 更新原則屬性 {#patch}

若要更新個別原則的屬性，請向以下發出PATCH請求： `/policies` 端點，同時在請求路徑中提供您要更新之原則的ID。

**API格式**

```http
PATCH /policies/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| {POLICY_ID} | 您要更新的原則ID。 |

**请求**

以下請求會取代 `/description` 在原則ID中 `c3863937-5d40-448d-a7be-416e538f955e`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "replace",
        "path": "/description",
        "value": "Pre-set policy to be applied for ACME"
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

成功回應會傳回查詢的原則識別碼和更新的說明。

```json
{
    "id": "c3863937-5d40-448d-a7be-416e538f955e",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "acp_accessControlService",
    "createdAt": 1652988384458,
    "modifiedBy": "acp_accessControlService",
    "modifiedAt": 1652988384458,
    "name": "acme-integration-policy",
    "description": "Pre-set policy to be applied for ACME",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "read"
            ]
        }
    ],
    "_etag": null
}
```

## 刪除原則 {#delete}

若要刪除原則，請向以下發出DELETE要求： `/policies` 端點，同時提供您要刪除之原則的ID。

**API格式**

```http
DELETE /policies/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| {POLICY_ID} | 您要刪除之原則的ID。 |

**请求**

以下請求會刪除ID為的原則 `c3863937-5d40-448d-a7be-416e538f955e`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的回應會傳回HTTP狀態204 （無內容）和空白內文。

您可以嘗試對原則進行查詢(GET)請求以確認刪除。 您會收到HTTP狀態404 （找不到），因為原則已從管理中移除。
