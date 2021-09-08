---
description: 此配置确定Adobe Experience Platform用户如何对您的目标端点进行身份验证以激活数据。
title: 目标SDK中凭据的配置选项
source-git-commit: 11f6421665acc2041aa9483b1e0efb6fe48b6dfb
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# 身份验证配置 {#credentials}

## 支持的身份验证类型 {#supported-authentication-types}

Adobe Experience Platform支持多种身份验证类型：

* 承载验证
* 具有授权代码的OAuth 2
* 具有密码授予的OUM第2个
* 具有客户端凭据授予的OAuth 2

对于各种受支持的OAuth 2流以及自定义OAuth 2支持，请阅读[OAuth 2身份验证](./oauth2-authentication.md)上的目标SDK文档。

您可以通过`/destinations`端点的`customerAuthenticationConfigurations`参数配置目标的身份验证信息。 请参阅目标配置文章中的[客户身份验证配置部分](./destination-configuration.md#customer-authentication-configurations)。

## 何时使用`/credentials` API端点 {#when-to-use}

>[!IMPORTANT]
>
>在大多数情况下，您&#x200B;*不*&#x200B;需要使用`/credentials` API端点。 相反，您可以通过`/destinations`端点的`customerAuthenticationConfigurations`参数配置目标的身份验证信息。

如果Adobe与目标之间存在全局身份验证系统，且[!DNL Platform]客户不需要提供任何身份验证凭据即可连接到您的目标，请使用`activation/authoring/credentials` API端点并在[目标配置](./destination-configuration.md#destination-delivery)中选择`PLATFORM_AUTHENTICATION`。 在这种情况下，必须使用`/credentials` API端点创建凭据对象。 请阅读[凭据API端点操作](./credentials-configuration-api.md) ，以获取可对`/credentials`端点执行的操作的完整列表。