---
title: Shopify流源
description: 了解如何创建源连接和数据流，以将流数据从Shopify实例摄取到Adobe Experience Platform
badge: Beta
exl-id: 4c83c08d-c744-4167-9e3b-ed9a995943f4
source-git-commit: feb05d5bddc4135c5fe14d3ec5d8fad62c5e2236
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 2%

---

# [!DNL Shopify Streaming]

>[!NOTE]
>
>的 [!DNL Shopify Streaming] 来源为测试版。 请阅读 [源概述](../../home.md#terms-and-conditions) 有关使用测试版标记的源的详细信息。

Adobe Experience Platform支持从流应用程序中摄取数据。 对流提供商的支持包括 [!DNL Shopify].

## 先决条件 {#prerequisites}

以下部分概述了在使用 [!DNL Shopify Streaming] 来源。

您必须拥有 [!DNL Shopify] 合作伙伴帐户，以便连接到 [!DNL Shopify] API。 如果您还没有合作伙伴帐户，请使用 [[!DNL Shopify] 合作伙伴仪表板](https://www.shopify.com/partners).

### 创建应用程序

具有 [!DNL Shopify] 合作伙伴帐户，您现在可以使用合作伙伴仪表板继续并创建您的应用程序。 有关如何在中创建应用程序的完整步骤 [!DNL Shopify]，阅读 [[!DNL Shopify] 入门指南](https://www.shopify.com/partners/blog/17056443-how-to-generate-a-shopify-api-token).

创建应用程序后，检索 **客户端ID** 和 **客户端密码** 从 **客户端凭据** 选项卡 [!DNL Shopify] 合作伙伴仪表板。 客户端ID和客户端密钥将在后续步骤中使用，以检索您的授权代码和访问令牌。

### 检索授权代码

接下来，通过输入域的 `myshopify.com` 浏览器中的URL，以及定义API密钥、作用域和重定向URI的查询字符串。

此URL的格式如下：

**API格式**

```http
https://{SHOP}.myshopify.com/admin/oauth/authorize?client_id={API_KEY}&scope={SCOPES}&redirect_uri={REDIRECT_URI}
```

| 参数 | 描述 |
| --- | --- |
| `shop` | 您的子域 `myshopify.com` URL。 |
| `api_key` | 您的 [!DNL Shopify] 客户端ID。 您可以从 **客户端凭据** 选项卡 [!DNL Shopify] 合作伙伴仪表板。 |
| `scopes` | 要定义的访问类型。 例如，您可以将范围设置为 `scope=write_orders,read_customers` 以允许修改订单和读取客户的权限。 |
| `redirect_uri` | 将生成访问令牌的脚本的URL。 |

**请求**

```http
https://connnectors-test.myshopify.com/admin/oauth/authorize?client_id=l6fiviermmzpram5i1spfub99shms3j9&scope=write_orders,read_customers&redirect_uri=https://acme.com
```

**响应**

成功响应会返回您的重定向URL，包括生成访问令牌所需的授权代码。

```http
https://www.acme.com/?code=k6j2palgrbljja228ou8c20fmn7w41gz&hmac=68c9163f772eecbc8848c90f695bca0460899c125af897a6d2b0ebbd59d3a43b&shop=connnectors-test.myshopify.com&state=123456×tamp=1658305460
```

### 检索您的访问令牌

现在，您已拥有客户端ID、客户端密钥和授权代码，接下来可以检索您的访问令牌。 要检索您的访问令牌，请向域的 `myshopify.com` URL，同时在 [!DNL Shopify's] API端点： `/admin/oauth/access_token`.

**API格式**

```https
POST /{SHOP}.myshopify.com/admin/oauth/access_token
```

**请求**

以下请求会为 [!DNL Shopify] 实例。

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

成功响应会返回您的访问令牌和权限范围。

```json
{
  "access_token": "shpca_wjhifwfc91psjtldysxd6rqli371tx54",
  "scope": "write_orders,read_customers"
}
```

## 创建用于流式传输的网页挂接 [!DNL Shopify] 数据 {#webhook}

Webhook允许应用程序与 [!DNL Shopify] 在商店中发生特定事件后执行数据或操作。 对于流 [!DNL Shopify] Experience Platform数据时，可以使用webhook定义http端点和订阅主题。

**请求**

以下请求会为您的 [!DNL Shopify Streaming] 数据。

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
| `webhook.topic` | 您的Webhook订阅主题。 有关更多信息，请阅读 [[!DNL Shopify] webhook事件主题指南](https://shopify.dev/docs/api/admin-rest/2023-04/resources/webhook#event-topics). |
| `webhook.format` | 数据的格式。 |

**响应**

成功的响应会返回有关您的Webhook的信息，包括其对应的信息 `id`、地址和其他元数据信息。

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

以下是在 [!DNL Shopify Streaming] 来源。

* 不能保证您能够为同一资源安排不同主题的提交顺序。 例如， `products/update` 网页挂接在 `products/create` 网钩。
* 您可以设置Webhook，以至少将Webhook事件交付一次到端点。 这意味着端点可能多次接收同一事件。 您可以通过比较 `X-Shopify-Webhook-Id` 头到先前的事件。
* [!DNL Shopify] 将HTTP 2xx状态响应视为成功通知。 任何其他状态代码响应都被视为失败。 [!DNL Shopify] 为失败的webhook通知提供重试机制。 如果存在 **等待5秒后没有响应**, [!DNL Shopify] 重试连接 **19次** 在下一步中 **48小时**. 如果在重试时段结束时仍没有响应，则 [!DNL Shopify] 删除网页挂钩。

## 后续步骤

以下教程提供了有关如何连接您的 [!DNL Shopify Streaming] 源到Experience Platform:

* [使用流服务API创建Shopify流源连接和数据流](../../tutorials/api/create/ecommerce/shopify-streaming.md)
* [在UI中创建Shopify流源连接和数据流](../../tutorials/ui/create/ecommerce/shopify-streaming.md)
