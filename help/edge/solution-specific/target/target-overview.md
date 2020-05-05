---
title: 'Adobe目标和Adobe Experience Platform Web SDK。 '
seo-title: Adobe Experience Platform Web SDK和使用Adobe目标
description: 了解如何使用Experience Platform Web SDK使用Adobe目标呈现个性化内容
seo-description: 了解如何使用Experience Platform Web SDK使用Adobe目标呈现个性化内容
translation-type: tm+mt
source-git-commit: db4bfec04a1116ce2b6a0be7ca0e8cb2f9639ad6

---


# 目标概述

Adobe Experience Platform Web SDK通过该个性化功能与Adobe目标 [集成](../../fundamentals/rendering-personalization-content.md) ，使您能轻松提供个性化内容和决策。

## 启用Adobe目标

要启用目标，您需要执行以下操作：

- 在边缘配置中 [启用目标](../../fundamentals/edge-configuration.md) ，并使用相应的客户端代码。
- 将选项 `renderDecisions` 添加到事件。

您也可以选择：

- 添加 `scopes` 到事件以检索特定活动(对于使用基于表单的书写器创建的活动很有用)。
- 添加预 [隐藏片段](../../fundamentals/managing-flicker.md) ，以仅隐藏页面的某些部分。

## 使用VEC

在SDK中，您可以正常使用VEC，但有一个例外，您需要安装 [目标VEC帮助程序扩](https://docs.adobe.com/content/help/en/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) 展并处于活动状态。

## 使用基于表单的书写器

还可以使用基于表单的书写器返回内容。 范围将作为位置(mBox)显示在目标UI中。 此外，如果您决定使用范围，您还需要确保开发人员正在查找响应。

## 受众XDM

在目标中，XDM数据将作为自定义参数显示在受众生成器中。 XDM使用点记号(例如， `web.webPageDetails.name`)

## 术语

__决策__ -在目标中，这些决策与从活动中选择的体验相关。

__范围__ -决定的范围。 在目标，这是mBox。 全局mBox是范 `__view__` 围。

__模式__ -决定的模式是目标中的优惠类型。

__XDM__ - XDM被串行化为点符号，然后作为mBox参数输入目标。