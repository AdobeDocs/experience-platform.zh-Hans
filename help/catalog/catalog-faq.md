---
keywords: 目录服务；问题；常见问题解答；常见问题解答；数据集常见问题解答
title: 常见问题解答
description: 有关Adobe Experience Platform目录服务和数据集的常见问题解答。
exl-id: 70d2a352-75bd-4bbc-98e6-aeea16306f63
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# 常见问题解答 {#faq}

本文档提供了有关Adobe Experience Platform目录服务和数据集的常见问题解答。 有关其他Experience Platform服务的问题和疑难解答，包括在所有Experience Platform API中遇到的问题，请参阅[Experience Platform疑难解答指南](../landing/troubleshooting.md)。

## 保留策略和规则 {#retention-policies-and-rules}

### 可以将保留策略规则应用到哪些类型的数据集？

+++回答

您可以在使用ExperienceEvent XDM类创建的数据集上设置保留策略。 对于配置文件服务，保留策略只能应用于ExperienceEvent数据集，前提是已为配置文件启用这些数据集。

+++

### 我可以为数据湖和配置文件服务设置不同的保留策略吗？

+++回答

可以，您可以对数据湖和配置文件服务应用不同的保留策略。

+++

## 保留作业执行和时间 {#retention-job-execution-and-timing}

### 数据集保留作业多久将从数据湖服务中删除数据？

+++回答

系统会每周评估和处理数据集过期时间，并删除过期的所有记录。 如果事件被摄取到Experience Platform超过30天（摄取日期> 30天），并且其事件日期超过定义的保留期，则被视为已过期。

+++

### 数据集保留作业多久将从配置文件服务中删除数据？

+++回答

设置保留策略后，如果现有事件的事件时间戳超过保留期限，则会立即从Experience Platform中删除这些事件。 一旦新事件的时间戳超过保留期，就会将其删除。

例如，如果您在5月15日应用30天到期策略，则会出现以下情况：

- 新事件在摄取后将接收30天过期。
- 时间戳早于4月15日的现有事件将被立即删除。
- 时间戳在4月15日之后的现有事件将设置为在其时间戳之后30天过期。 例如，从4月18日开始的事件将在5月18日删除。

+++

## 数据集使用和监控

### 如何检查我当前的数据集使用情况？

+++回答

您可以在[!UICONTROL 数据集]清单页面上，以单独的量度查看数据湖和配置文件中最新数据集级别的存储大小。 您还可以对列进行排序，以确定最大的数据集，并确保应用保留策略。 在“许可证使用情况”仪表板中提供了沙盒级别的使用情况。 有关详细信息，请参阅[许可证使用文档](../dashboards/guides/license-usage.md)。

+++

### 如何验证数据保留作业是否成功？

+++回答

您可以在[数据集保留配置UI](./datasets/user-guide.md#data-retention-policy)和[!UICONTROL 数据集]清单页面上检查上次数据保留作业的时间戳。 历史数据集使用情况报表当前不可用，但计划在未来版本中使用。

+++

## 数据恢复 {#data-recovery}

### 能否恢复已删除的数据？

+++回答

不会，应用保留策略后，任何超过保留期的数据都会被永久删除，并且无法恢复。

+++
