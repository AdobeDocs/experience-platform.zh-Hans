---
title: 应用程序内消息传送视图
description: 本指南详细介绍了Adobe Experience Platform Assurance中应用程序内消息传送视图的信息。
exl-id: 6131289a-aebb-4b3a-9045-4b2cf23415f8
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---

# Assurance中的“应用程序内消息传送”视图

Adobe Experience Platform Assurance中的“应用程序内消息传送”视图能够验证您的应用程序、监测传送到您设备的应用程序内消息以及模拟发送到您设备的消息。

## 设备上的消息

在顶部 **[!UICONTROL 设备上的消息]** 制表符为 **[!UICONTROL 消息]** 下拉菜单。 这将包括已在Assurance会话中收到的所有消息。 如果消息不在此列表中，则意味着应用程序从未收到该消息。

![消息](./images/in-app-messaging/message.png)

选择消息将显示有关该消息的许多信息，如下节所述。

### 消息预览

在右侧面板中为 **[!UICONTROL 消息预览]** 窗格，显示消息的预览。 选择 **[!UICONTROL 在设备上模拟]** 会将该消息发送到当前连接到会话的任何设备。

![预览](./images/in-app-messaging/preview.png)

### 消息行为

在 **[!UICONTROL 消息预览]** 窗格是 **[!UICONTROL 消息行为]** 选项卡。 其中包含有关消息显示方式的所有详细信息。 此信息包括定位信息、动画、轻扫手势和外观设置。

![行为](./images/in-app-messaging/gestures.png)

### “信息”选项卡

在左侧部分，有四个选项卡显示有关消息的详细信息。 此 **[!UICONTROL 信息]** 选项卡显示从Adobe Journey Optimizer (AJO)加载的关于消息促销活动的信息。

您还可以选择 **[!UICONTROL 查看营销活动]** 以在AJO中打开消息进行检查或编辑。

![信息](./images/in-app-messaging/info.png)

### “规则”选项卡

此 **[!UICONTROL 规则]** 选项卡显示需要发生什么才会显示此消息。 这可以让您深入了解触发消息显示的确切内容。 查看此示例：

![规则](./images/in-app-messaging/rules.png)

此示例显示了规则的三个不同条件。 如果选择某个事件（从事件列表、“分析”选项卡或时间线中），则将根据这些规则评估该事件。 如果事件与某个条件匹配，则会显示绿色复选标记：

![规则匹配](./images/in-app-messaging/rule-match.png)

如果事件不匹配，将显示一个红色图标：

![规则不匹配](./images/in-app-messaging/rule-mismatch.png)

如果三个条件都与当前事件匹配，则会显示消息。

### “分析”选项卡

此 **[!UICONTROL 分析]** 选项卡提供有关规则的更多分析。 在本例中，我们根据消息规则与事件的匹配程度筛选会话中的每个事件。

![分析](./images/in-app-messaging/analyze.png)

在以下示例中 **[!UICONTROL “规则”选项卡]** 部分，规则中包含三个条件。 此选项卡显示每个事件匹配的规则百分比。 大多数的比赛是33%（三个条件之一），其余的比赛是100%。

因此，您可以查找接近匹配但未完全匹配规则的事件。

![阈值](./images/in-app-messaging/threshold.png)

此 **[!UICONTROL 匹配阈值]** 通过滑块，可筛选应显示哪些事件。 例如，可将此值设置为50% - 90%，以获取与三个条件中的两个完全匹配的事件列表。

### “交互”选项卡

此 **[!UICONTROL 交互]** 选项卡显示出于跟踪目的而发送到Edge的交互事件列表。

![交互](./images/in-app-messaging/interactions.png)

每当显示消息时，通常有四个交互事件：

```
trigger > display > interact > dismiss
```

“interact”交互具有与其关联的附加“action”值。 可能的值包括“已单击”或“取消”。

验证列显示Edge是否正确接收和处理了交互事件。

## 验证

此 **[!UICONTROL 验证]** 选项卡针对当前会话运行验证，检查应用程序是否已正确配置为应用程序内消息传送：

![验证](./images/in-app-messaging/validation.png)

如果发现任何错误，将提供有关如何修复这些错误的详细信息。

## 事件列表

![验证](./images/in-app-messaging/event-list.png)

此 **[!UICONTROL 事件列表]** 选项卡可快速查看与应用程序内消息传送相关的保障会话中的所有事件。 您可以在此处看到的一些活动包括：

* 检索消息的请求和响应
* 显示消息事件
* 交互跟踪事件

在此视图中，您可以使用许多标准事件列表功能，包括应用搜索、应用过滤器、添加或删除列以及导出数据。

选择一个事件，以在右侧面板中查看该事件的原始详细信息。

从右侧详细信息面板中，可以标记选定的事件，这有助于标记应由其他人审阅的内容。
