---
title: Personalization配置设置
description: 在Web SDK标记扩展中配置个性化设置。
exl-id: 24009a40-92ad-49d6-b768-49d64dccf4e0
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 1%

---

# Personalization配置设置 {#personalization}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_personalization"
>title="个性化"
>abstract="确定标记扩展如何处理个性化内容。"

通过此配置部分，可决定如何在加载个性化内容时隐藏页面的某些部分。 正确配置后，这些设置可确保访客看到正确的个性化内容。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL Extensions]**，然后在&#x200B;**[!UICONTROL Configure]**&#x200B;信息卡上选择[!UICONTROL Adobe Experience Platform Web SDK]。
1. 向下滚动到&#x200B;**[!UICONTROL Personalization]**&#x200B;部分。

![在标记UI中显示Web SDK标记扩展的个性化设置的图像](../assets/web-sdk-ext-personalization.png)

可以使用以下选项：

## [!UICONTROL Migrate Target from at.js to the Web SDK]**

使用此选项可允许Web SDK读取和写入`mbox` 1.x或2.x库使用的旧版`mboxEdgeCluster`和`at.js` Cookie。 此设置有助于在使用Web SDK或同一网站上的`at.js`在页面之间移动时保持访客配置文件不变。 如果您未在网站上的任意位置实施`at.js`，则无需启用此复选框。 与此复选框等效的JavaScript库为[`targetMigrationEnabled`](/help/collection/js/commands/configure/targetmigrationenabled.md)。

启用此选项时，请确保同时在[`overrideMboxEdgeServer`中启用](https://experienceleague.adobe.com/en/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/targetglobalsettings#overridemboxedgeserver)`targetGlobalSettings()`。

## [!UICONTROL Prehiding style] {#prehiding-style}

使用预隐藏样式编辑器，可定义自定义CSS规则以隐藏页面的特定部分。 加载页面时，Web SDK使用此样式来隐藏需要个性化的部分，检索个性化，然后取消隐藏个性化的页面部分。 此工作流允许访客查看个性化内容，而不会看到个性化检索过程在中加载或闪烁。 与此代码编辑器等效的JavaScript库为[`prehidingStyle`](/help/collection/js/commands/configure/prehidingstyle.md)。

## [!UICONTROL Prehiding snippet] {#prehiding-snippet}

此部分不是直接配置设置，而是一个方便获取实施代码的位置。 在网站上的`<head>`标记中实施此预隐藏代码片段，以便在加载Web SDK库时隐藏所需的内容。

>[!IMPORTANT]
>
>使用预隐藏代码片段时，Adobe建议在预隐藏代码片段和预隐藏样式之间使用相同的CSS规则。

## [!UICONTROL Enable personalization storage]

允许Web SDK存储个性化事件的复选框。 在浏览器的本地存储中。 当您希望跟踪访客在各个页面加载中看到的体验时，此维度很有价值。

## [!UICONTROL Auto click collection for Adobe Journey Optimizer]

一个下拉菜单，用于确定Web SDK何时自动收集从Adobe Journey Optimizer返回的内容上的点击次数。

* **[!UICONTROL Always]**：收集与建议的所有交互。
* **[!UICONTROL Decorated elements only]**：仅收集具有`data-aep-click-label`或`data-aep-click-token`HTML属性的元素的交互。
* **[!UICONTROL Never]**：不收集与建议的交互。

与此下拉菜单等效的JavaScript库为[`autoCollectPropositionInteractions.AJO`](/help/collection/js/commands/configure/autocollectpropositioninteractions.md)。 其默认值为[!UICONTROL Always]。

## [!UICONTROL Auto click collection for Adobe Target]

一个下拉菜单，用于确定Web SDK何时自动收集从Adobe Target返回的内容上的点击次数。

* **[!UICONTROL Always]**：收集与建议的所有交互。
* **[!UICONTROL Decorated elements only]**：仅收集具有`data-aep-click-label`或`data-aep-click-token`HTML属性的元素的交互。
* **[!UICONTROL Never]**：不收集与建议的交互。

与此下拉菜单等效的JavaScript库为[`autoCollectPropositionInteractions.TGT`](/help/collection/js/commands/configure/autocollectpropositioninteractions.md)。 其默认值为[!UICONTROL Never]。
