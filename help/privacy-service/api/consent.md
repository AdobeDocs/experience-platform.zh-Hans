---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 同意API端点
description: 了解如何使用Privacy ServiceAPI管理Experience Cloud应用程序的客户同意请求。
role: Developer
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 1%

---

# 同意端点

某些法规要求客户明确同意才能收集其个人数据。 [!DNL Privacy Service] API中的`/consent`端点允许您处理客户同意请求并将它们集成到隐私工作流中。

在使用本指南之前，请参阅[快速入门](./getting-started.md)指南，了解有关以下示例API调用中提供的所需身份验证标头的信息。

## 处理客户同意请求

通过向`/consent`端点发出POST请求来处理同意请求。

**API格式**

```http
POST /consent
```

**请求**

以下请求为`entities`数组中提供的用户ID创建新的同意作业。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/consent \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `optOutOfSale` | 如果设置为true，则表示在`entities`下提供的用户希望选择退出出售或共享其个人数据。 |
| `entities` | 一个对象数组，指明同意请求应用于的用户。 每个对象都包含一个`namespace`和一个`values`数组，以匹配具有该命名空间的单个用户。 |
| `nameSpace` | `entities`数组中的每个对象都必须包含Privacy ServiceAPI可识别的[标准标识命名空间](./appendix.md#standard-namespaces)之一。 |
| `values` | 每个用户的值数组，与提供的`nameSpace`相对应。 |

{style="table-layout:auto"}

>[!NOTE]
>
>有关如何确定将哪些客户标识值发送到[!DNL Privacy Service]的更多信息，请参阅[提供标识数据](../identity-data.md)指南。

**响应**

成功的响应返回HTTP状态202 （已接受），没有有效负载，表示[!DNL Privacy Service]已接受请求并正在进行处理。
