---
title: 使用Adobe Experience Platform Assurance
description: 本指南介绍在安装和实施Adobe Experience Platform Assurance后如何使用它。
source-git-commit: 24f452bdb923179eefe53fdb28d3a92d43e533cd
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# 使用Adobe Experience Platform Assurance

本教程介绍如何使用Adobe Experience Platform Assurance。 有关如何安装和实施Adobe Experience Platform Assurance扩展的说明，请阅读 [实施保证扩展](./implement-assurance.md).

## 创建会话

登录后 [保证UI](https://experience.adobe.com/assurance)，您可以选择 **[!UICONTROL 创建会话]** 开始创建会话。

![此时会突出显示创建会话按钮，其中显示了可在何处创建会话。](./images/using-assurance/create-session.png)

的 **[!UICONTROL 创建新会话]** 对话框。 请查看给定的说明，并通过选择 **[!UICONTROL 开始]**.

![此时会显示“创建新会话”对话框，其中显示了有关如何使用“保证”的说明。](./images/using-assurance/create-new-session.png)

您现在可以输入用于标识会话的名称，然后提供 **[!UICONTROL 基本URL]** （您的应用程序的深层链接URL）。 提供这些详细信息后，选择 **[!UICONTROL 下一个]**.

>[!INFO]
>
>基本URL是用于从URL启动应用程序的根定义。 会话URL将生成，您可以通过该URL启动保证会话。 示例值可能如下所示： `myapp://default` 在 **[!UICONTROL 基本URL]** 字段中，键入应用程序的基本深层链接定义。

![将显示创建新会话的完整工作流。](./images/using-assurance/create-session.gif)

## 连接到会话

创建会话后，请确保看到 **[!UICONTROL 创建新会话]** 对话框现在会显示链接、二维码和个人识别码。

![将显示一个对话框，其中显示了用于连接到保证会话的选项。](./images/using-assurance/create-new-session-pin.png)

如果出现此对话框，您可以使用设备的相机应用程序扫描二维码并打开应用程序，或复制链接并在应用程序中打开。 当您的应用程序启动时，您应会看到覆盖的PIN条目屏幕。 在上一步中键入PIN并按 **[!UICONTROL 连接]**.

当应用程序上显示Adobe Experience Platform图标(红色Adobe“A”)时，您可以验证您的应用程序是否已连接到保障。

![将显示将应用程序连接到保证会话的完整工作流。](./images/using-assurance/connect-session.gif)

## 导出会话

要导出保证会话，请在应用程序的会话详细信息页面上，选择 **[!UICONTROL 导出到JSON]** 在会话中：

![导出会话](./images/using-assurance/export-session.png)

导出选项遵循搜索过滤器结果，并且只导出事件视图中显示的事件。 例如，如果您搜索了“track”事件，然后选择 **[!UICONTROL 导出到JSON]**，则仅导出“track”事件结果。
