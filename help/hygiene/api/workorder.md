---
title: 记录删除工作单
description: 了解如何使用数据卫生API中的/workorder端点在Adobe Experience Platform中管理记录删除工作单。 本指南涵盖配额、处理时间表和API使用情况。
role: Developer
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: 5ca3e4feae3096e41689610ac3afac7e93047149
workflow-type: tm+mt
source-wordcount: '3316'
ht-degree: 1%

---

# 记录删除工作单 {#work-order-endpoint}

使用数据卫生API中的`/workorder`端点在Adobe Experience Platform中创建、查看和管理记录删除工作单。 您可以跨数据集控制、监控和跟踪数据删除，以帮助您保持数据质量并支持组织的数据治理标准。

>[!IMPORTANT]
>
>记录删除工作单用于数据清理、匿名数据删除或数据最小化。 **请勿根据隐私法规（如GDPR）对数据主体权限请求使用记录删除工作单。**&#x200B;对于合规性用例，请使用[Adobe Experience Platform Privacy Service](../../privacy-service/home.md)。

## 快速入门

在开始之前，请参阅[概述](./overview.md)以了解所需的标头、如何读取示例API调用以及在何处查找相关文档。

## 配额和处理时间线 {#quotas}

记录删除工作单受每日和每月标识符提交限制的约束，具体由贵组织的许可证权利文件决定。 这些限制同时适用于基于UI和基于API的记录删除请求。

>[!NOTE]
>
>您每天最多可以提交&#x200B;**1,000,000个标识符**，但前提是剩余的每月配额允许这样做。 如果每月上限不到100万，则每日提交内容不能超过该上限。

### 按产品显示的每月提交权利 {#quota-limits}

下表显示了按产品和权利级别划分的标识符提交限制。 对于每个产品，每月上限是两个值中的较小值：固定标识符上限或与许可数据量绑定的基于百分比的阈值。 实际上，大多数组织会根据其实际可寻址受众或Adobe Customer Journey Analytics行授权，降低每月限额。

| 产品 | 权利描述 | 每月上限（以较小者为准） |
|----------|-------------------------|---------------------------------|
| Real-Time CDP或Adobe Journey Optimizer | 不带Privacy and Security Shield或Healthcare Shield附加组件 | 2,000,000个标识符或可寻址受众的5% |
| Real-Time CDP或Adobe Journey Optimizer | 带有Privacy and Security Shield或Healthcare Shield附加组件 | 15,000,000个标识符或10%的可寻址受众 |
| Customer Journey Analytics | 不带Privacy and Security Shield或Healthcare Shield附加组件 | 2,000,000个标识符或每百万Customer Journey Analytics权利行有100个标识符 |
| Customer Journey Analytics | 带有Privacy and Security Shield或Healthcare Shield附加组件 | 15,000,000个标识符或每百万Customer Journey Analytics权利行有200个标识符 |

>[!NOTE]
>
>- 配额在每个日历月的第一天重置。 未使用的配额&#x200B;**未**&#x200B;延期。
>- 配额使用量基于贵组织为&#x200B;**提交的标识符**&#x200B;授予的每月授权。 系统护栏不强制执行配额，但可以监视和审查配额。
>- 记录删除工作单产能是&#x200B;**共享服务**。 您的每月上限反映了Real-Time CDP、Adobe Journey Optimizer、Customer Journey Analytics和任何适用的Shield加载项中的最高权限。

### 处理标识符提交的时间表 {#sla-processing-timelines}

提交后，系统会根据您的权利级别对记录删除工作单进行排队和处理。

| 产品和权利描述 | 队列持续时间 | 最长处理时间(SLA) |
|------------------------------------|---------------------|-------------------------------|
| 不带Privacy and Security Shield或Healthcare Shield附加组件 | 长达15天 | 30 天 |
| 带有Privacy and Security Shield或Healthcare Shield附加组件 | 通常为24小时 | 15 天 |

如果贵组织需要更高的限制，请联系您的Adobe代表进行权利审查。

