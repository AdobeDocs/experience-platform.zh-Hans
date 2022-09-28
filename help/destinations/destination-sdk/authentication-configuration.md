---
description: 使用Adobe Experience Platform Destination SDK中支持的身份验证配置来验证用户并将数据激活到目标端点。
title: 身份验证配置
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: 9b4c7da5aa02ae27608c2841b1d825445ac3015e
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# 身份验证配置 {#credentials}

## 支持的身份验证类型 {#supported-authentication-types}

您选择的身份验证配置决定了Experience Platform在平台UI中对目标进行身份验证的方式。

Adobe Experience Platform Destination SDK支持多种身份验证类型：

* [承载验证](#bearer)
* [[!DNL Amazon S3] 身份验证](#s3)
* [[!DNL Azure Blob] 存储](#blob)
* [[!DNL Azure Data Lake Storage]](#adls)
* [[!DNL Google Cloud Storage]](#gcs)
* [具有SSH密钥的SFTP](#sftp-ssh)
* [带密码的SFTP](#sftp-password)
* [具有授权代码的OAuth 2](#oauth2)
* [具有密码授予的OUM第2个](#oauth2)
* [具有客户端凭据授予的OAuth 2](#oauth2)

您可以通过 `customerAuthenticationConfigurations` 参数 `/destinations` 端点。

有关每种类型目标的身份验证配置详细信息，请参阅以下部分：

* [流目标的身份验证配置](destination-configuration.md#customer-authentication-configurations)
* [基于文件的目标的身份验证配置](file-based-destination-configuration.md#customer-authentication-configurations)

## 承载验证 {#bearer}

支持对Experience Platform中的流目标进行承载身份验证。

要为目标设置承载类型身份验证，请配置 `customerAuthenticationConfigurations` 参数 `/destinations` 端点，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## [!DNL Amazon S3] 身份验证 {#s3}

[!DNL Amazon S3] Experience Platform中基于文件的目标支持身份验证。

设置 [!DNL Amazon S3] 目标的身份验证，配置 `customerAuthenticationConfigurations` 参数 `/destinations` 端点，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## [!DNL Azure Blob Storage] {#blob}

[!DNL Azure Blob Storage] Experience Platform中基于文件的目标支持身份验证。

设置 [!DNL Azure Blob] 目标的身份验证，配置 `customerAuthenticationConfigurations` 参数 `/destinations` 端点，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## [!DNL Azure Data Lake Storage] {#adls}

[!DNL Azure Data Lake Storage] Experience Platform中基于文件的目标支持身份验证。

设置 [!DNL Azure Data Lake Storage] (ADLS)目标的身份验证，配置 `customerAuthenticationConfigurations` 参数 `/destinations` 端点，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## [!DNL Google Cloud Storage] {#gcs}

[!DNL Google Cloud Storage] Experience Platform中基于文件的目标支持身份验证。

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```


## [!DNL SFTP] 验证 [!DNL SSH] key {#sftp-ssh}

[!DNL SFTP] 验证 [!DNL SSH] 键值支持用于Experience Platform中基于文件的目标。

要为目标设置使用SSH密钥的SFTP身份验证，请配置 `customerAuthenticationConfigurations` 参数 `/destinations` 端点，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## [!DNL SFTP] 密码验证 {#sftp-password}

[!DNL SFTP] Experience Platform中基于文件的目标支持使用密码进行身份验证。

要使用密码设置目标的SFTP身份验证，请配置 `customerAuthenticationConfigurations` 参数 `/destinations` 端点，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## [!DNL OAuth 2] 身份验证 {#oauth2}

[!DNL OAuth 2] Experience Platform中的流目标支持身份验证。

有关如何设置各种受支持的 [!DNL OAuth 2] 流，以及自定义 [!DNL OAuth 2] 支持，请阅读Destination SDK文档 [[!DNL OAuth 2] 身份验证](./oauth2-authentication.md).


## 何时使用 `/credentials` API端点 {#when-to-use}

>[!IMPORTANT]
>
>在大多数情况下，您 *不* 需要使用 `/credentials` API端点。 您而是可以通过 `customerAuthenticationConfigurations` 参数 `/destinations` 端点。

的 `/credentials` 当Adobe与您的目标之间存在全局身份验证系统，并且与 [!DNL Platform] 客户无需提供任何身份验证凭据即可连接到您的目标。

在这种情况下，必须使用 `/credentials` API端点。 您还必须选择 `PLATFORM_AUTHENTICATION` 在 [目标配置](./destination-configuration.md#destination-delivery). 读取 [凭据API端点操作](./credentials-configuration-api.md) 以获取可对执行的操作的完整列表 `/credentials` 端点。
