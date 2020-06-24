---
title: 向Adobe Audience Manager发送数据
seo-title: 使用Adobe Experience PlatformWeb SDK向Adobe Audience Manager发送数据
description: 了解如何使用Experience PlatformWeb SDK将数据发送到Adobe Audience Manager
seo-description: 了解如何使用Experience PlatformWeb SDK将数据发送到Adobe Audience Manager
translation-type: tm+mt
source-git-commit: 6a83ab1c6405f45700f4f8899139010d50010b0c
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Audience ManagerExperience Platform边缘网络

Adobe Experience PlatformWeb SDK与Adobe Audience Manager集成，支持从Audience Manager、Cookie和URL目标以及ID同步发送和接收数据。

## 启用Audience Manager

要启用Audience Manager，您需要执行以下操作：

- 在边缘配置中 [启用Audience Manager](../../fundamentals/edge-configuration.md)。
- 启用或禁用Cookie和URL目标。
- 为外部合作伙伴同步指定ID同步容器（可选）

## 同步身份

Adobe Experience PlatformWeb SDK支持通过SyncIdentity命令声明客户ID及其身份验证 [状态](../../fundamentals/identity.md) 。

syncIdentity方法使 [用Identity Service命名空间](../../../identity/../identity-service/namespaces.md) ，以指示与身份相关的上下文。 作为Audience Manager客户，您所有使用ID类型的现有数据源： 跨设备将自动具有相应的身份命名空间。 要查找您的Audience Manager数据源的相应身份命名空间，请登录Adobe Experience Platform并导航到“身份”部分。

![视图命名空间UI](../../../assets/edge_configuration_identity.png)

您可以在此按名称搜索Audience Manager数据源。 syncIdentity方法使用Identity Symbol来声明命名空间。

使用ID类型的任何新Audience Manager数据源： 跨设备将生成相应的标识命名空间。 当前不支持数据源ID类型Cookie和设备广告ID。 此外，在Adobe Experience Platform中创建的任何身份命名空间都将生成相应的Audience Manager数据源，但请注意，syncIdentity方法仅支持命名空间身份符号。
