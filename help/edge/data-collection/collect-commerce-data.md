---
title: 使用Adobe Experience Platform Web SDK收集商务和产品信息
description: 了解如何使用Adobe Experience Platform Web SDK添加与产品或购物车相关的数据。
keywords: 产品；商务；度量；度量；订单；购物车放弃；结账；productListAdds;productListOpens;productListRepons;productListViews;productViews；购买；saveForLaters;currencyCode;paymentAmount;paymentType;transactionID;priceTotal;purchaseID;purchaseOrderNumber;
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: 51a18ca3a9d0817eafeecea328900eb2f4d1d9a4
workflow-type: tm+mt
source-wordcount: '1326'
ht-degree: 6%

---

# 收集商务和产品信息

如果您的网站上有产品，则这是您可能想要发送的一组默认内容，用于启用Adobe中的大多数功能。 尽管这是一项建议，但它从一开始就提供了一组非常强的数据。

本文档使用 [ExperienceEvent商务详细信息](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) 架构字段组。 的 `commerce` 字段组分为两部分：the `commerce` 对象和 `productListItems` 数组。 的 `commerce` 对象允许您指示正在执行哪些操作 `productListItems` 数组。

>[!TIP]
>
>如果您熟悉Adobe Analytics, `commerce` 与 `events` 变量。 的 `productListItems` 与 `products` 变量。

## 与产品相关的操作

以下是 `measures` 在 `commerce` 对象。

>[!TIP]
>
>度量包含两个字段： `id` 和 `value`. 大多数情况下，您会使用 `value` (例如， `'value':1`)。 的 `id` 字段中，您可以设置唯一标识符，以用于跟踪测量发送的时间。 有关 [测量](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md).

| **测量** | **推荐** | **描述** |
|---|---|---|
| [cartAnabonts](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | 可选 | 用户无法再访问或购买购物车。 |
| [结账](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | 强烈建议 | 用户不再浏览产品，而是正在购买产品。 |
| [productListAdds](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | 强烈建议 | 产品会添加到列表中。 确保在 `productListItems` 同时。 |
| [productListOpens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | 可选 | 随即会创建新的产品列表。 （例如，会创建一个新购物车。） |
| [productListRemuves](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | 强烈建议 | 产品将从产品列表中删除。 |
| [productListReopens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | 可选 | 用户将重新激活产品列表。 这通常发生在再营销活动中。 |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | 强烈建议 | 将查看产品列表。 |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | 强烈建议 | 出现产品视图。 确保在 `productListItems`. |
| [购买](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | 强烈建议 | 接受命令。 必须具有产品列表。 |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | 可选 | 产品已保存以供将来使用。 |

以下是如何设置这些值的示例 `Measures` 中。

```javascript
alloy("sendEvent", {
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    }
  }
});
```

商务对象还具有一个用于收集订单详细信息的特殊字段，称为 `order`.

| **订购** | **选项** | **推荐** | **描述** |
|---|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | 的 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 订单合计的货币。 |
| [payments[paymentItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | 订单上的付款清单。 A [paymentItem](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) 包括以下内容。 |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | 可选 | 的 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 此付款方法的货币。 |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | 强烈建议 | 以指定的货币代码表示的付款值。 |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | 强烈建议 | 付款类型(例如， `credit_card`, `gift_card`, `paypal`)。 查看 [已知值](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values) 以了解详细信息。 |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | 可选 | 此付款交易的唯一ID。 |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | 强烈建议 | 在应用所有折扣和税后，此订单的合计。 |
| [purchaseID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseid) |  | 强烈推荐 | 卖方为此购买分配的唯一标识符。 |
| [purchaseOrderNumber](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseordernumber) |  | 可选 | 购买者为此购买分配的唯一标识符。 |

以下是SDK中典型购买的示例。

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currencyCode":"USD",
        "priceTotal":39.98,
        "payments":[
          {
            "transactionID":"amx12345",
            "paymentAmount":39.98,
            "paymentType":"credit_card",
            "currencyCode":"USD"
          }
        ]
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "priceTotal":29.99,
        "quantity":1
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "priceTotal":9.99,
        "quantity":1
      }
    ]
  }
});
```

## 产品列表

产品列表指示哪些产品与相应的操作相关。 这是 [productListItems](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md). 每个产品都有许多可选字段。

| **字段** | **推荐** | **描述** |
|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | 可选 | 的 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 产品的货币。 仅当您可以拥有具有不同货币代码的产品且产品适用时，此功能才有用。 例如，当购物车或添加到购物车时。 |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | 强烈建议 | 仅应在适用时进行设置。 例如，可能无法在 `productView` 事件，因为产品的不同变体可能具有不同的价格，但 `productListAdds` 事件。 |
| [产品](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | 强烈建议 | 产品的XDM ID。 |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | 强烈建议 | 访客用于将产品项目添加到列表的方法。 设置为 `productListAdds` 度量，且仅当产品添加到列表时才应使用。 示例包括 `add to cart button`、`quick add` 和 `upsell`。 |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | 强烈建议 | 此名称设置为产品的显示名称或人类可读名称。 |
| [数量](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | 强烈建议 | 客户表示他们需要产品的件数。 应设置为 `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters`，等等。 |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | 强烈建议 | 储存单元。 它是产品的唯一标识符。 |

## 示例

`productViews` 事件

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
      }
    ]
  }
});
```

`productListAdds` 事件

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productListAdds":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "quantity":1,
        "priceTotal":29.99,
        "productAddMethod":"Add to Cart Button"
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "quantity":1,
        "priceTotal":9.99,
        "productAddMethod":"Add-on"
      }
    ]
  }
});
```

`checkouts` 事件

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "checkouts":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "quantity":1,
        "priceTotal":29.99
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "quantity":1,
        "priceTotal":9.99
      }
    ]
  }
});
```

`order` 事件

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currencyCode":"USD",
        "priceTotal":39.98,
        "payments":[
          {
            "transactionID":"amx12345",
            "paymentAmount":39.98,
            "paymentType":"credit_card",
            "currencyCode":"USD"
          }
        ]
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "priceTotal":29.99,
        "quantity":1
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "priceTotal":9.99,
        "quantity":1
      }
    ]
  }
});
```
