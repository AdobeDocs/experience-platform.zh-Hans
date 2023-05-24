---
keywords: Experience Platform；首頁；熱門主題；查詢服務；API指南；查詢服務；查詢服務帳戶；帳戶；
solution: Experience Platform
title: 帳戶API端點
description: 您可以為永久性建立查詢服務帳戶。
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 4%

---

# 帳戶端點

在Adobe Experience Platform Query Service中，帳戶是用來建立可搭配外部SQL使用者端使用的不會到期的認證。 您可以使用 `/accounts` Query Service API中的端點，可讓您以程式設計方式建立、擷取、編輯和刪除您的Query Service整合帳戶（也稱為技術帳戶）。

## 快速入门

本指南中使用的端點是Query Service API的一部分。 在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需成功呼叫API所需的重要資訊，包括必要的標頭及如何讀取範例API呼叫。

## 建立帳戶

您可以透過向以下發出POST請求來建立查詢服務整合帳戶： `/accounts` 端點。

**API格式**

```http
POST /accounts
```

**请求**

以下請求將為您的組織建立新的查詢服務整合帳戶。

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
| `accountName` | **必填** 查詢服務整合帳戶的名稱。 |
| `assignedToUser` | **必填** 將為其建立查詢服務整合帳戶的Adobe ID。 |
| `credential` | *（可選）* 用於查詢服務整合的認證。 如果未指定，系統會自動為您產生認證。 |
| `description` | *（可選）* 查詢服務整合帳戶的說明。 |

**响应**

成功的回應會傳回HTTP狀態200，以及您新建立的查詢服務整合帳戶的詳細資料。 您可以使用這些帳戶詳細資料來連線查詢服務與外部使用者端。

```json
{
    "technicalAccountName": "2428A037-D963-47C2-A14D-CD816EFB0AA3@TECHACCT.ADOBE.COM",
    "technicalAccountId": "E09A0DFB5FDB25D90A494012",
    "credential": "samplecredential"
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `technicalAccountName` | 查詢服務整合帳戶的名稱。 |
| `technicalAccountId` | 查詢服務整合帳戶的ID。 此專案連同 `credential`，為您的帳戶撰寫密碼。 |
| `credential` | 查詢服務整合帳戶的認證。 此專案連同 `technicalAccountId`，為您的帳戶撰寫密碼。 |

## 更新帳戶

您可以透過向發出PUT請求來更新您的查詢服務整合帳戶 `/accounts` 端點。

**API格式**

```http
POST /accounts/{ACCOUNT_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{ACCOUNT_ID}` | 您要更新的查詢服務整合帳戶ID。 |

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
| `accountName` | *（可選）* 查詢服務整合帳戶的更新名稱。 |
| `assignedToUser` | *（可選）* 查詢服務整合帳戶所連結的更新Adobe ID。 |
| `credential` | *（可選）* 更新您的Query Service帳戶的認證。 |
| `description` | *（可選）* 查詢服務整合帳戶的更新說明。 |

**响应**

成功回應會傳回HTTP狀態200，其中包含您新更新查詢服務整合帳戶的相關資訊。

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

## 列出所有帳戶

您可以透過向以下專案發出GET要求，擷取所有查詢服務整合帳戶的清單： `/accounts` 端點。

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

成功的回應會傳回HTTP狀態200，並包含所有查詢服務整合帳戶的清單。

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

## 刪除帳戶

您可以透過向發出DELETE請求來刪除您的查詢服務整合帳戶 `/accounts` 端點。

**API格式**

```http
DELETE /accounts/{ACCOUNT_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{ACCOUNT_ID}` | 您要刪除的查詢服務整合帳戶ID。 |

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功回應會傳回HTTP狀態200，並出現訊息，指出已成功刪除帳戶。

```json
{
    "result": "Success"
}
```
