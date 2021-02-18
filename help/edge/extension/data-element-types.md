---
title: Adobe Experience Platform Web SDK扩展中的数据元素类型
description: 了解Adobe Experience Platform Launch中Adobe Experience Platform Web SDK扩展提供的不同数据元素类型。
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 78%

---


# 数据元素类型

在[Adobe Experience Platform Web SDK扩展](web-sdk-extension.md)中为[Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html)设置[操作类型](action-types.md)后，请配置数据元素类型。

本页介绍可用的数据元素类型。

## 事件合并 ID

此数据元素在使用时提供事件合并 ID。此数据元素无需配置。提供的数据元素在访客离开页面或使用“重置事件合并 ID”操作类型之前保持不变。

## 标识映射

标识映射数据元素允许您根据您指定的其他数据元素或其他值创建标识。您创建的所有标识都必须绑定回到相应的命名空间。此数据元素提供一个下拉列表，其中显示所有默认的命名空间以及您创建的任何内容。

![](./assets/identity-map-data-element.png)

## XDM 对象

您发送到 Adobe Experience Platform Web SDK 的任何数据都应采用 XDM 格式。使用 XDM 对象数据元素可以更轻松地格式化数据。首次打开此数据元素时，请选择正确的 Adobe Experience Platform 沙箱和架构。选择架构后，您将会看到架构的结构，可以轻松地在其中填写。

![](./assets/XDM-object.png)

请注意，打开架构的某些字段（如 `web.webPageDetails.URL`）时，会自动收集一些项目。即使自动收集了多个项目，您还是可以选择根据需要覆盖任何项目。所有值都可以手动填写或使用其他数据元素进行填写。

>[!NOTE]
>
>您只需填写自己有兴趣收集的信息即可。将数据发送到解决方案时，会忽略未填写的任何项目。
