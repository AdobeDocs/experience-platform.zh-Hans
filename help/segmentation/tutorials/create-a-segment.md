---
keywords: Experience Platform；主页；热门主题；区段；区段；创建区段；分段；创建区段；分段服务；
solution: Experience Platform
title: 使用分段服务API创建区段
type: Tutorial
description: 按照本教程了解如何使用Adobe Experience Platform分段服务API来开发、测试、预览和保存区段定义。
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 1%

---

# 使用分段服务API创建区段

此文档提供了一个教程，介绍如何使用来开发、测试、预览和保存区段定义。 [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

有关如何使用用户界面构建区段的信息，请参阅 [Segment Builder指南](../ui/overview.md).

## 快速入门

本教程需要对各种 [!DNL Adobe Experience Platform] 创建受众区段时涉及的服务。 在开始本教程之前，请查看以下服务的文档：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md)：用于从实时客户档案数据构建受众区段。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Platform] 组织客户体验数据。 为了更好地利用分段，请确保您的数据被摄取为用户档案和事件，并符合 [数据建模的最佳实践](../../xdm/schema/best-practices.md).

以下部分提供了成功调用 [!DNL Platform] API。

### 正在读取示例API调用

本教程提供了示例API调用来演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将提供所有中所有所需标头的值 [!DNL Experience Platform] API调用，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定的虚拟沙盒隔离。 的所有请求 [!DNL Platform] API需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信息 [!DNL Platform]，请参见 [沙盒概述文档](../../sandboxes/home.md).

包含有效负载(POST、PUT、PATCH)的所有请求都需要额外的标头：

- Content-Type： application/json

## 制定区段定义

区段划分的第一步是定义区段，该区段通过称为区段定义的构造来表示。 区段定义是一个对象，它封装了写入的查询 [!DNL Profile Query Language] (PQL)。 此对象也称为PQL谓词。 PQL谓词根据与您提供给的任何记录或时序数据相关的条件定义区段的规则 [!DNL Real-Time Customer Profile]. 请参阅 [PQL指南](../pql/overview.md) 有关编写PQL查询的更多信息。

您可以通过向以下对象发出POST请求来创建新的区段定义： `/segment/definitions` 中的端点 [!DNL Segmentation] API。 以下示例概述了如何设置定义请求的格式，包括成功定义区段所需的信息。

有关如何定义区段的详细说明，请参阅 [区段定义开发人员指南](../api/segment-definitions.md#create).

## 估计和预览受众 {#estimate-and-preview-an-audience}

在开发区段定义时，您可以使用中的估算和预览工具 [!DNL Real-Time Customer Profile] 查看摘要级别的信息，以帮助确保您隔离预期的受众。 估算提供有关区段定义的统计信息，例如预计受众规模和置信区间。 预览可提供符合区段定义的用户档案分页列表，以便您将结果与预期结果进行比较。

通过估计和预览受众，您可以测试和优化PQL谓词，直到它们产生所需的结果，然后可以在更新的区段定义中使用它们。

要预览或获取区段的估计值，需要执行两个步骤：

1. [创建预览作业](#create-a-preview-job)
2. [查看估算或预览](#view-an-estimate-or-preview) 使用预览作业的ID

### 如何生成估计

数据样本用于评估区段和估计符合条件的用户档案的数量。 每天早上（上午12点至凌晨2点，即UTC时间上午7-9点）将新数据加载到内存中，并使用当天的样本数据估计所有分段查询。 因此，任何新增的字段或收集的其他数据都将反映在第二天的估计数中。

样本大小取决于配置文件存储区中的实体总数。 下表显示了这些样本量：

| 配置文件存储中的实体 | 样本大小 |
| ------------------------- | ----------- |
| 少于100万 | 完整数据集 |
| 100万到2000万 | 100万 |
| 超过2000万 | 占总数的5% |

估计值通常在10-15秒内运行，从粗略估计值开始，并随着读取更多记录而优化。

### 创建预览作业

您可以通过向以下对象发出POST请求来创建新的预览作业： `/preview` 端点。

有关创建预览作业的详细说明，请参阅 [预览和估计端点指南](../api/previews-and-estimates.md#create-preview).

### 查看估算或预览

估算和预览进程是异步运行的，因为不同的查询可能需要不同的时间长度才能完成。 启动查询后，您可以使用API调用检索(GET)估算或预览的当前状态。

使用 [!DNL Segmentation Service] API中，您可以通过预览作业的ID来查找其当前状态。 如果状态为“RESULT_READY”，则可以查看结果。 要查找预览作业的当前状态，请阅读以下部分： [检索预览作业部分](../api/previews-and-estimates.md#get-preview) 在预览和估计端点指南中。 要查找估算作业的当前状态，请阅读以下部分： [检索估计作业](../api/previews-and-estimates.md#get-estimate) 在预览和估计端点指南中。


## 后续步骤

开发、测试和保存区段定义后，即可使用创建区段作业来构建受众。 [!DNL Segmentation Service] API。 请参阅上的教程 [评估和访问区段结果](./evaluate-a-segment.md) 有关如何完成此操作的详细步骤。
