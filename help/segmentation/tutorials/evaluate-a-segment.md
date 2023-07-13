---
solution: Experience Platform
title: 评估和访问区段结果
type: Tutorial
description: 阅读本教程，了解如何使用Adobe Experience Platform分段服务API评估区段定义并访问分段结果。
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 0%

---

# 评估和访问区段定义结果

本文档提供了一个教程，用于评估区段定义并使用访问这些结果。 [[!DNL Segmentation API]](../api/getting-started.md).

## 快速入门

本教程需要对各种 [!DNL Adobe Experience Platform] 创建受众时涉及的服务。 在开始本教程之前，请查看以下服务的文档：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个来源的汇总数据实时提供统一的客户用户档案。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md)：允许您从构建受众 [!DNL Real-Time Customer Profile] 数据。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：Platform用于组织客户体验数据的标准化框架。 为了更好地利用分段，请确保您的数据被摄取为用户档案和事件，并符合 [数据建模的最佳实践](../../xdm/schema/best-practices.md).
- [沙盒](../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

### 必需的标头

此外，本教程还要求您已完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功调用 [!DNL Platform] API。 完成身份验证教程将提供所有中所有所需标头的值 [!DNL Experience Platform] API调用，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定的虚拟沙盒隔离。 请求 [!DNL Platform] API需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信息 [!DNL Platform]，请参见 [沙盒概述文档](../../sandboxes/home.md).

所有POST、PUT和PATCH请求都需要额外的标头：

- Content-Type： application/json

## 评估区段定义 {#evaluate-a-segment}

在开发、测试和保存区段定义后，您可以通过计划评估或按需评估来评估区段定义。

[计划评估](#scheduled-evaluation) （也称为“计划分段”）允许您创建用于在特定时间运行导出作业的定期计划，而 [按需评估](#on-demand-evaluation) 涉及创建区段作业以立即构建受众。 下面概述了每种方法的步骤。

如果您尚未完成 [使用分段API创建区段定义](./create-a-segment.md) 教程或创建区段定义，使用 [区段生成器](../ui/overview.md)，请在继续阅读本教程之前完成此操作。

## 计划评估 {#scheduled-evaluation}

通过计划的评估，您的组织可以创建定期计划以自动运行导出作业。

>[!NOTE]
>
>可以为最多具有五(5)个合并策略的沙盒启用计划评估 [!DNL XDM Individual Profile]. 如果贵组织有五个以上的合并策略 [!DNL XDM Individual Profile] 在单个沙盒环境中，您将无法使用计划的评估。

### 创建计划

向发出POST请求 `/config/schedules` 端点，您可以创建一个计划并包括应触发该计划的特定时间。

有关使用此端点的更多详细信息，请参阅 [计划端点指南](../api/schedules.md#create)

### 启用计划

默认情况下，计划在创建时处于不活动状态，除非 `state` 属性设置为 `active` (POST)请求正文中的。 您可以启用计划(设置 `state` 到 `active`)向发出PATCH请求 `/config/schedules` 端点并在路径中包含计划的ID。

有关使用此端点的更多详细信息，请参阅 [计划端点指南](../api/schedules.md#update-state)

### 更新计划时间

可以通过向以下网站发出PATCH请求来更新时间表计时： `/config/schedules` 端点并在路径中包含计划的ID。

有关使用此端点的更多详细信息，请参阅 [计划端点指南](../api/schedules.md#update-schedule)

## 按需评估

按需评估允许您创建区段作业，以便在需要时生成受众。 与计划的评估不同，这仅在请求时发生，并且不是定期的。

### 创建区段作业

区段作业是一个异步过程，可根据需要创建受众区段。 它引用区段定义，以及控制区段划分方式的任何合并策略 [!DNL Real-Time Customer Profile] 合并配置文件片段中的重叠属性。 成功完成区段作业后，您可以收集有关区段定义的各种信息，例如处理过程中可能发生的任何错误以及最终的受众规模。 每次要刷新区段定义当前符合条件的受众时，都需要运行区段作业。

您可以通过向以下对象发出POST请求来创建新的区段作业： `/segment/jobs` 中的端点 [!DNL Real-Time Customer Profile] API。

有关使用此端点的更多详细信息，请参阅 [区段作业端点指南](../api/segment-jobs.md#create)

### 查找区段作业状态

您可以使用 `id` 执行查找请求(GET)的特定区段作业，以查看该作业的当前状态。

有关使用此端点的更多详细信息，请参阅 [区段作业端点指南](../api/segment-jobs.md#get)

## 解释区段作业结果

成功运行区段作业后， `segmentMembership` 区段定义中包含的每个配置文件都会更新映射。 `segmentMembership` 还会存储任何被摄取到的预评估受众 [!DNL Platform]，允许与其他解决方案集成，例如 [!DNL Adobe Audience Manager].

以下示例显示了 `segmentMembership` 属性的外观与每个个人资料记录相似：

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
>中的任何区段成员资格 `exited` 超过30天的状态，基于 `lastQualificationTime`，将被删除。

## 访问区段作业结果

可以通过以下两种方式之一访问区段作业的结果：可以访问单个用户档案，或将整个受众导出到数据集。

以下各节更详细地概述了这些选项。

## 查找配置文件

如果您知道要访问的特定用户档案，可以使用 [!DNL Real-Time Customer Profile] API。 有关访问各个用户档案的完整步骤，请参阅 [使用配置文件API访问实时客户配置文件数据](../../profile/api/entities.md) 教程。

## 导出区段 {#export}

成功完成分段作业后( `status` 属性为“SUCCEEDED”)，您可以将受众导出到可在其中进行访问和操作的数据集。

导出受众需要执行以下步骤：

- [创建目标数据集](#create-a-target-dataset)  — 创建数据集以保存受众成员。
- [在数据集中生成受众配置文件](#generate-profiles)  — 根据区段作业的结果使用XDM个人资料填充数据集。
- [监控导出进度](#monitor-export-progress)  — 检查导出过程的当前进度。
- [读取受众数据](#next-steps)  — 检索生成的XDM个人资料，这些个人资料表示受众的成员。

### 创建目标数据集 {#create-dataset}

导出受众时，必须首先创建目标数据集。 请务必正确配置数据集，以确保成功导出。

关键注意事项之一是数据集所基于的架构(`schemaRef.id` （在下面的API示例请求中）。 要导出区段定义，数据集必须基于 [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`)。 合并架构是系统生成的只读架构，它聚合共享同一类的架构的字段，在本例中是XDM Individual Profile类。 有关合并视图架构的更多信息，请参阅 [Schema Registry开发人员指南的Real-time Customer Profile部分](../../xdm/api/getting-started.md).

有两种方法可创建必要的数据集：

- **使用API：** 本教程中介绍的步骤概述了如何创建引用 [!DNL XDM Individual Profile Union Schema] 使用 [!DNL Catalog] API。
- **使用UI：** 要使用 [!DNL Adobe Experience Platform] 用户界面要创建引用合并架构的数据集，请按照 [用户界面教程](../ui/overview.md) 然后返回到本教程以继续执行以下步骤 [生成受众配置文件](#generate-profiles).

如果您已经有一个兼容的数据集并且知道其ID，则可以直接继续执行步骤 [生成受众配置文件](#generate-profiles).

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

POST拥有合并持久化数据集后，您可以创建一个导出作业，通过对 `/export/jobs` 中的端点 [!DNL Real-Time Customer Profile] API并提供要导出的区段定义的数据集ID和区段定义信息。

有关使用此端点的更多详细信息，请参阅 [导出作业端点指南](../api/export-jobs.md#create)

### 监控导出进度

导出作业进行时，您可以通过向以下对象发出GET请求来监控其状态： `/export/jobs` 端点并包括 `id` 路径中导出作业的ID。 导出作业在 `status` 字段返回值“SUCCEEDED”。

有关使用此端点的更多详细信息，请参阅 [导出作业端点指南](../api/export-jobs.md#get)

## 后续步骤

成功完成导出后，您的数据便可在 [!DNL Data Lake] 在 [!DNL Experience Platform]. 然后，您可以使用 [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) 以使用访问数据 `batchId` 与导出关联。 根据区段定义的大小，数据可能以块为单位，批量可能由多个文件组成。

有关如何使用 [!DNL Data Access] 访问和下载批处理文件的API，请按照 [数据访问教程](../../data-access/tutorials/dataset-data.md).

您还可以使用以下方式访问成功导出的区段定义数据 [!DNL Adobe Experience Platform Query Service]. 使用UI或RESTful API， [!DNL Query Service] 允许您编写、验证和运行 [!DNL Data Lake].

有关如何查询受众数据的更多信息，请查看以下文档： [[!DNL Query Service]](../../query-service/home.md).
