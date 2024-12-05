---
keywords: Experience Platform；安全性；ip-access；QS-Auth；API指南；查询服务；IP范围
title: IP访问端点
description: 了解如何使用IP访问API端点在查询服务中管理沙盒访问的IP范围。
role: Developer
exl-id: fc15ab50-c125-4f00-a311-81fd41697c7d
source-git-commit: d0f4a295928b000b6091172800e453d79dc44e3a
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 3%

---

# IP访问端点

>[!AVAILABILITY]
>
>此功能适用于购买了Data Distiller附加产品的客户。 有关更多信息，请与您的 Adobe 代表联系。

要保护指定查询服务沙盒中的数据访问，请使用IP访问端点管理允许的IP范围。 您可以使用此API获取、配置或删除与组织ID关联的IP范围。

您可以使用IP访问API执行以下操作：

- **获取所有IP范围**
- **设置新IP范围**
- **删除现有IP范围**

本文档介绍您可以从`/security/ip-access`端点发出和接收的请求和响应。

>[!NOTE]
>
>您必须具有用户令牌才能调用此API。 有关获取每个标头所需值的信息，请参阅[快速入门指南](./getting-started.md)。

## 获取所有IP范围 {#fetch-all-ip-ranges}

检索为您的沙盒配置的所有IP范围列表。 如果未设置IP范围，则默认情况下允许所有IP，并且响应在`allowedIpRanges`中返回空列表。

**API格式**

```http
GET /security/ip-access
```

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/queryauth/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，其中包含沙盒允许的IP范围列表。

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "allowedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "101.10.1.1"}
  ]
}
```

下表提供了响应模式属性的说明和示例：

| 属性 | 描述 | 示例 |
|------------------|---------------------------------------------|-----------------------------------------------------------------------------------------------|
| `imsOrg` | 沙盒的组织ID。 | `{ORG_ID}` |
| `sandboxName` | 应用IP限制的沙盒的名称。 | `prod` |
| `channel` | IP限制的访问模式。 当前唯一接受的值为`data_distiller`。 此值表示IP限制应用于PSQL或JDBC连接。 | `data_distiller` |
| `allowedIpRanges` | CIDR或固定IP格式中允许的IP列表。 每个条目可以包含可选描述。 | `[{"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"}]` |

>[!NOTE]
>
>`allowedIpRanges`字段可以包含两种类型的IP规范：<br><ul><li>**CIDR**：用于定义IP范围的标准CIDR表示法（例如`"136.23.110.0/23"`）。</li><li>**已修复IP**：单个访问权限只有一个IP（例如，`"101.10.1.1"`）。</li></ul>

## 设置新IP范围

通过设置沙盒的新列表覆盖现有IP范围。 此操作需要提供完整的IP范围列表，包括任何保持不变的IP范围。

**API格式**

```http
PUT /security/ip-access
```

**请求**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/queryauth/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "ipRanges": [
       {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
       {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
       {"ipRange": "101.10.1.1"},
       {"ipRange": "163.77.30.9", "description": "Test server IP"}
     ]
   }'
```

**响应**

成功的响应返回HTTP状态200以及新配置的IP范围的详细信息。

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "allowedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
    {"ipRange": "101.10.1.1"},
    {"ipRange": "163.77.30.9", "description": "Test server IP"}
  ]
}
```

## 删除IP范围 {#delete-ip-ranges}

为沙盒删除所有配置的IP范围。 此操作删除IP范围并返回已删除的IP列表。

>[!NOTE]
>
>删除操作适用于组织(`imsOrg`) ID，并影响为沙盒配置的所有IP范围。

**API格式**

```http
DELETE /security/ip-access
```

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/queryauth/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200及已删除的IP范围的详细信息。

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "deletedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
    {"ipRange": "101.10.1.1"},
    {"ipRange": "163.77.30.9", "description": "Test server IP"}
  ]
}
```
