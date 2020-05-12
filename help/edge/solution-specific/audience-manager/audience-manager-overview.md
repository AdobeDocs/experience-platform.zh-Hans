---
title: 将数据发送到Adobe受众管理器
seo-title: 使用Adobe Experience Platform Web SDK将受众发送到Adobe Experience Manager
description: 了解如何使用Experience Platform Web SDK将受众发送到Adobe Design Manager
seo-description: 了解如何使用Experience Platform Web SDK将受众发送到Adobe Design Manager
translation-type: tm+mt
source-git-commit: cfb23e7fde246ca224d5e1f2688651aa7d992b2c
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 2%

---


# （测试版）Experience Platform Edge Network上的受众MAnager

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前为测试版，并非所有用户都可用。 文档和功能可能会发生变化。

Adobe Experience Platform Web SDK与Adobe受众管理器集成，支持从受众管理器、Cookie和URL目标以及ID同步发送和接收数据。

## 启用受众管理器

要启用受众管理器，您需要执行以下操作：

- 在边缘配置中启用 [受众管理器](../../fundamentals/edge-configuration.md)。
- 启用或禁用Cookie和URL目标。
- 为外部合作伙伴同步指定ID同步容器（可选）

## 同步身份

Adobe Experience Platform Web SDK支持通过SyncIdentity命令声明客户ID及其身份验证 [状态](../../fundamentals/identity.md) 。

syncIdentity方法使 [用Identity Service命名空间](../../../identity/../identity-service/namespaces.md) ，以指示与身份相关的上下文。 作为受众经理客户，您现有的所有使用ID类型的数据源： 跨设备将自动具有相应的身份命名空间。 要查找您的受众管理器数据源的相应身份命名空间，请登录Adobe Experience Platform并导航到“身份”部分。

![视图命名空间UI](../../../assets/edge_configuration_identity.png)

您可以在此按名称搜索受众管理器数据源。 syncIdentity方法使用Identity Symbol来声明命名空间。

任何使用ID类型的新受众管理器数据源： 跨设备将生成相应的标识命名空间。 当前不支持数据源ID类型Cookie和设备广告ID。 此外，在Adobe Experience Platform中创建的任何身份命名空间都将生成相应的受众管理器数据源，但请注意，syncIdentity方法仅支持命名空间身份符号。
