---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 数据摄取质量
topic: overview
translation-type: tm+mt
source-git-commit: 24df962656706d769a7034020d96a545e8f905ca

---


# Adobe Experience Platform中的数据质量

Adobe Experience Platform为通过批处理或流式摄取上传的任何数据提供了明确定义的完整性、准确性和一致性保证。 以下文档概述了Experience Platform中针对批处理和流摄取的支持的检查和验证行为。

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

批处理和流式摄取都通过移动数据以在数据湖中进行检索和分析，防止了故障数据向下游移动。 数据摄取为批处理和流摄取提供以下验证。

### 批量摄取

对批摄取完成以下验证：

| 验证区域 | 描述 |
| --------------- | ----------- |
| 模式 | 确保模式不 **为空** ，并包含对合并模式的引用，如下所示： `"meta:immutableTags": ["union"]` |
| `identityField` | 确保定义了所有有效的标识描述符。 |
| `createdUser` | 确保摄取批的用户可以摄取批。 |

### 流摄取

对流摄取完成以下验证：

| 验证区域 | 描述 |
| --------------- | ----------- |
| 模式 | 确保模式不 **为空** ，并包含对合并模式的引用，如下所示： `"meta:immutableTags": ["union"]` |
| `identityField` | 确保定义了所有有效的标识描述符。 |
| JSON | 确保JSON有效。 |
| IMS组织 | 确保列出的IMS组织是有效的组织。 |
| 源名称 | 确保指定数据源的名称。 |
| 数据集 | 确保指定、启用和未删除数据集。 |
| Header | 确保指定标题且标题有效。 |

有关平台如何监视和验证数据的更多信息，请参阅监 [视数据流文档](./monitor-data-flows.md)。
