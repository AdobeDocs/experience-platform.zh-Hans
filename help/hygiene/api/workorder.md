---
title: 记录删除请求（工单端点）
description: 数据卫生API中的/workorder端点允许您以编程方式管理标识的删除任务。
role: Developer
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: d569b1d04fa76e0a0e48364a586e8a1a773b9bf2
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 2%

---

# 记录删除请求（工单端点） {#work-order-endpoint}

数据卫生API中的`/workorder`端点允许您在Adobe Experience Platform中以编程方式管理记录删除请求。

>[!IMPORTANT]
> 
>记录删除旨在用于数据清理、匿名数据删除或数据最小化。 它们&#x200B;**不是**&#x200B;用于数据主体权利请求（合规性），因为它与《通用数据保护条例》(GDPR)等隐私法规相关。 对于所有合规性用例，请改用[Adobe Experience Platform Privacy Service](../../privacy-service/home.md)。

## 快速入门

本指南中使用的端点属于数据卫生API。 在继续之前，请查看[概述](./overview.md)，以了解相关文档的链接、此文档中示例API调用的阅读指南，以及有关成功调用任何Experience Platform API所需的所需标头的重要信息。

## 配额和处理时间线 {#quotas}

记录删除请求受每天和每月标识符提交限制的约束，具体取决于贵组织的许可证权利。 这些限制同时适用于基于UI和基于API的删除请求。

>[!NOTE]
>
>您每天最多可以提交&#x200B;**1,000,000个标识符**，但前提是剩余的每月配额允许这样做。 如果每月上限不到100万，则每日提交内容不能超过该上限。

### 按产品显示的每月提交权利 {#quota-limits}

下表概述了按产品和权利级别划分的标识符提交限制。 对于每个产品，每月上限是两个值中的较小值：固定标识符上限或与许可数据量绑定的基于百分比的阈值。

| 产品 | 权利描述 | 每月上限（以较小者为准） |
|----------|-------------------------|---------------------------------|
| Real-Time CDP或Adobe Journey Optimizer | 不带Privacy and Security Shield或Healthcare Shield附加组件 | 2,000,000个标识符或可寻址受众的5% |
| Real-Time CDP或Adobe Journey Optimizer | 带有Privacy and Security Shield或Healthcare Shield附加组件 | 15,000,000个标识符或10%的可寻址受众 |
| Customer Journey Analytics | 不带Privacy and Security Shield或Healthcare Shield附加组件 | 2,000,000个标识符或每百万CJA权利行有100个标识符 |
| Customer Journey Analytics | 带有Privacy and Security Shield或Healthcare Shield附加组件 | 15,000,000个标识符或每百万CJA权利行有200个标识符 |

>[!NOTE]
>
> 根据大多数组织的实际可寻址受众或CJA行授权，其每月限制较低。

配额在每个日历月的第一天重置。 未使用的配额&#x200B;**未**&#x200B;延期。

>[!NOTE]
>
>配额基于贵组织为&#x200B;**提交的标识符**&#x200B;授予的每月授权。 系统护栏不强制执行这些操作，但可以对其进行监控和审查。
>
>记录删除是&#x200B;**共享服务**。 您的每月上限反映了Real-Time CDP、Adobe Journey Optimizer、Customer Journey Analytics和任何适用的Shield加载项中的最高权限。

### 处理标识符提交的时间表 {#sla-processing-timelines}

提交后，记录删除请求将根据您的权利级别进行排队和处理。