>[!TIP]
>
>要检查您当前的配额使用情况或权利层，请参阅[配额参考指南](../api/quota.md)。

## 列表记录删除工作单 {#list}

检索组织内数据卫生操作的分页记录删除工作单列表。 使用查询参数筛选结果。 每个工作单记录包括操作类型（如`identity-delete`）、状态、相关数据集和用户详细信息，以及审核元数据。

**API格式**

```http
GET /workorder
```

下表描述了可用于列出记录删除工作单的查询参数。

| 查询参数 | 描述 |
| --------------- | ------------|
| `search` | 以下字段中的部分匹配（通配符搜索）不区分大小写：author、displayName、description或datasetName。 此外，还要与确切的到期ID匹配。 |
| `type` | 按工作单类型（如`identity-delete`）筛选结果。 |
| `status` | 以逗号分隔的工作单状态列表。 状态值区分大小写。<br>枚举： `received`，`validated`，`submitted`，`ingested`，`completed`，`failed` |
| `author` | 查找最近更新工作单的人员（或原始创建者）。 接受文本或SQL模式。 |
| `displayName` | 工作单显示名称不区分大小写的匹配。 |
| `description` | 对工单说明进行不区分大小写的匹配。 |
| `workorderId` | 与工单ID完全匹配。 |
| `sandboxName` | 与请求中使用的沙盒名称完全匹配，或使用`*`包括所有沙盒。 |
| `fromDate` | 按在此日期或之后创建的工作单进行筛选。 需要设置`toDate`。 |
| `toDate` | 按在此日期或之前创建的工作单进行筛选。 需要设置`fromDate`。 |
| `filterDate` | 仅返回在此日期创建、更新或更改状态的工作单。 |
| `page` | 要返回的页面索引（从0开始）。 |
| `limit` | 每页最大结果数（1-100，默认值： 25）。 |
| `orderBy` | 结果的排序顺序。 使用`+`或`-`前缀进行升序/降序。 示例：`orderBy=-datasetName`。 |
| `properties` | 每个结果要包含的其他字段的逗号分隔列表。 可选。 |


**请求**

以下请求检索所有已完成的记录删除工作单，每页最多检索两个工作单：

