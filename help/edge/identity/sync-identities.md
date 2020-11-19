---
title: 与Audience Manager和Adobe Experience Platform同步身份
seo-title: 将身份与Audience Manager、Adobe Experience Platform与Adobe Experience PlatformWeb SDK同步
description: 了解如何使用Experience PlatformWeb SDK与Adobe Audience Manager同步身份
seo-description: 了解如何使用Experience PlatformWeb SDK与Adobe Audience Manager同步身份
keywords: audience manager;aam;identities;sync identities;namespace;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# 同步身份

Adobe Experience PlatformWeb SDK支持通过sendEvent命令声明客户ID及其身份验证 [状态](./overview.md#syncing-identities) 。

从Identity Service命名空间 [中选择命名空间](../../identity/../identity-service/namespaces.md) ，以使用“Identity Symbol”列中的值指示与身份相关的上下文：

![视图命名空间UI](../../assets/edge_namespaceUI_identity-symbol.png)

作为Audience Manager客户，您所有使用ID类型的现有数据源：跨设备会自动拥有相应的身份命名空间。 要查找您的Audience Manager数据源的相应身份命名空间，请登录Adobe Experience Platform并导航到“身份”部分。

使用ID [!DNL Audience Manager] 类型的任何新数据源：跨设备将生成相应的标识命名空间。 当前不支持数据源ID类型Cookie和设备广告ID。 此外，在Adobe Experience Platform创建的任何身份命名空间都将生成相 [!DNL Audience Manager] 应的数据源，但请注意，syncIdentity方法仅支持命名空间身份符号。
