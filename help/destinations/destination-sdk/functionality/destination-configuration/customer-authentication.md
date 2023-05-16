---
description: 了解如何为目标设置身份验证机制，并根据您选择的身份验证方法，深入了解用户在UI中将看到的内容。
title: 客户身份验证配置
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 0%

---


# 客户身份验证配置

Experience Platform为合作伙伴和客户提供的身份验证协议提供了极大的灵活性。 您可以配置目标以支持任何行业标准身份验证方法，例如 [!DNL OAuth2]、承载令牌身份验证、密码身份验证等。

本页介绍如何使用首选的身份验证方法设置目标。 根据您在创建目标时使用的身份验证配置，客户在Experience PlatformUI中连接到目标时，将看到不同类型的身份验证页面。

要了解此组件在与Destination SDK创建的集成中的位置，请参阅 [配置选项](../configuration-options.md) 文档或请参阅以下目标配置概述页面：

* [使用Destination SDK配置流目标](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [使用Destination SDK配置基于文件的目标](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

客户必须先按照 [目标连接](../../../ui/connect-destination.md) 教程。

When [创建目标](../../authoring-api/destination-configuration/create-destination-configuration.md) 通过Destination SDK, `customerAuthenticationConfigurations` 部分定义客户在 [身份验证屏幕](../../../ui/connect-destination.md#authenticate). 根据目标身份验证类型，客户必须提供各种身份验证详细信息，例如：

* 对于使用 [基本身份验证](#basic)，则用户必须直接在Experience PlatformUI身份验证页面中提供用户名和密码。
* 对于使用 [载体认证](#bearer)，用户必须提供载体令牌。
* 对于使用 [OAuth2身份验证](#oauth2)，则用户将被重定向到您目标的登录页面，在该页面中，用户可以使用其凭据登录。
* 对于 [Amazon S3](#s3) 目标，用户必须提供 [!DNL Amazon S3] 访问密钥和密钥。
* 对于 [Azure Blob](#blob) 目标，用户必须提供 [!DNL Azure Blob] 连接字符串。

您可以通过 `/authoring/destinations` 端点。 有关详细的API调用示例，请参阅以下API参考页面，您可以在其中配置此页面中显示的组件。

* [创建目标配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目标配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文介绍了可用于目标的所有受支持的客户身份验证配置，并根据您为目标设置的身份验证方法，显示客户将在Experience PlatformUI中看到的内容。

>[!IMPORTANT]
>
>客户身份验证配置不要求您配置任何参数。 当 [创建](../../authoring-api/destination-configuration/create-destination-configuration.md) 或 [更新](../../authoring-api/destination-configuration/update-destination-configuration.md) 目标配置，您的用户将在平台UI中看到相应的身份验证屏幕。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值均为 **区分大小写**. 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 支持的集成类型 {#supported-integration-types}

有关哪些类型的集成支持本页所述功能的详细信息，请参阅下表。

| 集成类型 | 支持功能 |
|---|---|
| 实时（流）集成 | 是 |
| 基于文件的（批处理）集成 | 是 |

## 身份验证规则配置 {#authentication-rule}

使用本页中介绍的任何客户身份验证配置时，始终将 `authenticationRule` 参数 [目标投放](destination-delivery.md) to `"CUSTOMER_AUTHENTICATION"`，如下所示。

```json {line-numbers="true" highlight="4"
{
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

## 基本身份验证 {#basic}

Experience Platform中的实时（流）集成支持基本身份验证。

配置基本身份验证类型时，用户需要输入用户名和密码才能连接到您的目标。

![UI通过基本身份验证呈现](../../assets/functionality/destination-configuration/basic-authentication-ui.png)

要为目标设置基本身份验证，请配置 `customerAuthenticationConfigurations` 部分 `/destinations` 端点，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BASIC"
   }
]
```

## 承载验证 {#bearer}

当您配置承载身份验证类型时，用户需要输入他们从您的目标获取的承载令牌。

![具有承载身份验证的UI呈现](../../assets/functionality/destination-configuration/bearer-authentication-ui.png)

要为目标设置承载类型身份验证，请配置 `customerAuthenticationConfigurations` 部分 `/destinations` 端点，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## OAuth 2身份验证 {#oauth2}

用户选择 **[!UICONTROL 连接到目标]** 触发到您目标的OAuth 2身份验证流，如以下Twitter自定义受众目标示例所示。 有关将OAuth 2身份验证配置到目标端点的详细信息，请阅读专用 [Destination SDKOAuth 2身份验证页面](oauth2-authentication.md).

![使用OAuth 2身份验证渲染UI](../../assets/functionality/destination-configuration/oauth2-authentication-ui.png)

设置 [!DNL OAuth2] 目标的身份验证，配置 `customerAuthenticationConfigurations` 部分 `/destinations` 端点，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"OAUTH2"
   }
]
```

## Amazon S3身份验证 {#s3}

[!DNL Amazon S3] Experience Platform中基于文件的目标支持身份验证。

配置Amazon S3身份验证类型时，用户需要输入其S3凭据。

![UI通过S3身份验证呈现](../../assets/functionality/destination-configuration/s3-authentication-ui.png)

设置 [!DNL Amazon S3] 目标的身份验证，配置 `customerAuthenticationConfigurations` 部分 `/destinations` 端点，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## Azure Blob身份验证  {#blob}

[!DNL Azure Blob Storage] Experience Platform中基于文件的目标支持身份验证。

配置Azure Blob身份验证类型时，需要用户输入连接字符串。

![UI通过Blob身份验证呈现](../../assets/functionality/destination-configuration/blob-authentication-ui.png)

设置 [!DNL Azure Blob] 目标的身份验证，配置 `customerAuthenticationConfigurations` 参数 `/destinations` 端点，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## [!DNL Azure Data Lake Storage] 身份验证 {#adls}

[!DNL Azure Data Lake Storage] Experience Platform中基于文件的目标支持身份验证。

当您配置 [!DNL Azure Data Lake Storage] 身份验证类型，用户需要输入Azure服务主体凭据及其租户信息。

![UI呈现为 [!DNL Azure Data Lake Storage] 身份验证](../../assets/functionality/destination-configuration/adls-authentication-ui.png)

设置 [!DNL Azure Data Lake Storage] (ADLS)目标的身份验证，配置 `customerAuthenticationConfigurations` 参数 `/destinations` 端点，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## 具有密码身份验证的SFTP

[!DNL SFTP] Experience Platform中基于文件的目标支持使用密码进行身份验证。

使用密码身份验证类型配置SFTP时，用户需要输入SFTP用户名和密码，以及SFTP域和端口（默认端口为22）。

![UI通过SFTP进行密码身份验证来呈现](../../assets/functionality/destination-configuration/sftp-password-authentication-ui.png)

要使用密码设置目标的SFTP身份验证，请配置 `customerAuthenticationConfigurations` 参数 `/destinations` 端点，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## 通过SSH密钥身份验证的SFTP

[!DNL SFTP] 验证 [!DNL SSH] 键值支持用于Experience Platform中基于文件的目标。

使用SSH密钥身份验证类型配置SFTP时，需要用户输入SFTP用户名和SSH密钥，以及SFTP域和端口（默认端口为22）。

![通过SFTP通过SSH密钥身份验证来呈现UI](../../assets/functionality/destination-configuration/sftp-key-authentication-ui.png)

要为目标设置使用SSH密钥的SFTP身份验证，请配置 `customerAuthenticationConfigurations` 参数 `/destinations` 端点，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## [!DNL Google Cloud Storage] 身份验证 {#gcs}

[!DNL Google Cloud Storage] Experience Platform中基于文件的目标支持身份验证。

当您配置 [!DNL Google Cloud Storage] 身份验证类型，用户需要输入 [!DNL Google Cloud Storage] [!UICONTROL 访问密钥ID] 和 [!UICONTROL 密钥访问密钥].

![通过Google云存储身份验证呈现UI](../../assets/functionality/destination-configuration/google-cloud-storage-ui.png)

设置 [!DNL Google Cloud Storage] 目标的身份验证，配置 `customerAuthenticationConfigurations` 参数 `/destinations` 端点，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```

## 后续步骤 {#next-steps}

阅读本文后，您应该对如何配置目标平台的用户身份验证有了更好的了解。

要了解有关其他目标组件的更多信息，请参阅以下文章：

* [OAuth2身份验证](oauth2-authentication.md)
* [客户数据字段](customer-data-fields.md)
* [UI属性](ui-attributes.md)
* [架构配置](schema-configuration.md)
* [身份命名空间配置](identity-namespace-configuration.md)
* [支持的映射配置](supported-mapping-configurations.md)
* [目标投放](destination-delivery.md)
* [受众元数据配置](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批量配置](batch-configuration.md)
* [历史用户档案资格](historical-profile-qualifications.md)