```shell
curl -X GET \
  "https://platform.adobe.io/data/core/hygiene/workorder?status=completed&limit=2" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回记录删除工作单的分页列表。

```json
{
  "results": [
    {
      "workorderId": "DI-1729d091-b08b-47f4-923f-6a4af52c93ac",
      "orgId": "9C1F2AC143214567890ABCDE@AcmeOrg",
      "bundleId": "BN-4cfabf02-c22a-45ef-b21f-bd8c3d631f41",
      "action": "identity-delete",
      "createdAt": "2034-03-15T11:02:10.935Z",
      "updatedAt": "2034-03-15T11:10:10.938Z",
      "operationCount": 3,
      "targetServices": [
        "profile",
        "datalake",
        "identity",
        "ajo"
      ],
      "status": "received",
      "createdBy": "a.stark@acme.com <a.stark@acme.com> BD8C3D631F41@acme.com",
      "datasetId": "a7b7c8f3a1b8457eaa5321ab",
      "datasetName": "Acme_Customer_Exports",
      "displayName": "Customer Identity Delete Request",
      "description": "Scheduled identity deletion for compliance"
    }
  ],
  "total": 1,
  "count": 1,
  "_links": {
    "next": {
      "href": "https://platform.adobe.io/workorder?page=1&limit=2",
      "templated": false
    },
    "page": {
      "href": "https://platform.adobe.io/workorder?limit={limit}&page={page}",
      "templated": true
    }
  }
}
```

下表描述了响应中的属性。

| 属性 | 描述 |
| --- | --- |
| `results` | 删除工单对象的记录数组。 每个对象都包含以下字段。 |
| `workorderId` | 记录删除工作单的唯一标识符。 |
| `orgId` | 您的独特组织标识符。 |
| `bundleId` | 包含此记录删除工作单的捆绑的唯一标识符。 捆绑功能允许下游服务将多个删除订单分组在一起进行处理。 |
| `action` | 工作单中请求的操作类型。 |
| `createdAt` | 创建工作单时的时间戳。 |
| `updatedAt` | 上次更新工作单的时间戳。 |
| `operationCount` | 工作单中包含的工序数。 |
| `targetServices` | 处理删除的目标服务集。 默认值取决于您组织的权利。 对于具有Real-Time CDP或Adobe Journey Optimizer的组织，默认设置是一整套支持的服务(`["datalake", "identity", "profile", "ajo"]`)。 对于仅Customer Journey Analytics组织（没有实时客户配置文件权利），唯一有效值为[&quot;datalake&quot;]。 |
| `status` | 工作单的当前状态。 可能的值为： `received`、`validated`、`submitted`、`ingested`、`completed`和`failed`。 |
| `createdBy` | 创建工作单的用户的电子邮件和标识符。 |
| `datasetId` | 工作单所针对的数据集：单个数据集ID、以逗号分隔的数据集ID列表（多数据集）或文本`ALL`。 当请求使用仅配置文件模式时，此值为`ALL`。 |
| `datasetName` | 与工作单关联的数据集的名称。 |
| `displayName` | 工单的可读标签。 |
| `description` | 工作单用途的描述。 |
| `total` | 与查询匹配的记录删除工作单的总数。 |
| `count` | 当前页删除工作单的记录数。 |
| `_links` | 分页和导航链接。 |
| `next` | 下一页具有`href` （字符串）和`templated` （布尔值）的对象。 |
| `page` | 用于页面导航的具有`href` （字符串）和`templated` （布尔值）的对象。 |

{style="table-layout:auto"}

## 创建记录删除工作单 {#create}

要从单个数据集、多个数据集或所有数据集中删除与一个或多个身份关联的记录，请对`/workorder`端点发出POST请求。

工作单以异步方式处理，并在提交后显示在工作单列表中。 从2026年3月Experience Platform版本开始，所有客户通常都可以使用多数据集和仅配置文件（目标服务）选项。

>[!TIP]
>
>通过API提交的每个记录删除工作单最多可包含&#x200B;**100,000个标识**。 提交每个请求尽可能多的身份以最大限度地提高效率。 避免低容量提交，如单个ID工单。

**API格式**

```http
POST /workorder
```

>[!IMPORTANT]
>
>记录删除工作单仅对&#x200B;**主标识**&#x200B;字段起作用。 以下限制适用：
>
>- **数据集架构必须定义主标识或标识映射。**&#x200B;您只能从关联XDM架构定义主标识或标识映射的数据集中删除记录。
>- **未扫描辅助标识。**&#x200B;如果数据集包含多个标识字段，则仅使用主标识进行匹配。 无法根据非主标识定位或删除记录。
>- **跳过没有填充主标识的记录。**&#x200B;如果记录未填充主身份元数据，则无法将其删除。
>- **在身份配置之前摄取的数据不合格。**&#x200B;如果在数据摄取后将主标识字段添加到架构，则无法通过记录删除工作单来删除以前摄取的记录。

>[!NOTE]
>
>如果尝试为已具有活动过期时间的数据集创建记录删除工作单，请求将返回HTTP 400（错误请求）。 活动到期是指任何尚未完成的计划删除。

### 身份有效负载格式（`namespacesIdentities`或`identities`）

请求正文必须正好包含以下&#x200B;**项之一**。

| 格式 | 属性 | 形状 | 使用时间 |
|--------|----------|-------|-------------|
| **推荐** | `namespacesIdentities` | 具有`namespace` （例如，`{ "code": "email" }`）和`ids` （标识字符串数组）的对象数组。 | 用于所有负载，无论是手动构建还是代码生成。 当多个身份共享同一命名空间时，这尤其可以有效减少有效负载大小。 |
| **也接受** | `identities` | 具有`namespace` （例如，`{ "code": "email" }`）和单个`id` （字符串）的对象数组。 | 接受以向后兼容。 这是[csv到数据卫生转换脚本](#convert-id-lists-to-json-for-record-delete-requests)生成的格式。 该服务在内部标准化此格式，因此产生的行为是相同的。 |

如果您同时发送&#x200B;**两个属性**，**两个属性**，或者为您包括的属性提供&#x200B;**空数组**，则API会返回&#x200B;**HTTP 400 （错误请求）**，并显示以下消息之一：

- **提供的两个属性：** `"Identities and NamespacesIdentities are not allowed at the same time"`
- **未提供或列表为空：** `"Identities are Empty for Delete Identity request."`

**请求**

以下请求从特定数据集中删除与指定电子邮件地址关联的所有记录。 它使用推荐的`namespacesIdentities`格式。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "displayName": "Acme Loyalty - Customer Data Deletion",
        "description": "Delete all records associated with the specified email addresses from the Acme_Loyalty_2023 dataset.",
        "action": "delete_identity",
        "datasetId": "7eab61f3e5c34810a49a1ab3",
        "namespacesIdentities": [
          {
            "namespace": {
              "code": "email"
            },
            "ids": [
              "alice.smith@acmecorp.com",
              "bob.jones@acmecorp.com",
              "charlie.brown@acmecorp.com"
            ]
          }
        ]
      }'
```

