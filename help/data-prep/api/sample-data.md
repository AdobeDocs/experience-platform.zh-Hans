---
keywords: Experience Platform；主页；热门主题；数据准备；API指南；示例数据；
solution: Experience Platform
title: 示例数据API端点
topic-legacy: sample data
description: '您可以使用Adobe Experience Platform API中的“/samples”端点以编程方式检索、创建、更新和验证映射示例数据。 '
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 4%

---


# 示例数据端点

在为映射集创建架构时，可以使用示例数据。 您可以使用 `/samples` 数据准备API中的端点，以编程方式检索、创建和更新示例数据。

## 列出示例数据

您可以通过向 `/samples` 端点。

**API格式**

的 `/samples` 端点支持多个查询参数来帮助筛选结果。 目前，您必须同时包含 `start` 和 `limit` 参数。

```http
GET /samples?limit={LIMIT}&start={START}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{LIMIT}` | **必需**. 指定返回的映射示例数据的数量。 |
| `{START}` | **必需**. 指定结果页的偏移。 要获取结果的第一页，请将值设置为 `start=0`. |

**请求**

以下请求将检索IMS组织内的最后两个映射示例数据。

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples?limit=2&start=0 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态200，其中包含有关映射示例数据的最后两个对象的信息。

```json
{
    "data": [
        {
            "id": "2a429a0057ce47109a4b3e2bc256d755",
            "version": 0,
            "createdDate": 1582250863000,
            "modifiedDate": 1582250863000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "sampleData": "{\"id\":\"\",\"first_name\":\"\",\"last_name\":\"\",\"email\":\"\",\"gender\":\"\",\"ip_address\":\"\"}",
            "sampleType": "JSON"
        },
        {
            "id": "0248bfb352214f908bdd6cf9c19447e1",
            "version": 0,
            "createdDate": 1582250892000,
            "modifiedDate": 1582250892000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "sampleData": "{\"id\":\"\",\"first_name\":\"\",\"last_name\":\"\",\"email\":\"\",\"gender\":\"\",\"ip_address\":\"\"}",
            "sampleType": "JSON"
        }
    ],
    "_page": {
        "count": 2,
        "limit": 2
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `sampleData` |  |
| `sampleType` |  |

## 创建示例数据

您可以通过向 `/samples` 端点。

```http
POST /samples
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Smith\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**响应**

成功响应会返回HTTP状态200，其中包含有关新创建的示例数据的信息。

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 0,
    "createdDate": 1615335404492,
    "modifiedDate": 1615335404492,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## 通过上传文件创建示例数据

您可以通过向 `/samples/upload` 端点。

**API格式**

```http
POST /samples/upload
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: multipart/form-data' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'file=@{PATH_TO_FILE}.json'
```

**响应**

成功响应会返回HTTP状态200，其中包含有关新创建的示例数据的信息。

```json
{
    "id": "1fb33209ed126bdcdc0b6c20bae49d8a",
    "version": 0,
    "createdDate": 1615335404492,
    "modifiedDate": 1615335404492,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## 查找特定的示例数据对象

您可以查找示例数据的特定对象，方法是在向提供GET请求的路径中提供其ID `/samples` 端点。

**API格式**

```http
GET /samples/{SAMPLE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SAMPLE_ID}` | 要检索的示例数据对象的ID。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态200，其中包含要检索的示例数据对象的信息。

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 0,
    "createdDate": 1615335404000,
    "modifiedDate": 1615335404000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## 更新示例数据

您可以通过在向提供PUT请求的路径中提供特定示例数据对象的ID，来更新特定示例数据对象 `/samples` 端点。

**API格式**

```http
PUT /samples/{SAMPLE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SAMPLE_ID}` | 要更新的示例数据对象的ID。 |

**请求**

以下请求会更新指定的示例数据。 具体而言，它将姓氏从“Smith”更新为“Lee”。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**响应**

成功响应会返回HTTP状态200，其中包含有关更新的示例数据的信息。

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 1,
    "createdDate": 1615335404000,
    "modifiedDate": 1615337870375,
    "createdBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "modifiedBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```
