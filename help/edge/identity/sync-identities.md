---
title: 使用平台Web SDK在Audience Manager和Adobe Experience Platform之间同步身份
description: 了解如何使用Platform Web SDK在Audience Manager和Adobe Experience Platform之间同步身份
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: audience manager;aam；身份；同步身份；命名空间；
source-git-commit: f5270d1d1b9697173bc60d16c94c54d001ae175a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# 在Audience Manager和Experience Platform之间同步身份

Adobe Experience Platform Web SDK支持通过 [sendEvent](./overview.md#syncing-identities) 命令。

从 [身份服务命名空间](../../identity/../identity-service/namespaces.md) 要通过使用“身份符号”列中的值指示与身份相关的上下文，请执行以下操作：

![命名空间UI的视图](../assets/identity/edge_namespaceUI_identity-symbol.png)

作为Audience Manager客户，您现有的所有使用ID类型的数据源：跨设备自动具有相应的身份命名空间。 要查找Audience Manager数据源的相应身份命名空间，请登录Adobe Experience Platform并导航到身份部分。

任何新 [!DNL Audience Manager] 使用ID类型的数据源：跨设备将生成相应的身份命名空间。 数据源ID类型Cookie和设备广告ID当前不受支持。 此外，在Adobe Experience Platform中创建的任何身份命名空间都将生成一个对应的 [!DNL Audience Manager] 数据源，但请注意，syncIdentity方法仅支持命名空间标识符号。
