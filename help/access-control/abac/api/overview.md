---
keywords: Experience Platform；主页；热门主题；API；基于属性的访问控制；基于属性的访问控制
solution: Experience Platform
title: 基于属性的访问控制API指南
description: 基于属性的访问控制API允许您以编程方式管理Adobe Experience Platform中的角色和访问策略。 参阅本指南，了解如何使用 API 执行关键操作。
exl-id: 0fc32354-4869-4392-9501-b1dbea1bc55e
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 4%

---

# 基于属性的访问控制API指南

基于属性的访问控制是Adobe Experience Platform的一项功能，它使管理员能够根据属性控制对特定对象和/或功能的访问。 属性可以是添加到对象的元数据，如添加到架构字段或区段的标签。 管理员定义包含属性的访问策略以管理用户访问权限。

基于属性的访问控制API用于在Adobe Experience Platform中访问角色、产品、权限类别和权限集，从而提供可从中访问所有可用库资源的用户界面和RESTful API。

>[!IMPORTANT]
>
>基于属性的访问控制不要与Experience Platform的数据管理功能混淆，这些功能允许您使用标签和策略来控制数据在Platform中的使用方式，而不是让组织中的哪些用户有权访问数据。 请参阅 [策略服务API指南](../../../data-governance/api/overview.md) 了解如何以编程方式利用这些功能的步骤。

下面概述了这些端点。 有关详细信息，请访问各个端点指南，并参阅 [入门指南](./getting-started.md) 有关所需标头、读取示例API调用等的重要信息。

## 角色

角色定义管理员、专家或最终用户对您组织中的资源的访问权限。 在基于角色的访问控制环境中，用户访问设置是通过共同的责任和需求分组的。 角色具有一组给定的权限，并且可以根据角色需要的查看或写入权限，将组织的成员分配给一个或多个角色。 请参阅 [角色端点指南](./roles.md) 以了解有关在API中使用角色的更多信息。

## 支持

政策是将属性集合在一起以确立允许和不允许的行动的声明。 策略可以是本地策略，也可以是全局策略，并且可以覆盖其他策略。 的 `/policies` 端点允许您以编程方式管理组织中的策略。 请参阅 [策略端点指南](./policies.md) 有关在API中使用策略的更多信息。

## 产品

的 `/products` 基于属性的访问控制API中的端点允许您以编程方式管理产品以及与组织中的产品关联的权限类别和权限集。 请参阅 [products endpoint指南](./products.md) 有关在API中使用产品及其相应权限类别和权限集的更多信息。

## 后续步骤

要开始使用基于属性的访问控制API进行调用，请阅读 [入门指南](./getting-started.md) 然后，选择一个端点指南以了解如何使用特定端点。
