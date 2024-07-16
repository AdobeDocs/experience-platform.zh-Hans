---
title: Shopify Streaming Source
description: 了解如何创建源连接和数据流，以将流数据从Shopify实例摄取到Adobe Experience Platform
badge: Beta 版
last-substantial-update: 2023-04-26T00:00:00Z
exl-id: ae991913-68b5-4bbb-b8a5-e566d67a4c1a
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 2%

---

# [!DNL Shopify Streaming]

>[!NOTE]
>
>[!DNL Shopify Streaming]源为测试版。 有关使用测试版标记源的更多信息，请阅读[源概述](../../home.md#terms-and-conditions)。

Adobe Experience Platform支持从流应用程序中摄取数据。 对流式提供程序的支持包括[!DNL Shopify]。

## 先决条件 {#prerequisites}

以下部分概述了在使用[!DNL Shopify Streaming]源之前要完成的先决步骤。

您必须拥有有效的[!DNL Shopify]合作伙伴帐户才能连接到[!DNL Shopify] API。 如果您还没有合作伙伴帐户，请使用[[!DNL Shopify] 合作伙伴信息板](https://www.shopify.com/partners)进行注册。

### 创建应用程序

现在，使用有效的[!DNL Shopify]合作伙伴帐户，您可以使用合作伙伴仪表板继续创建您的应用程序。 有关如何在[!DNL Shopify]中创建应用程序的完整步骤，请阅读[[!DNL Shopify] 入门指南](https://www.shopify.com/partners/blog/17056443-how-to-generate-a-shopify-api-token)。

创建应用程序后，请从[!DNL Shopify]合作伙伴仪表板的&#x200B;**客户端凭据**&#x200B;选项卡中检索您的&#x200B;**客户端ID**&#x200B;和&#x200B;**客户端密钥**。 客户端ID和客户端密钥将在后续步骤中使用，以检索您的授权代码和访问令牌。

### 检索授权码

接下来，通过在浏览器中输入域的`myshopify.com` URL以及定义API密钥、范围和重定向URI的查询字符串，检索您的授权代码。

此URL的格式如下：

**API格式**

```http
https://{SHOP}.myshopify.com/admin/oauth/authorize?client_id={API_KEY}&scope={SCOPES}&redirect_uri={REDIRECT_URI}
```

| 参数 | 描述 |
| --- | --- |
| `shop` | 您的子域`myshopify.com` URL。 |
| `api_key` | 您的[!DNL Shopify]客户端ID。 您可以从[!DNL Shopify]合作伙伴仪表板的&#x200B;**客户端凭据**&#x200B;选项卡中检索您的客户端ID。 |
| `scopes` | 要定义的访问权限类型。 例如，您可以将范围设置为`scope=write_orders,read_customers`以允许修改订单和读取客户的权限。 |
| `redirect_uri` | 将生成访问令牌的脚本的URL。 |

**请求**

```http
https://connnectors-test.myshopify.com/admin/oauth/authorize?client_id=l6fiviermmzpram5i1spfub99shms3j9&scope=write_orders,read_customers&redirect_uri=https://acme.com
```

**响应**

成功的响应将返回您的重定向URL，包括生成访问令牌所需的授权代码。

```http
https://www.acme.com/?code=k6j2palgrbljja228ou8c20fmn7w41gz&hmac=68c9163f772eecbc8848c90f695bca0460899c125af897a6d2b0ebbd59d3a43b&shop=connnectors-test.myshopify.com&state=123456×tamp=1658305460
```

### 检索您的访问令牌

现在，您已拥有客户端ID、客户端密钥和授权码，您可以检索访问令牌了。 要检索您的访问令牌，请在使用[!DNL Shopify's] API终结点追加此URL时向域的`myshopify.com` URL发出POST请求： `/admin/oauth/access_token`。

**API格式**

```https
POST /{SHOP}.myshopify.com/admin/oauth/access_token
```

**请求**

以下请求为您的[!DNL Shopify]实例生成访问令牌。

```shell
curl -X POST \
  'https://connnectors-test.myshopify.com/admin/oauth/access_token' \
  -H 'developer-token: {DEVELOPER_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'Cookie: _master_udr=xxx; request_method=POST'
  -d '{
    "client_id": "l6fiviermmzpram5i1spfub99shms3j9",
    "client_secret": "dajn3caxz9s7ti624ncyv_m4f60jnwi3ii3y3k",
    "code": "k6j2palgrbljja228ou8c20fmn7w41gz"
}'
```

**响应**

成功的响应将返回您的访问令牌和权限范围。

```json
{
  "access_token": "shpca_wjhifwfc91psjtldysxd6rqli371tx54",
  "scope": "write_orders,read_customers"
}
```

## 创建用于流式传输[!DNL Shopify]数据的webhook {#webhook}

Webhook允许应用程序与您的[!DNL Shopify]数据保持同步，或在商店中发生特定事件后执行操作。 对于流式传输[!DNL Shopify]数据以Experience Platform，可以使用Webhook定义http端点和订阅主题。

**请求**

以下请求为您的[!DNL Shopify Streaming]数据创建一个webhook。

```shell
curl -X POST \
  'https://connnectors-test.myshopify.com/admin/api/2022-07/webhooks.json' \
  -H 'X-Shopify-Access-Token: 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' \
  -H 'Content-Type: application/json' \; request_method=POST' \
  -d '{
  "webhook": {
    "address": "https://dcs.adobedc.net/collection/9d411a24aa3c0a3eded92bac6c64d0da986ee7a8212f87168c5fb42d9ddc3227",
    "topic": "orders/create",
    "format": "json"
  }
}'
```

| 参数 | 描述 |
| --- | --- | 
| `webhook.address` | 发送流消息的http端点。 |
| `webhook.topic` | webhook订阅的主题。 有关详细信息，请阅读[[!DNL Shopify] webhook活动主题指南](https://shopify.dev/docs/api/admin-rest/2023-04/resources/webhook#event-topics)。 |
| `webhook.format` | 数据的格式。 |

**响应**

成功的响应将返回有关webhook的信息，包括其对应的`id`、地址和其他元数据信息。

```json
{
  "webhook": {
    "id": 1091138715786,
    "address": "https://dcs.adobedc.net/collection/9d411a24aa3c0a3eded92bac6c64d0da986ee7a8212f87168c5fb42d9ddc3227",
    "topic": "orders/create",
    "created_at": "2022-07-20T07:15:23-04:00",
    "updated_at": "2022-07-20T07:15:23-04:00",
    "format": "json",
    "fields": [],
    "metafield_namespaces": [],
    "api_version": "2021-10",
    "private_metafield_namespaces": []
  }
}
```

### 限制 {#limitations}

以下是将webhook与[!DNL Shopify Streaming]源结合使用时可能会遇到的已知限制列表。

* 我们并不保证您可以为同一资源安排不同主题的交付顺序。 例如，可能会在`products/create` webhook之前交付`products/update` webhook。
* 您可以设置webhook以至少向端点投放webhook事件一次。 这意味着端点可能会多次接收同一事件。 您可以通过将`X-Shopify-Webhook-Id`标头与先前的事件进行比较，来扫描重复的webhook事件。
* [!DNL Shopify]将HTTP 2xx状态响应视为成功通知。 任何其他状态代码响应均被视为失败。 [!DNL Shopify]为失败的webhook通知提供重试机制。 如果等待5秒后&#x200B;**没有响应**，则[!DNL Shopify]在接下来的&#x200B;**48小时**&#x200B;内重试连接&#x200B;**19次**。 如果在重试期间结束时仍然没有响应，则[!DNL Shopify]将删除webhook。

## 后续步骤

以下教程提供了有关如何使用API和UI将[!DNL Shopify Streaming]源连接到Experience Platform的步骤：

* [使用流服务API创建Shopify流源连接和数据流](../../tutorials/api/create/ecommerce/shopify-streaming.md)
* [在UI中创建Shopify流源连接和数据流](../../tutorials/ui/create/ecommerce/shopify-streaming.md)
