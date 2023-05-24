---
keywords: Experience Platform；首頁；熱門主題；有效原則；存取控制api
solution: Experience Platform
title: 有效原則API端點
description: 瞭解如何使用Adobe Experience Platform的存取控制API檢視有效的存取原則。
exl-id: 555d73db-115d-4f4c-8bd2-b91477799591
source-git-commit: 16d85a2a4ee8967fc701a3fe631c9daaba9c9d70
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 1%

---

# 有效原則端點

>[!NOTE]
>
>如果傳遞的是使用者權杖，則權杖的使用者必須具有請求組織的「組織管理員」角色。

若要檢視目前使用者的有效存取控制原則，請向下列使用者發出POST要求： `/acl/effective-policies` 中的端點 [!DNL Access Control] API。 您要在要求裝載中擷取的許可權和資源型別必須以陣列形式提供。 這會在以下範例API呼叫中說明。

**API格式**

```http
POST /acl/effective-policies
```

**请求**

以下請求會擷取關於「[!UICONTROL 管理資料集]「對」的許可權和存取權」[!UICONTROL 結構描述]「目前使用者的資源型別。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/acl/effective-policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    "/permissions/manage-datasets",
    "/resource-types/schemas"
  ]'
```

>[!NOTE]
>
>如需可在承載陣列中提供的許可權和資源型別的完整清單，請參閱附錄 [接受的許可權和資源型別](#accepted-permissions-and-resource-types).

**响应**

成功的回應會傳回要求中提供的許可權和資源型別相關資訊。 回應包含目前使用者對請求中指定的資源型別具有的使用中許可權。 如果要求裝載中包含的任何許可權對目前使用者而言是作用中的，API會傳回帶有星號(`*`)以表示許可權為使用中。 請求中提供的任何非使用者作用中的許可權會在回應裝載中忽略。

```json
{
    "policies": {
        "/resource-types/schemas": [
            "read",
            "write",
            "delete"
        ],
        "/permissions/manage-datasets": [
            "*"
        ]
    }
}
```

## 后续步骤

本檔案說明如何呼叫 [!DNL Access Control] API可傳回有關資源型別的作用中許可權和相關存取原則的資訊。 如需關於存取控制的詳細資訊， [!DNL Experience Platform]，請參閱 [存取控制總覽](../home.md).

## 附录

本節提供使用的補充資訊 [!DNL Access Control] API。

### 接受的許可權和資源型別

以下是可包含在對的POST請求之裝載中的許可權和資源型別清單 `/acl/active-permissions` 端點。

**Permissions**

```plaintext
permissions/activate-destinations
permissions/evaluate-segments
permissions/execute-decisioning-activities
permissions/export-audience-for-segment
permissions/manage-datasets
permissions/manage-decisioning-activities
permissions/manage-decisioning-options
permissions/manage-destinations
permissions/manage-dsw
permissions/manage-dule-labels
permissions/manage-dule-policies
permissions/manage-identity-namespaces
permissions/manage-privacy-workflows
permissions/manage-profile-configs
permissions/manage-profiles
permissions/manage-queries
permissions/manage-schemas
permissions/manage-segments
permissions/manage-sources
permissions/reset-sandboxes
permissions/view-datasets
permissions/view-destinations
permissions/view-dule-labels
permissions/view-dule-policies
permissions/view-identity-namespaces
permissions/view-monitoring-dashboard
permissions/view-privacy-workflows
permissions/view-profile-configs
permissions/view-profiles
permissions/view-sandboxes
permissions/view-schemas
permissions/view-segments
permissions/view-sources
```

**資源型別**

```plaintext
resource-types/activation-associations
resource-types/activations
resource-types/activities
resource-types/analytics-source
resource-types/audience-manager-source
resource-types/bizible-source
resource-types/connection
resource-types/customer-attributes-source
resource-types/data-science-workspace
resource-types/dataset-preview
resource-types/datasets
resource-types/dule-label
resource-types/dule-policy
resource-types/enterprise-source
resource-types/identity-descriptor
resource-types/identity-namespaces
resource-types/launch-source
resource-types/marketing-action
resource-types/marketo-source
resource-types/monitoring
resource-types/offers
resource-types/placements
resource-types/privacy-consent
resource-types/privacy-content-delivery
resource-types/privacy-job
resource-types/profile-configs
resource-types/profile-datasets
resource-types/profiles
resource-types/query
resource-types/relationship-descriptor
resource-types/sandboxes
resource-types/schemas
resource-types/segment-jobs
resource-types/segments
resource-types/streaming-source
```
