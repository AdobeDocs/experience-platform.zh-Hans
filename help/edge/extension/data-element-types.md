---
title: Adobe Experience Platform Web SDK扩展中的数据元素类型
description: 了解Adobe Experience Platform Web SDK标记扩展提供的不同数据元素类型。
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: db7700d5c504e484f9571bbb82ff096497d0c96e
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 8%

---


# 数据元素类型

在设置 [操作类型](action-types.md) 在 [Adobe Experience Platform Web SDK标记扩展](web-sdk-extension-configuration.md)，则必须配置数据元素类型。 本页介绍可用的数据元素类型。

## 事件合并ID {#event-merge-id}

此数据元素在使用时提供事件合并 ID。此数据元素无需配置。提供的数据元素在访客离开页面或 **[!UICONTROL 重置事件合并ID]** 操作类型。

## 身份映射 {#identity-map}

身份映射允许您为网页的访客建立身份。 身份映射由命名空间组成，如 _手机_ 或 _电子邮件_，每个命名空间包含一个或多个标识符。 例如，如果您网站上的个人提供了两个电话号码，则您的电话命名空间应包含两个标识符。

在 [!UICONTROL 身份映射] 数据元素中，您将为每个标识符提供以下信息：

* **[!UICONTROL ID]**:标识访客的值。 例如，如果标识符属于 _手机_ 命名空间， [!UICONTROL ID] 可能 _555-555-5555_. 此值通常从JavaScript变量或页面上的某些其他数据中派生，因此最好创建一个引用页面数据的数据元素，然后在 [!UICONTROL ID] 字段 [!UICONTROL 身份映射] 数据元素。 如果ID值不是填充的字符串，则在您的页面上运行时，该标识符将自动从标识映射中删除。
* **[!UICONTROL 已验证状态]**:指示访客是否已验证的选项。
* **[!UICONTROL 主要]**:指示是否应将标识符用作个人的主要标识符的选择。 如果没有将标识符标记为主标识符，则会将ECID用作主标识符。

![显示“编辑数据元素”屏幕的UI图像。](./assets/identity-map-data-element.png)

您不应提供 [!DNL ECID] 构建身份映射时。 使用SDK时， [!DNL ECID] 将在服务器上自动生成并包含在身份映射中。

身份映射数据元素通常与 [[!UICONTROL XDM对象] 数据元素类型](#xdm-object) 和 [[!UICONTROL 设置同意] 操作类型](action-types.md#set-consent).

有关更多信息 [Adobe Experience Platform Identity Service](../../identity-service/home.md).

## XDM对象 {#xdm-object}

使用XDM对象数据元素，可以更轻松地将数据格式化为XDM。 首次打开此数据元素时，请选择正确的 Adobe Experience Platform 沙箱和架构。选择架构后，您会看到架构的结构，您可以轻松填写该结构。

![显示XDM对象结构的UI图像。](assets/XDM-object.png)

请注意，当您打开架构的某些字段时，例如 `web.webPageDetails.URL`，则会自动收集某些项目。 即使自动收集了多个项目，您仍可以根据需要覆盖任意项目。 所有值都可以手动填写或使用其他数据元素进行填写。

>[!NOTE]
>
>只填写您感兴趣的信息。 将数据发送到解决方案时，将忽略未填充的任何内容。

## （测试版）变量 {#variable}

>[!IMPORTANT]
>
>这目前是测试版功能，可能会发生更改。 将来版本可能包含中断更改。

创建XDM对象的另一种方法是使用 **[!UICONTROL 变量]** 数据元素。 当引用XDM对象数据元素时(例如在 `sendEvent` 命令， **[!UICONTROL 变量]** 数据元素可以通过 [!UICONTROL 更新变量] 操作。 要使用数据元素，请选择正确的Adobe Experience Platform沙盒和架构。

![显示“创建数据元素”屏幕的UI图像。](assets/variable-data-element.png)

创建此数据元素后，即可使用 [更新变量](./action-types.md#update-variable) 操作来修改数据元素。 然后，在发送事件操作中，将变量数据元素用于XDM选项。

## 后续步骤 {#next-steps}

了解特定用例，例如 [访问ECID](accessing-the-ecid.md).