下表描述了用于创建记录删除工作单的属性。

| 属性 | 描述 |
| --- | --- |
| `displayName` | 此记录删除工作单的人工可读标签。 |
| `description` | 记录删除工作单的描述。 |
| `action` | 为记录删除工作单请求的操作。 要删除与给定身份关联的记录，请使用`delete_identity`。 |
| `datasetId` | 数据集的唯一标识符。 该值必须恰好为以下值之一：文本`ALL`、单个数据集ID或两个或多个数据集ID的逗号分隔列表（例如`"id1,id2,id3"`）。 您无法将`ALL`与特定ID相结合。 与以前一样，单数据集请求的行为是，多数据集请求从每个列出的数据集中删除身份，`ALL`定向每个数据集。 数据集必须具有主身份映射或身份映射。 如果存在标识映射，则它将显示为名为`identityMap`的顶级字段。<br>**注意**：数据集行的标识映射中可能具有多个标识，但只能将一个标识标记为主标识。 必须包含`"primary": true`以强制`id`匹配主标识。<br>使用`targetServices`进行仅配置文件删除时，`datasetId`必须为`ALL`。 |
| `targetServices` | 可选。 指定哪些服务应该处理删除。 默认值取决于您组织的权利。 默认情况下，具有Real-Time CDP或Adobe Journey Optimizer的组织将接收全套支持的服务(`["datalake", "identity", "profile", "ajo"]`)。 具有Customer Journey Analytics但没有Real-time Customer Profile权利的组织只能使用[&quot;datalake&quot;]。 要将删除限制为仅删除与配置文件相关的数据并保留数据湖不变，请将此项设置为`["identity", "profile", "ajo"]`（按任何顺序）。 此仅配置文件模式需要Real-Time CDP或Adobe Journey Optimizer权利，并且`datasetId`必须为`ALL`。 |
| `identities` | **只使用`identities`或`namespacesIdentities`之一。**&#x200B;对象数组，每个对象具有`namespace` （具有`code`的对象，例如`"email"`）和`id` （单一标识字符串）。 接受以向后兼容，由转换脚本生成。 服务在内部标准化此格式；行为相同。 请参阅上面的[身份有效负载格式](#identity-payload-format-identities-or-namespacesidentities)。 |
| `namespacesIdentities` | **只使用`identities`或`namespacesIdentities`之一。**&#x200B;对象数组，每个对象具有`namespace` （具有`code`的对象，例如`"email"`）和`ids` （标识字符串数组）。 建议所有负载均使用。 当多个标识共享一个命名空间时，`namespacesIdentities`属性会更加紧凑。 请参阅上面的[身份有效负载格式](#identity-payload-format-identities-or-namespacesidentities)。 身份命名空间： [身份命名空间文档](../../identity-service/features/namespaces.md)，[身份服务API](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces)。 |

**响应**

成功的响应将返回新记录删除工作单的详细信息。

