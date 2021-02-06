---
keywords: Experience Platform；主题；热门主题；区段；区段；创建区段；分段；创建区段；分段服务；
solution: Experience Platform
title: 使用Segmentation Service API创建区段
topic: tutorial
type: Tutorial
description: 按照本教程学习如何使用Adobe Experience Platform分段服务API开发、测试、预览和保存段定义。
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---


# 使用Segmentation Service API创建区段

本文档提供了使用[[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md)开发、测试、预览和保存段定义的教程。

有关如何使用用户界面构建区段的信息，请参阅[区段生成器指南](../ui/overview.md)。

## 入门指南

本教程需要对创建受众段时涉及的各种[!DNL Adobe Experience Platform]服务进行有效的了解。 在开始本教程之前，请查看以下服务的相关文档：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md):允许您根据实时受众数据构建用户档案细分。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):组织客户体验数 [!DNL Platform] 据的标准化框架。

以下各节提供了成功调用[!DNL Platform] API所需了解的其他信息。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参见[!DNL Experience Platform]疑难解答指南中关于如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的一节。[

### 收集所需标题的值

要调用[!DNL Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

- 授权：载体`{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有资源都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Platform]中沙箱的详细信息，请参阅[沙箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要附加标头：

- 内容类型：application/json

## 开发细分定义

分段的第一步是定义分段，在称为段定义的构造中表示。 段定义是封装写入[!DNL Profile Query Language](PQL)的查询的对象。 此对象也称为PQL谓词。 PQL谓词根据与提供给[!DNL Real-time Customer Profile]的任何记录或时间序列数据相关的条件定义段规则。 有关编写PQL查询的详细信息，请参阅[ PQL指南](../pql/overview.md)。

您可以通过向[!DNL Segmentation] API中的`/segment/definitions`端点发出POST请求来创建新的段定义。 以下示例概述了如何设置定义请求的格式，包括成功定义区段所需的信息。

有关如何定义区段的详细说明，请阅读[区段定义开发人员指南](../api/segment-definitions.md#create)。

## 估计和预览受众{#estimate-and-preview-an-audience}

在开发细分定义时，您可以使用[!DNL Real-time Customer Profile]中的估计和预览工具来视图摘要级别信息，以帮助确保隔离预期受众。 估计提供有关细分定义的统计信息，如预测受众大小和置信区间。 预览为区段定义提供符合条件的列表的分页用户档案，允许您将结果与预期进行比较。

通过评估和预览受众，您可以测试和优化PQL谓词，直到它们产生可预期的结果，然后在更新的段定义中使用它们。

预览或获取区段估计需要执行两个步骤：

1. [创建预览作业](#create-a-preview-job)
2. [视图估](#view-an-estimate-or-preview) 计或使用预览作业的ID进行预览

### 估计的生成方式

数据样本用于评估区段和估计符合条件的用户档案数。 每天早晨，新数据将加载到内存中（在12AM-2AM PT之间，即7-9AM UTC），所有分段查询都使用当天的样本数据进行估计。 因此，所添加的任何新字段或所收集的其他数据都将反映在次日的估计中。

样本大小取决于用户档案存储中的实体总数。 下表显示了这些示例大小：

| 用户档案商店中的实体 | 样本大小 |
| ------------------------- | ----------- |
| 不到100万 | 完整数据集 |
| 1000万到2000万 | 100万 |
| 2000多万 | 总共5% |

估计通常在10到15秒之间，从粗略估计开始，随着读取更多记录，会进行优化。

### 创建预览作业

可以通过向`/preview`端点发出预览请求来创建新POST作业。

有关创建预览作业的详细说明，请参阅[预览和估计端点指南](../api/previews-and-estimates.md#create-preview)。

### 视图估计或预览

评估和预览过程以异步方式运行，因为不同的查询可能需要不同的时间来完成。 启动查询后，您可以使用API调用来检索(GET)评估或预览的当前状态（当它进行时）。

使用[!DNL Segmentation Service] API，您可以通过预览作业的ID查找该作业的当前状态。 如果状态为“RESULT_READY”，则可以视图结果。 要查找预览作业的当前状态，请阅读预览和估计端点指南中关于[检索预览作业部分](../api/previews-and-estimates.md#get-preview)的部分。 要查找估计作业的当前状态，请阅读预览和估计终结点指南中[检索估计作业](../api/previews-and-estimates.md#get-estimate)一节。


## 后续步骤

开发、测试和保存区段定义后，您可以创建区段作业，以使用[!DNL Segmentation Service] API构建受众。 有关如何完成此操作的详细步骤，请参见教程中的[评估和访问区段结果](./evaluate-a-segment.md)。