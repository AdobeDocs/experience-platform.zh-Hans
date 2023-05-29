---
title: Shopify Streaming Source
description: 了解如何创建源连接和数据流，以将流数据从Shopify实例摄取到Adobe Experience Platform
badge: 测试版
last-substantial-update: 2023-04-26T00:00:00Z
exl-id: 4c83c08d-c744-4167-9e3b-ed9a995943f4
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 2%

---

# [!DNL Shopify Streaming]

>[!NOTE]
>
>此 [!DNL Shopify Streaming] 源为测试版。 请阅读 [源概述](../../home.md#terms-and-conditions) 有关使用测试版标记源的更多信息。

Adobe Experience Platform支持从流应用程序中摄取数据。 对流媒体提供商的支持包括 [!DNL Shopify].

## 先决条件 {#prerequisites}

以下部分概述了在使用之前要完成的先决条件步骤 [!DNL Shopify Streaming] 源。

您必须拥有有效的 [!DNL Shopify] 合作伙伴帐户，以便连接到 [!DNL Shopify] API。 如果您还没有合作伙伴帐户，请使用 [[!DNL Shopify] 合作伙伴信息板](https://www.shopify.com/partners).

### 创建应用程序

使用有效的 [!DNL Shopify] 合作伙伴帐户后，您现在可以使用合作伙伴功能板继续创建应用程序。 有关如何在中创建应用程序的完整步骤 [!DNL Shopify]，请阅读 [[!DNL Shopify] 入门指南](https://www.shopify.com/partners/blog/17056443-how-to-generate-a-shopify-api-token).

创建应用程序后，检索您的 **客户端ID** 和 **客户端密码** 从 **客户端凭据** 的选项卡 [!DNL Shopify] 合作伙伴信息板。 客户端ID和客户端密钥将在后续步骤中使用，以检索您的授权代码和访问令牌。

### 检索授权码

接下来，通过输入域的 `myshopify.com` 浏览器URL以及定义API密钥、范围和重定向URI的查询字符串。

此URL的格式如下：

**API格式**

```http
https://{SHOP}.myshopify.com/admin/oauth/authorize?client_id={API_KEY}&scope={SCOPES}&redirect_uri={REDIRECT_URI}
```

| 参数 | 描述 |
| --- | --- |
| `shop` | 您的子域 `myshopify.com` URL。 |
| `api_key` | 您的 [!DNL Shopify] 客户端ID。 您可以从以下位置检索客户端ID： **客户端凭据** 的选项卡 [!DNL Shopify] 合作伙伴信息板。 |
| `scopes` | 要定义的访问权限类型。 例如，您可以将范围设置为 `scope=write_orders,read_customers` 允许修改订单和读取客户的权限。 |
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

现在您已经拥有了客户端ID、客户端密钥和授权代码，您可以检索访问令牌。 POST要检索您的访问令牌，请向域的 `myshopify.com` 将此URL附加到时的URL [!DNL Shopify's] API端点： `/admin/oauth/access_token`.

**API格式**

```https
POST /{SHOP}.myshopify.com/admin/oauth/access_token
```

**请求**

以下请求为您的生成一个访问令牌 [!DNL Shopify] 实例。

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

## 创建用于流的webhook [!DNL Shopify] 数据 {#webhook}

Webhook允许应用程序与您的 [!DNL Shopify] 在车间中发生特定事件后数据或执行操作。 用于流 [!DNL Shopify] 要Experience Platform的数据，webhook可用于定义http端点和订阅主题。

**请求**

以下请求为创建webhook [!DNL Shopify Streaming] 数据。

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
| `webhook.topic` | webhook订阅的主题。 有关详细信息，请阅读 [[!DNL Shopify] webhook事件主题指南](https://shopify.dev/docs/api/admin-rest/2023-04/resources/webhook#event-topics). |
| `webhook.format` | 数据的格式。 |

**响应**

成功的响应将返回有关webhook的信息，包括其对应的 `id`、地址和其他元数据信息。

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

以下列出您在将webhook与结合使用时可能会遇到的已知限制 [!DNL Shopify Streaming] 源。

* 不能保证您能够为同一资源安排不同主题的交付顺序。 例如，可能是 `products/update` webhook在 `products/create` webhook。
* 您可以将webhook设置为至少向端点投放webhook事件一次。 这意味着端点可能会多次接收同一事件。 您可以通过比较 `X-Shopify-Webhook-Id` 标头到以前的事件。
* [!DNL Shopify] 将HTTP 2xx状态响应视为成功通知。 任何其他状态代码响应均被视为故障。 [!DNL Shopify] 为失败的webhook通知提供重试机制。 如果有 **等待5秒后无响应**， [!DNL Shopify] 重试连接 **19次** 在下一个过程中 **48小时**. 如果在重试期结束时仍然没有响应，则 [!DNL Shopify] 删除webhook。

## 后续步骤

以下教程提供了有关如何连接 [!DNL Shopify Streaming] 要使用API和UIExperience Platform的源：

* [使用流服务API创建Shopify流源连接和数据流](../../tutorials/api/create/ecommerce/shopify-streaming.md)
* [在UI中创建Shopify流源连接和数据流](../../tutorials/ui/create/ecommerce/shopify-streaming.md)
