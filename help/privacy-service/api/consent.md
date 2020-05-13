---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 同意
topic: developer guide
translation-type: tm+mt
source-git-commit: a3178ab54a7ab5eacd6c5f605b8bd894779f9e85
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 1%

---


# 同意

某些法规要求客户明确同意后才能收集其个人数据。 隐私 `/consent` 服务API中的端点允许您处理客户同意请求并将其集成到您的隐私工作流程中。

在使用本指南之前，请参阅 [入门部分](./getting-started.md) ，了解以下示例API调用中显示的所需身份验证头。

## 处理客户同意请求

通过向端点发出POST请求来处理同意 `/consent` 请求。

**API格式**

```http
POST /consent
```

**请求**

以下请求为阵列中提供的用户ID创建新的同意 `entities` 作业。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/consent \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
        "optOutOfSale": true,
        "entities": [
          {
            "nameSpace": "email",
            "values": [
              "dsmith@acme.com",
              "ajones@acme.com"
            ]
          },
          {
            "nameSpace": "ECID",
            "values": [
              "443636576799758681021090721276"
            ]
          }
        ]
      }'
```

| 属性 | 描述 |
| --- | --- |
| `optOutOfSale` | 设置为true时，表示根据提供的用户 `entities` 希望退出销售或共享其个人数据。 |
| `entities` | 一组对象，指示同意请求的用户。 每个对象都包 `namespace` 含一个和一组 `values` 用于将单个用户与该命名空间匹配的对象。 |
| `nameSpace` | 数组中的每个 `entities` 对象都必须包含 [Privacy Service API识别](./appendix.md#standard-namespaces) 的标准标识命名空间之一。 |
| `values` | 每个用户的值的数组，对应于所提供的 `nameSpace`。 |

>[!NOTE] 有关如何确定要发送到隐私服务的客户身份值的更多信息，请参阅提供身 [份数据指南](../identity-data.md)。

**响应**

成功的响应返回没有有效负荷的HTTP状态202（已接受），表示该请求已被隐私服务接受并且正在处理。