---
title: 使用 Adobe Experience Platform Assurance
description: 本指南解释了安装并实施 Adobe Experience Platform Assurance 后如何使用它。
exl-id: 872c83d1-82e8-40d8-9b66-3e51a91a955f
source-git-commit: f8576e7f7e1da7351f7860cba27d5d09d0161132
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 28%

---

# 使用 Adobe Experience Platform Assurance

本教程介绍了如何使用 Adobe Experience Platform Assurance。有关如何安装和实施 Adobe Experience Platform Assurance 扩展程序的说明，请阅读有关[实施 Assurance 扩展程序](./implement-assurance.md)的教程。

## 创建会话

登录[Assurance UI](https://experience.adobe.com/assurance)后，您可以选择&#x200B;**[!UICONTROL Create Session]**&#x200B;开始创建会话。

![创建会话按钮会突出显示，提示您可以在哪里创建会话。](./images/using-assurance/create-session.png)

此时将显示&#x200B;**[!UICONTROL Create New Session]**&#x200B;对话框，其中包含两个用于创建会话的选项：

### 深层链接连接

选择此选项可生成唯一的会话URL、QR代码和PIN。 扫描二维码或在应用程序中手动打开会话链接，然后输入PIN码以建立连接。

选择&#x200B;**[!UICONTROL Deep link connect]**，然后选择&#x200B;**[!UICONTROL Start]**&#x200B;以继续。

![已选择“创建新会话”对话框，其中显示了“深层链接连接”选项。](./images/using-assurance/create-new-session-deep-link.png)

您现在可以输入名称来标识会话，然后提供&#x200B;**[!UICONTROL Base URL]**（应用程序的深层链接URL）。 提供这些详细信息后，选择&#x200B;**[!UICONTROL Next]**。

>[!INFO]
>
>基础 URL 是用于从 URL 启动应用程序的根定义。系统会生成一个会话 URL，您可以通过该 URL 启动 Assurance 会话。示例值可能如下所示： `myapp://default`在&#x200B;**[!UICONTROL Base URL]**&#x200B;字段中，键入应用程序的基本深层链接定义。

![将显示会话名称和基本URL输入字段。](./images/using-assurance/create-session-form-deep-link.png)

### 快速连接

触发来自应用程序的连接，设备将显示在可用设备列表中。 选择&#x200B;**[!UICONTROL Quick connect]**&#x200B;以创建Assurance会话。

#### 先决条件

在使用Quick Connect之前，请确保您的应用程序具有所需的SDK版本和实施：

**Android SDK要求：**

- Mobile Core v3.1.0 或更高版本
- Adobe Journey Optimizer v3.1.0 或更高版本
- Adobe Experience Platform Assurance v3.0.4或更高版本

**iOS SDK要求：**

- Mobile Core v5.2.0 或更高版本
- Adobe Journey Optimizer v5.1.1 或更高版本
- Adobe Experience Platform Assurance v5.0.0或更高版本

**实现：**

您的应用程序必须实施[`startSession` API](https://developer.adobe.com/client-sdks/home/base/assurance/api-reference/#startsession-quick-connect)才能触发Assurance连接。 此API调用通常包含在操作集中或在应用程序中触发。

#### 创建快速连接会话

![已选择“创建新会话”对话框，其中显示了“快速连接”选项。](./images/using-assurance/create-new-session-quick-connect.png)

选择&#x200B;**[!UICONTROL Quick connect]**，然后选择&#x200B;**[!UICONTROL Start]**&#x200B;继续操作，您将看到设备选取器界面：

1. **触发Assurance连接** — 在您的移动应用程序或实现中，触发使用`startSession` API启动Assurance连接的操作。 这将使您的设备可发现。

2. **选择并连接你的设备** — 你的设备一旦出现在可用设备列表中，请选择它并单击&#x200B;**[!UICONTROL Connect]**。

![显示可用设备的Quick Connect设备选择器接口。](./images/using-assurance/quick-connect-device-picker.png)

## 连接到会话

连接的步骤取决于您使用的会话类型：

### 深层链接连接会话

对于使用&#x200B;**[!UICONTROL Deep Link Connect]**&#x200B;创建的会话：

1. 导航到会话详细信息页面（适用于现有会话）或继续创建会话以查看链接、二维码和PIN
2. 使用您设备的相机应用程序扫描二维码，或复制链接并在应用程序中打开
3. 应用程序启动时，您会看到PIN输入屏幕被覆盖。 输入PIN并按&#x200B;**[!UICONTROL Connect]**

![一个显示连接到 Assurance 会话选项的对话框会出现。](./images/using-assurance/deep-link-connection.png)

### 快速连接会话

对于使用&#x200B;**[!UICONTROL Quick Connect]**&#x200B;创建的会话（可由以`adobeassurance://`开头的会话URL识别），通过设备选取器界面自动进行连接：

1. 导航到会话详细信息页面（适用于现有会话）或继续创建会话
2. 在&#x200B;**[!UICONTROL Connect Device]**&#x200B;部分中，您将看到设备选取器界面
3. 触发在应用程序中设置的操作，以便发现设备
4. 从列表中选择您的设备，然后单击&#x200B;**[!UICONTROL Connect]**

![设备选择器接口显示要连接的可用设备。](./images/using-assurance/quick-connect-device-picker.png)

### 正在验证连接

当您的应用程序上显示 Adobe Experience Platform 图标（红色 Adobe“A”）时，您可以验证您的应用程序是否已连接到 Assurance。

## 导出会话

要导出Assurance会话，请在应用程序的会话详细信息页面上，选择会话中的&#x200B;**[!UICONTROL Export to JSON]**：

![导出会话](./images/using-assurance/export-session.png)

导出选项尊重搜索筛选的结果&#x200B;&#x200B;，仅会导出事件视图中显示的事件。例如，如果您搜索“track”事件，然后选择&#x200B;**[!UICONTROL Export to JSON]**，则仅导出“track”事件结果。