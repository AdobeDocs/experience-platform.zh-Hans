---
description: 使用Adobe Experience Platform目标SDK中支持的身份验证配置来验证用户并激活到您的目标端点的数据。
title: 身份验证配置
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: e6d922800c17312df8529061c56d8a2deac46662
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# 身份验证配置 {#credentials}

## 支持的身份验证类型 {#supported-authentication-types}

Adobe Experience Platform目标SDK支持多种身份验证类型：

* 承载验证
* 具有授权代码的OAuth 2
* 具有密码授予的OUM第2个
* 具有客户端凭据授予的OAuth 2

您可以通过 `customerAuthenticationConfigurations` 参数 `/destinations` 端点。 请参阅 [客户身份验证配置部分](./destination-configuration.md#customer-authentication-configurations) 在目标配置文章和以下部分中，了解有关每种身份验证类型的配置的特定信息。

## 承载验证 {#bearer}

要为目标设置载体类型身份验证，您只需配置 `customerAuthenticationConfigurations` 参数 `/destinations` 端点，如下所示：

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ]
```

## OAuth 2身份验证 {#oauth2}

有关如何设置各种受支持的OAuth 2流以及自定义OAuth 2支持的信息，请阅读上的目标SDK文档 [OAuth 2身份验证](./oauth2-authentication.md).


## 何时使用 `/credentials` API端点 {#when-to-use}

>[!IMPORTANT]
>
>在大多数情况下，您 *不* 需要使用 `/credentials` API端点。 您而是可以通过 `customerAuthenticationConfigurations` 参数 `/destinations` 端点。

的 `/credentials` 当Adobe与您的目标之间存在全局身份验证系统，并且与 [!DNL Platform] 客户无需提供任何身份验证凭据即可连接到您的目标。

在这种情况下，必须使用 `/credentials` API端点。 您还必须选择 `PLATFORM_AUTHENTICATION` 在 [目标配置](./destination-configuration.md#destination-delivery). 读取 [凭据API端点操作](./credentials-configuration-api.md) 以获取可对执行的操作的完整列表 `/credentials` 端点。
