---
keywords: Experience Platform；主页；热门主题；数据质量；质量；支持的验证；验证；支持的验证；
solution: Experience Platform
title: 数据质量
description: 以下文档概要介绍了Adobe Experience Platform中批量摄取和流式摄取受支持的检查和验证行为。
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 5%

---

# Adobe Experience Platform中的数据质量

Adobe Experience Platform为通过批量摄取或流式摄取上传的任何数据提供了明确定义的完整性、准确性和一致性保证。 以下文档概要介绍了中支持的批量和流式引入检查和验证行为 [!DNL Experience Platform].

## 支持的检查

|   | 批量摄取 | 流式摄取 |
| ------ | --------------- | ------------------- |
| 数据类型检查 | 是 | 是 |
| 枚举检查 | 是 | 是 |
| 范围检查（最小、最大） | 是 | 是 |
| 必填字段检查 | 是 | 是 |
| 模式检查 | 否 | 是 |
| 格式检查 | 否 | 是 |

## 支持的验证行为

批量摄取和流式摄取都会通过移动错误数据以在 [!DNL Data Lake]. 数据摄取为批量摄取和流式摄取提供了以下验证。

### 批量摄取

已完成以下批量摄取验证：

| 验证区域 | 描述 |
| --------------- | ----------- |
| 架构 | 确保架构为 **not** empty并包含对并集架构的引用，如下所示： `"meta:immutableTags": ["union"]` |
| `identityField` | 确保定义所有有效的身份描述符。 |
| `createdUser` | 确保允许摄取批次的用户摄取该批次。 |

### 流式摄取

对流式引入完成了以下验证：

| 验证区域 | 描述 |
| --------------- | ----------- |
| 架构 | 确保架构为 **not** empty并包含对并集架构的引用，如下所示： `"meta:immutableTags": ["union"]` |
| `identityField` | 确保定义所有有效的身份描述符。 |
| JSON | 确保JSON有效。 |
| IMS组织 | 确保列出的IMS组织是有效的组织。 |
| 源名称 | 确保指定数据源的名称。 |
| 数据集 | 确保指定、启用且未删除数据集。 |
| 标头 | 确保指定了标头并且有效。 |

有关如何 [!DNL Platform] 可在 [监控数据流文档](./monitor-data-ingestion.md).

## 身份值验证

下表概述了为了确保身份值成功验证必须遵循的现有规则。

| 命名空间 | 验证规则 | 违反规则时的系统行为 |
| --- | --- | --- |
| ECID | <ul><li>ECID的标识值必须恰好为38个字符。</li><li>ECID的标识值只能由数字组成。</li></ul> | <ul><li>如果ECID的标识值不完全为38个字符，则会跳过该记录。</li><li>如果ECID的标识值包含非数字字符，则会跳过该记录。</li></ul> |
| 非ECID | 标识值不能超过1024个字符。 | 如果标识值超过1024个字符，则会跳过该记录。 |

有关 [!DNL Identity Service] 护栏，看 [[!DNL Identity Service] 护栏概述](../../identity-service/guardrails.md).
