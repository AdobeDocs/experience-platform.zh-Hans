---
title: 使用Platform Web SDK在Audience Manager和Adobe Experience Platform之间同步身份
description: 了解如何使用Platform Web SDK在Audience Manager和Adobe Experience Platform之间同步身份
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: audience manager；aam；身份；同步身份；命名空间；
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# 在Audience Manager和Experience Platform之间同步身份

Adobe Experience Platform Web SDK支持通过以下方式声明客户ID及其身份验证状态 [sendEvent](./overview.md#syncing-identities) 命令。

从中选择您的命名空间 [Identity服务命名空间](../../identity/../identity-service/features/namespaces.md) 通过使用“身份符号”列中的值，指示与身份相关的上下文：

![命名空间UI视图](../assets/identity/edge_namespaceUI_identity-symbol.png)

作为Audience Manager客户，您所有使用ID类型“Cross-Device”的现有数据源都会自动具有相应的身份命名空间。 要查找Audience Manager数据源对应的身份命名空间，请登录Adobe Experience Platform并导航到身份部分。

任何新 [!DNL Audience Manager] 使用ID类型的数据源：跨设备将生成相应的身份命名空间。 当前不支持数据源ID类型Cookie和设备广告ID。 此外，在Adobe Experience Platform中创建的任何身份命名空间都将生成相应的 [!DNL Audience Manager] 数据源，但请注意，syncIdentity方法仅支持命名空间标识符号。
