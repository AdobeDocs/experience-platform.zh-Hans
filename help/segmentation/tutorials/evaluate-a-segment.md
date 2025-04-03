---
solution: Experience Platform
title: 评估和访问区段结果
type: Tutorial
description: 阅读本教程，了解如何使用Adobe Experience Platform分段服务API评估区段定义并访问分段结果。
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '1594'
ht-degree: 1%

---

# 评估和访问区段定义结果

此文档提供了一个教程，用于评估区段定义并使用[[!DNL Segmentation API]](../api/getting-started.md)访问这些结果。

## 快速入门

本教程需要对创建受众中涉及的各种[!DNL Adobe Experience Platform]服务有一定的了解。 在开始本教程之前，请查看以下服务的文档：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个源的汇总数据，实时提供统一的客户个人资料。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md)：允许您从[!DNL Real-Time Customer Profile]数据构建受众。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： Platform用于组织客户体验数据的标准化框架。 为了更好地利用分段，请确保根据用于数据建模的[最佳实践](../../xdm/schema/best-practices.md)，将您的数据作为配置文件和事件摄取。
- [沙盒](../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 必需的标头

本教程还要求您完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功调用[!DNL Experience Platform] API。 完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

- 授权：持有人`{ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有资源都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的请求需要一个标头，该标头指定将在其中执行操作的沙盒的名称：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Experience Platform]中沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

所有POST、PUT和PATCH请求都需要额外的标头：

- Content-Type： application/json

## 评估区段定义 {#evaluate-a-segment}

开发、测试和保存区段定义后，您可以通过计划评估或按需评估来评估区段定义。

[计划评估](#scheduled-evaluation)（也称为“计划分段”）允许您创建在特定时间运行导出作业的定期计划，而[按需评估](#on-demand-evaluation)涉及创建区段作业以立即构建受众。 下面概述了每种方法的步骤。

如果您尚未完成[使用分段API](./create-a-segment.md)教程创建区段定义，或使用[区段生成器](../ui/segment-builder.md)创建区段定义，请先完成这些操作，然后再继续阅读本教程。

## 计划的评估 {#scheduled-evaluation}

通过计划的评估，您的组织可以创建定期计划以自动运行导出作业。

>[!NOTE]
>
>可以为[!DNL XDM Individual Profile]最多有五(5)个合并策略的沙盒启用计划评估。 如果贵组织在单个沙盒环境中为[!DNL XDM Individual Profile]提供了五个以上的合并策略，您将无法使用计划的评估。

### 创建计划

通过向`/config/schedules`端点发出POST请求，您可以创建计划并包含应触发该计划的特定时间。

有关使用此端点的更多详细信息，请参阅[计划端点指南](../api/schedules.md#create)

### 启用计划

默认情况下，创建计划时处于非活动状态，除非在创建(POST)请求正文中将`state`属性设置为`active`。 您可以通过向`/config/schedules`端点发出PATCH请求并在路径中包含计划的ID来启用计划（将`state`设置为`active`）。

有关使用此端点的更多详细信息，请参阅[计划端点指南](../api/schedules.md#update-state)

### 更新计划时间

通过向`/config/schedules`端点发出PATCH请求并在路径中包含计划的ID，可以更新计划计时。

有关使用此端点的更多详细信息，请参阅[计划端点指南](../api/schedules.md#update-schedule)

## 按需评估

按需评估允许您创建区段作业，以便在需要时生成受众。 与计划的评估不同，仅在请求时才会发生此情况，并且不会重复发生。

### 创建区段作业

区段作业是一个异步过程，可按需创建受众区段。 它引用区段定义以及控制[!DNL Real-Time Customer Profile]如何在您的配置文件片段中合并重叠属性的任何合并策略。 成功完成区段作业后，您可以收集有关区段定义的各种信息，例如处理期间可能发生的任何错误以及最终的受众规模。 每次要刷新区段定义当前符合条件的受众时，都需要运行区段作业。

您可以通过向[!DNL Real-Time Customer Profile] API中的`/segment/jobs`端点发出POST请求来创建新的区段作业。

有关使用此端点的更多详细信息可在[区段作业端点指南](../api/segment-jobs.md#create)中找到

### 查找区段作业状态

您可以对特定区段作业使用`id`来执行查找请求(GET)以查看作业的当前状态。

有关使用此端点的更多详细信息可在[区段作业端点指南](../api/segment-jobs.md#get)中找到

## 解释区段作业结果

成功运行区段作业后，将为区段定义中包含的每个配置文件更新`segmentMembership`映射。 `segmentMembership`还存储了提取到[!DNL Experience Platform]中的任何预评估受众，从而允许与其他解决方案（如[!DNL Adobe Audience Manager]）集成。

以下示例显示了`segmentMembership`属性对于每个个人资料记录的外观：

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `lastQualificationTime` | 进行区段成员资格断言以及用户档案输入或退出区段定义时的时间戳。 |
| `status` | 作为当前请求一部分的区段定义的参与状态。 必须等于以下已知值之一： <ul><li>`realized`：实体符合区段定义的条件。</li><li>`exited`：实体正在退出区段定义。</li></ul> |

>[!NOTE]
>
>任何基于`lastQualificationTime`且处于`exited`状态超过30天的区段成员资格都将被删除。

## 访问区段作业结果

可以通过以下两种方式之一访问区段作业的结果：访问各个用户档案或将整个受众导出到数据集。

以下各节更详细地概述了这些选项。

## 查找配置文件

如果您知道要访问的特定配置文件，则可以使用[!DNL Real-Time Customer Profile] API来访问。 在[使用配置文件API访问实时客户配置文件数据](../../profile/api/entities.md)教程中提供了访问各个配置文件的完整步骤。

## 导出区段 {#export}

成功完成分段作业后（`status`属性的值为“SUCCEEDED”），您可以将受众导出到可在其中访问和操作的数据集。

导出受众需要执行以下步骤：

- [创建目标数据集](#create-a-target-dataset) — 创建数据集以保存受众成员。
- [在数据集内生成受众配置文件](#generate-profiles) — 根据区段作业的结果使用XDM个人配置文件填充数据集。
- [监视导出进度](#monitor-export-progress) — 检查导出进程的当前进度。
- [读取受众数据](#next-steps) — 检索代表受众成员的生成XDM个人配置文件。

### 创建目标数据集 {#create-dataset}

导出受众时，必须首先创建目标数据集。 请务必正确配置数据集以确保成功导出。

关键注意事项之一是数据集所基于的架构（以下API示例请求中的`schemaRef.id`）。 为了导出区段定义，数据集必须基于[!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`)。 合并架构是一个系统生成的只读架构，它聚合了共享同一类（在本例中是XDM个人资料类）的架构字段。 有关合并视图架构的详细信息，请参阅架构注册表开发人员指南](../../xdm/api/getting-started.md)的[实时客户配置文件部分。

有两种方法可创建必要的数据集：

- **使用API：**&#x200B;本教程中接下来的步骤概述了如何使用[!DNL Catalog] API创建引用[!DNL XDM Individual Profile Union Schema]的数据集。
- **使用UI：**&#x200B;要使用[!DNL Adobe Experience Platform]用户界面创建引用合并架构的数据集，请按照[UI教程](../ui/overview.md)中的步骤操作，然后返回本教程以继续执行[生成受众配置文件](#generate-profiles)的步骤。

如果您已经具有兼容的数据集并且知道其ID，则可以直接进入[生成受众配置文件](#generate-profiles)的步骤。

**API格式**

```http
POST /dataSets
```

**请求**

以下请求创建一个新数据集，在有效负载中提供配置参数。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 数据集的描述性名称。 |
| `schemaRef.id` | 数据集将关联的合并视图（架构）的ID。 |

**响应**

成功的响应会返回一个数组，其中包含新创建的数据集的系统生成的只读ID。 需要正确配置的数据集ID才能成功导出受众成员。

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 为受众成员生成配置文件 {#generate-profiles}

拥有一个合并持久化数据集后，您可以创建一个导出作业以将受众成员持久化到该数据集，具体方法是：对[!DNL Real-Time Customer Profile] API中的`/export/jobs`端点发起POST请求，并为要导出的区段定义提供数据集ID和区段定义信息。

有关使用此端点的更多详细信息，请参阅[导出作业端点指南](../api/export-jobs.md#create)

### 监控导出进度

导出作业处理时，您可以通过向`/export/jobs`端点发出GET请求并在路径中包含导出作业的`id`来监视其状态。 一旦`status`字段返回值“SUCCEEDED”，导出作业即完成。

有关使用此端点的更多详细信息，请参阅[导出作业端点指南](../api/export-jobs.md#get)

## 后续步骤

成功完成导出后，您的数据将在[!DNL Experience Platform]的[!DNL Data Lake]内可用。 然后，您可以使用[[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/)，通过与导出关联的`batchId`来访问数据。 根据区段定义的大小，数据可能以块为单位，并且批处理可能包含多个文件。

有关如何使用[!DNL Data Access] API访问和下载批处理文件的分步说明，请按照[数据访问教程](../../data-access/tutorials/dataset-data.md)操作。

您还可以使用[!DNL Adobe Experience Platform Query Service]访问已成功导出的区段定义数据。 使用UI或RESTful API，[!DNL Query Service]允许您对[!DNL Data Lake]中的数据写入、验证和运行查询。

有关如何查询受众数据的更多信息，请查阅[[!DNL Query Service]](../../query-service/home.md)上的文档。
