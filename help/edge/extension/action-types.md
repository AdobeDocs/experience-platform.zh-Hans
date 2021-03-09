---
title: Adobe Experience Platform Web SDK扩展中的操作类型
description: 了解Adobe Experience Platform Launch中Adobe Experience Platform Web SDK扩展提供的不同操作类型。
translation-type: tm+mt
source-git-commit: ff261c507d310b8132912680b6ddd1e7d5675d08
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 6%

---


# 操作类型

为[Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html)配置[Adobe Experience Platform Web SDK扩展](web-sdk-extension.md)后，请配置您的操作类型。

本页介绍了可用的操作类型。

## 发送事件

向Adobe [!DNL Experience Platform]发送事件，以便Adobe Experience Platform可以收集您发送的数据并对该信息执行操作。 选择一个实例（如果您有多个实例）。 如果事件发生在页面加载开始时或在单页应用程序的视图更改期间，请选择&#x200B;**[!UICONTROL 在视图的开始发生]**。

您要发送的任何数据都可以在&#x200B;**[!UICONTROL XDM数据]**&#x200B;字段中发送。 使用符合XDM模式结构的JSON对象。 可以在您的页面上创建此对象，也可以通过&#x200B;**[!UICONTROL 自定义代码]** **[!UICONTROL 数据元素]**&#x200B;创建此对象。

## 设置同意

在您收到用户的同意后，必须使用“设置同意”操作类型将此同意通知Adobe Experience Platform Web SDK。 目前，支持两种类型的标准：“Adobe”和“IAB TCF”。请参阅[支持客户同意首选项](../consent/supporting-consent.md)。 使用Adobe 2.0版时，仅支持数据元素值。 您需要创建一个解析到同意对象的数据元素。

在此操作中，您还会获得一个可选字段，用于包含身份映射，以便在收到同意后可以同步身份。 同步在同意配置为“待定”或“已退出”时很有用，因为同意呼叫可能是第一个要触发的呼叫。

## 重置事件合并 ID

如果要在页面上重置事件合并ID，则可以通过此操作重置。 要重置您的ID，请选择要重置的合并ID，并根据需要触发操作。

## 下一步

设置操作类型后，[配置数据元素类型](data-element-types.md)。