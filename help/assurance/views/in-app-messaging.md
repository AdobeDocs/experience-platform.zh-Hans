---
title: 应用程序内消息传送视图
description: 本指南详细介绍了Adobe Experience Platform Assurance中的应用程序内消息传送视图。
source-git-commit: 5778d4db27d0f57281821dc8e042a31b69745514
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---


# Assurance中的应用程序内消息传送视图

Adobe Experience Platform Assurance中的应用程序内消息传送视图提供了以下功能：验证您的应用程序，监控交付到您的设备的应用程序内消息，以及模拟发送到您设备的消息。

## 设备上的消息

在 **[!UICONTROL 设备上的消息]** 选项卡 **[!UICONTROL 消息]** 下拉列表。 这将包括在保证会话中收到的所有消息。 如果此列表中没有消息，则表示应用程序从未收到该消息。

![消息](./images/in-app-messaging/message.png)

选择消息将显示有关该消息的大量信息，如以下各节所述。

### 消息预览

在右侧面板中， **[!UICONTROL 消息预览]** 窗格，显示消息的预览。 选择 **[!UICONTROL 在设备上模拟]** 将向当前连接到会话的任何设备发送该消息。

![预览](./images/in-app-messaging/preview.png)

### 消息行为

在 **[!UICONTROL 消息预览]** 窗格 **[!UICONTROL 消息行为]** 选项卡。 其中包含有关消息显示方式的所有详细信息。 此信息包括定位信息、动画、轻扫手势和外观设置。

![行为](./images/in-app-messaging/gestures.png)

### “信息”选项卡

在左侧，有四个选项卡，显示有关消息的详细信息。 的 **[!UICONTROL 信息]** 选项卡显示从Adobe Journey Optimizer(AJO)加载的有关消息营销活动的信息。

您还可以选择 **[!UICONTROL 查看营销活动]** 以在AJO中打开消息进行检查或编辑。

![信息](./images/in-app-messaging/info.png)

### “规则”选项卡

的 **[!UICONTROL 规则]** 选项卡，显示显示此消息需要执行的操作。 这可以深入分析哪些因素会触发要显示的消息。 查看此示例：

![规则](./images/in-app-messaging/rules.png)

该示例显示了规则的三个不同条件。 如果您（从事件列表、分析选项卡或时间轴中）选择事件，则会根据这些规则评估该事件。 如果事件与条件匹配，则会显示绿色复选标记：

![规则匹配](./images/in-app-messaging/rule-match.png)

如果事件不匹配，则会显示红色图标：

![规则不匹配](./images/in-app-messaging/rule-mismatch.png)

如果所有三个条件都与当前事件匹配，则会显示消息。

### “分析”选项卡

的 **[!UICONTROL 分析]** 选项卡提供了有关规则的更多分析。 在此，我们会根据消息规则与会话事件的接近度，筛选会话中的每个事件。

![分析](./images/in-app-messaging/analyze.png)

在 **[!UICONTROL “规则”选项卡]** 部分，规则中有三个条件。 此选项卡显示每个事件所匹配的规则的百分比。 大多数事件的匹配率为33%（三个条件中的一个），其余的匹配率为100%。

因此，您可以找到接近匹配但不完全匹配规则的事件。

![阈值](./images/in-app-messaging/threshold.png)

的 **[!UICONTROL 匹配阈值]** 滑块可让您过滤应显示的事件。 例如，可以将此值设置为50% - 90%，以获取与三个条件中的两个完全匹配的事件列表。

### “交互”选项卡

的 **[!UICONTROL 交互]** 选项卡显示出于跟踪目的发送到Edge的交互事件列表。

![交互](./images/in-app-messaging/interactions.png)

每当显示消息时，通常会有四个交互事件：

```
trigger > display > interact > dismiss
```

“交互”交互具有与其关联的其他“操作”值。 可能的值包括“已单击”或“取消”。

验证列显示Edge是否正确接收和处理了交互事件。

## 验证

的 **[!UICONTROL 验证]** 选项卡会针对您的当前会话运行验证，并检查应用程序是否已正确配置了应用程序内消息传送：

![验证](./images/in-app-messaging/validation.png)

如果发现任何错误，将提供有关如何修复这些错误的详细信息。

## 事件列表

![验证](./images/in-app-messaging/event-list.png)

的 **[!UICONTROL 事件列表]** 选项卡提供了有关“保证”会话中与应用程序内消息传送相关的所有事件的概览。 您可能会在此处看到以下事件：

* 用于检索消息的请求和响应
* 显示消息事件
* 交互跟踪事件

在此视图中，您可以使用许多标准事件列表功能，包括应用搜索、应用过滤器、添加或删除列以及导出数据。

选择一个事件，以在右侧面板中查看该事件的原始详细信息。

从右侧的详细信息面板中，可以标记选定的事件，这有助于标记应由其他人审阅的内容。
