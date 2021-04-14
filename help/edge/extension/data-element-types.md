---
title: Adobe Experience Platform Web SDK扩展中的数据元素类型
description: 了解Adobe Experience Platform Launch中Adobe Experience Platform Web SDK扩展提供的不同数据元素类型。
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
translation-type: tm+mt
source-git-commit: 3f7808a08d033c5940d2115006c269b8c4079822
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 47%

---

# 数据元素类型

在[Adobe Experience Platform Web SDK扩展](web-sdk-extension.md)中为[Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html)设置[操作类型](action-types.md)后，请配置数据元素类型。

本页介绍可用的数据元素类型。

## 事件合并 ID

此数据元素在使用时提供事件合并 ID。此数据元素无需配置。提供的数据元素在访客离开页面或使用“重置事件合并 ID”操作类型之前保持不变。

## 标识映射

标识映射数据元素允许您根据您指定的其他数据元素或其他值创建标识。您创建的所有标识都必须绑定回到相应的命名空间。此命名空间元素提供一个下拉列表，显示所有默认数据以及您创建的任何数据。

![](./assets/identity-map-data-element.png)

## XDM 对象 {#xdm-object}

使用XDM格式将任何数据发送到Adobe Experience Platform Web SDK。 使用 XDM 对象数据元素可以更轻松地格式化数据。首次打开此数据元素时，请选择正确的 Adobe Experience Platform 沙箱和架构。选择模式后，您会看到模式的结构，您可以轻松填写。

![](./assets/XDM-object.png)

请注意，打开架构的某些字段（如 `web.webPageDetails.URL`）时，会自动收集一些项目。即使自动收集了多个项目，您也可以根据需要覆盖任何项目。 所有值都可以手动填写或使用其他数据元素进行填写。

>[!NOTE]
>
>只填写您感兴趣收集的信息。 将数据发送到解决方案时，将忽略未填写的任何内容。
