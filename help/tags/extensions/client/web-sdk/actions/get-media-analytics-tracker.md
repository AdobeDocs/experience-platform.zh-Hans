---
title: 获取Media Analytics跟踪器
description: 将旧版Media API导出到窗口对象。
source-git-commit: c55e425f146e4afdb2314b432c9dc48391e02e63
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 0%

---

# 获取Media Analytics跟踪器

**[!UICONTROL Get Media Analytics tracker]**&#x200B;操作用于获取旧版Media Analytics API。 配置操作并提供对象名称时，会将旧版Media Analytics API导出到该窗口对象。 此操作适用于从旧版Media Analytics迁移到Streaming Media Analytics。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL Rules]**，然后选择所需的规则。
1. 在[!UICONTROL Actions]下，选择现有操作或创建操作。
1. 将[!UICONTROL Extension]下拉字段设置为&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，然后将[!UICONTROL Action type]设置为&#x200B;**[!UICONTROL Get Media Analytics tracker]**。

![Experience Platform UI图像显示“获取Media Analytics跟踪器”操作类型。](../assets/get-media-analytics-tracker.png)

此操作包含单个可配置的字段：

* **[!UICONTROL Export the Media Legacy API to this window object]**：选择要将媒体旧版API导出到的所需对象。 如果未提供任何内容，则该操作会将API导出到`window.Media`。
