---
title: Adobe Advertising配置设置
description: 启用或禁用需求端平台功能。
source-git-commit: 526cb473a6288f367db9cb00c0277cce7543cd57
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Adobe Advertising配置设置

>[!AVAILABILITY]
>
>适用于Web SDK的Adobe Advertising当前处于&#x200B;**测试版**&#x200B;中。 功能和文档可能会发生更改。

**[!UICONTROL Adobe Advertising]**&#x200B;部分允许您启用或禁用需求端平台(DSP)功能（如果在实施中使用）。 仅当您的实施使用DSP时，才需要设置此字段。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL Extensions]**，然后在&#x200B;**[!UICONTROL Configure]**&#x200B;信息卡上选择[!UICONTROL Adobe Experience Platform Web SDK]。
1. 向下滚动到&#x200B;**[!UICONTROL Adobe Advertising]**&#x200B;部分。

目前有一个可用选项。

## [!UICONTROL Adobe Advertising DSP]

一个下拉菜单，可启用或禁用Adobe Advertising的DSP功能。

* **[!UICONTROL Enabled]**：启用浏览跟踪功能。
* **[!UICONTROL Disabled]**：禁用显示到达跟踪。

启用后，以下设置可用：

* **[!UICONTROL Advertisers]**：要为其启用显示到达跟踪的广告商。
* **[!UICONTROL ID5 partner ID]**：可选。 您组织的ID5合作伙伴ID。 此设置允许Web SDK收集ID5通用ID。
* **[!UICONTROL RampID JavaScript path]**：可选。 您组织的[!DNL LiveRamp RampID] JavaScript代码(`ats.js`)的路径。  此设置允许Web SDK收集[!DNL RampID]个通用ID。
