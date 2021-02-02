---
keywords: Experience Platform；主题；热门话题；区段评价；分段服务；分段；分段；评价区段；访问区段结果；评价和访问区段；
solution: Experience Platform
title: 评估区段
topic: tutorial
type: Tutorial
description: 本文档提供了一个教程，用于使用分段API评估区段和访问区段结果。
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '1560'
ht-degree: 0%

---


# 评估和访问区段结果

本文档提供了使用[[!DNL Segmentation API]](../api/getting-started.md)评估区段和访问区段结果的教程。

## 入门指南

本教程需要对创建受众段时涉及的各种[!DNL Adobe Experience Platform]服务进行有效的了解。 在开始本教程之前，请查看以下服务的相关文档：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据，实时提供统一的客户用户档案。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md):允许您根据数据构建受众 [!DNL Real-time Customer Profile] 细分。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):平台组织客户体验数据的标准化框架。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

### 所需的标题

本教程还要求您完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)，以成功调用[!DNL Platform] API。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

- 授权：载体`{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有资源都隔离到特定虚拟沙箱。 对[!DNL Platform] API的请求需要一个标头，它指定操作将在中进行的沙箱的名称：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Platform]中沙箱的详细信息，请参阅[沙箱概述文档](../../sandboxes/home.md)。

所有POST、PUT和PATCH请求都需要额外的标题：

- 内容类型：application/json

## 评估区段

开发、测试和保存区段定义后，您便可以通过计划评估或按需评估来评估区段。

[计划评估](#scheduled-evaluation) （也称为“计划分段”）允许您创建在特定时间运行导出作业的循环计划，而 [按需](#on-demand-evaluation) 评估涉及创建区段作业以立即构建受众。下面列出了每个步骤。

如果您尚未使用分段API](./create-a-segment.md)教程完成[创建段，或使用[段生成器](../ui/overview.md)创建段定义，请在继续本教程之前执行此操作。

## 计划评估{#scheduled-evaluation}

通过计划的评估，您的IMS组织可以创建循环计划以自动运行导出作业。

>[!NOTE]
>
>对于[!DNL XDM Individual Profile]具有最多五(5)个合并策略的沙箱，可启用计划评估。 如果您的组织在单个沙箱环境内有[!DNL XDM Individual Profile]的五个以上合并策略，您将无法使用计划的评估。

### 创建计划

通过向`/config/schedules`端点发出POST请求，可以创建计划并包含应触发计划的特定时间。

有关使用此端点的详细信息，请参阅[计划端点指南](../api/schedules.md#create)

### 启用计划

默认情况下，创建计划时，POST处于非活动状态，除非在create()请求主体中将`state`属性设置为`active`。 您可以通过向`/config/schedules`端点发出计划请求并在路径中包含计划的ID来启用PATCH（将`state`设置为`active`）。

有关使用此端点的详细信息，请参阅[计划端点指南](../api/schedules.md#update-state)

### 更新计划时间

计划时间可以通过向`/config/schedules`端点发出PATCH请求并在路径中包含计划的ID来更新。

有关使用此端点的详细信息，请参阅[计划端点指南](../api/schedules.md#update-schedule)

## 按需评估

按需评估允许您创建区段作业，以便根据需要生成受众区段。 与计划评估不同，仅当请求时才会发生，且不再重复。

### 创建区段作业

段作业是创建新受众段的异步进程。 它引用区段定义，以及控制[!DNL Real-time Customer Profile]如何在用户档案片段中合并重叠属性的任何合并策略。 当区段作业成功完成时，您可以收集有关区段的各种信息，如处理过程中可能发生的任何错误以及受众的最终大小。

您可以通过向[!DNL Real-time Customer Profile] API中的`/segment/jobs`端点发出POST请求来创建新的段作业。

有关使用此端点的详细信息，请参阅[段作业端点指南](../api/segment-jobs.md#create)


### 查找区段作业状态

您可以使用特定段作业的`id`执行查找请求(GET)，以视图作业的当前状态。

有关使用此端点的详细信息，请参阅[段作业端点指南](../api/segment-jobs.md#get)

## 解释区段结果

成功运行段作业时，`segmentMembership`映射会针对段中包含的每个用户档案进行更新。 `segmentMembership` 还存储任何已引入的预评估受众细分， [!DNL Platform]允许与其他解决方案(如 [!DNL Adobe Audience Manager]:

以下示例显示每个用户档案记录的`segmentMembership`属性的外观：

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
| `lastQualificationTime` | 断言区段成员身份和用户档案进入或退出区段的时间戳。 |
| `status` | 作为当前请求一部分的区段参与状态。 必须等于以下已知值之一： <ul><li>`existing`:实体继续在分部中。</li><li>`realized`:实体正在输入区段。</li><li>`exited`:实体正在退出区段。</li></ul> |

## 访问区段结果

区段作业的结果可通过以下两种方式之一进行访问：您可以访问单个用户档案或将整个受众导出到数据集。

以下各节将更详细地介绍这些选项。

## 查找用户档案

如果您知道要访问的特定用户档案，可以使用[!DNL Real-time Customer Profile] API进行访问。 [使用用户档案API](../../profile/api/entities.md)教程访问实时客户用户档案数据中提供了访问各个用户档案的完整步骤。

## 导出区段{#export}

分段作业成功完成后（`status`属性的值为“SUCCEEDED”），您可以将受众导出到数据集，在该数据集中可以访问并执行操作。

导出受众需要执行以下步骤：

- [创建目标数据集](#create-a-target-dataset) -创建数据集以容纳受众成员。
- [在数据集中生成受众用户档案](#generate-profiles-for-audience-members) -根据区段作业的结果，用XDM单个用户档案填充数据集。
- [监视导出进度](#monitor-export-progress) -检查导出过程的当前进度。
- [读取受众](#next-steps) -检索表示受众成员的结果XDM单个用户档案。

### 创建目标数据集

导出受众时，必须先创建目标数据集。 必须正确配置数据集以确保导出成功。

一个主要考虑事项是数据集所基于的模式（`schemaRef.id`在下面的API示例请求中）。 要导出区段，数据集必须基于[!DNL XDM Individual Profile Union Schema](`https://ns.adobe.com/xdm/context/profile__union`)。 合并模式是系统生成的只读模式，它聚合共享同一类的模式的字段，在本例中为XDM个人用户档案类。 有关合并视图模式的详细信息，请参阅模式注册开发人员指南](../../xdm/api/getting-started.md)的[实时客户用户档案部分。