```json
{
  "workorderId": "DI-95c40d52-6229-44e8-881b-fc7f072de63d",
  "orgId": "8B1F2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-c61bec61-5ce8-498f-a538-fb84b094adc6",
  "action": "identity-delete",
  "createdAt": "2035-06-02T09:21:00.000Z",
  "updatedAt": "2035-06-02T09:21:05.000Z",
  "operationCount": 1,
  "targetServices": [
    "profile",
    "datalake",
    "identity",
    "ajo"
  ],
  "status": "received",
  "createdBy": "c.lannister@acme.com <c.lannister@acme.com> 7EAB61F3E5C34810A49A1AB3@acme.com",
  "datasetId": "7eab61f3e5c34810a49a1ab3",
  "datasetName": "Acme_Loyalty_2023",
  "displayName": "Loyalty Identity Delete Request",
  "description": "Schedule deletion for Acme loyalty program dataset"
}
```

下表描述了响应中的属性。

| 属性 | 描述 |
| --- | --- |
| `workorderId` | 记录删除工作单的唯一标识符。 使用此值查找删除的状态或详细信息。 |
| `orgId` | 您的独特组织标识符。 |
| `bundleId` | 包含此记录删除工作单的捆绑的唯一标识符。 捆绑功能允许下游服务将多个删除订单分组在一起进行处理。 |
| `action` | 记录删除工作单中请求的操作类型。 |
| `createdAt` | 创建工作单时的时间戳。 |
| `updatedAt` | 上次更新工作单的时间戳。 |
| `operationCount` | 工作单中包含的工序数。 |
| `targetServices` | 记录删除工作单的目标服务列表。 |
| `status` | 记录删除工作单的当前状态。 |
| `createdBy` | 创建记录删除工作单的用户的电子邮件和标识符。 |
| `datasetId` | 数据集的唯一标识符。 如果请求适用于所有数据集，则该值将设置为`ALL`。 对于多数据集请求，值反映提交的逗号分隔列表或单个ID。 |
| `datasetName` | 此记录删除工作单的数据集名称。 |
| `displayName` | 记录删除工作单的人工可读标签。 |
| `description` | 记录删除工作单的描述。 |

{style="table-layout:auto"}

响应`targetServices`值与您的请求一致，或者在忽略时显示完整的默认设置（请参阅上面的响应表）。

### 多数据集和仅配置文件(API) {#multi-dataset-profile-only}

以下选项仅通过API提供，在数据卫生UI中不受支持。 它们控制哪些数据集以及哪些服务会处理删除，从而支持多数据集提交和仅用于用户档案的目标服务请求。

下表汇总了每个选项的请求正文和行为更改的方式。

| 选项 | 请求正文更改 | 行为 |
|--------|---------------------|----------|
| **多数据集** | 在`datasetId`中使用逗号分隔的列表（如`"id1,id2,id3"`）。 单个ID或`ALL`未更改。 | 标识将从列出的数据集（或一个数据集，或在`ALL`时从所有数据集）中删除。 |
| **仅配置文件（目标服务）** | 添加`targetServices`和`["identity", "profile", "ajo"]`（任何顺序）。 需要`datasetId`： `"ALL"`。 | 只有Identity、Profile和Adobe Journey Optimizer会处理删除；数据湖不会修改。 |

#### 多数据集请求

`datasetId`字段用逗号拆分：使用单个ID（与之前相同的行为）、以逗号分隔的ID列表或文本`ALL`。 要在一个工作单中从多个特定数据集中删除身份，请提供以逗号分隔的列表：

```json
"datasetId": "6707eb36eef4d42ab86d9fbe,6643f00c16ddf51767fcf780"
```

然后，从列出的每个数据集中删除身份。 单个数据集请求始终有效；使用`ALL`定位每个数据集。 该值必须正好为以下值之一：`ALL`、单个数据集ID或以逗号分隔的两个或多个数据集ID（不将`ALL`与特定ID组合）。

#### 仅配置文件（目标服务）

