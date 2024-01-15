---
keywords: Experience Platform；主页；热门主题；身份；XDM图形；身份服务；身份服务
solution: Experience Platform
title: Identity服务概述
description: Adobe Experience Platform Identity Service通过跨设备和系统桥接身份，允许您实时提供有影响力的个人数字体验，从而帮助您更好地了解客户及其行为。
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: 876613610f8e3b369bc3fd41d235c214b791fd4d
workflow-type: tm+mt
source-wordcount: '1452'
ht-degree: 2%

---

# Adobe Experience Platform Identity Service

为了提供相关的数字体验，您需要对构成客户群的真实实体进行全面而准确的呈现。

如今，组织和企业面临着大量不同的数据集：您的个人客户由各种不同的标识符表示。 您的客户可以链接到不同的Web浏览器(Safari、Google Chrome)、硬件设备（电话、笔记本电脑）和其他人员标识符（CRM ID、电子邮件帐户）。 这会造成客户的视图脱节。

您可以使用Adobe Experience Platform Identity Service及其功能解决这些挑战，以便：

* 生成 **身份图** 可将不同的身份链接在一起，从而为您提供客户如何跨不同渠道与您的品牌互动的可视化表示形式。
* 提供用于验证和调试的工具。
* 为实时客户档案创建图形，然后将该图形用于通过合并属性和行为来创建客户的综合视图。

本文档概述了Identity Service，以及在Experience Platform上下文中如何使用其功能。

## 术语 {#terminology}

在详细了解Identity Service之前，请阅读下表以概览关键术语：

| 搜索词 | 定义 |
| --- | --- |
| 标识 | 身份是实体特有的数据。 通常，这是一个现实世界中的对象，例如个人、硬件设备或Web浏览器（由Cookie表示）。 完全限定的标识由两个元素组成： **身份命名空间** 和 **标识值**. |
| 标识命名空间 | 身份命名空间是给定身份的上下文。 例如，命名空间 `Email` 可能对应于 **朱利安<span>@acme.com**. 同样，命名空间 `Phone` 可能对应于 `555-555-1234`. 欲知更多信息，请参阅 [身份命名空间概述](./namespaces.md) |
| 标识值 | 身份值是一个字符串，它表示真实世界的实体，并通过命名空间在Identity Service中分类。 例如，电子邮件 **朱利安<span>@acme.com** 可以归类为 `Email` 命名空间。 |
| 标识类型 | 身份类型是身份命名空间的组件。 身份类型指定是否在身份图中链接身份数据。 |
| 链接 | 链接或链接是一种确定两个不同的身份表示同一实体的方法。 例如，“”之间的链接`Email` =朱利安<span>@acme.com”和“`Phone` = 555-555-1234”表示两个身份代表同一实体。 这表明，已与您的品牌交互的客户同时使用了julien的电子邮件地址<span>@acme.com和电话号码555-555-1234相同。 |
| 身份服务 | Identity Service是Experience Platform中的一项服务，用于链接（或取消链接）身份以维护身份图。 |
| 身份图 | 身份图是表示单个客户的身份集合。 有关详细信息，请阅读上的指南 [使用身份图查看器](./ui/identity-graph-viewer.md). |
| 实时客户配置文件 | 实时客户资料是Adobe Experience Platform中的一项服务，该服务： <ul><li>合并配置文件片段以基于身份图创建配置文件。</li><li>对配置文件进行分段，以便随后将这些配置文件发送到目标进行激活。</li></ul> |
| 配置文件 | 用户档案是主题、组织或个人的表示形式。 用户档案由两个元素组成： <ul><li>属性：属性提供姓名、年龄或性别等信息。</li><li>行为：行为提供有关给定用户档案活动的信息。 例如，配置文件行为可以判断给定配置文件是“搜索凉鞋”还是“订购T恤”。</li></ul> |

{style="table-layout:auto"}

## 什么是Identity Service？

![Platform上的身份拼接](./images/identity-service-stitching.png)

在“企业对客户”(B2C)上下文中，客户与您的业务进行交互，并与您的品牌建立关系。 典型客户可能在您组织的数据基础架构内的任意数量的系统中处于活动状态。 任何给定客户都可能在您的电子商务、忠诚度和技术支持系统中处于活动状态。 同一客户还可以在任意数量的不同设备上匿名或通过身份验证方式进行互动。

考虑以下客户历程：

