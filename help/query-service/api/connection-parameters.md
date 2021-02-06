---
keywords: Experience Platform；主题；热门主题；查询服务；api指南；连接参数；查询服务；
solution: Experience Platform
title: 连接参数API端点
topic: connection parameters
description: 通过向/connection_parameters端点发出GET请求，可以检索连接参数以使用交互式服务。
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 1%

---


# 连接参数端点

## 示例API调用

既然您了解了要使用哪些标头，就可以开始调用[!DNL Query Service] API。 以下各节将介绍您可以使用[!DNL Query Service] API进行的各种API调用。 每个调用都包括常规API格式、显示所需标头的示例请求和示例响应。

### 请求连接参数

您可以通过向`/connection_parameters`端点发出GET请求来检索连接参数。 有关使用连接参数通过交互式服务连接的客户端的详细信息，请阅读[查询服务客户端](../clients/overview.md)的相关文档。

**API格式**

```http
GET /connection_parameters
```

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/connection_parameters
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会使用连接参数返回HTTP状态200。

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
