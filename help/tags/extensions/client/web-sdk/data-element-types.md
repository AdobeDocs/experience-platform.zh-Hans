---
title: Adobe Experience Platform Web SDK扩展中的数据元素类型
description: 了解Adobe Experience Platform Web SDK标记扩展提供的各种数据元素类型。
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: e34a9ee5b1a09ff3391e5b0e981215fefbc157fc
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 5%

---


# 数据元素类型

在[Adobe Experience Platform Web SDK标记扩展](web-sdk-extension-configuration.md)中设置[操作类型](action-types.md)后，必须配置数据元素类型。 本页介绍可用的数据元素类型。

## 标识映射 {#identity-map}

标识映射允许您为网页的访客建立标识。 标识映射由命名空间（如`CRMID`、`Phone`或`Email`）组成，每个命名空间包含一个或多个标识符。 例如，如果网站上的个人提供了两个电话号码，则您的手机命名空间应包含两个标识符。

在[!UICONTROL 标识映射]数据元素中，您将为每个标识符提供以下信息：

* **[!UICONTROL ID]**：标识访客的值。 例如，如果标识符属于&#x200B;_phone_&#x200B;命名空间，[!UICONTROL ID]可以是&#x200B;_555-555-5555_。 此值通常派生自页面上的JavaScript变量或某些其他数据，因此最好创建一个引用页面数据的数据元素，然后引用[!UICONTROL 标识映射]数据元素内[!UICONTROL ID]字段中的数据元素。 如果在您的页面上运行时，ID值不是填充的字符串，则将从身份映射中自动删除该标识符。
* **[!UICONTROL 已验证状态]**：指示访客是否已验证的选择。
* **[!UICONTROL Primary]**：一个选择，指示标识符是否应用作个人的主要标识符。 如果未将任何标识符标记为主标识符，则将使用ECID作为主标识符。

![显示“编辑数据元素”屏幕的UI图像。](assets/identity-map-data-element.png)

>[!TIP]
>
>Adobe建议将代表人员的身份（如`Luma CRM Id`）作为主要身份发送。
>
>如果身份映射包含人员标识符（例如`Luma CRM Id`），则人员标识符将成为主标识符。 否则，`ECID`将成为主标识。

在构建标识映射时，您不应提供[!DNL ECID]。 使用SDK时，将在服务器上自动生成[!DNL ECID]并将其包含在身份映射中。

标识映射数据元素通常与[[!UICONTROL XDM对象]数据元素类型](#xdm-object)和[[!UICONTROL 设置同意]操作类型](action-types.md#set-consent)一起使用。

阅读有关[Adobe Experience Platform Identity服务](../../../../identity-service/home.md)的更多信息。

## XDM对象 {#xdm-object}

使用XDM对象数据元素可更轻松地将数据格式化为XDM。 首次打开此数据元素时，请选择正确的 Adobe Experience Platform 沙盒和架构。选择架构后，您会看到架构的结构，可以轻松地在其中填写。

显示XDM对象结构的![UI图像。](assets/XDM-object.png)

请注意，打开架构的某些字段（如`web.webPageDetails.URL`）时，会自动收集一些项目。 即使自动收集了多个项目，您也可以根据需要覆盖任何项目。 所有值都可以手动填写或使用其他数据元素进行填写。

>[!NOTE]
>
>只填写您有兴趣收集的信息段。 将数据发送到解决方案时，会忽略未填写的任何内容。

## Variable {#variable}

您可以使用&#x200B;**[!UICONTROL 变量]**&#x200B;数据元素创建有效负荷对象。 同时支持[!UICONTROL XDM]和[!UICONTROL Data]对象。

* 当您选择[!UICONTROL XDM]时，请选择所需的[!UICONTROL 沙盒]和[!UICONTROL 架构]。
* 当您选择[!UICONTROL 数据]时，请选择所需的解决方案。 可用的解决方案包括[!UICONTROL Adobe Analytics]和[!UICONTROL Adobe Target]。

![显示数据元素选项的标记UI图像。](assets/variable-data-element.png)

创建此数据元素后，可以使用[更新变量](./action-types.md#update-variable)操作对其进行修改。 准备就绪后，您可以在[发送事件](./action-types.md#send-event)操作中包含此数据元素，以便将数据发送到数据流。

## 媒体：体验质量 {#quality-experience}

在将流媒体事件发送到Adobe Experience Platform时，**[!UICONTROL 体验质量]**&#x200B;数据元素非常有用。 您可以在创建媒体会话时添加此元素，以下媒体事件将包含更新的体验质量数据。

显示“创建体验数据元素质量”屏幕的![UI图像。](assets/qoe-data-element.png)

## 后续步骤 {#next-steps}

了解特定用例，如[访问ECID](accessing-the-ecid.md)。
