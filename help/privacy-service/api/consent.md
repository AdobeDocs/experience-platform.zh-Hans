---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 同意API端点
description: 了解如何使用Privacy ServiceAPI管理Experience Cloud应用程序的客户同意请求。
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 1%

---

# 同意端点

某些法规要求在收集其个人数据之前获得客户的明确同意。 此 `/consent` 中的端点 [!DNL Privacy Service] API允许您处理客户同意请求并将它们集成到您的隐私工作流中。

在使用本指南之前，请参阅 [快速入门](./getting-started.md) 指南，以了解有关以下示例API调用中提供的所需身份验证标头的信息。

## 处理客户同意请求

同意请求是通过向以下对象发出POST请求来处理的 `/consent` 端点。

**API格式**

```http
POST /consent
```

**请求**

以下请求为中提供的用户ID创建新的同意作业 `entities` 数组。

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
| `optOutOfSale` | 当设置为true时，表示提供的用户位于 `entities` 希望选择退出出售或共享其个人数据。 |
| `entities` | 一个对象数组，指明同意请求应用于的用户。 每个对象都包含 `namespace` 和数组 `values` 将单个用户与该命名空间进行匹配。 |
| `nameSpace` | 中的每个对象 `entities` 数组必须包含一个 [标准身份命名空间](./appendix.md#standard-namespaces) 由Privacy ServiceAPI识别。 |
| `values` | 每个用户的值数组，对应于提供的 `nameSpace`. |

{style="table-layout:auto"}

>[!NOTE]
>
>有关如何确定要将哪些客户标识值发送到的更多信息 [!DNL Privacy Service]，请参阅指南，网址为 [提供身份数据](../identity-data.md).

**响应**

成功的响应返回HTTP状态202 （已接受），没有任何有效负载，表示请求已被接受 [!DNL Privacy Service] 并正在进行处理。