若要在保持数据湖不变的情况下仅删除标识和配置文件相关数据，请按照任意顺序包含具有这三个值的`targetServices`： `identity`、`profile`和`ajo`。 明确包括Identity、Profile和AJO；排除数据湖。 在此模式下，`datasetId`必须为`ALL`（用例为完全配置文件删除，而不是按数据集片段）。

以下示例创建仅配置文件记录删除工作单：

```shell
curl -X POST \
  "https://platform.adobe.io/data/core/hygiene/workorder" \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
    "action": "delete_identity",
    "datasetId": "ALL",
    "displayName": "Profile-only delete for specified identity",
    "description": "Delete identity, profile, and AJO data only; datalake unchanged.",
    "targetServices": ["identity", "profile", "ajo"],
    "namespacesIdentities": [
      {
        "namespace": { "code": "email" },
        "ids": ["user@example.com"]
      }
    ]
  }'
```

多数据集或仅用于用户档案的请求的成功响应遵循与其他工作单响应相同的形状。 返回的`datasetId`和`targetServices`反映请求中的值（或忽略`targetServices`时的完整默认列表），因此您可以确认提交的内容。

>[!NOTE]
>
>记录删除工作单的操作属性当前在API响应中为`identity-delete`。 如果API更改为使用其他值（如`delete_identity`），则将相应地更新此文档。

## 将ID列表转换为JSON以用于记录删除请求(#convert-id-lists-to-json-for-record-delete-requests)

