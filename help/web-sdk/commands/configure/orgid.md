---
title: orgId
description: orgId属性是一个字符串，用于告知Adobe将数据发送到哪个组织。
exl-id: 0e04e85a-800c-4927-a165-80a5a578f4c2
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# `orgId`

`orgId`属性是一个字符串，用于告知Adobe该数据将发送到哪个组织。 **使用Web SDK发送的所有数据都需要此属性。**

要查找您的`orgID`，请执行以下操作：

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 在Adobe Experience Cloud中的任何位置，按&#x200B;**`[Ctrl]`** + **`[I]`**。 将打开[!UICONTROL 用户数据调试器]窗口。
1. 单击[!UICONTROL 当前组织ID]旁边的&#x200B;**[!UICONTROL 复制]** ![复制](../../assets/copy.png)，或单击&#x200B;**[!UICONTROL 分配的组织]**&#x200B;选项卡以查看您可以访问的其他组织ID。
1. 完成查找所需信息后，单击&#x200B;**[!UICONTROL 关闭]**。

组织ID始终为24个字符的字母数字字符串，且始终以`@AdobeOrg`结尾。

## 使用Web SDK标记扩展配置`orgID`

在[配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)时，在&#x200B;**[!UICONTROL IMS组织ID]**&#x200B;文本字段中输入组织ID。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL 扩展]**，然后单击[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 配置]**。
1. 将所需的组织ID输入顶部附近的[!UICONTROL IMS组织ID]文本字段中。
1. 单击&#x200B;**[!UICONTROL 保存]**，然后发布更改。

## 使用Web SDK JavaScript库配置`orgID`

运行`configure`命令时设置`orgId`字符串。 如果在配置Web SDK时省略此属性，则Web SDK会引发控制台错误，并且数据不会发送到Adobe。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```
