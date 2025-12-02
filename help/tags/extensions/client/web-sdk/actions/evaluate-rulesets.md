---
title: 评估规则集
description: 手动触发规则集评估。
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# 评估规则集

**[!UICONTROL Evaluate rulesets]**&#x200B;操作类型允许您手动触发规则集评估。 Adobe Journey Optimizer返回规则集以支持浏览器内消息等功能。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL Rules]**，然后选择所需的规则。
1. 在[!UICONTROL Actions]下，选择现有操作或创建操作。
1. 将[!UICONTROL Extension]下拉字段设置为&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，然后将[!UICONTROL Action type]设置为&#x200B;**[!UICONTROL Evaluate rulesets]**。

![显示“评估规则集”响应操作类型的Experience Platform用户界面的图像。](../assets/evaluate-rulesets.png)

## 可用字段

此操作类型支持以下选项：

* **[!UICONTROL Render visual personalization decisions]**：一个复选框，在启用时，它将为匹配的规则集项目呈现可视化个性化决策。
* **[!UICONTROL Decision context]**：在评估设备上决策的Adobe Journey Optimizer规则集时使用的键值映射。 您可以手动或通过数据元素提供决策上下文。
