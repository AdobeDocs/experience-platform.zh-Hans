---
title: 使用平台Web SDK在Audience Manager和Adobe Experience Platform之间同步身份
description: 了解如何使用Platform Web SDK在Audience Manager和Adobe Experience Platform之间同步身份
seo-description: 了解如何使用Experience Platform Web SDK将身份与Adobe Audience Manager同步
keywords: 受众管理器；aam；标识；同步标识；命名空间;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# 在Audience Manager和Experience Platform之间同步身份

Adobe Experience Platform Web SDK支持通过[sendEvent](./overview.md#syncing-identities)命令声明客户ID及其身份验证状态的功能。

从[Identity Service命名空间](../../identity/../identity-service/namespaces.md)中选择您的命名空间，以使用“标识符号”列中的值指示标识与之相关的上下文：

![视图命名空间UI](../../assets/edge_namespaceUI_identity-symbol.png)

作为Audience Manager客户，您所有使用ID类型的现有数据源：跨设备会自动拥有相应的身份命名空间。 要查找您的Audience Manager数据源的相应身份命名空间，请登录Adobe Experience Platform并导航到“身份”部分。

使用ID类型的任何新[!DNL Audience Manager]数据源：跨设备将生成相应的身份命名空间。 当前不支持数据源ID类型Cookie和设备广告ID。 此外，在Adobe Experience Platform中创建的任何身份命名空间都将生成相应的[!DNL Audience Manager]数据源，但请注意，syncIdentity方法仅支持命名空间身份符号。
