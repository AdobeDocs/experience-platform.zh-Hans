---
keywords: Experience Platform；主页；热门主题；区段评估；分段服务；分段；评估区段；访问区段结果；评估和访问区段；
solution: Experience Platform
title: 评估和访问区段结果
topic-legacy: tutorial
type: Tutorial
description: 请阅读本教程，了解如何使用Adobe Experience Platform Segmentation Service API评估区段并访问区段结果。
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '1548'
ht-degree: 0%

---

# 评估和访问区段结果

本文档提供了有关使用[[!DNL Segmentation API]](../api/getting-started.md)评估区段和访问区段结果的教程。

## 快速入门

本教程需要对创建受众区段时涉及的各种[!DNL Adobe Experience Platform]服务有一定的了解。 在开始本教程之前，请查阅以下服务的文档：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据，实时提供统一的客户用户档案。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md):允许您根据数据构建受众 [!DNL Real-time Customer Profile] 区段。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):Platform用来组织客户体验数据的标准化框架。
- [沙盒](../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 必需标题

本教程还要求您完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功调用[!DNL Platform] API。 完成身份验证教程可为所有[!DNL Experience Platform] API调用中每个所需标头的值，如下所示：

- 授权：载体`{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

[!DNL Experience Platform]中的所有资源均与特定虚拟沙箱隔离。 对[!DNL Platform] API的请求需要一个标头来指定操作将在其中进行的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Platform]中沙箱的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

所有POST、PUT和PATCH请求都需要一个额外的标头：

- Content-Type:application/json

## 评估区段

开发、测试并保存区段定义后，您随后可以通过计划评估或按需评估来评估区段。

[计划评估](#scheduled-evaluation) （也称为“计划分段”）允许您创建在特定时间运行导出作业的定期计划，而按需评 [估](#on-demand-evaluation) 涉及创建区段作业以立即构建受众。下面概述了每个步骤的步骤。

如果您尚未使用分段API](./create-a-segment.md)教程完成[创建区段，或者使用[区段生成器](../ui/overview.md)创建区段定义，请在继续阅读本教程之前执行此操作。

## 计划评估 {#scheduled-evaluation}

通过计划评估，您的IMS组织可以创建循环计划以自动运行导出作业。

>[!NOTE]
>
>对于[!DNL XDM Individual Profile]最多包含五(5)个合并策略的沙箱，可启用计划评估。 如果贵组织在单个沙盒环境中有五个以上的[!DNL XDM Individual Profile]合并策略，您将无法使用计划评估。

### 创建计划

通过向`/config/schedules`端点发出POST请求，可以创建调度并包含应触发该调度的特定时间。

有关使用此端点的详细信息，请参阅[计划终结点指南](../api/schedules.md#create)

### 启用计划

默认情况下，创建计划时，该计划处于非活动状态，除非在创建(POST)请求正文中将`state`属性设置为`active`。 您可以通过向`/config/schedules`端点发出PATCH请求并在路径中包含调度的ID来启用调度（将`state`设置为`active`）。

有关使用此端点的详细信息，请参阅[计划终结点指南](../api/schedules.md#update-state)

### 更新计划时间

通过向`/config/schedules`端点发出PATCH请求并在路径中包含调度的ID，可以更新调度时间。

有关使用此端点的详细信息，请参阅[计划终结点指南](../api/schedules.md#update-schedule)

## 按需评估

按需评估允许您创建区段作业，以便根据需要生成受众区段。 与计划评估不同，只有在请求时才会执行此操作，而不会重复执行。

### 创建区段作业

区段作业是创建新受众区段的异步过程。 它引用了区段定义以及任何合并策略，这些策略控制[!DNL Real-time Customer Profile]如何在配置文件片段中合并重叠属性。 成功完成区段作业后，您可以收集有关该区段的各种信息，例如处理过程中可能发生的任何错误以及受众的最终大小。

您可以通过向[!DNL Real-time Customer Profile] API的`/segment/jobs`端点发出POST请求来创建新的区段作业。

有关使用此端点的详细信息，请参阅[segment jobs端点指南](../api/segment-jobs.md#create)


### 查找区段作业状态

您可以对特定区段作业使用`id`来执行查找请求(GET)，以查看作业的当前状态。

有关使用此端点的详细信息，请参阅[segment jobs端点指南](../api/segment-jobs.md#get)

## 解释区段结果

成功运行区段作业时，会为区段中包含的每个配置文件更新`segmentMembership`映射。 `segmentMembership` 此外，还会存储被摄取到中的任何预评估受众区段， [!DNL Platform]以便与其他解决方案（如）集 [!DNL Adobe Audience Manager]成。

以下示例显示了每个配置文件记录的`segmentMembership`属性的外观：

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

如果您知道要访问的特定配置文件，可以使用[!DNL Real-time Customer Profile] API执行此操作。 [使用配置文件API](../../profile/api/entities.md)教程访问实时客户配置文件数据中提供了访问各个配置文件的完整步骤。

## 导出区段 {#export}

成功完成分段作业后（`status`属性的值为“SUCCEEDED”），您可以将受众导出到可在其中访问并对其执行操作的数据集。

导出受众时需要执行以下步骤：

- [创建目标数据集](#create-a-target-dataset)  — 创建数据集以保留受众成员。
- [在数据集中生成受众配置文件](#generate-profiles-for-audience-members)  — 根据区段作业的结果，使用XDM个人配置文件填充数据集。
- [监视导出进度](#monitor-export-progress)  — 检查导出过程的当前进度。
- [读取受众数据](#next-steps)  — 检索表示受众成员的生成的XDM个人用户档案。

### 创建目标数据集

在导出受众时，必须首先创建目标数据集。 必须正确配置数据集，以确保成功导出。

其中一个关键注意事项是数据集所基于的架构（在下面的API示例请求中为`schemaRef.id`）。 要导出区段，数据集必须基于[!DNL XDM Individual Profile Union Schema](`https://ns.adobe.com/xdm/context/profile__union`)。 并集架构是系统生成的只读架构，用于聚合共享相同类的架构的字段（在本例中为XDM Indivial Profile类）。 有关并集视图架构的更多信息，请参阅架构注册开发人员指南](../../xdm/api/getting-started.md)的[实时客户配置文件部分。

有两种方法可创建必要的数据集：

- **使用API:** 本教程中遵循的步骤将简要介绍如何使用API创建引 [!DNL XDM Individual Profile Union Schema] 用的 [!DNL Catalog] 数据集。
- **使用UI:** 要使用用 [!DNL Adobe Experience Platform] 户界面创建引用并集架构的数据集，请按照UI教程中的步骤操作，然后返回本教程，以继续执行生成受众配置文 [件的步骤](../ui/overview.md)  [](#generate-xdm-profiles-for-audience-members)。

如果您已经有一个兼容的数据集并且知道其ID，则可以直接继续执行[生成受众配置文件](#generate-xdm-profiles-for-audience-members)的步骤。

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

拥有并集持久保留的数据集后，您可以创建一个导出作业，以将受众成员保留到数据集，方法是向[!DNL Real-time Customer Profile] API的`/export/jobs`端点发出POST请求，并提供要导出的区段的数据集ID和区段信息。

有关使用此端点的详细信息，请参阅[导出作业端点指南](../api/export-jobs.md#create)

### 监视导出进度

在导出作业进程中，您可以通过向`/export/jobs`端点发出GET请求并在路径中包含导出作业的`id`来监视其状态。 `status`字段返回值“SUCCEEDED”后，导出作业即完成。

有关使用此端点的详细信息，请参阅[导出作业端点指南](../api/export-jobs.md#get)

## 后续步骤

成功完成导出后，您的数据即可在[!DNL Experience Platform]的[!DNL Data Lake]中使用。 然后，可以使用[[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/)使用与导出关联的`batchId`访问数据。 根据区段的大小，数据可能以块为单位，并且批处理可能由多个文件组成。

有关如何使用[!DNL Data Access] API访问和下载批处理文件的分步说明，请参阅[数据访问教程](../../data-access/tutorials/dataset-data.md)。

您还可以使用[!DNL Adobe Experience Platform Query Service]访问已成功导出的区段数据。 [!DNL Query Service]使用UI或RESTful API，可以对[!DNL Data Lake]中的数据写入、验证和运行查询。

有关如何查询受众数据的更多信息，请查阅[[!DNL Query Service]](../../query-service/home.md)上的文档。
