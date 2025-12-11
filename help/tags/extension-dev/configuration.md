---
title: 扩展配置
description: 了解如何在Adobe Experience Platform UI或数据收集UI中配置标记扩展以从用户那里收集全局设置。
exl-id: 2bf33617-1398-499f-8325-3849dbdb1f97
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 69%

---

# 扩展配置

扩展配置是扩展从用户那里收集全局设置的方式。例如，假定某个扩展允许用户使用“发送信标”操作发送信标，并且该信标必须始终包含帐户 ID。我们不想在用户每次配置“发送信标”操作时都询问其帐户 ID，这会给用户增添一些麻烦。取而代之的是，扩展应从扩展配置视图中询问一次帐户 ID。每次发送信标时，“发送信标”操作库模块都可从扩展配置中提取帐户 ID 并将其添加到信标。

当用户将扩展安装到Adobe Experience Platform中的标记属性时，将向用户显示扩展将提供的扩展配置视图。 如果未完成扩展配置，用户将无法完成扩展的安装。请参阅有关[视图](./web/views.md)的文档，以了解如何创建扩展配置视图。

从扩展配置视图中保存设置后，这些设置将会发出到标记运行时库。 随后，您可以通过调用 [`turbine.getExtensionSettings()`](./turbine.md#get-extension-settings)，从扩展库模块中访问这些设置。

扩展配置是一项可选功能，您可以选择不使用这项功能。
