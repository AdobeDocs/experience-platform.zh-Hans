---
keywords: Experience Platform;home;popular topics;Data quality;quality;Quality;Supported validation;Validation;supported validation;
solution: Experience Platform
title: 数据获取质量
topic: overview
translation-type: tm+mt
source-git-commit: c04fb056d4564e53f192e0734a700a13820f5ba7
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 6%

---


# Adobe Experience Platform的数据质量

Adobe Experience Platform为通过批处理或流式接收上传的任何数据提供明确的完整性、准确性和一致性保证。 以下文档概述了中支持的批处理和流接收检查和验证行为 [!DNL Experience Platform]。

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

批处理和流式摄取都通过移动用于检索和分析的坏数据来防止故障数据下游 [!DNL Data Lake]。 数据摄取为批处理和流摄取提供以下验证。

### 批量摄取

对批摄取完成以下验证：

| 验证区域 | 描述 |
| --------------- | ----------- |
| 架构 | 确保模式不 **为空** ，并包含对合并模式的引用，如下所示： `"meta:immutableTags": ["union"]` |
| `identityField` | 确保定义了所有有效的标识描述符。 |
| `createdUser` | 确保摄取批的用户可以摄取批。 |

### 流摄取

对流式接收完成以下验证：

| 验证区域 | 描述 |
| --------------- | ----------- |
| 架构 | 确保模式不 **为空** ，并包含对合并模式的引用，如下所示： `"meta:immutableTags": ["union"]` |
| `identityField` | 确保定义了所有有效的标识描述符。 |
| JSON | 确保JSON有效。 |
| IMS组织 | 确保列出的IMS组织是有效的组织。 |
| 源名称 | 确保指定数据源的名称。 |
| 数据集 | 确保指定、启用和未删除数据集。 |
| Header | 确保已指定标头且其有效。 |

有关如何监视 [!DNL Platform] 和验证数据的更多信息，请参 [阅监视数据流文档](./monitor-data-flows.md)。
