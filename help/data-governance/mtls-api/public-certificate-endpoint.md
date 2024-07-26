---
title: 公共证书端点
description: 了解如何使用MTLS服务API的/public-certificate端点检索公共证书。
role: Developer
source-git-commit: ce02c1a15d4e87c130de5e6133edda6b66cc2196
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 2%

---

# 公共证书端点

本指南介绍如何使用公共证书端点安全地检索组织Adobe应用程序的公共证书。 它包括一个示例API调用和详细说明，帮助开发人员验证和验证数据交换。

## 快速入门

在继续之前，请查看[快速入门指南](./getting-started.md)以了解成功调用API所需了解的重要信息，包括所需的标头以及如何读取示例API调用。

## API路径 {#paths}

以下信息是使用mTLS服务API所需的基本API路径。 这些资源包括平台网关URL、API的基本路径以及用于检索公共证书的完整路径的示例。

- 平台网关URL： `https://platform.adobe.io/`
- 此API的基本路径： `/data/core/mtls`
- 完整路径示例： `https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate`

## 检索您的公共证书 {#list}

您可以通过向`/v1/certificate/public-certificate`端点发出GET请求来检索贵组织的任何Adobe应用程序的公共证书。

**API格式**

```http
GET /v1/certificate/public-certificate
```

在检索公共证书时，可以使用以下可选查询参数。

| 查询参数 | 描述 | 示例 |
| --------------- | ----------- | ------- |
| `page` | 指定请求结果的开始页面。 | `page=5` |
| `limit` | 每页要检索的公共证书的最大数目。 | `limit=20` |

{style="table-layout:auto"}

**请求**

返回与您的组织关联的公共证书的请求示例，请参见下面的可折叠部分。

+++示例请求

```shell
curl -X GET https://experience.adobe.io/data/core/mtls/v1/certificate/public-certificate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' 
```

+++

**响应**

成功的响应返回HTTP状态200并列出组织的公共证书。

+++成功响应的示例

```json
{
   "results":[
      {
         "certCommonName":"Adobe Experience Platform",
         "publicCertificate":"-----BEGIN CERTIFICATE-----\nMIIDQTCCAimgAwIBAgITBmyfACAfma......KJY5u89CjAwj\n-----END CERTIFICATE-----",
         "expiryDate":"2024-07-17T21:27:57.434Z"
      }
   ],
   "total":0,
   "count":0,
   "_links":{
      "next":{
         "href":"string",
         "templated":true
      },
      "prev":{
         "href":"string",
         "templated":true
      },
      "page":{
         "href":"string",
         "templated":true
      }
   }
}
```

| 属性 | 描述 |
| --- | --- |
| `certCommonName` | 证书的公共名称(CN)，通常表示证书颁发到的服务器或实体的名称或身份。 |
| `publicCertificate` | 字符串格式的实际公共证书，用于验证和加密通信。 |
| `expiryDate` | 公共证书到期的日期和时间，格式为ISO 8601 (UTC)。 |

{style="table-layout:auto"}

+++

## 后续步骤

阅读本指南后，您现在了解了如何使用Adobe Experience Platform API检索公共证书。 要了解有关管理客户数据以确保遵守法规和组织政策的更多信息，请参阅[数据管理概述](../home.md)。

<!-- To test this API call, navigate to the [MTLS API reference page]() to interact with the Experience Platform API endpoints. -->

<!-- Add link after developer page is live -->

