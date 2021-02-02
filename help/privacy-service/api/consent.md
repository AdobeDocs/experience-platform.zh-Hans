---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 同意端点
topic: developer guide
description: 了解如何使用Experience CloudAPI管理Privacy Service应用程序的客户同意请求。
translation-type: tm+mt
source-git-commit: 238a9200e4b43d41335bed0efab079780b252717
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 1%

---


# 同意端点

某些法规要求客户明确同意后才能收集其个人数据。 使用[!DNL Privacy Service] API中的`/consent`端点，您可以处理客户同意请求并将其集成到您的隐私工作流中。

在使用本指南之前，请参阅[快速入门](./getting-started.md)部分，了解以下示例API调用中显示的所需身份验证头。

## 处理客户同意请求

通过向`/consent`端点发出POST请求来处理同意请求。

**API格式**

```http
POST /consent
```

**请求**

以下请求为`entities`阵列中提供的用户ID创建新的同意作业。

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
| `optOutOfSale` | 如果设置为true，则表示在`entities`下提供的用户希望退出销售或共享其个人数据。 |
| `entities` | 一组对象，指示同意请求的用户。 每个对象都包含一个`namespace`和一个`values`数组，以将各个用户与该命名空间相匹配。 |
| `nameSpace` | `entities`数组中的每个对象都必须包含由Privacy ServiceAPI识别的[标准标识命名空间](./appendix.md#standard-namespaces)中的一个。 |
| `values` | 每个用户的值数组，与提供的`nameSpace`对应。 |

>[!NOTE]
>
>有关如何确定要发送到[!DNL Privacy Service]的客户身份值的详细信息，请参阅[提供身份数据](../identity-data.md)的指南。

**响应**

成功的响应返回没有有效负荷的HTTP状态202（已接受），表示请求已被[!DNL Privacy Service]接受，且正在处理中。