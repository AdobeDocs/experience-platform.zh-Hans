---
title: Adobe Experience Platform Web SDK扩展中的数据元素类型
description: 了解Adobe Experience Platform Web SDK标记扩展提供的不同数据元素类型。
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 4caab19e1f58fc5cec5a3c56c43e47786d49c3dc
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 19%

---

# 数据元素类型

在[Adobe Experience Platform Web SDK标记扩展](web-sdk-extension-configuration.md)中设置[操作类型](action-types.md)后，配置数据元素类型。

本页介绍可用的数据元素类型。


## 事件合并 ID

此数据元素在使用时提供事件合并 ID。此数据元素无需配置。提供的数据元素在访客离开页面或使用“重置事件合并 ID”操作类型之前保持不变。

## 标识映射

身份映射允许您为网页的访客建立身份。 身份映射由命名空间（如&#x200B;_phone_&#x200B;或&#x200B;_email_）组成，每个命名空间都包含一个或多个标识符。 例如，如果您网站上的个人提供了两个电话号码，则您的电话命名空间应包含两个标识符。

在[!UICONTROL Identity map]数据元素中，您将为每个标识符提供以下信息：

* **[!UICONTROL ID]**:标识访客的值。例如，如果标识符属于&#x200B;_phone_&#x200B;命名空间，则[!UICONTROL ID]可能为&#x200B;_555-555-5555_。 此值通常从JavaScript变量或您页面上的某些其他数据段中派生，因此最好创建引用页面数据的数据元素，然后在[!UICONTROL Identity map]数据元素的[!UICONTROL ID]字段中引用该数据元素。 如果ID值不是填充的字符串，则在您的页面上运行时，该标识符将自动从标识映射中删除。
* **[!UICONTROL 已验证状态]**:指示访客是否已验证的选项。
* **[!UICONTROL 主要]**:指示是否应将标识符用作个人的主要标识符的选择。如果没有将标识符标记为主标识符，则会将ECID用作主标识符。

构建身份映射时，您不应提供ECID。 使用SDK时，会在服务器上自动生成ECID并将其包含在身份映射中。

身份映射数据元素通常与[[!UICONTROL XDM对象]数据元素类型](#xdm-object)和[[!UICONTROL Set consent]操作类型](action-types.md#set-consent)结合使用。

有关[Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=zh-Hans)的更多信息。

![](./assets/identity-map-data-element.png)

## XDM 对象 {#xdm-object}

使用XDM格式将任何数据发送到Adobe Experience Platform Web SDK。 使用 XDM 对象数据元素可以更轻松地格式化数据。首次打开此数据元素时，请选择正确的 Adobe Experience Platform 沙箱和架构。选择架构后，您会看到架构的结构，您可以轻松填写该结构。

![](./assets/XDM-object.png)

请注意，当您打开架构的某些字段（如`web.webPageDetails.URL`）时，系统会自动收集一些项目。 即使自动收集了多个项目，您仍可以根据需要覆盖任意项目。 所有值都可以手动填写或使用其他数据元素进行填写。

>[!NOTE]
>
>只填写您感兴趣的信息。 将数据发送到解决方案时，将忽略未填充的任何内容。
