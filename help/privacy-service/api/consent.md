---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 同意API端点
description: 了解如何使用Experience CloudAPI管理Privacy Service应用程序的客户同意请求。
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 2%

---

# 同意端点

某些法规要求客户明确同意后才能收集其个人数据。 的 `/consent` 的端点 [!DNL Privacy Service] API允许您处理客户同意请求，并将它们集成到隐私工作流程中。

在使用本指南之前，请参阅 [入门](./getting-started.md) 指南，以了解有关以下示例API调用中所需身份验证标头的信息。

## 处理客户同意请求

同意请求通过向 `/consent` 端点。

**API格式**

```http
POST /consent
```

**请求**

以下请求会为 `entities` 数组。

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
| `optOutOfSale` | 当设置为true时，表示用户在 `entities` 希望选择退出出售或共享其个人数据。 |
| `entities` | 一个对象数组，用于指示同意请求适用的用户。 每个对象都包含 `namespace` 和 `values` 以使用该命名空间匹配单个用户。 |
| `nameSpace` | 中的每个对象 `entities` 数组必须包含 [标准身份命名空间](./appendix.md#standard-namespaces) 由Privacy ServiceAPI识别。 |
| `values` | 每个用户的值数组，与提供的 `nameSpace`. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>有关如何确定要发送到的客户身份值的更多信息 [!DNL Privacy Service]，请参阅 [提供身份数据](../identity-data.md).

**响应**

成功响应会返回无负载的HTTP状态202（已接受），表示已接受该请求 [!DNL Privacy Service] 和正在进行处理。