当您的标识符为CSV、TSV或TXT文件时，使用转换脚本为`/workorder`端点生成所需的JSON负载。 此方法在处理现有数据文件时特别有用。 有关现成的脚本和说明，请参阅[csv到数据卫生GitHub存储库](https://github.com/perlmonger42/csv-to-data-hygiene)。

脚本输出&#x200B;**`identities`**&#x200B;格式 — 每个具有`id`的对象一个`namespace`。 API按原样接受此格式；您可以直接在POST正文中将生成的JSON发送到`/workorder`，而无需进行转换。 建议的格式为&#x200B;**`namespacesIdentities`**；请参阅[创建记录删除工作单](#create)和[标识有效负荷格式](#identity-payload-format-identities-or-namespacesidentities)。

### 生成JSON负载

以下bash脚本示例演示了如何在Python或Ruby中运行转换脚本：

>[!BEGINTABS]

>[!TAB 运行Python脚本的示例]

```bash
#!/usr/bin/env bash

rm -rf ./output && mkdir output
for NAME in UTF8 CSV TSV TXT XYZ big; do
  ./csv-to-DI-payload.py sample/sample-$NAME.* \
      --verbose \
      --column 2 \
      --namespace email \
      --dataset-id 66f4161cc19b0f2aef3edf10 \
      --description 'a simple sample' \
      --output-dir output
  echo Checking output/sample-$NAME-*.json against expect/sample-$NAME-*.json
  diff <(cat output/sample-$NAME-*.json) <(cat expect/sample-$NAME-*.json) || echo Unexpected output in sample-$NAME-*.*
done
```

>[!TAB 运行Ruby脚本的示例]

```bash
#!/usr/bin/env bash

rm -rf ./output && mkdir output
for NAME in UTF8 CSV TSV TXT XYZ big; do
  ./csv-to-DI-payload.rb sample/sample-$NAME.* \
      --verbose \
      --column 2 \
      --namespace email \
      --dataset-id 66f4161cc19b0f2aef3edf10 \
      --description 'a simple sample' \
      --output-dir output
  echo Checking output/sample-$NAME-*.json against expect/sample-$NAME-*.json
  diff <(cat output/sample-$NAME-*.json) <(cat expect/sample-$NAME-*.json) || echo Unexpected output in sample-$NAME-*.*
done
```

>[!ENDTABS]

下表介绍了bash脚本中的参数。

| 参数 | 描述 |
| ---           | ---     |
| `verbose` | 启用详细输出。 |
| `column` | 包含要删除的标识值的列的索引（从1开始）或标头名称。 如果未指定，则默认为第一列。 |
| `namespace` | 传递给脚本的身份命名空间代码（例如，`email`）。 生成的JSON在每个对象的`namespace.code`属性中使用此属性。 |
| `dataset-id` | 数据集的唯一标识符：单个ID，多个数据集使用逗号分隔的ID，或所有数据集使用`ALL`。 |
| `description` | 记录删除工作单的描述。 |
| `output-dir` | 用于写入输出JSON有效负载的目录。 |

{style="table-layout:auto"}

以下示例展示了从CSV、TSV或TXT文件转换而来的成功JSON有效负载。 它包含与指定命名空间关联的记录，用于删除由电子邮件地址标识的记录。

```json
{
  "action": "delete_identity",
  "datasetId": "66f4161cc19b0f2aef3edf10",
  "displayName": "output/sample-big-001.json",
  "description": "a simple sample",
  "identities": [
    {
      "namespace": {
        "code": "email"
      },
      "id": "1"
    },
    {
      "namespace": {
        "code": "email"
      },
      "id": "2"
    }
  ]
}
```

下表介绍了JSON有效负载中的属性。

| 属性 | 描述 |
| ---          | ---     |
| `action` | 为记录删除工作单请求的操作。 转换脚本自动设置为`delete_identity`。 |
| `datasetId` | 数据集的唯一标识符：单个ID、逗号分隔的ID或`ALL`。 |
| `displayName` | 此记录删除工作单的人工可读标签。 |
| `description` | 记录删除工作单的描述。 |
| `identities` | 一个对象数组，每个对象包含：<br><ul><li> `namespace`：具有`code`属性的对象，该属性指定身份命名空间（例如，“email”）。</li><li> `id`：要删除此命名空间的身份值。</li></ul> |

{style="table-layout:auto"}

### 将生成的JSON数据提交到`/workorder`端点

脚本输出使用`identities`格式，API按原样接受该格式。 在将`-d` POST请求发送到`curl`端点时，使用转换的JSON有效负载作为请求正文(`/workorder`)。 有关完整的请求选项和验证规则，请参阅[创建记录删除工作单](#create)。

## 检索特定记录删除工作单的详细信息 {#lookup}

通过向`/workorder/{WORKORDER_ID}`发出GET请求，检索特定记录删除工作单的信息。 响应包括操作类型、状态、关联的数据集和用户信息以及审核元数据。

**API格式**

```http
GET /workorder/{WORKORDER_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{WORK_ORDER_ID}` | 您所查找的记录删除工作单的唯一标识符。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/DI-6fa98d52-7bd2-42a5-bf61-fb5c22ec9427 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回指定记录删除工作单的详细信息。

```json
{
  "workorderId": "DI-6fa98d52-7bd2-42a5-bf61-fb5c22ec9427",
  "orgId": "3C7F2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-dbe3ffad-cb0b-401f-91ae-01c189f8e7b2",
  "action": "identity-delete",
  "createdAt": "2037-01-21T08:25:45.119Z",
  "updatedAt": "2037-01-21T08:30:45.233Z",
  "operationCount": 3,
  "targetServices": [
    "ajo",
    "profile",
    "datalake",
    "identity"
  ],
  "status": "received",
  "createdBy": "g.baratheon@acme.com <g.baratheon@acme.com> C189F8E7B2@acme.com",
  "datasetId": "d2f1c8a4b8f747d0ba3521e2",
  "datasetName": "Acme_Marketing_Events",
  "displayName": "Marketing Identity Delete Request",
  "description": "Scheduled identity deletion for marketing compliance"
}
```

下表描述了响应中的属性。

| 属性 | 描述 |
| --- | --- |
| `workorderId` | 记录删除工作单的唯一标识符。 |
| `orgId` | 您组织的唯一标识符。 |
| `bundleId` | 包含此记录删除工作单的捆绑的唯一标识符。 捆绑功能允许下游服务将多个删除订单分组在一起进行处理。 |
| `action` | 记录删除工作单中请求的操作类型。 |
| `createdAt` | 创建工作单时的时间戳。 |
| `updatedAt` | 上次更新工作单的时间戳。 |
| `operationCount` | 工作单中包含的工序数。 |
| `targetServices` | 受此记录删除工作单影响的目标服务列表。 |
| `status` | 记录删除工作单的当前状态。 |
| `createdBy` | 创建记录删除工作单的用户的电子邮件和标识符。 |
| `datasetId` | 与工作单关联的数据集的唯一标识符（单个ID、逗号分隔的ID或`ALL`）。 |
| `datasetName` | 与工作单关联的数据集的名称。 |
| `displayName` | 记录删除工作单的人工可读标签。 |
| `description` | 记录删除工作单的描述。 |

## 更新记录删除工作单 {#update}

通过向`name`端点发出PUT请求，为记录删除工作单更新`description`和`/workorder/{WORKORDER_ID}`。

**API格式**

```http
PUT /workorder/{WORKORDER_ID}
```

下表描述了此请求的参数。

| 参数 | 描述 |
| --- | --- |
| `{WORK_ORDER_ID}` | 要更新的记录删除工作单的唯一标识符。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/workorder/DI-893a6b1d-47c2-41e1-b3f1-2d7c2956aabb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Updated Marketing Identity Delete Request",
        "description": "Updated deletion request for marketing data"
      }'
```

下表描述了可以更新的属性。

| 属性 | 描述 |
| --- | --- |
| `name` | 记录删除工作单的更新后的人类可读标签。 |
| `description` | 记录删除工作单的更新描述。 |

{style="table-layout:auto"}

**响应**

成功的响应会返回更新的工作单请求。

```json
{
  "workorderId": "DI-893a6b1d-47c2-41e1-b3f1-2d7c2956aabb",
  "orgId": "7D4E2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-12abcf45-32ea-45bc-9d1c-8e7b321cabc8",
  "action": "identity-delete",
  "createdAt": "2038-04-15T12:14:29.210Z",
  "updatedAt": "2038-04-15T12:30:29.442Z",
  "operationCount": 2,
  "targetServices": [
    "profile",
    "datalake"
  ],
  "status": "received",
  "createdBy": "b.tarth@acme.com <b.tarth@acme.com> 8E7B321CABC8@acme.com",
  "datasetId": "1a2b3c4d5e6f7890abcdef12",
  "datasetName": "Acme_Marketing_2024",
  "displayName": "Updated Marketing Identity Delete Request",
  "description": "Updated deletion request for marketing data",
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
| ---------------- | ----------------------------------------------------------------------------------------- |
| `workorderId` | 记录删除工作单的唯一标识符。 |
| `orgId` | 您组织的唯一标识符。 |
| `bundleId` | 包含此记录删除工作单的捆绑的唯一标识符。 捆绑功能允许下游服务将多个删除订单分组在一起进行处理。 |
| `action` | 记录删除工作单中请求的操作类型。 |
| `createdAt` | 创建工作单时的时间戳。 |
| `updatedAt` | 上次更新工作单的时间戳。 |
| `operationCount` | 工作单中包含的工序数。 |
| `targetServices` | 受此记录删除工作单影响的目标服务列表。 |
| `status` | 记录删除工作单的当前状态。 可能的值为： `received`、`validated`、`submitted`、`ingested`、`completed`和`failed`。 |
| `createdBy` | 创建记录删除工作单的用户的电子邮件和标识符。 |
| `datasetId` | 与记录删除工作单关联的数据集的唯一标识符（单个ID、逗号分隔的ID或`ALL`）。 |
| `datasetName` | 与记录删除工作单关联的数据集的名称。 |
| `displayName` | 记录删除工作单的人工可读标签。 |
| `description` | 记录删除工作单的描述。 |
| `productStatusDetails` | 列出请求下游进程的当前状态的数组。 每个对象包含：<ul><li>`productName`：下游服务的名称。</li><li>`productStatus`：下游服务的当前处理状态。</li><li>`createdAt`：服务发布最新状态时的时间戳。</li></ul>在将工作单提交到下游服务以开始处理之后，此属性可用。 |

{style="table-layout:auto"}