* Julien已在您的电子商务网站上创建了一个帐户，并且以前订购过一些商品。 Julien通常使用自己的笔记本电脑购物，并在每次使用时登录到自己的帐户。
* 但是，在访问您的网站期间，她使用平板电脑搜索凉鞋。 在此会话中，由于她使用的是其他设备，因此她既不登录，也不下订单。
* 此时，Julien的活动将以两个单独的用户档案表示：
   * 她的第一个配置文件是她的电子商务登录ID。 当她在电子商务网站上使用用户名和密码组合来验证其会话时，将使用此配置文件。 此配置文件由跨设备标识符标识。
   * 她的第二个个人资料是她的平板电脑设备。 此配置文件是在她使用平板电脑匿名浏览您的电子商务网站后创建的，无需登录到她的帐户。 此配置文件由Cookie标识符标识。
* 稍后，Julien恢复她的平板电脑会话。 不过，这次她登录了自己的帐户。 因此，Identity Service现在会将Julien的平板电脑设备活动与她的电子商务登录ID相关联。
* 接下来，您的目标内容可能会反映Julien的完整个人资料、购买历史记录和匿名浏览活动。

>[!IMPORTANT]
>
>您可以使用Identity Service来关联身份，并将分散在不同系统中的客户的完整情况拼合在一起。

## Identity Service有何用途？

Identity Service为实现其任务提供了以下操作：

可以使用Identity Service实现以下操作：

* 创建自定义命名空间以满足您组织的需求。
* 创建、更新和查看身份图。
* 删除基于数据集的身份。
* 删除身份以确保法规遵从性。

>[!BEGINSHADEBOX]

## Identity Service如何链接身份

当标识命名空间与标识值匹配时，将在两个标识之间建立链接。

典型的登录事件 **发送两个身份** Experience Platform：

* 代表经过身份验证的用户的人员标识符（如CRM ID）。
* 表示Web浏览器的浏览器标识符（如ECID）。

请仔细研究下面的示例：

* 您使用笔记本电脑登录电子商务网站，并使用用户名和密码组合登录。 此事件使您符合经过身份验证的用户的资格，因此Identity Service可识别您的CRM ID。
* 您使用浏览器访问电子商务网站的情况也会被Identity Service识别为事件。 此事件通过ECID在Identity Service中表示。
* 在幕后， Identity Service将按照以下方式处理这两个事件： `CRM_ID:ABC, ECID:123`.
   * CRM ID： ABC是代表您作为经过身份验证的用户的命名空间和值。
   * ECID： 123是命名空间和值，表示您在笔记本电脑上使用Web浏览器的情况。
* 接下来，如果您使用相同的凭据登录同一电子商务网站，但使用的是手机上的Web浏览器，而不是笔记本电脑上的Web浏览器，则将在Identity Service中注册一个新的ECID。
* 在幕后， Identity Service将此新事件处理为 `{CRM_ID:ABC, ECID:456}`，其中CRM_ID：ABC表示经过身份验证的客户ID，ECID：456表示移动设备上的Web浏览器。

考虑到上述情况，Identity Service建立了 `CRM_ID:ABC, ECID:123`以及 `{CRM_ID:ABC, ECID:456}`. 这将生成一个标识图，您“拥有”三个标识：一个用于人员标识符(CRM ID)，两个用于Cookie标识符(ECID)。

>[!ENDSHADEBOX]

## 身份图

身份图是不同身份命名空间之间关系的映射，允许您可视化并更好地了解哪些客户身份以及如何拼合在一起。 阅读有关的教程 [使用身份图查看器](./ui/identity-graph-viewer.md) 以了解更多信息。

以下视频旨在支持您了解身份和身份图。

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## 了解Identity Service在Experience Platform基础设施中的作用

Identity Service在Experience Platform中扮演着至关重要的角色。 其中一些关键集成包括：

* [Real-time Customer Profile](../profile/home.md)：在合并给定用户档案的属性和事件之前，Real-time Customer Profile可以引用身份图。
* [架构](../xdm/home.md)：在给定的架构中，标记为身份的架构字段允许构建身份图。
* [数据集](../catalog/datasets/overview.md)：当启用了数据集以摄取到Real-time Customer Profile中时，如果数据集至少有两个标记为身份的字段，则会从数据集生成身份图。
* [目标](../destinations/home.md)：目标可以根据身份命名空间将配置文件信息发送到其他系统，如经过哈希处理的电子邮件。
* [区段匹配](../segmentation/ui/segment-match/overview.md)：区段匹配可匹配两个不同沙盒中的两个配置文件，这两个沙盒具有相同的身份命名空间和身份值。
* [Privacy Service](../privacy-service/home.md)：如果删除请求包含 `identity`，则可以使用Privacy Service中的隐私请求处理功能从身份服务中删除指定的命名空间和身份值组合。
