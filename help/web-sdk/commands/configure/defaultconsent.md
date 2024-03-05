---
title: defaultconsent
description: 设置默认同意收集方法。
source-git-commit: b9db136a9077e3420bfeb44ae45e7d72c322acbb
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# `defaultConsent`

此 `defaultConsent` 属性确定在调用 [`setConsent`](../setconsent.md) 命令。 当您不希望意外从居住在数据收集之前需要获得同意的区域中的个人收集数据时，此属性很有价值。

此属性允许三个值：

* **在**：数据收集会正常进行，直到用户选择退出为止。
* **去话**：数据将永久丢弃，直到用户选择加入为止。
* **待处理**：数据存储在本地，直到用户选择使用 [`setConsent`](../setconsent.md) 命令。 在页面加载之间，数据不会保留。

如果您的访客不属于《通用数据保护条例》(GDPR)的管辖范围，则默认同意可以设置为 `in`. GDPR管辖区内的访客可以将他们的默认同意设置为 `pending`. 您的同意管理平台(CMP)可以检测客户的区域并提供标记 `gdprApplies` 到IAB TCF 2.0。此标记可用于设置默认同意。

## 使用Web SDK标记扩展设置默认同意

在下选择所需的单选按钮 **[!UICONTROL 默认同意]** 时间 [配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 扩展]**，然后单击 **[!UICONTROL 配置]** 在 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下滚动到 [!UICONTROL 隐私] 部分，然后选择所需的 **[!UICONTROL 默认同意]**.
1. 单击 **[!UICONTROL 保存]**，然后发布更改。

## 使用Web SDK JavaScript库设置默认同意

设置 `defaultConsent` 字符串属性达到所需的同意级别 `configure` 命令。 此属性区分大小写，并且仅支持以下三个值： `"in"`， `"out"`、和 `"pending"`. 如果尝试使用任何其他值，则库会引发错误。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```
