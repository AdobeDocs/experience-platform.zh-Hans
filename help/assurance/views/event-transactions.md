---
title: 事件交易记录视图
description: 本指南详细介绍了有关Adobe Experience Platform Assurance中的“事件交易”视图的信息。
exl-id: ad97f2c1-5bbc-49e2-8378-edcb8af149a3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---

# “事件事务处理”视图

Adobe Experience Platform Assurance中的“事件交易”视图允许您验证和调试Edge Network客户端实施，并近乎实时地查看上游验证结果。

## 为Edge Network工作流设置保证

晚于 [设置Assurance](../tutorials/implement-assurance.md)，确保已在应用程序中实施最新版本的Assurance和Edge Network扩展。

要查看您的事件，请从左侧菜单中选择 **[!UICONTROL 事件事务]** 在 **[!UICONTROL Adobe Experience Platform Edge]** 部分。

如果没有看到此选项，请选择 **[!UICONTROL 配置]** 在窗口的左下角，添加 **[!UICONTROL 事件事务]** 查看和选择 **[!UICONTROL 保存]**.

## 开始使用“事件事务处理”视图

在此部分中，熟悉事件交易视图，并了解如何有效地使用它在Edge Network工作流上进行端到端验证。

### 事件处理流程

![事件交易记录视图](./images/event-transactions/event-transactions-view.png)

“事件事务处理”视图按事件处理流的顺序显示三个列：

- **[!UICONTROL 客户端]**：此列显示客户端处理或接收的事件，可由Mobile SDK访问。 这包括使用API调用创建的事件，例如 `Edge.sendEvent`和客户端从Edge Network服务器接收的响应事件句柄（如果有）。 客户端事件示例：
   - AEP请求事件是通过Edge扩展发送的事件，包含XDM和可选的自由格式数据。
   - AEP响应事件句柄是从Edge Network收到的响应AEP请求事件的事件句柄。 一个请求事件可以接收无、一个或多个响应事件句柄。
   - 在出现错误的情况下，可能会看到AEP错误响应，例如，如果无法处理XDM有效负载或某个上游服务返回了错误或警告。
- **[!UICONTROL 边缘网络]**：此列显示Edge Network通过网络请求在服务器端收到的事件，以及该事件包含的数据和元数据。
- **[!UICONTROL 上游]**：此列显示配置的上游服务接收的事件，包括有关传入事件的处理和/或验证结果的详细信息。
请注意，此列是动态的，可能会根据以下两个主要因素显示不同类型的信息：
   - 数据流配置和在其上启用的服务。
   - 发送到Edge Network的事件类型。

### Inspect事件

“事件事务处理”视图中显示的事件提供了有关每个状态下正在处理的数据的格式和内容的信息，以及有关上游处理数据时遇到的任何警告或错误的深入详细信息。 该视图有助于缩小事件/请求级别的调试信息范围，并可在开发周期早期识别错误。

#### 展开事件详细信息

要检查事件，请从视图中选择所需的事件。 此操作将展开 **[!UICONTROL 事件详细信息]** 在屏幕右侧查看。
嵌套数据以树格式显示。 您可以通过选择 **+** 键名称左侧的（加号）按钮。

![事件详细信息](./images/event-transactions/event-details.png)

#### Inspect警告或错误

每个事件名称都有一个图标作为前缀，该图标指示该事件处理的高级状态：

- 如果已成功处理事件，则会显示绿色复选标记。
- 如果检测到警告或错误，将显示警告符号。 选择相关事件，以详细了解 **[!UICONTROL 事件详细信息]** 视图。

### 配置设置

您可以通过选择旁边的信息工具提示来检查当前使用的数据流标识符。 **[!UICONTROL 边缘网络]** 列标题。

![显示数据流Id](./images/event-transactions/show-datastream-id.png)

>[!INFO]
>
>当多个客户端连接到同一保证会话并使用不同的数据流ID时，您将看到此处显示的所有这些ID。 但是，这并不意味着您当前的实施正在使用多个数据流。 只有应用程序使用的标记（移动属性）中设置的当前数据流ID才能用于处理来自该客户端的新事件。 当测试具有不同配置设置且连接了多个客户端的更复杂的用例时，使用单独的保证会话来简化验证过程可能很有帮助。
