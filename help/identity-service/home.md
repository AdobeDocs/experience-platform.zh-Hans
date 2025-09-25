---
keywords: Experience Platform；主页；热门主题；身份；XDM图形；身份服务；身份服务
solution: Experience Platform
title: 身份标识服务概述
description: Adobe Experience Platform Identity Service通过跨设备和系统桥接身份，允许您实时提供有影响力的个人数字体验，从而帮助您更好地了解客户及其行为。
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: f791940300036159ceaad11ff725eecfaa8332f4
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 2%

---

# Adobe Experience Platform 身份标识服务

为了提供相关的数字体验，您需要对构成客户群的真实实体进行全面而准确的呈现。

如今，组织和企业面临着大量不同的数据集：您的个人客户由各种不同的标识符表示。 您的客户可以链接到不同的Web浏览器(Safari、Google Chrome)、硬件设备（电话、笔记本电脑）和其他人员标识符（CRMID、电子邮件帐户）。 这会造成客户的视图脱节。

您可以使用Adobe Experience Platform Identity Service及其功能解决这些挑战，以便：

* 生成将不同的标识链接在一起的&#x200B;**标识图**，从而直观地呈现客户如何跨不同渠道与您的品牌互动。
* 为实时客户档案创建图形，然后将该图形用于通过合并属性和行为来创建客户的综合视图。
* 使用各种工具执行验证和调试。

本文档概述了Identity Service，以及在Experience Platform上下文中如何使用其功能。

## 术语 {#terminology}

在详细了解Identity Service之前，请阅读下表以概览关键术语：

| 术语 | 定义 |
| --- | --- |
| 身份标识 | 身份是实体特有的数据。 通常，这是一个现实世界中的对象，例如个人、硬件设备或Web浏览器（由Cookie表示）。 完全限定的标识由两个元素组成：**标识命名空间**&#x200B;和&#x200B;**标识值**。 |
| 身份标识命名空间 | 身份标识命名空间是给定身份标识的上下文。例如，`Email`的命名空间可能与标识值&#x200B;**julien<span>@acme.com**&#x200B;相对应。 同样，`Phone`的命名空间可以与标识值`555-555-1234`对应。 有关详细信息，请阅读[身份命名空间概述](./features/namespaces.md)。 |
| 身份标识值 | 身份值是一个字符串，它表示真实世界的实体，并通过命名空间在Identity Service中分类。 例如，标识值（字符串） **julien<span>@acme.com**&#x200B;可以分类为`Email`命名空间。 |
| 身份标识类型 | 身份类型是身份命名空间的组件。 身份类型指定是否在身份图中链接身份数据。 |
| 链接 | 链接或链接是一种确定两个不同的身份表示同一实体的方法。 例如，“`Email` = julien<span>@acme.com”和“`Phone` = 555-555-1234”之间的链接意味着两个身份代表同一实体。 这表明，与您的品牌互动的电子邮件地址为julien<span>@acme.com且电话号码为555-555-1234的客户是相同的。 |
| 身份标识服务 | Identity Service是Experience Platform中的一项服务，用于链接（或取消链接）身份以维护身份图。 |
| 身份标识图 | 身份图是表示单个客户的身份集合。 有关详细信息，请阅读[上的使用身份图查看器](./features/identity-graph-viewer.md)的指南。 |
| 实时客户轮廓 | 实时客户资料是Adobe Experience Platform中的一项服务，该服务： <ul><li>合并配置文件片段以基于身份图创建配置文件。</li><li>对配置文件进行分段，以便随后将这些配置文件发送到目标进行激活。</li></ul> |
| 轮廓 | 用户档案是主题、组织或个人的表示形式。 用户档案由四个元素组成： <ul><li>属性：属性提供姓名、年龄或性别等信息。</li><li>行为：行为提供有关给定用户档案活动的信息。 例如，配置文件行为可以判断给定配置文件是“搜索凉鞋”还是“订购T恤”。</li><li>身份：对于合并的个人资料，这将提供与人员关联的所有身份的信息。 身份可分为三类：人员（CRMID、电子邮件、电话）、设备(IDFA、GAID)和Cookie(ECID、AAID)。</li><li>受众成员资格：配置文件所属的组（忠诚用户、住在加利福尼亚的用户等）</li></ul> |

