---
keywords: Experience Platform；主页；热门主题；区段评估；分段服务；分段；评估区段；访问区段结果；评估和访问区段；
solution: Experience Platform
title: 评估和访问区段结果
topic-legacy: tutorial
type: Tutorial
description: 请阅读本教程，了解如何使用Adobe Experience Platform Segmentation Service API评估区段并访问区段结果。
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: 885ebbcae223229f4614acd5b50266ea11bcf906
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 0%

---

# 评估和访问区段结果

本文档提供了一个教程，用于评估区段并使用 [[!DNL Segmentation API]](../api/getting-started.md).

## 快速入门

本教程需要对 [!DNL Adobe Experience Platform] 创建受众区段时涉及的服务。 在开始本教程之前，请查阅以下服务的文档：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据，实时提供统一的客户用户档案。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md):允许您从 [!DNL Real-time Customer Profile] 数据。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):Platform用来组织客户体验数据的标准化框架。 为了最好地利用分段，请确保根据 [数据建模最佳实践](../../xdm/schema/best-practices.md).
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

### 必需标题

本教程还要求您完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功调用 [!DNL Platform] API。 完成身份验证教程将为所有中每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有资源 [!DNL Experience Platform] 与特定虚拟沙箱隔离。 请求 [!DNL Platform] API需要一个标头来指定操作将在其中执行的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关 [!DNL Platform]，请参阅 [沙盒概述文档](../../sandboxes/home.md).

所有POST、PUT和PATCH请求都需要一个额外的标头：

- Content-Type:application/json

## 评估区段

开发、测试并保存区段定义后，您随后可以通过计划评估或按需评估来评估区段。

