---
description: 了解如何为目标设置身份验证机制，并深入了解根据您选择的身份验证方法用户将在UI中看到的内容。
title: 客户身份验证配置
exl-id: 3912012e-0870-47d2-9a6f-7f1fc469a781
source-git-commit: 82ba4e62d5bb29ba4fef22c5add864a556e62c12
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 0%

---

# 客户身份验证配置

Experience Platform为合作伙伴和客户提供的身份验证协议提供了极大的灵活性。 您可以将目标配置为支持任何行业标准身份验证方法，例如 [!DNL OAuth2]、持有者令牌身份验证、密码身份验证等。

本页说明如何使用首选身份验证方法设置目标。 根据您在创建目标时使用的身份验证配置，客户在Experience PlatformUI中连接到目标时将看到不同类型的身份验证页面。

要了解此组件在何处适合使用Destination SDK创建的集成，请参阅中的图表 [配置选项](../configuration-options.md) 文档或参阅以下目标配置概述页面：

* [使用Destination SDK配置流目标](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [使用Destination SDK配置基于文件的目标](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Experience Platform在客户将数据从Platform导出到您的目标之前，他们必须按照 [目标连接](../../../ui/connect-destination.md) 教程。

时间 [创建目标](../../authoring-api/destination-configuration/create-destination-configuration.md) 通过Destination SDK， `customerAuthenticationConfigurations` 部分定义客户在中看到的内容 [身份验证屏幕](../../../ui/connect-destination.md#authenticate). 根据目标身份验证类型，客户必须提供各种身份验证详细信息，例如：

* 对于目标，使用 [基本身份验证](#basic)，用户必须直接在Experience PlatformUI身份验证页面中提供用户名和密码。
* 对于目标，使用 [承载认证](#bearer)，用户必须提供持有者令牌。
* 对于目标，使用 [OAuth2授权](#oauth2)，则用户将被重定向到您目标的登录页面，以便他们能够使用其凭据进行登录。
* 对象 [Amazon S3](#s3) 目标，用户必须提供其 [!DNL Amazon S3] 访问密钥和密钥。
* 对象 [Azure Blob](#blob) 目标，用户必须提供其 [!DNL Azure Blob] 连接字符串。

您可以通过以下方式配置客户身份验证详细信息 `/authoring/destinations` 端点。 有关详细的API调用示例，请参阅以下API参考页面，您可以在其中配置此页面中显示的组件。

* [创建目标配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目标配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文介绍了可用于您的目标的所有受支持的客户身份验证配置，并显示客户将基于您为目标设置的身份验证方法在Experience PlatformUI中看到的内容。

>[!IMPORTANT]
>
>客户身份验证配置不需要配置任何参数。 在以下情况下，您可以在API调用中复制并粘贴此页面中显示的代码片段 [创建](../../authoring-api/destination-configuration/create-destination-configuration.md) 或 [正在更新](../../authoring-api/destination-configuration/update-destination-configuration.md) 目标配置，您的用户将在Platform UI中看到相应的身份验证屏幕。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值包括 **区分大小写**. 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 支持的集成类型 {#supported-integration-types}

有关哪些类型的集成支持此页面上描述的功能，请参阅下表。

| 集成类型 | 支持功能 |
|---|---|
| 实时（流）集成 | 是 |
| 基于文件（批处理）的集成 | 是 |

## 身份验证规则配置 {#authentication-rule}

使用本页中介绍的任何客户身份验证配置时，请始终设置 `authenticationRule` 中的参数 [目标投放](destination-delivery.md) 到 `"CUSTOMER_AUTHENTICATION"`，如下所示。

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

对于Experience Platform中的实时（流）集成，支持基本身份验证。

配置基本身份验证类型时，用户需要输入用户名和密码以连接到您的目标。

![使用基本身份验证呈现UI](../../assets/functionality/destination-configuration/basic-authentication-ui.png)

要为您的目标设置基本身份验证，请配置 `customerAuthenticationConfigurations` 的部分，通过 `/destinations` 端点，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BASIC"
   }
]
```

## 持有者身份验证 {#bearer}

配置持有者身份验证类型时，用户需要输入他们从您的目标获得的持有者令牌。

![使用持有者身份验证的UI渲染](../../assets/functionality/destination-configuration/bearer-authentication-ui.png)

要为目标设置持有者类型身份验证，请配置 `customerAuthenticationConfigurations` 的部分，通过 `/destinations` 端点，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## OAuth 2身份验证 {#oauth2}

用户选择 **[!UICONTROL 连接到目标]** 以触发指向您目标的OAuth 2身份验证流程，如Twitter自定义受众目标的以下示例所示。 有关为目标端点配置OAuth 2身份验证的详细信息，请阅读专用 [Destination SDKOAuth 2身份验证页面](oauth2-authorization.md).

![使用OAuth 2身份验证呈现UI](../../assets/functionality/destination-configuration/oauth2-authentication-ui.png)

设置 [!DNL OAuth2] 身份验证，配置 `customerAuthenticationConfigurations` 的部分，通过 `/destinations` 端点，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"OAUTH2"
   }
]
```

## Amazon S3身份验证 {#s3}

[!DNL Amazon S3] Experience Platform中基于文件的目标支持身份验证。

配置Amazon S3身份验证类型时，要求用户输入其S3凭据。

![使用S3身份验证呈现UI](../../assets/functionality/destination-configuration/s3-authentication-ui.png)

设置 [!DNL Amazon S3] 身份验证，配置 `customerAuthenticationConfigurations` 的部分，通过 `/destinations` 端点，如下所示：

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

![使用Blob身份验证呈现UI](../../assets/functionality/destination-configuration/blob-authentication-ui.png)

设置 [!DNL Azure Blob] 身份验证，配置 `customerAuthenticationConfigurations` 中的参数 `/destinations` 端点，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## [!DNL Azure Data Lake Storage] 身份验证 {#adls}

[!DNL Azure Data Lake Storage] Experience Platform中基于文件的目标支持身份验证。

当您配置 [!DNL Azure Data Lake Storage] 身份验证类型，要求用户输入Azure服务主体凭据及其租户信息。

![UI呈现方式 [!DNL Azure Data Lake Storage] 身份验证](../../assets/functionality/destination-configuration/adls-authentication-ui.png)

设置 [!DNL Azure Data Lake Storage] (ADLS)身份验证，配置 `customerAuthenticationConfigurations` 中的参数 `/destinations` 端点，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## 具有密码身份验证的SFTP

[!DNL SFTP] 对于Experience Platform中基于文件的目标，支持使用密码进行身份验证。

在配置具有密码身份验证类型的SFTP时，用户需要输入SFTP用户名和密码，以及SFTP域和端口（默认端口为22）。

![通过带有密码身份验证的SFTP呈现UI](../../assets/functionality/destination-configuration/sftp-password-authentication-ui.png)

要为您的目标设置带有密码的SFTP身份验证，请配置 `customerAuthenticationConfigurations` 中的参数 `/destinations` 端点，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## 具有SSH密钥身份验证的SFTP

[!DNL SFTP] 身份验证 [!DNL SSH] Experience Platform中基于文件的目标支持密钥。

在配置具有SSH密钥身份验证类型的SFTP时，用户需要输入SFTP用户名和SSH密钥，以及SFTP域和端口（默认端口为22）。

![使用SSH密钥身份验证的SFTP呈现UI](../../assets/functionality/destination-configuration/sftp-key-authentication-ui.png)

要为您的目标设置使用SSH密钥的SFTP身份验证，请配置 `customerAuthenticationConfigurations` 中的参数 `/destinations` 端点，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## [!DNL Google Cloud Storage] 身份验证 {#gcs}

[!DNL Google Cloud Storage] Experience Platform中基于文件的目标支持身份验证。

当您配置 [!DNL Google Cloud Storage] 身份验证类型，要求用户输入其 [!DNL Google Cloud Storage] [!UICONTROL 访问密钥ID] 和 [!UICONTROL 访问密钥].

![使用Google Cloud Storage身份验证呈现UI](../../assets/functionality/destination-configuration/google-cloud-storage-ui.png)

设置 [!DNL Google Cloud Storage] 身份验证，配置 `customerAuthenticationConfigurations` 中的参数 `/destinations` 端点，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```

## 后续步骤 {#next-steps}

阅读本文后，您应该更好地了解如何为目标平台配置用户身份验证。

要了解有关其他目标组件的更多信息，请参阅以下文章：

* [OAuth2授权](oauth2-authorization.md)
* [客户数据字段](customer-data-fields.md)
* [UI属性](ui-attributes.md)
* [架构配置](schema-configuration.md)
* [身份命名空间配置](identity-namespace-configuration.md)
* [支持的映射配置](supported-mapping-configurations.md)
* [目标投放](destination-delivery.md)
* [受众元数据配置](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批次配置](batch-configuration.md)
* [历史配置文件资格](historical-profile-qualifications.md)
