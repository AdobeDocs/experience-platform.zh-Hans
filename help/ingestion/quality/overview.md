---
keywords: Experience Platform；主页；热门主题；数据质量；质量；质量；支持的验证；验证；支持的验证；
solution: Experience Platform
title: 数据质量
topic-legacy: overview
description: 以下文档概述了Adobe Experience Platform中针对批处理和流式接收的支持检查和验证行为。
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 6%

---

# Adobe Experience Platform中的数据质量

Adobe Experience Platform为通过批处理或流式摄取上传的任何数据提供明确定义的完整性、准确性和一致性保证。 以下文档概述了[!DNL Experience Platform]中针对批处理和流式摄取的支持检查和验证行为。

## 支持的检查

|   | 批量摄取 | 流摄取 |
| ------ | --------------- | ------------------- |
| 数据类型检查 | 是 | 是 |
| 枚举检查 | 是 | 是 |
| 范围检查（最小、最大） | 是 | 是 |
| 必填字段检查 | 是 | 是 |
| 图案检查 | 否 | 是 |
| 格式检查 | 否 | 是 |

## 支持的验证行为

批处理和流式摄取都通过在[!DNL Data Lake]中移动用于检索和分析的坏数据来防止失败数据下游。 数据摄取为批处理和流摄取提供以下验证。

### 批量摄取

对批摄取完成以下验证：

| 验证区域 | 描述 |
| --------------- | ----------- |
| 架构 | 确保模式&#x200B;**不**&#x200B;为空并包含对合并模式的引用，如下所示：`"meta:immutableTags": ["union"]` |
| `identityField` | 确保定义了所有有效的身份描述符。 |
| `createdUser` | 确保允许摄取批的用户摄取批。 |

### 流式摄取

对流摄取完成了以下验证：

| 验证区域 | 描述 |
| --------------- | ----------- |
| 架构 | 确保模式&#x200B;**不**&#x200B;为空并包含对合并模式的引用，如下所示：`"meta:immutableTags": ["union"]` |
| `identityField` | 确保定义了所有有效的身份描述符。 |
| JSON | 确保JSON有效。 |
| IMS组织 | 确保列出的IMS组织是有效组织。 |
| 源名称 | 确保指定数据源的名称。 |
| 数据集 | 确保指定、启用且未删除数据集。 |
| 标头 | 确保已指定标题且其有效。 |

有关[!DNL Platform]如何监视和验证数据的详细信息，请参阅[监视数据流文档](./monitor-data-ingestion.md)。