[计划评估](#scheduled-evaluation) （也称为“计划分段”）允许您创建在特定时间运行导出作业的定期计划，但 [按需评估](#on-demand-evaluation) 包括创建区段作业以立即构建受众。 下面概述了每个步骤的步骤。

如果您尚未完成 [使用分段API创建区段](./create-a-segment.md) 教程或使用 [区段生成器](../ui/overview.md)，请在继续阅读本教程之前执行此操作。

## 计划评估 {#scheduled-evaluation}

通过计划评估，您的IMS组织可以创建循环计划以自动运行导出作业。

>[!NOTE]
>
>对于最多五(5)个合并策略的沙箱，可以启用计划评估 [!DNL XDM Individual Profile]. 如果贵组织有五个以上的合并策略， [!DNL XDM Individual Profile] 在单个沙盒环境中，您将无法使用计划评估。

### 创建计划

通过向 `/config/schedules` 端点，您可以创建计划并包含应触发计划的特定时间。

有关使用此端点的更多详细信息，请参阅 [schedules endpoint guide](../api/schedules.md#create)

### 启用计划

默认情况下，计划在创建时处于不活动状态，除非 `state` 属性设置为 `active` (在创建(POST)请求正文中)。 您可以启用计划(设置 `state` to `active`)，方法是向 `/config/schedules` 端点，并在路径中包含调度的ID。

有关使用此端点的更多详细信息，请参阅 [schedules endpoint guide](../api/schedules.md#update-state)

### 更新计划时间

可以通过向 `/config/schedules` 端点，并在路径中包含调度的ID。

有关使用此端点的更多详细信息，请参阅 [schedules endpoint guide](../api/schedules.md#update-schedule)

## 按需评估

按需评估允许您创建区段作业，以便根据需要生成受众区段。 与计划评估不同，只有在请求时才会执行此操作，而不会重复执行。

### 创建区段作业

区段作业是一种异步流程，可根据需要创建受众区段。 它引用区段定义，以及控制如何 [!DNL Real-time Customer Profile] 合并配置文件片段中的重叠属性。 成功完成区段作业后，您可以收集有关该区段的各种信息，例如处理过程中可能发生的任何错误以及受众的最终大小。 每次要刷新当前符合区段定义条件的受众时，都需要运行区段作业。

您可以通过向 `/segment/jobs` 的端点 [!DNL Real-time Customer Profile] API。

有关使用此端点的更多详细信息，请参阅 [segment jobs endpoint wide](../api/segment-jobs.md#create)

### 查找区段作业状态

您可以使用 `id` 用于特定区段作业以执行查找请求(GET)，以查看作业的当前状态。

有关使用此端点的更多详细信息，请参阅 [segment jobs endpoint wide](../api/segment-jobs.md#get)

## 解释区段结果

成功运行区段作业时， `segmentMembership` 该区段中包含的每个用户档案的地图都会更新。 `segmentMembership` 还会存储被摄取到的任何预评估受众区段 [!DNL Platform]，允许与其他解决方案(如 [!DNL Adobe Audience Manager].

以下示例显示了 `segmentMembership` 属性与每个个人配置文件记录类似：

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "existing"
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
| `lastQualificationTime` | 断言区段成员资格以及进入或退出区段的用户档案的时间戳。 |
| `status` | 作为当前请求一部分的区段参与状态。 必须等于以下已知值之一： <ul><li>`existing`:实体继续在分部中。</li><li>`realized`:实体正在输入区段。</li><li>`exited`:实体正在退出区段。</li></ul> |

## 访问区段结果

可以通过以下两种方式之一访问区段作业的结果：您可以访问单个用户档案或将整个受众导出到数据集。

以下各节将更详细地介绍这些选项。

## 查找用户档案

如果您知道要访问的特定用户档案，可以使用 [!DNL Real-time Customer Profile] API。 有关访问各个用户档案的完整步骤，请参阅 [使用用户档案API访问实时客户档案数据](../../profile/api/entities.md) 教程。

## 导出区段 {#export}

成功完成分段作业后( `status` 属性为“成功”)，则可以将受众导出到可在其中访问并执行操作的数据集。

导出受众时需要执行以下步骤：

- [创建目标数据集](#create-a-target-dataset)  — 创建数据集以保存受众成员。
- [在数据集中生成受众配置文件](#generate-profiles)  — 根据区段作业的结果，使用XDM个人用户档案填充数据集。
- [监视导出进度](#monitor-export-progress)  — 检查导出过程的当前进度。
- [读取受众数据](#next-steps)  — 检索表示受众成员的生成的XDM个人用户档案。

### 创建目标数据集 {#create-dataset}

在导出受众时，必须首先创建目标数据集。 必须正确配置数据集，以确保成功导出。

其中一个关键注意事项是数据集所基于的架构(`schemaRef.id` （在下面的API示例请求中）。 要导出区段，数据集必须基于 [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`)。 并集架构是系统生成的只读架构，用于聚合共享相同类的架构的字段（在本例中为XDM Indivial Profile类）。 有关并集视图架构的更多信息，请参阅 [架构注册开发人员指南的“实时客户资料”部分](../../xdm/api/getting-started.md).

有两种方法可创建必要的数据集：

- **使用API:** 本教程中遵循的步骤将简要介绍如何创建引用 [!DNL XDM Individual Profile Union Schema] 使用 [!DNL Catalog] API。
- **使用UI:** 使用 [!DNL Adobe Experience Platform] 用户界面以创建引用并集模式的数据集，请按照 [UI教程](../ui/overview.md) ，然后返回到本教程以继续执行 [生成受众用户档案](#generate-profiles).

如果您已经有一个兼容的数据集并且知道其ID，则可以直接继续执行的步骤 [生成受众用户档案](#generate-profiles).

**API格式**

```http
POST /dataSets
```

**请求**

以下请求会创建一个新数据集，并在有效负载中提供配置参数。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `schemaRef.id` | 数据集将与之关联的并集视图（架构）的ID。 |

**响应**

成功的响应会返回一个数组，其中包含新创建数据集的只读、系统生成的唯一ID。 要成功导出受众成员，需要正确配置的数据集ID。

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 为受众成员生成用户档案 {#generate-profiles}

在您拥有一个并行保留的数据集后，可以创建一个导出作业，通过向 `/export/jobs` 的端点 [!DNL Real-time Customer Profile] API和提供要导出的区段的数据集ID和区段信息。

有关使用此端点的更多详细信息，请参阅 [导出作业端点指南](../api/export-jobs.md#create)

### 监视导出进度

在导出作业流程中，您可以通过向 `/export/jobs` 端点和包含 `id` 中的导出作业。 导出作业在 `status` 字段会返回值“SUCCEEDED”。

有关使用此端点的更多详细信息，请参阅 [导出作业端点指南](../api/export-jobs.md#get)

## 后续步骤

成功完成导出后，您的数据即可在 [!DNL Data Lake] in [!DNL Experience Platform]. 然后，您可以使用 [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) 使用 `batchId` 与导出关联。 根据区段的大小，数据可能以块为单位，并且批处理可能由多个文件组成。

有关如何使用的分步说明 [!DNL Data Access] 用于访问和下载批处理文件的API，请按照 [数据访问教程](../../data-access/tutorials/dataset-data.md).

您还可以使用 [!DNL Adobe Experience Platform Query Service]. 使用UI或RESTful API， [!DNL Query Service] 允许您在 [!DNL Data Lake].

有关如何查询受众数据的更多信息，请参阅 [[!DNL Query Service]](../../query-service/home.md).
