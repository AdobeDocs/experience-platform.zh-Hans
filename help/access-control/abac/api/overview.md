---
keywords: Experience Platform；主页；热门主题；API；基于属性的访问控制；基于属性的访问控制
solution: Experience Platform
title: 基于属性的访问控制API指南
description: 基于属性的访问控制API允许您以编程方式管理Adobe Experience Platform中的角色和访问策略。 参阅本指南，了解如何使用 API 执行关键操作。
exl-id: 0fc32354-4869-4392-9501-b1dbea1bc55e
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 14%

---

# 基于属性的访问控制API指南

基于属性的访问控制是Adobe Experience Platform的一项功能，它使管理员能够根据属性控制对特定对象和/或功能的访问。 属性可以是添加到对象的元数据，例如添加到架构字段或区段的标签。 管理员定义包含用于管理用户访问权限的属性的访问策略。

基于属性的访问控制API用于访问Adobe Experience Platform中的角色、产品、权限类别和权限集，并提供一个用户界面和RESTful API，所有可用库资源都可从该API访问。

>[!IMPORTANT]
>
>切勿将基于属性的访问控制与Experience Platform的数据治理功能混为一谈，后者允许您使用标签和策略来控制数据在Platform中的使用方式，而不是让组织中的哪些用户有权访问该数据。 请参阅 [策略服务API指南](../../../data-governance/api/overview.md) 提供了有关如何以编程方式利用这些功能的步骤。

这些端点概述如下。 有关详细信息，请访问各个端点指南，并参阅 [快速入门指南](./getting-started.md) 有关所需标头的重要信息，请阅读示例API调用等。

## 角色

角色定义了管理员、专家或最终用户对组织中资源的访问权限。 在基于角色的访问控制环境中，用户访问配置是通过通用责任和需求进行分组的。 一个角色具有一组给定的权限，可将您组织的成员分配给一个或多个角色，具体取决于他们需要的查看或写入访问权限的范围。请参阅 [角色端点指南](./roles.md) 有关在API中使用角色的详细信息。

## 支持

策略是一些语句，它将若干属性组合在一起以确定允许执行和不允许执行的操作。策略可以是本地策略，也可以是全局策略，并且可以覆盖其他策略。 此 `/policies` 端点允许您以编程方式管理组织中的策略。 请参阅 [策略端点指南](./policies.md) 有关在API中使用策略的详细信息。

## 产品

此 `/products` 基于属性的访问控制API中的端点允许您以编程方式管理产品以及与组织中产品关联的权限类别和权限集。 请参阅 [products端点指南](./products.md) 有关在API中使用产品及其相应权限类别和权限集的更多信息。

## 后续步骤

要开始使用基于属性的访问控制API进行调用，请阅读 [快速入门指南](./getting-started.md) 然后选择其中一个端点指南以了解如何使用特定端点。
