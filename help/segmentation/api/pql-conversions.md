---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: PQL转换
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# PQL转换

介绍

- 从pql/text和pql/json转换格式

## 入门指南

本指南中使用的API端点是分段API的一部分。 在继续之前，请查阅分段开 [发人员指南](./getting-started.md)。

特别是，分段开 [发人员指南的入门部分](./getting-started.md#getting-started) ，包括相关主题的链接、在文档中阅读示例API调用的指南，以及成功调用任何Experience Platform API所需的标题的重要信息。

## 从pql/text和pql/json转换格式

**API格式**

```http
POST /segment/conversion
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/conversion \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "name": "People who ordered in the last 30 days",
  "expression": {
    "type": "PQL",
    "format": "pql/text",
    "value": "workAddress.country = \"US\""
  },
  "schema": {
    "name": "_xdm.context.profile"
  },
  "ttlInDays": 60
}
 '
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 区段定义的唯一名称。 |
| `expression.type` | 表达式类型。 它可以是 `PQL` 或 `ARL`。 |
| `expression.format` | 表达式格式。 它可以是 `pql/text` 或 `pql/json`。 |
| `expression.value` | 要转换的查询的表达式字符串。 |
| `schema.name` | 您引用的模式的类ID。 |
| `ttlInDays` | 表示生存时间(TTL)的整数。 |

**响应**

成功的响应会返回HTTP状态200，其中包含已转换段的详细信息。

```json
{
    "ttlInDays": 60,
    "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"country\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"workAddress\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}},{\"nodeType\":\"literal\",\"literalType\":\"String\",\"value\":\"US\"}]}"
    }
}
```

## 后续步骤
