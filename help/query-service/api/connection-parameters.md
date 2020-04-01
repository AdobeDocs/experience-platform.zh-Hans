---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 查询服务开发人员指南
topic: connection parameters
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# 连接参数

## 示例API调用

既然您了解了要使用哪些标头，就可以开始调用查询服务API了。 以下各节将介绍您可以使用查询服务API进行的各种API调用。 每个调用包括常规API格式、显示所需标题的示例请求和示例响应。

### 请求交互式服务的连接参数

可以通过向端点发出GET请求 [来检索连接参数](../creating-queries/writing-queries.md) ，以便使用交互式 `/connection_parameters` 服务。 有关使用连接参数通过交互式服务连接的客户端的详细信息，请阅读有关 [查询服务客户端的文档](../clients/overview.md)。

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
