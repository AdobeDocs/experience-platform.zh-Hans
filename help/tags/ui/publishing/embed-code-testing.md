---
title: 使用Adobe Experience Platform Debugger测试嵌入代码
description: 了解如何使用Platform Debugger在本地测试您网站上Adobe Experience Platform的不同嵌入代码。
exl-id: ae6183b9-0d25-49d0-b0e9-f8b5ba58ab33
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 62%

---

# 使用 Adobe Experience Platform Debugger 测试嵌入代码

>[!NOTE]
>
>Adobe Experience Platform Launch已更名为Adobe Experience Platform中的一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

当您更改Adobe Experience Platform中的标记库内部版本时，应先测试这些更改，然后再将该内部版本部署到生产环境。 如果您没有专门的网站暂存或开发环境，则可以使用 Adobe Experience Platform Debugger 在本地测试网站中的不同嵌入代码。

## 先决条件

本教程需要对标记环境和嵌入代码的使用有一定的了解。 有关更多信息，请参阅[环境概述](./environments.md)。

此外，本教程还要求您已安装 Platform Debugger 浏览器扩展。仅提供适用于 Chrome 和 Firefox 浏览器的 Platform Debugger。请先使用以下链接之一安装相应的扩展，然后再开始学习本教程：

* [适用于 Chrome 的 Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)
* [适用于 Firefox 的 Platform Debugger](https://addons.mozilla.org/zh-CN/firefox/addon/adobe-experience-platform-dbg/)

## 在您的网站上打开 Platform Debugger

使用您选择的浏览器，导航到您的网站并打开 Platform Debugger 扩展。窗口底部会显示 Platform Debugger 当前所连接的网站。如果您的网站上当前运行有标记，则该标记将列在 [!UICONTROL 摘要] 选项卡。

![](./images/embed-code-testing/summary.png)

>[!NOTE]
>
>如果 Platform Debugger 最初未连接，您可能需要先重新加载显示您网站的浏览器选项卡，然后再重试。

## 替换嵌入代码

Platform Debugger连接到您的网站后，选择 **[!UICONTROL Launch]** 左侧导航栏中。 在这里，您可以看到您的网站上当前正运行的库版本相关信息，包括运行环境和相关扩展。从此处选择 **[!UICONTROL 配置]** 以显示用于管理嵌入代码的控件。

![](./images/embed-code-testing/launch-tab.png)

下 [!UICONTROL 页面嵌入代码]，则会显示您的网站当前使用的嵌入代码。 选择 **[!UICONTROL 操作]** （位于嵌入代码的右侧），然后选择 **[!UICONTROL Replace]**.

![](./images/embed-code-testing/replace.png)

此时会出现一个弹出窗口，提示您提供用于替换当前代码的嵌入代码。请注意，使用 Platform Debugger 替换嵌入代码不会更改网站上已部署的嵌入代码。实际上，它只替换在本地运行的嵌入代码，以便您可以测试和调试其实施。

将要测试的嵌入代码粘贴到提供的文本框中，然后选择 **[!UICONTROL 应用]**.

![](./images/embed-code-testing/paste-code.png)

此 **[!UICONTROL 配置]** 此时，选项卡将重新显示，其中显示活动嵌入代码已替换为您提供的代码。 现在，您可以使用 Web 浏览器查看您正在测试的嵌入代码是否按预期工作。

![](./images/embed-code-testing/code-replaced.png)

## 后续步骤

本教程介绍了如何使用 Platform Debugger 在本地切换嵌入代码以进行测试。请参阅 [Platform Debugger 文档](../../../debugger/home.md)，了解有关其各种功能的更多信息。
