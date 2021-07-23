---
title: 使用平台Web SDK在Audience Manager和Adobe Experience Platform之间同步身份
description: 了解如何使用Platform Web SDK在Audience Manager和Adobe Experience Platform之间同步身份
seo-description: 了解如何将身份与Adobe Audience Manager与Experience PlatformWeb SDK同步
keywords: audience manager;aam；身份；同步身份；命名空间；
source-git-commit: 3a1d08a4ea87ee3db7a2a8b048d5721fa679c372
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# 在Audience Manager和Experience Platform之间同步身份

Adobe Experience Platform Web SDK支持通过[sendEvent](./overview.md#syncing-identities)命令声明客户ID及其身份验证状态。

从[Identity Service命名空间](../../identity/../identity-service/namespaces.md)中选择您的命名空间，以使用身份符号列中的值指示与身份相关的上下文：

![命名空间UI的视图](../images/identity/edge_namespaceUI_identity-symbol.png)

作为Audience Manager客户，您现有的所有使用ID类型的数据源：跨设备自动具有相应的身份命名空间。 要查找Audience Manager数据源的相应身份命名空间，请登录Adobe Experience Platform并导航到身份部分。

任何使用ID类型的新[!DNL Audience Manager]数据源：跨设备将生成相应的身份命名空间。 数据源ID类型Cookie和设备广告ID当前不受支持。 此外，在Adobe Experience Platform中创建的任何身份命名空间都将生成相应的[!DNL Audience Manager]数据源，但请注意，syncIdentity方法仅支持命名空间身份符号。
