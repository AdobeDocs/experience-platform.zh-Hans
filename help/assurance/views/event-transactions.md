---
title: 事件交易视图
description: 本指南详细介绍了 Adobe Experience Platform Assurance 中的事件交易视图的信息。
exl-id: ad97f2c1-5bbc-49e2-8378-edcb8af149a3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 100%

---

# 事件交易视图

Adobe Experience Platform Assurance 中的事件交易视图允许您验证和调试 Edge Network 客户端实施，并可近乎实时地查看上游验证结果。

## 为 Edge Network 工作流程设置 Assurance

在[设置 Assurance](../tutorials/implement-assurance.md) 后，确保您已在应用程序中实施最新版本的 Assurance 和 Edge Network 扩展。

要查看您的事件，请从左侧菜单中，在 **[!UICONTROL Adobe Experience Platform Edge]** 部分下选择&#x200B;**[!UICONTROL 事件交易]**。

如果您没有看到此选项，请在窗口的左下角选择&#x200B;**[!UICONTROL 配置]**，添加&#x200B;**[!UICONTROL 事件交易]**&#x200B;视图，然后选择&#x200B;**[!UICONTROL 保存]**。

## 开始使用事件交易视图

在本节中，熟悉事件交易视图，并了解如何有效地使用它对 Edge Network 工作流程进行端到端验证。

### 事件处理流程

![事件交易视图](./images/event-transactions/event-transactions-view.png)

事件交易视图按事件处理流程的顺序显示三列：

- **[!UICONTROL 客户端]**：此列显示客户端处理或接收的事件，可供 Mobile SDK 访问。这包括使用 API 调用创建的事件，例如 `Edge.sendEvent`，以及客户端从 Edge Network 服务器接收到的响应事件句柄（如果有）。客户端事件示例：
   - AEP 请求事件是通过边缘扩展发送的事件，并包含 XDM 和可选的自由格式数据。
   - AEP 响应事件句柄是从 Edge Network 接收的响应 AEP 请求事件的事件句柄。请求事件可以不接收、接收一个或多个响应事件句柄。
   - 在发生错误时可能会看到 AEP 错误响应，例如，如果无法处理 XDM 有效负载或者上游服务之一返回错误或警告时。
- **[!UICONTROL Edge Network]**：此列显示 Edge Network 通过网络请求在服务器端接收到的事件以及该事件包含的数据和元数据。
- **[!UICONTROL 上游]**：此列显示已配置的上游服务接收到的事件，包括有关传入事件的处理和/或验证结果的详细信息。
请注意，此列是动态的，可能会根据两个主要因素显示不同类型的信息：
   - 数据流配置及其上启用的服务。
   - 发送到 Edge Network 的事件类型。

### 检查事件

“事件交易”视图中显示的事件提供有关每个状态下正在处理的数据的格式和内容的信息，以及有关在上游处理数据时遇到的任何警告或错误的深入详情。该视图有助于缩小事件/请求级别的调试信息范围，并在开发周期的早期识别错误。

#### 展开事件详情

要检查事件，请从视图中选择所需的事件。该操作可扩展屏幕右侧的&#x200B;**[!UICONTROL 事件详情]**视图。
嵌套数据以树形格式显示。您可以通过选择键名称左侧的 **+**（加号）按钮来检查嵌套的键值。

![事件详细信息](./images/event-transactions/event-details.png)

#### 检查警告或错误

每个事件名称都带有一个图标前缀，该图标指示该事件处理的高级状态：

- 如果事件处理成功，则会显示绿色复选标记。
- 如果检测到警告或错误，则会显示警告标志。在&#x200B;**[!UICONTROL 事件详细信息]**&#x200B;视图中，选择相关事件以了解有关警告或错误原因的更多信息。

### 配置设置 

可通过选择 **[!UICONTROL Edge Network]** 列标题旁的信息工具提示而检查当前使用的数据流标识符。

![显示数据流 ID](./images/event-transactions/show-datastream-id.png)

>[!INFO]
>
>当多个客户端连接到同一个 Assurance 会话并使用不同的数据流 ID 时，您会在此处看到所有这些 ID。但是，这并不意味着您当前的实施正在使用多个数据流。仅应用程序使用的标记（移动设备）中设置的当前数据流 ID 会用于处理来自该客户端的新事件。在测试具有不同的配置设置和多个相连客户端的更为复杂的用例时，建议使用单独的 Assurance 会话来简化验证过程。
