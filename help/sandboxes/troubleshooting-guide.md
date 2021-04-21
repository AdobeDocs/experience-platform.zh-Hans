---
keywords: Experience Platform；主页；热门主题；沙箱疑难解答
solution: Experience Platform
title: 沙箱疑难解答指南
topic-legacy: troubleshooting guide
description: 此文档提供有关Adobe Experience Platform中沙箱的常见问题解答。
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# 沙箱疑难解答指南

此文档提供有关Adobe Experience Platform中沙箱的常见问题解答。 有关其他平台服务的问题和疑难解答，请参阅[Experience Platform疑难解答指南](../landing/troubleshooting.md)。

沙箱将单个平台实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。 有关详细信息，请参阅[沙箱概述](home.md)。

## 什么是沙箱？

沙箱是单个Experience Platform实例中的虚拟分区。 每个沙箱都维护其自己的独立平台资源库(包括模式、数据集、用户档案等)。 在沙箱内执行的所有内容和操作仅限于该沙箱，不影响任何其他沙箱。 有关详细信息，请参阅[沙箱概述](home.md)。

## 有哪些类型的沙箱可用，它们有何差异？

Experience Platform中有两种沙箱类型：

* 生产沙箱
* 非生产沙箱

Experience Platform提供了单个生产沙箱，无法删除或重置。 单个平台实例只能存在一个生产沙箱。

相反，沙箱管理员可以为单个平台实例创建多个非生产沙箱。 非生产沙箱允许您测试功能、运行实验和制作自定义配置，而不会影响您的生产沙箱。 此外，非生产沙箱具有重置功能，可从沙箱中删除所有客户创建的资源。 无法将非生产沙箱转换为生产沙箱。 默认Experience Platform许可证授予您五个沙箱（一个生产箱和四个非生产箱）。 您最多可以添加十个非生产沙箱包，最多可添加75个沙箱。 有关详细信息，请与IMS组织管理员或Adobe销售代表联系。

有关详细信息，请参阅[沙箱概述](./home.md)。

## 我是否可以从多个沙箱访问资源？

沙箱是单个平台实例的独立分区，每个沙箱都维护其自己独立的资源库。 不能从任何其他沙箱访问存在于一个沙箱中的资源，而不管沙箱类型（生产或非生产）。

## 我能有多少个制作沙箱？

Experience Platform仅支持每个IMS组织一个生产沙箱，现成提供。 虽然可以重命名生产沙箱，但无法删除或重置它。 具有“沙箱管理”权限的用户只能创建、重置和删除非生产沙箱。

## 我能有多少个非生产沙箱？

Experience Platform目前允许在单个IMS组织内活动多达15个非生产沙箱。

## 我刚刚创建了一个沙箱。 如何设置将使用此沙箱的用户的权限？

Adobe Admin Console通过使用产品用户档案将用户链接到沙箱和权限。 创建新沙箱后，导航到要授予访问权限的产品用户档案的&#x200B;**权限**&#x200B;选项卡，然后单击&#x200B;**沙箱**。 在此处，您可以以与其他权限相同的方式添加或删除对新沙箱的访问。

如果您希望向特定沙箱的用户添加唯一权限，您可能需要创建应用了相应沙箱和权限的新产品用户档案，并将这些用户分配给该用户档案。

有关管理Admin Console中沙箱和权限的详细信息，请参阅[访问控制用户指南](../access-control/ui/overview.md)。
