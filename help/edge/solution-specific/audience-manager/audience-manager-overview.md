---
title: 将数据发送到Adobe Audience Manager
seo-title: 使用Adobe Experience PlatformWeb SDK向Adobe Audience Manager发送数据
description: 了解如何使用Experience PlatformWeb SDK将数据发送到Adobe Audience Manager
seo-description: 了解如何使用Experience PlatformWeb SDK将数据发送到Adobe Audience Manager
keywords: audience manager;aam;identities;sync identities;namespace;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# [!DNL Audience Manager] 在 [!DNL Experience Platform Edge Network]

Adobe Experience Platform [!DNL Web SDK] 与Adobe Audience Manager集成，支持从Cookie和URL目的地和ID同 [!DNL Audience Manager]步发送和接收数据。

## 启用 [!DNL Audience Manager]

要启 [!DNL Audience Manager] 用，您需要执行以下操作：

- 在您 [!DNL Audience Manager] 的边缘 [配置中启用](../../fundamentals/edge-configuration.md)。
- 启用或禁用Cookie和URL目标。
- 为外部合作伙伴同步指定ID同步容器（可选）

## 同步身份

Adobe Experience PlatformWeb SDK支持通过sendEvent命令声明客户ID及其身份验证 [状态](../../fundamentals/identity.md#syncing-identities) 。

从Identity Service命名空间 [中选择命名空间](../../../identity/../identity-service/namespaces.md) ，以使用“标识符”列中的值指示标识与之相关的上下文：

![视图命名空间UI](../../../assets/edge_namespaceUI_identity-symbol.png)

作为Audience Manager客户，您所有使用ID类型的现有数据源：跨设备会自动拥有相应的身份命名空间。 要查找您的Audience Manager数据源的相应身份命名空间，请登录Adobe Experience Platform并导航到“身份”部分。

使用ID [!DNL Audience Manager] 类型的任何新数据源：跨设备将生成相应的标识命名空间。 当前不支持数据源ID类型Cookie和设备广告ID。 此外，在Adobe Experience Platform创建的任何身份命名空间都将生成相 [!DNL Audience Manager] 应的数据源，但请注意，syncIdentity方法仅支持命名空间身份符号。
