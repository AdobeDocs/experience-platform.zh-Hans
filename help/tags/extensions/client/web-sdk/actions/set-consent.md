---
title: 设置同意
description: 为访客设置所需的同意。
source-git-commit: 8dd658c46fc92ae6d450213ab79f2766f4211c53
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# 设置同意

**[!UICONTROL Set consent]**&#x200B;操作确定标记扩展是应发送数据（选择启用）、丢弃数据（选择禁用）还是使用[默认同意](../configure/consent.md)（同意未知）。 当用户允许或拒绝您网站上的同意时，您可以使用此操作将其首选项与标记扩展同步。 此操作的JavaScript库等效项是[`setConsent`](/help/collection/js/commands/setconsent.md)命令。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL Rules]**，然后选择所需的规则。
1. 在[!UICONTROL Actions]下，选择现有操作或创建操作。
1. 将[!UICONTROL Extension]下拉字段设置为&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，然后将[!UICONTROL Action type]设置为&#x200B;**[!UICONTROL Set consent]**。

标记扩展支持以下标准：

* **[Adobe standard](/help/landing/governance-privacy-security/consent/adobe/overview.md)**：同时支持1.0和2.0标准。
* **[IAB透明度和同意框架](/help/landing/governance-privacy-security/consent/iab/overview.md)**：如果使用此标准，且您的实施配置正确，则访客的实时客户配置文件将更新为同意信息：
   1. XDM个人配置文件架构包含[IAB TCF 2.0同意字段组](/help/xdm/field-groups/profile/iab.md)。
   1. 体验事件架构包含[IAB TCF 2.0同意字段组](/help/xdm/field-groups/event/iab.md)。

Adobe建议单独存储任何同意对话框首选项，例如存储在数据元素中。 标记扩展不提供检索同意的方法。 要确保用户首选项与标记扩展保持同步，您可以在每次加载页面时执行此操作。

## 可用字段

此操作类型支持以下配置选项：

* **[!UICONTROL Instance]**：操作适用的SDK实例。 如果您的实施使用单个SDK实例，则会禁用此下拉菜单。
* **[!UICONTROL Identity map]**：控制如何生成ECID以及将哪些ID同意信息绑定到的数据元素。
* **[!UICONTROL Consent information]**：确定您是要填写表单，还是要提供包含同意信息的数据元素。
* **[!UICONTROL Standard]**：要使用的同意标准。 可用选项包括“[!UICONTROL Adobe]”和“[!UICONTROL IAB TCF]”。
* **[!UICONTROL Version]**：要使用的同意标准的版本。
* **[!UICONTROL Datastream configuration overrides]**：此命令支持数据流配置覆盖，从而使您能够控制哪些应用和服务接收此数据。 当在单个命令和标记扩展配置设置中设置数据流配置覆盖时，单个命令优先。 有关详细信息，请参阅[数据流配置覆盖](../configure/configuration-overrides.md)。

## 创建可更新同意信息的规则

使用此操作的理想时机是客户的同意偏好设置发生更改时。 您可以创建标记规则来侦听此更改。

1. 在标记属性中，导航到&#x200B;**[!UICONTROL Rules]**&#x200B;并选择&#x200B;**[!UICONTROL Add rule]**。
1. 为规则指定所需的名称，然后选择`+`旁边的“**[!UICONTROL Events]**”图标。
1. 在左侧设置以下属性：
   * **[!UICONTROL Extension]**: [!UICONTROL Core]
   * **[!UICONTROL EVent type]**: [!UICONTROL Custom code]
1. 打开右侧的编辑器，然后使用以下代码作为模板：

```javascript
// Wait for window.__tcfapi to be defined, then trigger when the customer has completed their consent and preferences.
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && tcData.eventStatus === "useractioncomplete") {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF Consent GDPR", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn't defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

1. 选择 **[!UICONTROL Keep changes]**。

上述自定义代码块执行两项操作：

* 同意首选项发生更改时触发规则。
* 设置两个数据元素： **IAB TCF同意字符串**&#x200B;和&#x200B;**IAB TCF同意GDPR**。

在设置“[!UICONTROL Set Consent]”操作时，这些数据元素很有用：

1. 选择`+`旁边的“**[!UICONTROL Actions]**”图标。
1. 在左侧设置以下属性：
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Action type]**: [!UICONTROL Set consent]
1. 在右侧设置以下属性：
   * **[!UICONTROL Standard]**: [!UICONTROL IAB TCF]
   * **[!UICONTROL Version]**: [!UICONTROL 2.0]
   * **[!UICONTROL Value]**: `%IAB TCF Consent String%`
   * **[!UICONTROL Does GDPR apply to this consent value]**： [!UICONTROL Provide a data element]，值为`%IAB TCF Consent GDPR%`

![IAB设置同意操作](../assets/iab-action.png)

>[!NOTE]
>
>无法使用数据元素选择器选择这些数据元素，因为它们是通过自定义代码创建的。 您必须键入带有百分比符号的数据元素名称。
