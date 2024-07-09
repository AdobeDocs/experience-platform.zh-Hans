---
solution: Experience Platform
title: 使用分段服务API创建区段定义
type: Tutorial
description: 按照本教程了解如何使用Adobe Experience Platform分段服务API来开发、测试、预览和保存区段定义。
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 6%

---

# 使用分段服务API创建区段定义

此文档提供了一个教程，介绍如何使用开发、测试、预览和保存区段定义。 [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

有关如何使用用户界面构建区段定义的信息，请参阅 [区段生成器指南](../ui/segment-builder.md).

## 快速入门

本教程需要对各种 [!DNL Adobe Experience Platform] 创建区段定义时涉及的服务。 在开始本教程之前，请查看以下服务的文档：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md)：允许您使用区段定义或其他外部源从实时客户档案数据构建受众。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Platform] 组织客户体验数据。 为了更好地利用分段，请确保您的数据被作为配置文件和事件摄取，并根据 [数据建模的最佳实践](../../xdm/schema/best-practices.md).

以下部分提供成功调用 [!DNL Platform] API。

### 正在读取示例 API 调用

本教程提供了示例API调用来演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关文档中用于示例API调用的惯例的信息，请参阅 [如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标头的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

中的所有资源 [!DNL Experience Platform] 被隔离到特定的虚拟沙盒中。 所有请求 [!DNL Platform] API需要一个标头，该标头应指定将在其中执行操作的沙盒的名称：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信息 [!DNL Platform]，请参见 [沙盒概述文档](../../sandboxes/home.md).

包含负载 (POST、PUT、PATCH) 的所有请求都需要额外的标头：

- Content-Type： application/json

## 制定区段定义

分段的第一步是定义区段定义。 区段定义是一个对象，它封装了写入的查询 [!DNL Profile Query Language] (PQL)。 此对象也称为PQL谓词。 PQL谓词根据与您提供给的任何记录或时间序列数据相关的条件定义区段定义的规则 [!DNL Real-Time Customer Profile]. 请参阅 [PQL指南](../pql/overview.md) 有关编写PQL查询的更多信息。

您可以通过向以下对象发出POST请求来创建新的区段定义： `/segment/definitions` 中的端点 [!DNL Segmentation] API。 以下示例概述了如何设置定义请求的格式，包括成功定义区段定义所需的信息。

有关如何定义区段定义的详细说明，请参阅 [区段定义开发人员指南](../api/segment-definitions.md#create).

## 估计和预览受众 {#estimate-and-preview-an-audience}

在开发区段定义时，您可以使用中的估算和预览工具 [!DNL Real-Time Customer Profile] 查看摘要级别的信息，以帮助确保隔离预期的受众。 估算提供有关区段定义的统计信息，例如预计受众大小和置信区间。 预览可提供符合区段定义的用户档案的分页列表，以便您将结果与预期结果进行比较。

通过估计和预览受众，您可以测试和优化PQL谓词，直到它们产生所需的结果，然后可以在更新的区段定义中使用它们。

要预览或获取区段定义的估计值，需要执行两个步骤：

1. [创建预览作业](#create-a-preview-job)
2. [查看估计或预览](#view-an-estimate-or-preview) 使用预览作业的ID

### 如何生成估算

启用实时客户资料的数据被摄取到Platform后，将存储在资料数据存储中。 当将记录摄取到配置文件存储中增加或减少总配置文件计数超过5%时，将触发取样作业以更新计数。 如果配置文件数的变化不超过5%，则取样作业将每周自动运行。

触发示例的方式取决于所使用的摄取类型：

- 对于流数据工作流，会每小时进行一次检查，以确定是否满足了5%的增加或减少阈值。 如果达到此阈值，则会自动触发示例作业以更新计数。
- 对于批量摄取，在成功将批次摄取到配置文件存储区后15分钟内，如果满足5%的增加或减少阈值，则会运行作业以更新计数。 使用配置文件API，您可以预览最新成功的示例作业，以及按数据集和身份命名空间列出配置文件分发。

样本大小取决于配置文件存储中的实体总数。 下表显示了这些样本量：

| 配置文件存储中的实体 | 样本大小 |
| ------------------------- | ----------- |
| 少于100万 | 完整数据集 |
| 100万到2000万 | 100万 |
| 超过2000万 | 占总数的5% |

估计值通常在10-15秒内运行，从粗略估计开始，并随着读取更多记录而优化。

### 创建预览作业

您可以通过向以下对象发出POST请求来创建新的预览作业： `/preview` 端点。

有关创建预览作业的详细说明，请参阅 [预览和估计端点指南](../api/previews-and-estimates.md#create-preview).

### 查看估计或预览

估算和预览流程是异步运行的，因为不同的查询可能需要不同的时间长度才能完成。 启动查询后，您可以使用API调用在估计或预览的过程中检索(GET)其当前状态。

使用 [!DNL Segmentation Service] API中，您可以通过预览作业的ID来查找其当前状态。 如果状态为“RESULT_READY”，则可以查看结果。 要查找预览作业的当前状态，请阅读以下部分： [检索预览作业部分](../api/previews-and-estimates.md#get-preview) 在预览和估计端点指南中。 要查找估算作业的当前状态，请阅读以下部分： [检索估计作业](../api/previews-and-estimates.md#get-estimate) 在预览和估计端点指南中。


## 后续步骤

开发、测试和保存区段定义后，即可使用创建区段作业以构建受众。 [!DNL Segmentation Service] API。 请参阅上的教程 [评估和访问区段结果](./evaluate-a-segment.md) 有关如何完成此操作的详细步骤。
