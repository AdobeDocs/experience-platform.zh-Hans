---
keywords: Experience Platform；主页；热门主题；数据质量；质量；支持的验证；验证；支持的验证；
solution: Experience Platform
title: 数据质量
description: 以下文档概述了Adobe Experience Platform中针对批量摄取和流式摄取支持的检查和验证行为。
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 5%

---

# Adobe Experience Platform中的数据质量

Adobe Experience Platform为通过批量摄取或流式摄取上传的任何数据提供了完整、准确和一致的明确定义保证。 以下文档汇总了[!DNL Experience Platform]中支持批量摄取和流式摄取的检查和验证行为。

## 支持的检查

|   | 批量摄取 | 流式摄取 |
| ------ | --------------- | ------------------- |
| 数据类型检查 | 是 | 是 |
| 枚举检查 | 是 | 是 |
| 范围检查（最小、最大） | 是 | 是 |
| 必填字段检查 | 是 | 是 |
| 图案检查 | 否 | 是 |
| 格式检查 | 否 | 是 |

## 支持的验证行为

通过将不良数据移动到[!DNL Data Lake]中进行检索和分析，批次摄取和流式摄取都会防止故障数据向下游传输。 数据摄取为批量摄取和流式摄取提供了以下验证。

### 批量摄取

对批量摄取会完成以下验证：

| 验证区域 | 描述 |
| --------------- | ----------- |
| 架构 | 确保架构为&#x200B;**非**&#x200B;空并包含对合并架构的引用，如下所示： `"meta:immutableTags": ["union"]` |
| `identityField` | 确保已定义所有有效的身份描述符。 |
| `createdUser` | 确保允许提取批次的用户提取批次。 |

### 流式摄取

对流式摄取执行以下验证：

| 验证区域 | 描述 |
| --------------- | ----------- |
| 架构 | 确保架构为&#x200B;**非**&#x200B;空并包含对合并架构的引用，如下所示： `"meta:immutableTags": ["union"]` |
| `identityField` | 确保已定义所有有效的身份描述符。 |
| JSON | 确保JSON有效。 |
| 组织 | 确保列出的组织是有效的。 |
| 源名称 | 确保指定了数据源的名称。 |
| 数据集 | 确保指定、启用且未移除数据集。 |
| 标头 | 确保标头已指定并且有效。 |

有关[!DNL Experience Platform]如何监视和验证数据的详细信息，请参阅[监视数据流文档](./monitor-data-ingestion.md)。

## 身份值验证

下表概述了必须遵循的现有规则，以确保成功验证标识值。

| 命名空间 | 验证规则 | 违反规则时的系统行为 |
| --- | --- | --- |
| ECID | <ul><li>ECID的标识值必须刚好38个字符。</li><li>ECID的标识值必须仅由数字组成。</li></ul> | <ul><li>如果ECID的标识值不完全为38个字符，则会跳过该记录。</li><li>如果ECID的标识值包含非数字字符，则会跳过记录。</li></ul> |
| 非ECID | 标识值不能超过1024个字符。 | 如果标识值超过1024个字符，则会跳过该记录。 |

有关[!DNL Identity Service]护栏的详细信息，请参阅[[!DNL Identity Service] 护栏概述](../../identity-service/guardrails.md)。
