---
keywords: Experience Platform;home;popular topics;effective policies;access control api
solution: Experience Platform
title: 视图有效策略
topic: developer guide
description: Adobe Experience Platform的访问控制允许您通过使用Adobe Admin Console管理各种平台功能的角色和权限。 本文档指导您如何使用Adobe Experience Platform的访问控制API视图有效的策略。
translation-type: tm+mt
source-git-commit: 8967a820ab19bceb2be69f37e3399ed99f0b8e72
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 1%

---


# 视图有效策略

要视图当前用户的有效策略，请向API中的端点 `/acl/effective-policies` 发出POST [!DNL Access Control] 请求。 您要检索的权限和资源类型必须以数组形式在请求有效负荷中提供。 以下示例API调用中演示了这一点。

**API格式**

```http
POST /acl/effective-policies
```

**请求**

以下请求检索有关“管理[!UICONTROL 数据集]”权限的信息，并访问当前[!UICONTROL 用户的]“模式”资源类型。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/acl/effective-policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    "/permissions/manage-datasets",
    "/resource-types/schemas"
  ]'
```

>[!NOTE]
>
>有关可以在有效负荷阵列中提供的权限和资源类型的完整列表，请参阅附录部分中 [的已接受权限和资源类型](#accepted-permissions-and-resource-types)。

**响应**

成功的响应会返回有关请求中提供的权限和资源类型的信息。 响应包括当前用户对请求中指定的资源类型具有的活动权限。 如果请求有效负荷中包含的任何权限对当前用户处于活动状态，API将返回具有临时磁盘()的权`*`限，以指示该权限处于活动状态。 响应有效负荷将忽略请求中提供的对用户不处于活动状态的任何权限。

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

此文档介绍了如何调用API [!DNL Access Control] 以返回有关资源类型的活动权限和相关策略的信息。 有关访问控制的详细信 [!DNL Experience Platform]息，请参阅 [访问控制概述](../home.md)。

## 附录

本节提供有关使用API的补充 [!DNL Access Control] 信息。

### 接受的权限和资源类型

以下是权限和资源类型的列表，您可以在到端点的POST请求的有效负荷中包含这些 `/acl/active-permissions` 权限。

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

**资源类型**

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
