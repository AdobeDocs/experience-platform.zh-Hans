---
keywords: Experience Platform；用户指南；归因人工智能；热门主题；访问控制；创建模型；
feature: Attribution AI
title: Attribution AI的治理策略
description: Adobe Experience Platform提供了多项服务和工具，使您能够放心地控制收集的体验数据。
exl-id: 448b10c8-8eac-41cb-9b77-66aa283c0a9d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# Attribution AI中的治理策略

完成工作流创建模型并提交模型的配置后，[策略实施](../../../data-governance/enforcement/auto-enforcement.md)将检查是否存在任何违规。 如果发生策略冲突，则会出现一个弹出窗口，指示已违反一个或多个策略。 这是为了确保您的Experience Platform中的数据操作和营销操作符合数据使用策略。

## 策略违规弹出框

[显示有关策略违规信息的弹出框](../../attribution-ai/images/data-governance/policy-violation-popover-aai.png)。

弹出框提供有关违规的特定信息。 您可以通过策略设置和其他与配置工作流不直接相关的度量来解决这些违规。 例如，您可以更改标签，以便允许将某些字段用于数据科学目的。 或者，也可以修改模型配置本身，使其不使用带有标签的任何内容。 请参阅文档，详细了解如何设置策略。