| 产品和权利描述 | 队列持续时间 | 最长处理时间(SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| 不带Privacy and Security Shield或Healthcare Shield附加组件 | 长达15天 | 30 天 |
| 带有Privacy and Security Shield或Healthcare Shield附加组件 | 通常为24小时 | 15 天 |

如果贵组织需要更高的限制，请联系您的Adobe代表进行权利审查。

>[!TIP]
>
>要检查您当前的配额使用情况或权利层，请参阅[配额参考指南](../api/quota.md)。

## 创建记录删除请求 {#create}

您可以通过向`/workorder`端点发出POST请求，从单个数据集或所有数据集中删除一个或多个身份。

>[!TIP]
>
>通过API提交的每个记录删除请求最多可包含&#x200B;**100,000个标识**。 为了最大限度地提高效率，请在每个请求中提交尽可能多的身份，避免提交低容量申请，如单个ID工作单。

**API格式**

```http
POST /workorder
```

>[!NOTE]
>
>数据生命周期请求只能根据主身份或身份映射修改数据集。 请求必须指定主标识或提供标识映射。

**请求**

根据请求有效负载中提供的`datasetId`的值，API调用将从所有数据集或您指定的单个数据集中删除身份。 以下请求从特定数据集中删除三个身份。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "action": "delete_identity",
        "datasetId": "c48b51623ec641a2949d339bad69cb15",
        "displayName": "Example Record Delete Request",
        "description": "Cleanup identities required by Jira request 12345.",
        "identities": [
          {
            "namespace": {
              "code": "email"
            },
            "id": "poul.anderson@example.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cordwainer.smith@gmail.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cyril.kornbluth@yahoo.com"
          }
        ]
      }'
```

| 属性 | 描述 |
| --- | --- |
| `action` | 要执行的操作。 记录删除的值必须设置为`delete_identity`。 |
| `datasetId` | 如果您要从单个数据集中删除，此值必须是相关数据集的ID。 如果要从所有数据集中删除，则将该值设置为`ALL`。<br><br>如果指定单个数据集，则该数据集的关联体验数据模型(XDM)架构必须定义主标识。 如果数据集没有主标识，则必须具有标识映射，才能被数据生命周期请求修改。<br>如果存在标识映射，它将以名为`identityMap`的顶级字段的形式出现。<br>请注意，数据集行在其标识映射中可能具有多个标识，但只能将一个标识标记为主标识。 必须包含`"primary": true`以强制`id`匹配主标识。 |
| `displayName` | 记录删除请求的显示名称。 |
| `description` | 记录删除请求的描述。 |
| `identities` | 一个数组，其中包含您要删除其信息的至少一个用户的身份。 每个身份由[身份命名空间](../../identity-service/features/namespaces.md)和一个值组成：<ul><li>`namespace`：包含代表身份命名空间的单个字符串属性`code`。 </li><li>`id`：标识值。</ul>如果`datasetId`指定了单个数据集，则`identities`下的每个实体必须使用与架构的主标识相同的标识命名空间。<br><br>如果将`datasetId`设置为`ALL`，则`identities`数组不受任何单个命名空间的约束，因为每个数据集可能不同。 但是，如[Identity Service](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces)所报告，您的请求仍受组织可用的命名空间限制。 |

{style="table-layout:auto"}

**响应**

成功的响应将返回记录删除的详细信息。

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Record Delete Request",
  "description": "Cleanup identities required by Jira request 12345."
}
```

| 属性 | 描述 |
| --- | --- |
| `workorderId` | 删除订单的ID。 这可用于稍后查找删除的状态。 |
| `orgId` | 您的组织ID。 |
| `bundleId` | 与此删除顺序关联的捆绑包的ID，用于调试目的。 多个删除订单捆绑在一起，由下游服务处理。 |
| `action` | 工作单正在执行的操作。 对于记录删除，值为`identity-delete`。 |
| `createdAt` | 创建删除顺序的时间戳。 |
| `updatedAt` | 上次更新删除顺序的时间戳。 |
| `status` | 删除顺序的当前状态。 |
| `createdBy` | 创建删除顺序的用户。 |
| `datasetId` | 受请求约束的数据集的ID。 如果请求适用于所有数据集，则该值将设置为`ALL`。 |

{style="table-layout:auto"}

## 检索记录删除的状态 {#lookup}

