---
keywords: Experience Platform;home;popular topics;segment;Segment;create segment
solution: Experience Platform
title: 创建区段
topic: tutorial
description: 本文档提供了一个教程，用于使用Adobe Experience Platform分段服务API开发、测试、预览和保存段定义。
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%

---


# 创建区段

本文档提供了使用[!DNLAdobe Experience Platform分段服务API]开发、测 [试、预览和保存段定义的教程](../api/getting-started.md)。

有关如何使用用户界面构建区段的信息，请参阅“区段 [构建器指南”](../ui/overview.md)。

## 入门指南

本教程需要对创建受众段时涉及的 [!DNL Adobe Experience Platform] 各种服务进行有效的了解。 在开始本教程之前，请查看以下服务的相关文档：

- [[!DNL实时客户用户档案]](../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
- [[!DNLAdobe Experience Platform分段服务]](../home.md):允许您根据实时受众数据构建用户档案细分。
- [[!DNL体验数据模型(XDM)]](../../xdm/home.md):组织客户体验数 [!DNL Platform] 据的标准化框架。

以下各节提供了成功调用API所需了解的其他信 [!DNL Platform] 息。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

- 授权：承载者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有资源 [!DNL Experience Platform] 都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信 [!DNL Platform]息，请参阅 [沙箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要附加标头：

- 内容类型：application/json

## 开发细分定义

分段的第一步是定义分段，在称为段定义的构造中 **表示**。 段定义是封装写入(PQL)的查询 [!DNL Profile Query Language] 的对象。 此对象也称为 **PQL谓词**。 PQL谓词根据与您提供给的任何记录或时间序列数据相关的条件定义段规则 [!DNL Real-time Customer Profile]。 有关编写 [PQL查询](../pql/overview.md) ，请参阅PQL指南。

您可以通过向API中的端点发出POST请求来 `/segment/definitions` 创建新的段 [!DNL Segmentation] 定义。 以下示例概述了如何设置定义请求的格式，包括成功定义区段所需的信息。

有关如何定义区段的详细说明，请阅读区段定 [义开发人员指南](../api/segment-definitions.md#create)。

## 估计和预览受众 {#estimate-and-preview-an-audience}

在开发细分定义时，您可以使用中的估计和预览工具来 [!DNL Real-time Customer Profile] 视图摘要级别信息，以帮助确保隔离预期受众。 估计提供有关细分定义的统计信息，如预测受众大小和置信区间。 预览为区段定义提供符合条件的列表的分页用户档案，允许您将结果与预期进行比较。

通过评估和预览受众，您可以测试和优化PQL谓词，直到它们产生可预期的结果，然后在更新的段定义中使用它们。

预览或获取区段估计需要执行两个步骤：

1. [创建预览作业](#create-a-preview-job)
2. [视图估计或预览](#view-an-estimate-or-preview) ，使用预览作业的ID

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

您可以通过向端点发出预览请求来创建新的POST `/preview` 作业。

有关创建预览作业的详细说明，请参阅“预览 [和评估终端指南”](../api/previews-and-estimates.md#create-preview)。

### 视图估计或预览

评估和预览过程以异步方式运行，因为不同的查询可能需要不同的时间来完成。 启动查询后，您可以使用API调用来检索(GET)评估或预览的当前状态（当它进行时）。

使用 [!DNL Segmentation Service] API，您可以通过预览作业的ID查找该作业的当前状态。 如果状态为“RESULT_READY”，则可以视图结果。 要查找预览作业的当前状态，请阅读预览和估计终 [端指南中有关检索预览作](../api/previews-and-estimates.md#get-preview) 业部分的部分。 要查找评估作业的当前状态，请阅读预览和评估终 [端指南中有关检索](../api/previews-and-estimates.md#get-estimate) 评估作业的部分。


## 后续步骤

开发、测试和保存区段定义后，您可以创建区段作业，以使用API构建 [!DNL Segmentation Service] 受众。 有关如何完成此 [操作的详细步骤，请参](./evaluate-a-segment.md) 阅有关评估和访问区段结果的教程。