---
title: 使用 Adobe Experience Platform Assurance
description: 本指南解释了安装并实施 Adobe Experience Platform Assurance 后如何使用它。
exl-id: 872c83d1-82e8-40d8-9b66-3e51a91a955f
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 100%

---

# 使用 Adobe Experience Platform Assurance

本教程介绍了如何使用 Adobe Experience Platform Assurance。有关如何安装和实施 Adobe Experience Platform Assurance 扩展程序的说明，请阅读有关[实施 Assurance 扩展程序](./implement-assurance.md)的教程。

## 创建会话

登录[ Assurance UI ](https://experience.adobe.com/assurance)后，您可以选择&#x200B;**[!UICONTROL 创建会话]**，以开始创建会话。

![创建会话按钮会突出显示，提示您可以在哪里创建会话。](./images/using-assurance/create-session.png)

**[!UICONTROL 创建新会话]**&#x200B;对话框出现。请查看给定的说明，然后选择&#x200B;**[!UICONTROL 开始]**&#x200B;以继续。

![“创建新会话”对话框会出现，其中显示有关如何使用 Assurance 的说明。](./images/using-assurance/create-new-session.png)

您现在可以通过输入一个名称来标识会话，然后提供一个 **[!UICONTROL BASE URL]**（您的应用程序的深层链接 URL）。提供这些详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

>[!INFO]
>
>基础 URL 是用于从 URL 启动应用程序的根定义。系统会生成一个会话 URL，您可以通过该 URL 启动 Assurance 会话。示例值可能如下所示：`myapp://default`在&#x200B;**[!UICONTROL 基础 URL]**&#x200B;字段中，输入您应用程序的基础深层链接定义。

![创建新会话的完整工作流程会出现。](./images/using-assurance/create-session.gif)

## 连接到会话

创建会话后，请确保您看到&#x200B;**[!UICONTROL 创建新会话]**&#x200B;对话框现在显示一个链接、一个 QR 代码和一个 PIN。

![一个显示连接到 Assurance 会话选项的对话框会出现。](./images/using-assurance/create-new-session-pin.png)

如果出现此对话框，您可以使用设备的相机应用程序扫描二维码并打开您的应用程序，或者复制链接并在您的应用程序中打开。当您的应用程序启动时，您应该会看到 PIN 条目屏幕重叠。输入上一步中的 PIN，然后按&#x200B;**[!UICONTROL 连接]**。

当您的应用程序上显示 Adobe Experience Platform 图标（红色 Adobe“A”）时，您可以验证您的应用程序是否已连接到 Assurance。

![将应用程序连接到 Assurance 会话的完整工作流程将会显示。](./images/using-assurance/connect-session.gif)

## 导出会话

要导出 Assurance 会话，请在应用程序的会话详细信息页面上，在会话中选择&#x200B;**[!UICONTROL 导出为 JSON]**：

![导出会话](./images/using-assurance/export-session.png)

导出选项尊重搜索筛选的结果&#x200B;&#x200B;，仅会导出事件视图中显示的事件。例如，如果您搜索“跟踪”事件，然后选择&#x200B;**[!UICONTROL 导出为 JSON]**，则仅会导出“跟踪”事件结果。
