---
title: 带标识的重定向
description: 允许在贵组织的域之间共享访客标识符。
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---

# 带标识的重定向

**[!UICONTROL Redirect with identity]**&#x200B;操作类型允许您将当前页面的访客标识符共享到您的组织拥有的其他域。 它设计为与点击事件和值比较条件一起使用。 它的功能与JavaScript库中的[`appendIdentityToUrl`](/help/collection/js/commands/appendidentitytourl.md)命令类似。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL Rules]**，然后选择所需的规则。
1. 在[!UICONTROL Actions]下，选择现有操作或创建操作。
1. 将[!UICONTROL Extension]下拉字段设置为&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，然后将[!UICONTROL Action type]设置为&#x200B;**[!UICONTROL Redirect with identity]**。

## 用例

* **跨域识别个人**：如果访客从某个域单击到您组织拥有的另一个域，您可以使用此操作，以便他们仍被视为同一个人。 如果您的报表组合了来自多个域的数据，以防止访客虚增，则此识别方法特别有用。
* **识别从移动应用程序转到Web应用程序的个人**：如果访客在您的移动应用程序中，并且他们单击指向您的Web应用程序的链接，则可以使用此操作，以便Web SDK承认它是同一个人。 此工作流可为报告和个性化提供一致的体验。

## 可用字段

* **[!UICONTROL Instance]**：操作适用的SDK实例。 如果您的实施使用单个SDK实例，则会禁用此下拉菜单。
* **[!UICONTROL Datastream configuration overrides]**：此命令支持数据流配置覆盖，从而使您能够控制哪些应用和服务接收此数据。 当在单个命令和标记扩展配置设置中设置数据流配置覆盖时，单个命令优先。 有关详细信息，请参阅[数据流配置覆盖](../configure/configuration-overrides.md)。

## 示例规则

此命令通常与监听点击并检查所需域的特定规则一起使用。

+++规则事件条件

单击具有`href`属性的锚标记时触发。

* **[!UICONTROL Extension]**：核心
* **[!UICONTROL Event type]**：单击
* **[!UICONTROL When the user clicks on]**：特定元素
* **[!UICONTROL Elements matching the CSS selector]**: `a[href]`

![规则事件](../assets/id-sharing-event-configuration.png)

+++

+++规则条件

仅在所需的域上触发。

* **[!UICONTROL Logic type]**：常规
* **[!UICONTROL Extension]**：核心
* **[!UICONTROL Condition Type]**：值比较
* **[!UICONTROL Left Operand]**: `%this.hostname%`
* **[!UICONTROL Operator]**：匹配Regex
* **[!UICONTROL Right Operand]**：匹配所需域的正则表达式。 例如：`adobe.com$|behance.com$`

![规则条件](../assets/id-sharing-condition-configuration.png)

+++

+++规则操作

将标识附加到URL。

* **[!UICONTROL Extension]**： Adobe Experience Platform Web SDK
* **[!UICONTROL Action Type]**：使用标识重定向

![规则操作](../assets/id-sharing-action-configuration.png)

+++
