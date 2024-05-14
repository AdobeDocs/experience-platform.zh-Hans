---
title: Adobe Experience Platform Web SDK扩展中的数据元素类型
description: 了解Adobe Experience Platform Web SDK标记扩展提供的各种数据元素类型。
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 5%

---


# 数据元素类型

在您设置 [操作类型](action-types.md) 在 [Adobe Experience Platform Web SDK标记扩展](web-sdk-extension-configuration.md)中，您必须配置数据元素类型。 本页介绍可用的数据元素类型。

## 标识映射 {#identity-map}

标识映射允许您为网页的访客建立标识。 标识映射由命名空间组成，如 `CRMID`， `Phone` 或 `Email`，每个命名空间包含一个或多个标识符。 例如，如果网站上的个人提供了两个电话号码，则您的手机命名空间应包含两个标识符。

在 [!UICONTROL 标识映射] 数据元素时，您将为每个标识符提供以下信息：

* **[!UICONTROL ID]**：标识访客的值。 例如，如果标识符属于 _电话_ 命名空间， [!UICONTROL ID] 可以是 _555-555-5555_. 此值通常派生自JavaScript变量或页面上的其他某些数据，因此最好创建一个数据元素来引用页面数据，然后在页面中引用数据元素。 [!UICONTROL ID] 中的字段 [!UICONTROL 标识映射] 数据元素。 如果在您的页面上运行时，ID值不是填充的字符串，则将从身份映射中自动删除该标识符。
* **[!UICONTROL 已验证状态]**：指示访客是否已进行身份验证的选择。
* **[!UICONTROL 主要]**：一个选择，指示标识符是否应用作个人的主要标识符。 如果未将任何标识符标记为主标识符，则将使用ECID作为主标识符。

![显示“编辑数据元素”屏幕的UI图像。](assets/identity-map-data-element.png)

>[!TIP]
>
>Adobe建议发送代表个人的身份，例如 `Luma CRM Id` 作为主要标识。
>
>如果身份映射包含人员标识符(例如， `Luma CRM Id`)，则人员标识符将成为主要标识符。 否则， `ECID` 将成为主要标识。

您不应提供 [!DNL ECID] 构建标识映射时。 使用SDK时， [!DNL ECID] 自动在服务器上生成并包含在身份映射中。

标识映射数据元素通常与 [[!UICONTROL XDM对象] 数据元素类型](#xdm-object) 和 [[!UICONTROL 设置同意] 操作类型](action-types.md#set-consent).

详细了解 [Adobe Experience Platform Identity服务](../../../../identity-service/home.md).

## XDM对象 {#xdm-object}

使用XDM对象数据元素可更轻松地将数据格式化为XDM。 首次打开此数据元素时，请选择正确的 Adobe Experience Platform 沙盒和架构。选择架构后，您会看到架构的结构，可以轻松地在其中填写。

![显示XDM对象结构的UI图像。](assets/XDM-object.png)

请注意，打开架构的某些字段时，例如 `web.webPageDetails.URL`，则会自动收集某些项目。 即使自动收集了多个项目，您也可以根据需要覆盖任何项目。 所有值都可以手动填写或使用其他数据元素进行填写。

>[!NOTE]
>
>只填写您有兴趣收集的信息段。 将数据发送到解决方案时，会忽略未填写的任何内容。

## Variable {#variable}

您可以使用创建有效负荷对象 **[!UICONTROL 变量]** 数据元素。 两者 [!UICONTROL XDM] 和 [!UICONTROL 数据] 对象受支持。

* 当您选择时 [!UICONTROL XDM]，选择所需的 [!UICONTROL 沙盒] 和 [!UICONTROL 架构].
* 当您选择时 [!UICONTROL 数据]中，选择所需的解决方案。 可用的解决方案包括 [!UICONTROL Adobe Analytics] 和 [!UICONTROL Adobe Target].

![显示数据元素选项的标记UI的图像。](assets/variable-data-element.png)

创建此数据元素后，您可以使用 [更新变量](./action-types.md#update-variable) 操作来修改它。 准备就绪后，您可以将此数据元素包含在 [发送事件](./action-types.md#send-event) 将数据发送到数据流的操作。

## 后续步骤 {#next-steps}

了解特定用例，例如 [访问ECID](accessing-the-ecid.md).
