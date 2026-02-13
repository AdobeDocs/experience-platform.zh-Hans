---
title: 高级配置设置
description: 为Web SDK标记扩展配置高级设置。
exl-id: d830a210-77ab-4823-b5fa-c1194a01bea3
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 2%

---

# 高级配置设置 {#advanced}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_advanced"
>title="高级设置"
>abstract="高级配置设置。 Adobe建议在大多数实施中保持这些选项不变。"

此配置部分允许您更改高级设置。 Adobe建议在大多数实施中保持这些选项不变。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL Extensions]**，然后在&#x200B;**[!UICONTROL Configure]**&#x200B;信息卡上选择[!UICONTROL Adobe Experience Platform Web SDK]。
1. 向下滚动到&#x200B;**[!UICONTROL Advanced Settings]**&#x200B;部分。

![显示使用Web SDK标记扩展的高级设置的图像](../assets/advanced-settings.png)

目前有一个可用选项。

## [!UICONTROL Edge base path]

使用此字段可更改用于与Edge Network交互的基本路径。 如果您参与某些Alpha或Beta测试，Adobe可能会要求您更改此字段；否则，Adobe建议将其保留为默认值`ee`。

在配置JavaScript库时，此字段的标记等效于[`edgeBasePath`](/help/collection/js/commands/configure/edgebasepath.md)。
