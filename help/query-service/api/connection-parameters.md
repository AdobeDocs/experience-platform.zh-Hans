---
keywords: Experience Platform；主页；热门主题；查询服务；API指南；连接参数；查询服务；
solution: Experience Platform
title: 连接参数API端点
description: 通过向/connection_parameters端点发出GET请求，可以检索用于使用交互式服务的连接参数。
role: Developer
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 1%

---

# 连接参数端点

## 示例API调用

以下部分将指导您完成可以使用[!DNL Query Service] API进行的API调用。 该调用包括常规API格式、显示所需标头的示例请求以及示例响应。

### 请求连接参数

您可以通过向`/connection_parameters`端点发出GET请求来检索连接参数。 有关使用连接参数通过交互式服务进行连接的客户端的详细信息，请阅读有关[查询服务客户端](../clients/overview.md)的文档。

**API格式**

```http
GET /connection_parameters
```

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/connection_parameters
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回包含连接参数的HTTP状态200。

```json
{
    "username": "{USERNAME}",
    "dbName": "prod:all",
    "host": "{HOSTNAME}",
    "version": 1,
    "port": 80,
    "token": "{TOKEN}",
    "compressedToken": "{COMPRESSED_TOKEN}",
    "websocketHost": "{WEBSOCKET_HOSTNAME}"
}
```
