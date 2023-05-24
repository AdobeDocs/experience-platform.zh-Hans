---
title: 扩展配置
description: 瞭解如何設定標籤擴充功能，以從Adobe Experience Platform UI或資料收集UI的使用者收集全域設定。
exl-id: 2bf33617-1398-499f-8325-3849dbdb1f97
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 68%

---

# 扩展配置

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../term-updates.md)。

扩展配置是扩展从用户那里收集全局设置的方式。例如，假定某个扩展允许用户使用“发送信标”操作发送信标，并且该信标必须始终包含帐户 ID。我们不想在用户每次配置“发送信标”操作时都询问其帐户 ID，这会给用户增添一些麻烦。取而代之的是，扩展应从扩展配置视图中询问一次帐户 ID。每次发送信标时，“发送信标”操作库模块都可从扩展配置中提取帐户 ID 并将其添加到信标。

當使用者將擴充功能安裝至Adobe Experience Platform中的標籤屬性時，將會看到您的擴充功能將提供的擴充功能組態檢視。 如果未完成扩展配置，用户将无法完成扩展的安装。请参阅有关[视图](./web/views.md)的文档，以了解如何创建扩展配置视图。

從擴充功能組態檢視儲存設定後，這些設定就會在標籤執行階段程式庫中發出。 随后，您可以通过调用 [`turbine.getExtensionSettings()`](./turbine.md#get-extension-settings)，从扩展库模块中访问这些设置。

扩展配置是一项可选功能，您可以选择不使用这项功能。