有两种方法可创建必需的数据集：

- **使用API:** 本教程中接下来的步骤概述了如何创建使用API引 [!DNL XDM Individual Profile Union Schema] 用的 [!DNL Catalog] 数据集。
- **使用UI：要** 使用 [!DNL Adobe Experience Platform] 用户界面创建引用合并模式的数据集，请按照UI教程中的 [步](../ui/overview.md) 骤操作，然后返回本教程，继续执行生成受众用户档案 [的步骤](#generate-xdm-profiles-for-audience-members)。

如果您已经有一个兼容的数据集并且知道其ID，则可以直接继续执行[生成受众用户档案](#generate-xdm-profiles-for-audience-members)的步骤。

**API格式**

```http
POST /dataSets
```

**请求**

以下请求将创建新数据集，在有效负荷中提供配置参数。

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
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 数据集的描述性名称。 |
| `schemaRef.id` | 合并集将与之关联的视图(模式)的ID。 |
| `fileDescription.persisted` | 一个布尔值，当设置为`true`时，它使数据集能够保留在合并视图中。 |

**响应**

成功的响应会返回一个数组，其中包含新创建数据集的只读、系统生成的唯一ID。 要成功导出受众成员，需要正确配置的数据集ID。

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 为受众成员{#generate-profiles}生成用户档案

一旦有合并持久数据集，您就可以创建一个导出作业，通过向[!DNL Real-time Customer Profile] API中的`/export/jobs`端点发出POST请求并提供要导出的区段的数据集ID和区段信息，将受众成员保留到数据集。

有关使用此端点的详细信息，请参阅[导出作业端点指南](../api/export-jobs.md#create)

### 监视导出进度

作为导出作业进程，您可以通过向`/export/jobs`端点发出GET请求并在路径中包含导出作业的`id`来监视其状态。 `status`字段返回值“SUCCEEDED”后，导出作业即完成。

有关使用此端点的详细信息，请参阅[导出作业端点指南](../api/export-jobs.md#get)

## 后续步骤

成功完成导出后，您的数据便可在[!DNL Experience Platform]的[!DNL Data Lake]中使用。 然后，您可以使用与导出相关的`batchId`访问数据。 [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)根据区段的大小，数据可能以块为单位，而批可能由多个文件组成。

有关如何使用[!DNL Data Access] API访问和下载批处理文件的分步说明，请按照[数据访问教程](../../data-access/tutorials/dataset-data.md)进行操作。

您还可以使用[!DNL Adobe Experience Platform Query Service]访问成功导出的段数据。 [!DNL Query Service]使用UI或RESTful API，可以对[!DNL Data Lake]中的数据写入、验证和运行查询。

有关如何查询受众数据的更多信息，请查阅有关[[!DNL Query Service]](../../query-service/home.md)的文档。