在您[创建记录删除请求](#create)后，可以使用GET请求检查其状态。

**API格式**

```http
GET /workorder/{WORK_ORDER_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{WORK_ORDER_ID}` | 正在查找的记录删除的`workorderId`。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回删除操作的详细信息，包括其当前状态。

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Record Delete Request",
  "description": "Cleanup identities required by Jira request 12345.",
  "productStatusDetails": [
    {
        "productName": "Data Management",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:51:31.535872Z"
    },
    {
        "productName": "Identity Service",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:43:46.331150Z"
    },
    {
        "productName": "Profile Service",
        "productStatus": "waiting",
        "createdAt": "2022-08-08T16:37:13.443481Z"
    }
  ]
}
```

| 属性 | 描述 |
| --- | --- |
| `workorderId` | 删除订单的ID。 这可用于稍后查找删除的状态。 |
| `orgId` | 您的组织ID。 |
| `bundleId` | 与此删除顺序关联的捆绑包的ID，用于调试目的。 多个删除订单捆绑在一起，由下游服务处理。 |
| `action` | 工作单正在执行的操作。 对于记录删除，值为`identity-delete`。 |
| `createdAt` | 创建删除顺序的时间戳。 |
| `updatedAt` | 上次更新删除顺序的时间戳。 |
| `status` | 删除顺序的当前状态。 |
| `createdBy` | 创建删除顺序的用户。 |
| `datasetId` | 受请求约束的数据集的ID。 如果请求适用于所有数据集，则该值将设置为`ALL`。 |
| `productStatusDetails` | 一个数组，列出与请求相关的下游进程的当前状态。 每个数组对象包含以下属性：<ul><li>`productName`：下游服务的名称。</li><li>`productStatus`：来自下游服务的请求的当前处理状态。</li><li>`createdAt`：服务发布最新状态的时间戳。</li></ul> |

## 更新记录删除请求

您可以通过发出PUT请求来更新记录删除的`displayName`和`description`。

**API格式**

```http
PUT /workorder{WORK_ORDER_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{WORK_ORDER_ID}` | 正在查找的记录删除的`workorderId`。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "displayName" : "Update - displayName",
        "description" : "Update - description"
      }'
```

| 属性 | 描述 |
| --- | --- |
| `displayName` | 记录删除请求的更新显示名称。 |
| `description` | 更新了记录删除请求的描述。 |

{style="table-layout:auto"}

**响应**

成功的响应将返回记录删除的详细信息。

```json
{
    "workorderId": "DI-61828416-963a-463f-91c1-dbc4d0ddbd43",
    "orgId": "{ORG_ID}",
    "bundleId": "BN-aacacc09-d10c-48c5-a64c-2ced96a78fca",
    "action": "identity-delete",
    "createdAt": "2024-06-12T20:02:49.398448Z",
    "updatedAt": "2024-06-13T21:35:01.944749Z",
    "operationCount": 1,
    "status": "ingested",
    "createdBy": "{USER_ID}",
    "datasetId": "666950e6b7e2022c9e7d7a33",
    "datasetName": "Acme_Dataset_E2E_Identity_Map_Schema_5_1718178022379",
    "displayName": "Updated Display Name",
    "description": "Updated Description",
    "productStatusDetails": [
        {
            "productName": "Data Management",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Identity Service",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:36:09.020832Z"
        },
        {
            "productName": "Profile Service",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Journey Orchestrator",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:12:19.843199Z"
        }
    ]
}
```

| 属性 | 描述 |
| --- | --- |
| `workorderId` | 删除订单的ID。 这可用于稍后查找删除的状态。 |
| `orgId` | 您的组织ID。 |
| `bundleId` | 与此删除顺序关联的捆绑包的ID，用于调试目的。 多个删除订单捆绑在一起，由下游服务处理。 |
| `action` | 工作单正在执行的操作。 对于记录删除，值为`identity-delete`。 |
| `createdAt` | 创建删除顺序的时间戳。 |
| `updatedAt` | 上次更新删除顺序的时间戳。 |
| `status` | 删除顺序的当前状态。 |
| `createdBy` | 创建删除顺序的用户。 |
| `datasetId` | 受请求约束的数据集的ID。 如果请求适用于所有数据集，则该值将设置为`ALL`。 |
| `productStatusDetails` | 一个数组，列出与请求相关的下游进程的当前状态。 每个数组对象包含以下属性：<ul><li>`productName`：下游服务的名称。</li><li>`productStatus`：来自下游服务的请求的当前处理状态。</li><li>`createdAt`：服务发布最新状态的时间戳。</li></ul> |

{style="table-layout:auto"}
