---
title: 使用标记扩展安装Web SDK
description: 使用Adobe Experience Cloud数据收集引用Web SDK库。
exl-id: ba8348c9-f642-4230-9f7f-4496d4154d83
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 使用标记扩展安装Web SDK

Adobe提供了一个专用的标记扩展来实施和配置Web SDK。 此实施方法是Adobe推荐用于部署和维护数据收集代码的主要方法。

满足[先决条件](overview.md)后，可以使用以下步骤部署Web SDK标记扩展：

## 在标记中安装扩展

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**。
1. 选择所需的标记属性，或创建标记属性。
1. 导航到&#x200B;**[!UICONTROL 扩展]**，然后选择&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡。
1. 找到并安装&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**&#x200B;扩展。
1. 为每个环境选择适当的沙盒和数据流，然后单击&#x200B;**[!UICONTROL 保存]**。

有关详细信息，请参阅有关如何[配置Web SDK标记扩展](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)的文档。

## Publish要开发的标记代码

现在已为此标记安装了Web SDK扩展。 您现在可以发布标记代码以在开发环境中使用。

1. 导航到&#x200B;**[!UICONTROL 发布流]**，然后选择&#x200B;**[!UICONTROL 添加库]**。
1. 为此库指定所需的名称，如“添加Web SDK库”。 将[!UICONTROL 环境]下拉菜单设置为“开发”。
1. 选择&#x200B;**[!UICONTROL 添加所有更改的资源]**，然后单击&#x200B;**[!UICONTROL 保存并生成到开发]**。

## 在网站上安装加载器代码

现在，标记代码已发布，您可以将标记加载器代码添加到您的网站。

1. 导航到&#x200B;**[!UICONTROL 环境]**，然后单击“开发”旁边的框图标以打开包含此环境的安装说明的模式窗口。
1. 复制嵌入代码并将其粘贴到网站的`<head>`标记中。

## 填写实施并发布到生产环境

有关扩展本身的更多信息，请参阅[Web SDK扩展概述](../../tags/extensions/client/web-sdk/overview.md)；有关导航标记界面的更多信息，请参阅[标记概述](../../tags/home.md)。
