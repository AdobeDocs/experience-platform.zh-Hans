---
title: Adobe Experience Platform Web SDK扩展中的操作类型
description: 了解Adobe Experience Platform Launch中Adobe Experience Platform Web SDK扩展提供的不同操作类型。
translation-type: tm+mt
source-git-commit: 2a0ae9541a8bb2bb985d43a402d0842e73b23c81
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 18%

---


# 操作类型

为[Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html)配置[Adobe Experience Platform Web SDK扩展](web-sdk-extension.md)后，请配置您的操作类型。

本页介绍了可用的操作类型。

## 发送事件

向Adobe [!DNL Experience Platform]发送事件，以便Adobe Experience Platform可以收集您发送的数据并对该信息执行操作。 选择一个实例（如果您有多个实例）。 如果事件发生在页面加载开始时或在单页应用程序的视图更改期间，请选择&#x200B;**[!UICONTROL 在视图的开始发生]**。

您要发送的任何数据都可以在&#x200B;**[!UICONTROL XDM数据]**&#x200B;字段中发送。 使用符合XDM模式结构的JSON对象。 可以在您的页面上创建此对象，也可以通过&#x200B;**[!UICONTROL 自定义代码]** **[!UICONTROL 数据元素]**&#x200B;创建此对象。

## 设置同意

在您收到用户的同意后，必须使用“设置同意”操作类型将此同意通知Adobe Experience Platform Web SDK。 目前，支持两种类型的标准：“Adobe”和“IAB TCF”。如果使用 Adobe 标准，您目前可以将同意设置为“In”、“Out”，您也可以使用数据元素提供此值。如果使用 IAB TCF 标准，请提供要使用的版本和值，以及有关 GDPR 的其他信息。

在此操作中，您还会获得一个可选字段，用于包含身份映射，以便在收到同意后可以同步身份。 同步在同意配置为“待定”时很有用，因为同意呼叫可能是第一个触发的呼叫。

## 重置事件合并 ID

如果要在页面上重置事件合并ID，则可以通过此操作重置。 要重置您的ID，请选择要重置的合并ID，并根据需要触发操作。

## 下一步

设置操作类型后，[配置数据元素类型](data-element-types.md)。