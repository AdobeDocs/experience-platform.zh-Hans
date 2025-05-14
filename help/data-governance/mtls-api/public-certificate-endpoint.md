---
title: 公共证书端点
description: 了解如何使用MTLS服务API的/public-certificate端点检索公共证书。
role: Developer
exl-id: 8369c783-e595-476f-9546-801cf4f10f71
source-git-commit: d74353e70e992150c031397009d0c8add3df5e7b
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 2%

---

# 公共证书端点

>[!NOTE]
>
>Adobe不再支持静态下载公共mTLS证书。 使用此API为您的集成检索有效证书。 现在需要自动检索以避免服务中断。

本指南介绍如何使用公共证书端点安全地检索贵组织的Adobe应用程序的公共证书。 它包括一个示例API调用和详细说明，帮助开发人员验证和验证数据交换。

## 快速入门

在继续之前，请查看[快速入门指南](./getting-started.md)，了解有关所需标头以及如何解释示例API调用的重要详细信息。

## API路径 {#paths}

以下信息是使用mTLS服务API所需的基本API路径。 这些资源包括平台网关URL、API的基本路径以及用于检索公共证书的完整路径的示例。

- 平台网关URL： `https://platform.adobe.io/`
- 此API的基本路径： `/data/core/mtls`
- 完整路径示例： `https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate`

## 检索您的公共证书 {#list}

向`/v1/certificate/public-certificate`端点发出GET请求，以检索贵组织的任何Adobe应用程序的公共证书。

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
curl -X GET https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate
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

## 证书生命周期自动化 {#certificate-lifecycle-automation}

Adobe自动化了公共mTLS证书的生命周期，以确保连续性并减少服务中断。

- 证书将在过期前60天重新颁发。
- 证书将在过期前30天被吊销。

>[!NOTE]
>
>这些时间表将根据[CA/B论坛准则](https://www.digicert.com/blog/tls-certificate-lifetimes-will-officially-reduce-to-47-days)缩短时间，该准则旨在将证书生命周期减少到最多47天。

您必须更新集成，以支持通过API进行自动检索。 请勿依赖手动证书下载或静态副本，因为它们可能会导致证书过期或吊销。

## 后续步骤

使用API检索公共证书后，更新您的集成，以在证书过期之前定期调用此端点。 要以交互方式测试此调用，请访问[MTLS API参考页](https://developer.adobe.com/experience-platform-apis/references/mtls-service/)。 有关基于证书的集成的更广泛指导，请参阅[Adobe Experience Platform中的数据加密概述](../../landing/governance-privacy-security/encryption.md)或[数据管理概述](../home.md)。
