---
title: 平台Web SDK扩展操作类型
description: Adobe Experience PlatformAdobe Experience Platform LaunchWeb SDK扩展操作类型
translation-type: tm+mt
source-git-commit: 473cc1f7617f1d65cdb70ff0e758178ea0174f00
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 54%

---


# 操作类型

为[Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html)配置[Adobe Experience PlatformWeb SDK扩展](web-sdk-extension.md)后，请配置您的操作类型。

本页介绍可用的操作类型。

## 发送事件

向Adobe[!DNL Experience Platform]发送事件，以便Adobe Experience Platform能够收集您发送的数据并对该信息采取相应操作。 必须选择一个实例（如果您有多个实例）。如果事件发生在页面加载开始或单页应用程序的视图更改期间，请选择&#x200B;**[!UICONTROL 视图]**&#x200B;的开始发生。

要发送的任何数据都可以在&#x200B;**[!UICONTROL XDM数据]**&#x200B;字段中发送。 这应该是符合 XDM 架构的 JSON 对象。此对象可以在您的页面上创建，也可以通过&#x200B;**[!UICONTROL 自定义代码]** **[!UICONTROL 数据元素]**&#x200B;创建。

## 设置同意

在您收到用户的同意后，必须将此通知Adobe Experience PlatformWeb SDK。 您可以使用“设置同意”操作类型完成此操作。目前，支持两种类型的标准：“Adobe”和“IAB TCF”。如果使用 Adobe 标准，您目前可以将同意设置为“In”、“Out”，您也可以使用数据元素提供此值。如果使用 IAB TCF 标准，请提供要使用的版本和值，以及有关 GDPR 的其他信息。

在此操作中，还会向您提供一个可选字段，用于包含标识映射，以便在收到同意后可以同步标识。将同意配置为“Pending”时，这可能会很有用，因为同意调用可能是第一个要触发的调用。

## 重置事件合并 ID

如果要在页面上重置事件合并 ID，可以通过以下操作来完成。要重置 ID，您需要选择要重置的合并 ID，并根据需要触发操作。

## 下一步

设置操作类型后，[配置数据元素类型](data-element-types.md)。