{style="table-layout:auto"}

## 什么是Identity Service？

在Experience Platform上进行![身份拼接](./images/identity-service-stitching.png)

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

* 创建自定义命名空间以满足您组织的需求。
* 创建、更新和查看身份图。
* 删除基于数据集的身份。
* 删除身份以确保法规遵从性。

## Identity Service如何链接身份

>[!IMPORTANT]
>
>Identity服务区分大小写。 例如，**abc<span>@gmail.com**&#x200B;和&#x200B;**ABC<span>@GMAIL.COM**&#x200B;将被视为两个单独的电子邮件标识。

当标识命名空间与标识值匹配时，将在两个标识之间建立链接。

典型的登录事件&#x200B;**将两个标识**&#x200B;发送到Experience Platform中：

* 代表经过身份验证的用户的人员标识符（如CRMID）。
* 表示Web浏览器的浏览器标识符（如ECID）。

请仔细研究下面的示例：

* 您使用笔记本电脑登录电子商务网站，并使用用户名和密码组合登录。 此事件使您符合身份验证用户的资格，因此Identity Service可识别您的CRMID。
* 您使用浏览器访问电子商务网站的情况也会被Identity Service识别为事件。 此事件通过ECID在Identity Service中表示。
* 在后台，Identity Service将以下列方式处理这两个事件： `CRM_ID:ABC, ECID:123`。
   * CRMID： ABC是代表您作为经过身份验证的用户的命名空间和值。
   * ECID： 123是命名空间和值，表示您在笔记本电脑上使用Web浏览器的情况。
* 接下来，如果您使用相同的凭据登录同一电子商务网站，但使用的是手机上的Web浏览器，而不是笔记本电脑上的Web浏览器，则将在Identity Service中注册一个新的ECID。
* 在后台，Identity Service以`{CRM_ID:ABC, ECID:456}`形式处理此新事件，其中CRM_ID：ABC表示经过身份验证的客户ID，ECID:456表示移动设备上的Web浏览器。

考虑到上述情况，Identity Service在`{CRM_ID:ABC, ECID:123}`和`{CRM_ID:ABC, ECID:456}`之间建立链接。 这将生成一个标识图，其中您“拥有”三个标识：一个用于人员标识符(CRMID)，两个用于Cookie标识符(ECID)。

有关详细信息，请阅读[Identity Service如何链接身份](./features/identity-linking-logic.md)的指南。

## 身份图

身份图是不同身份命名空间之间关系的映射，允许您可视化并更好地了解哪些客户身份以及如何拼合在一起。 有关详细信息，请阅读有关[使用身份图查看器](./features/identity-graph-viewer.md)的教程。

以下视频旨在支持您了解身份和身份图。

>[!VIDEO](https://video.tv.adobe.com/v/3422769?quality=12&learn=on&captions=chi_hans)

## 了解Identity Service在Experience Platform基础架构中的角色

Identity服务在Experience Platform中起着至关重要的作用。 其中一些关键集成包括：

* [架构](../xdm/home.md)：在给定的架构中，标记为标识的架构字段允许生成标识图。
* [数据集](../catalog/datasets/overview.md)：启用数据集以摄取到Real-time Customer Profile时，将从该数据集生成身份图，假定该数据集至少有两个标记为身份的字段。
* [Web SDK](../web-sdk/home.md)： Web SDK将体验事件发送到Adobe Experience Platform，当事件中存在两个或多个标识时，标识服务会生成图形。
* [实时客户个人资料](../profile/home.md)：在合并给定个人资料的属性和事件之前，实时客户个人资料可以引用标识图。 有关详细信息，请阅读[上的指南，以了解Identity Service与Real-Time Customer Profile](./identity-and-profile.md)之间的关系。
* [目标](../destinations/home.md)：目标可以根据身份命名空间将配置文件信息发送到其他系统，如经过哈希处理的电子邮件。
* [区段匹配](../segmentation/ui/segment-match/overview.md)：区段匹配在两个不同沙盒中匹配两个配置文件，这两个沙盒具有相同的标识命名空间和标识值。
* [Privacy Service](../privacy-service/home.md)：如果删除请求包含`identity`，则可以使用Privacy Service中的隐私请求处理功能从身份服务中删除指定的命名空间和身份值组合。

