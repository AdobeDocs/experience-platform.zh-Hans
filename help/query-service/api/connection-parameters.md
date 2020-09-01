---
keywords: Experience Platform;home;popular topics;query service;api guide;connection parameters;Query service;
solution: Experience Platform
title: 查询服务开发人员指南
topic: connection parameters
translation-type: tm+mt
source-git-commit: c5d3be4706ca6d6a30e203067db6ddc894b9bfb4
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 1%

---


# 连接参数

## 示例API调用

现在，您已经了解要使用哪些标头，便可开始调用 [!DNL Query Service] API。 以下各节将介绍您可以使用API进行的各种API [!DNL Query Service] 调用。 每个调用都包括常规API格式、显示所需标头的示例请求和示例响应。

### 请求交互式服务的连接参数

通过向端点发出GET请求 [，可以检索连接参数以](../creating-queries/writing-queries.md) 使用交互式 `/connection_parameters` 服务。 有关使用连接参数通过交互式服务连接的客户端的详细信息，请阅读有关查询服务客户端 [的文档](../clients/overview.md)。

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
