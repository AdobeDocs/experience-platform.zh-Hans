---
title: 使用Audience Manager Web SDK在Experience Platform和Adobe Experience Platform之间同步身份
description: 了解如何使用Audience Manager Web SDK在Experience Platform和Adobe Experience Platform之间同步身份
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: audience manager；aam；身份；同步身份；命名空间；
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# 在Audience Manager和Experience Platform之间同步身份

Adobe Experience Platform Web SDK支持通过[sendEvent](./overview.md#syncing-identities)命令声明客户ID及其身份验证状态。

从[Identity Service命名空间](../../identity/../identity-service/features/namespaces.md)中选择您的命名空间，以使用“身份符号”列中的值指示与身份相关的上下文：

![命名空间UI视图](../assets/identity/edge_namespaceUI_identity-symbol.png)

作为Audience Manager客户，您所有使用ID类型“跨设备”的现有数据源都会自动具有相应的身份命名空间。 要查找Audience Manager Data Source的相应身份命名空间，请登录Adobe Experience Platform并导航到身份部分。

任何使用ID类型：跨设备的新[!DNL Audience Manager]数据Source都将生成相应的身份命名空间。 当前不支持Source ID类型Cookie和设备Advertising ID。 此外，在Adobe Experience Platform中创建的任何身份命名空间都将生成相应的[!DNL Audience Manager]数据Source，但请注意，syncIdentity方法仅支持命名空间身份符号。
