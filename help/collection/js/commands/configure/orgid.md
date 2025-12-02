---
title: orgId
description: orgId属性是一个字符串，用于告知Adobe将数据发送到哪个组织。
exl-id: 0e04e85a-800c-4927-a165-80a5a578f4c2
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# `orgId`

`orgId`属性是一个字符串，用于告知Adobe将数据发送到哪个组织。 **使用Web SDK发送的所有数据都需要此属性。**

要查找您的`orgID`，请执行以下操作：

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 在Adobe Experience Cloud中的任何位置，按&#x200B;**`[Ctrl]`** + **`[I]`**。 此时会打开[!UICONTROL User Data Debugger]窗口。
1. 单击&#x200B;**[!UICONTROL Copy]**&#x200B;旁边的![ ](../../assets/copy.png)复制[!UICONTROL Current Org ID]，或单击&#x200B;**[!UICONTROL Assigned Orgs]**&#x200B;选项卡以查看您可以访问的其他组织ID。
1. 完成查找所需信息后，单击&#x200B;**[!UICONTROL Close]**。

组织ID始终为24个字符的字母数字字符串，且始终以`@AdobeOrg`结尾。

运行`orgId`命令时设置`configure`字符串。 如果在配置Web SDK时忽略此属性，则Web SDK会引发控制台错误，并且数据不会发送到Adobe。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

## 使用Web SDK标记扩展设置组织ID

可以使用[SDK实例配置设置](/help/tags/extensions/client/web-sdk/configure/general.md)在Web SDK标记扩展中配置此设置。 字段会根据创建标记属性的组织自动填充。
