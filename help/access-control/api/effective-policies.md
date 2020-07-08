---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 视图有效策略
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 1%

---


# 视图有效策略

要视图当前用户的有效策略，请在访问控制API中向 `/acl/effective-policies` 端点发出POST请求。 您要检索的权限和资源类型必须以数组形式在请求有效负荷中提供。 以下示例API调用中演示了这一点。

**API格式**

```http
POST /acl/effective-policies
```

**请求**

以下请求会检索有关“管理模式集”权限的信息，并访问当前用户的“数据集”资源类型。

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

此文档介绍了如何调用访问控制API以返回有关资源类型的活动权限和相关策略的信息。 有关访问控制Experience Platform的详细信息，请参阅 [访问控制概述](../home.md)。

## 附录

本节提供使用访问控制API的补充信息。

### 接受的权限和资源类型

以下是权限和资源类型的列表，您可以在POST请求到端点的有效负荷中包含这些 `/acl/active-permissions` 权限。

**Permissions**

```plaintext
"permissions/activate-destinations"
"permissions/export-audience-for-segments"
"permissions/manage-datasets"
"permissions/manage-destinations"
"permissions/manage-identity-namespaces"
"permissions/manage-profiles"
"permissions/manage-sandboxes"
"permissions/manage-schemas"
"permissions/reset-sandboxes"
"permissions/view-datasets"
"permissions/view-destinations"
"permissions/view-identity-namespaces"
"permissions/view-monitoring-dashboard"
"permissions/view-profiles"
"permissions/view-sandboxes"
"permissions/view-schemas"
```

**资源类型**

```plaintext
"resource-types/classes"
"resource-types/connections"
"resource-types/data-types"
"resource-types/dataset-data"
"resource-types/datasets"
"resource-types/destinations"
"resource-types/dule-labels"
"resource-types/identity-descriptors"
"resource-types/identity-namespaces"
"resource-types/mixins"
"resource-types/monitoring"
"resource-types/profile-configs
"resource-types/profile-datasets"
"resource-types/profiles"
"resource-types/relationship-descriptors"
"resource-types/reset-sandboxes"
"resource-types/sandboxes"
"resource-types/schemas"
"resource-types/segment-jobs"
"resource-types/segments"
```
