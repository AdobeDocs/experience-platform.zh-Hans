---
keywords: Experience Platform；主页；热门主题；有效策略；访问控制api
solution: Experience Platform
title: 有效策略API端点
topic-legacy: developer guide
description: Adobe Experience Platform中的访问控制允许您使用Adobe Admin Console管理各种平台功能的角色和权限。 本文档是有关如何使用Adobe Experience Platform的访问控制 API视图有效策略的指南。
exl-id: 555d73db-115d-4f4c-8bd2-b91477799591
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 1%

---

# 有效策略端点

要视图当前用户的有效策略，请向[!DNL Access Control] API中的`/acl/effective-policies`端点发出POST请求。 您要检索的权限和资源类型必须以数组形式在请求有效负荷中提供。 以下示例API调用中演示了这一点。

**API格式**

```http
POST /acl/effective-policies
```

**请求**

以下请求检索有关“[!UICONTROL Manage Datasets]”权限的信息，并访问当前用户的“[!UICONTROL schemas]”资源类型。

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
>有关可以在负载数组中提供的权限和资源类型的完整列表，请参阅[接受的权限和资源类型](#accepted-permissions-and-resource-types)的附录部分。

**响应**

成功的响应返回有关请求中提供的权限和资源类型的信息。 响应包括当前用户对请求中指定的资源类型具有的活动权限。 如果请求有效负荷中包含的任何权限对当前用户处于活动状态，则API返回具有astrisk(`*`)的权限，以指示该权限处于活动状态。 响应负载将忽略请求中提供的对用户不处于活动状态的任何权限。

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

本文档介绍了如何调用[!DNL Access Control] API以返回有关资源类型的活动权限和相关策略的信息。 有关[!DNL Experience Platform]的访问控制的详细信息，请参阅[访问控制概述](../home.md)。

## 附录

本节提供使用[!DNL Access Control] API的补充信息。

### 接受的权限和资源类型

以下是权限和资源类型的列表，您可以包括在到`/acl/active-permissions`端点的POST请求的负载中。

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
