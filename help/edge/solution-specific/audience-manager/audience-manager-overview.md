---
title: 向Adobe Audience Manager发送数据
seo-title: 使用Adobe Experience PlatformWeb SDK向Adobe Audience Manager发送数据
description: 了解如何使用Experience PlatformWeb SDK将数据发送到Adobe Audience Manager
seo-description: 了解如何使用Experience PlatformWeb SDK将数据发送到Adobe Audience Manager
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# [!DNL Audience Manager] 在 [!DNL Experience Platform Edge Network]

该Adobe Experience Platform [!DNL Web SDK] 与Adobe Audience Manager集成，并支持从、Cookie和URL目 [!DNL Audience Manager]标以及ID同步发送和接收数据。

## 启用 [!DNL Audience Manager]

要启 [!DNL Audience Manager] 用，您需要执行以下操作：

- 在您 [!DNL Audience Manager] 的边缘 [配置中启用](../../fundamentals/edge-configuration.md)。
- 启用或禁用Cookie和URL目标。
- 为外部合作伙伴同步指定ID同步容器（可选）

## 同步身份

Adobe Experience Platform [!DNL Web SDK] 支持通过SyncIdentity命令声明客户ID及其身份验证 [状态](../../fundamentals/identity.md) 。

syncIdentity方法使 [用Identity Service命名空间](../../../identity/../identity-service/namespaces.md) ，以指示与身份相关的上下文。 作为客 [!DNL Audience Manager] 户，您使用ID类型的所有现有数据源： 跨设备将自动拥有相应的设备 [!DNL Identity Namespace]。 要查找相应 [!DNL Identity Namespace] 的Adobe Experience Platform [!DNL Audience Manager Data Source]，请登录到该并导航到该 [!DNL Identities] 部分。

![视图命名空间UI](../../../assets/edge_configuration_identity.png)

您可以在此按名称搜 [!DNL Audience Manager] 索数据源。 syncIdentity方法使用Identity Symbol来声明命名空间。

使用ID [!DNL Audience Manager] 类型的任何新数据源： 跨设备将生成相应的标识命名空间。 当前不支持数据源ID类型Cookie和设备广告ID。 此外，在Adobe Experience Platform中创建的任何身份命名空间都将生成相 [!DNL Audience Manager] 应的数据源，但请注意，syncIdentity方法仅支持命名空间身份符号。
