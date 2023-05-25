---
keywords: Experience Platform；主页；热门主题；数据质量；质量；支持的验证；验证；支持的验证；
solution: Experience Platform
title: 数据质量
description: 以下文档概述了Adobe Experience Platform中支持用于批量摄取和流式摄取的检查和验证行为。
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 6%

---

# Adobe Experience Platform中的数据质量

Adobe Experience Platform为通过批量或流式摄取上传的任何数据的完整性、准确性和一致性提供了明确定义的保证。 以下文档概述了中针对批量摄取和流式摄取支持的检查和验证行为 [!DNL Experience Platform].

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

批量摄取和流式摄取通过将不良数据移动到中进行检索和分析来防止故障数据下游 [!DNL Data Lake]. 数据摄取为批量摄取和流式摄取提供了以下验证。

### 批量摄取

对批量摄取会执行以下验证：

| 验证区域 | 描述 |
| --------------- | ----------- |
| 架构 | 确保架构为 **非** 为空，并包含对合并架构的引用，如下所示： `"meta:immutableTags": ["union"]` |
| `identityField` | 确保定义了所有有效的身份描述符。 |
| `createdUser` | 确保允许引入批次的用户引入批次。 |

### 流式摄取

对流式摄取进行了以下验证：

| 验证区域 | 描述 |
| --------------- | ----------- |
| 架构 | 确保架构为 **非** 为空，并包含对合并架构的引用，如下所示： `"meta:immutableTags": ["union"]` |
| `identityField` | 确保定义了所有有效的身份描述符。 |
| JSON | 确保JSON有效。 |
| 组织 | 确保列出的组织是有效的。 |
| 源名称 | 确保指定数据源的名称。 |
| 数据集 | 确保指定、启用且未删除数据集。 |
| 标头 | 确保标头已指定且有效。 |

有关以下内容的更多信息： [!DNL Platform] 监视和验证数据可在中找到 [监控数据流文档](./monitor-data-ingestion.md).

## 身份值验证

下表概述了为确保成功验证标识值而必须遵循的现有规则。

| 命名空间 | 验证规则 | 违反规则时的系统行为 |
| --- | --- | --- |
| ECID | <ul><li>ECID的标识值必须刚好38个字符。</li><li>ECID的标识值必须仅由数字组成。</li></ul> | <ul><li>如果ECID的标识值不是38个字符，则会跳过该记录。</li><li>如果ECID的标识值包含非数字字符，则会跳过该记录。</li></ul> |
| 非ECID | 标识值不能超过1024个字符。 | 如果标识值超过1024个字符，则会跳过该记录。 |

有关的详细信息 [!DNL Identity Service] 护栏，请参见 [[!DNL Identity Service] 护栏概述](../../identity-service/guardrails.md).
