---
keywords: Experience Platform；主页；热门主题；区段；区段；创建区段；分段；创建区段；分段服务；
solution: Experience Platform
title: 使用分段服务API创建区段
topic-legacy: tutorial
type: Tutorial
description: 请阅读本教程，了解如何使用Adobe Experience Platform Segmentation Service API开发、测试、预览和保存区段定义。
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---

# 使用Segmentation Service API创建区段

本文档提供了使用 [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

有关如何使用用户界面构建区段的信息，请参阅 [区段生成器指南](../ui/overview.md).

## 快速入门

本教程需要对 [!DNL Adobe Experience Platform] 创建受众区段时涉及的服务。 在开始本教程之前，请查阅以下服务的文档：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md):允许您根据实时客户资料数据构建受众区段。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):标准化框架， [!DNL Platform] 组织客户体验数据。 为了最好地利用分段，请确保根据 [数据建模最佳实践](../../xdm/schema/best-practices.md).

以下部分提供了成功调用所需了解的其他信息 [!DNL Platform] API。

### 读取示例API调用

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有中每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定操作将在其中执行的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关 [!DNL Platform]，请参阅 [沙盒概述文档](../../sandboxes/home.md).

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的标头：

- Content-Type:application/json

## 开发区段定义

分段的第一步是定义区段，在称为区段定义的结构中表示。 区段定义是封装在中写入的查询的对象 [!DNL Profile Query Language] (PQL)。 此对象也称为PQL谓词。 PQL谓词根据与您提供给的任何记录或时间序列数据相关的条件定义区段规则 [!DNL Real-time Customer Profile]. 请参阅 [PQL指南](../pql/overview.md) 有关编写PQL查询的更多信息。

您可以通过向 `/segment/definitions` 的端点 [!DNL Segmentation] API。 以下示例概述了如何设置定义请求的格式，包括为成功定义区段需要哪些信息。

有关如何定义区段的详细说明，请阅读 [区段定义开发人员指南](../api/segment-definitions.md#create).

## 评估和预览受众 {#estimate-and-preview-an-audience}

在开发区段定义时，您可以在 [!DNL Real-time Customer Profile] 查看摘要级别的信息，以帮助确保隔离预期受众。 估计可提供有关区段定义的统计信息，如预计受众规模和置信区间。 “预览”为区段定义提供符合条件的用户档案的分页列表，允许您将结果与预期结果进行比较。

通过估算和预览受众，您可以测试和优化PQL谓词，直到它们产生所需的结果为止，然后在更新的区段定义中使用它们。

要预览或获取区段的估计值，需要执行两个步骤：

1. [创建预览作业](#create-a-preview-job)
2. [查看预估或预览](#view-an-estimate-or-preview) 使用预览作业的ID

### 如何生成估计

数据示例用于评估区段并估计符合条件的用户档案数量。 每天早晨，新数据都会加载到内存中（在12AM-2AM PT之间，即7-9AM UTC），并且所有分段查询都会使用当天的样本数据进行估计。 因此，所添加的任何新字段或收集的其他数据都将反映在次日的估计中。

样本大小取决于配置文件存储中的实体总数。 下表显示了这些样本大小：

| 配置文件存储中的实体 | 示例大小 |
| ------------------------- | ----------- |
| 不到100万 | 完整数据集 |
| 1到2000万 | 100万 |
| 2000多万 | 总共5% |

估计值通常在10-15秒之内，从粗略估计开始，随着读取更多记录而优化。

### 创建预览作业

您可以通过向 `/preview` 端点。

有关创建预览作业的详细说明，请参阅 [预览和估计端点指南](../api/previews-and-estimates.md#create-preview).

### 查看预估或预览

评估和预览进程以异步方式运行，因为不同的查询可能需要不同的时间才能完成。 启动查询后，您可以使用API调用在查询继续过程中检索(GET)估计或预览的当前状态。

使用 [!DNL Segmentation Service] API中，您可以通过预览作业的ID查找其当前状态。 如果状态为“RESULT_READY”，则可以查看结果。 要查找预览作业的当前状态，请阅读 [检索预览作业部分](../api/previews-and-estimates.md#get-preview) 中的“预览和估计端点”指南。 要查找评估作业的当前状态，请阅读 [检索评估作业](../api/previews-and-estimates.md#get-estimate) 中的“预览和估计端点”指南。


## 后续步骤

开发、测试和保存区段定义后，即可创建区段作业以使用构建受众 [!DNL Segmentation Service] API。 请参阅 [评估和访问区段结果](./evaluate-a-segment.md) 以详细了解如何完成此操作。
