---
title: 使用Adobe Experience Platform Debugger测试嵌入代码
description: 了解如何使用Experience Platform Debugger在本地测试您网站上Adobe Experience Platform的各种嵌入代码。
exl-id: ae6183b9-0d25-49d0-b0e9-f8b5ba58ab33
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 34%

---

# 使用 Adobe Experience Platform Debugger 测试嵌入代码

>[!NOTE]
>
>经过品牌重塑，Adobe Experience Platform Launch 已变为 Adobe Experience Platform 中的一套数据收集技术。因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

当您更改Adobe Experience Platform中的标记库内部版本时，应先测试这些更改，然后再将内部版本部署到生产环境。 如果您没有专门的网站暂存或开发环境，则可以使用 Adobe Experience Platform Debugger 在本地测试网站中的不同嵌入代码。

## 先决条件

本教程需要对标记环境和嵌入代码的使用有一定的了解。 有关更多信息，请参阅[环境概述](./environments.md)。

此外，本教程还要求您已安装Experience Platform Debugger浏览器扩展。 Experience Platform Debugger可用于Chrome浏览器。 请在开始本教程之前，使用以下链接安装扩展：

* 适用于Chrome的[Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

## 在您的网站上打开Experience Platform Debugger

使用您选择的浏览器，导航到您的网站并打开Experience Platform Debugger扩展。 窗口底部会显示Experience Platform Debugger当前所连接的网站。 如果您的网站上当前正在运行标记，则标记将列在[!UICONTROL 摘要]选项卡中。

![](./images/embed-code-testing/summary.png)

>[!NOTE]
>
>如果Experience Platform Debugger最初未连接，您可能需要先重新加载显示您网站的浏览器选项卡，然后重试。

## 替换嵌入代码

Experience Platform Debugger连接到您的网站后，请在左侧导航中选择&#x200B;**[!UICONTROL Launch]**。 在这里，您可以看到您的网站上当前正运行的库版本相关信息，包括运行环境和相关扩展。从此处选择&#x200B;**[!UICONTROL 配置]**&#x200B;以显示用于管理嵌入代码的控件。

![](./images/embed-code-testing/launch-tab.png)

在[!UICONTROL 页面嵌入代码]下，将显示您的网站当前使用的嵌入代码。 选择嵌入代码右侧的&#x200B;**[!UICONTROL 操作]**，然后选择&#x200B;**[!UICONTROL 替换]**。

![](./images/embed-code-testing/replace.png)

此时会出现一个弹出窗口，提示您提供用于替换当前代码的嵌入代码。请注意，使用Experience Platform Debugger替换嵌入代码不会更改网站上已部署的嵌入代码。 实际上，它只替换在本地运行的嵌入代码，以便您可以测试和调试其实施。

将要测试的嵌入代码粘贴到提供的文本框中，然后选择&#x200B;**[!UICONTROL 应用]**。

![](./images/embed-code-testing/paste-code.png)

**[!UICONTROL 配置]**&#x200B;选项卡重新出现，其中显示活动嵌入代码已替换为您提供的代码。 现在，您可以使用 Web 浏览器查看您正在测试的嵌入代码是否按预期工作。

![](./images/embed-code-testing/code-replaced.png)

## 后续步骤

本教程介绍了如何使用Experience Platform Debugger在本地切换嵌入代码以进行测试。 请参阅[Experience Platform Debugger文档](../../../debugger/home.md)，了解有关其各种功能的更多信息。
