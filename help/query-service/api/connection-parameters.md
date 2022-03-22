---
keywords: Experience Platform；主页；热门主题；查询服务；API指南；连接参数；查询服务；
solution: Experience Platform
title: 连接参数API端点
topic-legacy: connection parameters
description: 通过向/connection_parameters端点发出GET请求，可以检索连接参数以使用交互式服务。
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: cff95575530e0db00d34ff1ea4c90e5422b6562d
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 1%

---

# 连接参数端点

## API调用示例

以下部分将指导您完成使用 [!DNL Query Service] API。 调用包括常规API格式、显示所需标头的示例请求和示例响应。

### 请求连接参数

您可以通过向 `/connection_parameters` 端点。 有关使用连接参数通过交互式服务连接的客户端的更多信息，请阅读 [查询服务客户端](../clients/overview.md).

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

成功响应会通过连接参数返回HTTP状态200。

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
