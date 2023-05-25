---
keywords: Experience Platform；主页；热门主题；查询服务；API指南；查询服务；查询服务帐户；帐户；
solution: Experience Platform
title: 帐户API端点
description: 您可以为持久性创建查询服务帐户。
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 4%

---

# 帐户端点

在Adobe Experience Platform查询服务中，帐户用于创建可外部SQL客户端使用的未过期的凭据。 您可以使用 `/accounts` 查询服务API中的端点，允许您以编程方式创建、检索、编辑和删除查询服务集成帐户（也称为技术帐户）。

## 快速入门

本指南中使用的端点是Query Service API的一部分。 在继续之前，请查看 [快速入门指南](./getting-started.md) 有关成功调用API所需了解的重要信息，包括所需的标头以及如何读取示例API调用。

## 创建帐户

您可以通过向以下对象发出POST请求来创建查询服务集成帐户： `/accounts` 端点。

**API格式**

```http
POST /accounts
```

**请求**

以下请求将为您的组织创建新的查询服务集成帐户。

```shell
curl -X POST https://platform.adobe.io/data/foundation/queryauth/accounts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
{
    "accountName": "sampleName",
    "assignedToUser": "sample@example.com",
    "credential": "samplecredential",
    "description": "Sample description"
}'
```

| 属性 | 描述 |
| -------- | ----------- |
| `accountName` | **必需** 查询服务集成帐户的名称。 |
| `assignedToUser` | **必需** 将为其创建查询服务集成帐户的Adobe ID。 |
| `credential` | *（可选）* 用于查询服务集成的凭据。 如果未指定，系统将自动为您生成凭据。 |
| `description` | *（可选）* 查询服务集成帐户的描述。 |

**响应**

成功响应会返回HTTP状态200，以及新创建的查询服务集成帐户的详细信息。 您可以使用这些帐户详细信息将查询服务与外部客户端连接。

```json
{
    "technicalAccountName": "2428A037-D963-47C2-A14D-CD816EFB0AA3@TECHACCT.ADOBE.COM",
    "technicalAccountId": "E09A0DFB5FDB25D90A494012",
    "credential": "samplecredential"
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `technicalAccountName` | 查询服务集成帐户的名称。 |
| `technicalAccountId` | 查询服务集成帐户的ID。 这个，以及 `credential`，为您的帐户构成密码。 |
| `credential` | 查询服务集成帐户的凭据。 这个，以及 `technicalAccountId`，为您的帐户构成密码。 |

## 更新帐户

您可以通过向以下网站发出PUT请求来更新查询服务集成帐户： `/accounts` 端点。

**API格式**

```http
POST /accounts/{ACCOUNT_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{ACCOUNT_ID}` | 要更新的查询服务集成帐户的ID。 |

**请求**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
     "accountName": "Updated account name",
     "assignedToUser": "sampleuser2@adobe.com",
     "credential": "UpdatedCredential",
     "description": "Updated description"
 }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `accountName` | *（可选）* 查询服务集成帐户的更新名称。 |
| `assignedToUser` | *（可选）* 查询服务集成帐户所链接的已更新Adobe ID。 |
| `credential` | *（可选）* 查询服务帐户的已更新凭据。 |
| `description` | *（可选）* 查询服务集成帐户的更新描述。 |

**响应**

成功响应会返回HTTP状态200，其中包含有关您新更新的查询服务集成帐户的信息。

```json
{
    "accountName": "Updated account name",
    "assignedToUser": "sampleuser2@adobe.com",
    "created": "2021-06-16T16:44:42.073Z",
    "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
    "credential": "UpdatedCredential",
    "description": "Updated description",
    "lastUpdated": "2021-08-03T23:47:46.588Z",
    "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
    "technicalAccountName": "2428A037-D963-47C2-A14D-CD816EFB0AA3@TECHACCT.ADOBE.COM",
    "technicalAccountId": "E09A0DFB5FDB25D90A494012"
}
```

## 列出所有帐户

您可以通过向以下网站发出GET请求，检索所有查询服务集成帐户的列表 `/accounts` 端点。

**API格式**

```http
GET /accounts
```

**请求**

```shell
curl -X GET https://platform.adobe.io/foundation/queryauth/accounts \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态200，其中包含所有查询服务集成帐户的列表。

```json
{
    "accounts": [
        {
            "lastUpdated": "2021-06-16T18:07:49.581Z",
            "accountName": "Use for XQL testing of account creation",
            "description": "Local test",
            "assignedToUser": "platform-ui-automation@adobe.com",
            "technicalAccountName": "ADC7EB19-63B4-4B9F-A192-EBE3CD0C034E@TECHACCT.ADOBE.COM",
            "technicalAccountId": "38645A7360CA3DF30A49400F",
            "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "created": "2021-06-16T18:07:49.581Z",
            "active": true
        },
        {
            "lastUpdated": "2021-06-16T16:44:42.073Z",
            "accountName": "Use for XQL testing of account creation",
            "description": " ",
            "assignedToUser": "platform-ui-automation@adobe.com",
            "technicalAccountName": "66E91FDD-4733-45E2-A312-D87580CFA55D@TECHACCT.ADOBE.COM",
            "technicalAccountId": "392202E060CA2A770A49420A",
            "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "created": "2021-06-16T16:44:42.073Z",
            "active": true
        }
    ],
    "_page": {
        "count": 2,
        "next": "2021-06-16T16:44:42.073Z",
        "orderby": "-created",
        "property": "active==true",
        "start": "2021-06-16T18:07:49.581Z"
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/queryauth/accounts?orderby=-created&property=active==true&start=2021-06-16T16:44:42.073Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/queryauth/accounts?orderby=-created&property=active==true&start=2021-06-16T18:07:49.581Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

## 删除帐户

您可以通过向以下网站发出DELETE请求来删除您的查询服务集成帐户： `/accounts` 端点。

**API格式**

```http
DELETE /accounts/{ACCOUNT_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{ACCOUNT_ID}` | 要删除的查询服务集成帐户的ID。 |

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应返回HTTP状态200，并显示一条消息，说明已成功删除该帐户。

```json
{
    "result": "Success"
}
```
