---
title: 产品
seo-title: 使用Adobe Experience Platform Web SDK支持产品
description: 了解如何通过Experience Platform Web SDK添加产品或购物车中的数据
seo-description: 了解如何通过Experience Platform Web SDK添加产品或购物车中的数据
translation-type: tm+mt
source-git-commit: 4bff4b20ccc1913151aa1783d5123ffbb141a7d0
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 5%

---


# 产品

如果您的网站上有产品，则这是您可能希望发送的默认内容集，以启用Adobe提供的大多数功能。 尽管这是一个建议，但它直接从开始提供了一组非常强大的数据。

此文档使用 [ExperienceEvent商务详细信](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) 息混合。 混 `commerce` 合物分为两部分： 对 `commerce` 象和数 `productListItems` 组。 该对 `commerce` 象允许您指示正在对数组执行哪些 `productListItems` 操作。

>[!Tip]
>如果您熟悉Adobe Analytics，则与 `commerce` 该变量关系最 `events` 密切。 该 `productListItems` 变量与变量更为 `products` 相关。

## 与产品相关的操作

以下是对象 `measures` 中可用的 `commerce` 列表。

>[!Tip]
>度量包含两个字段： `id` 和 `value`。 大多数情况下，您只 `value` 使用字段(例如 `'value':1`)。 该 `id` 字段允许您设置唯一标识符，以便跟踪度量的发送时间。 请参阅XDM文档以 [进行衡量](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md)。

| **度量** | **推荐** | **描述** |
|---|---|---|
| [购物车放弃](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | 可选 | 购物车不再可由用户访问或购买。 |
| [结帐](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | 强烈建议 | 用户不再浏览产品，但正在购买产品。 |
| [productListAdds](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | 强烈建议 | 产品会添加到列表。 务必同时设置 `productListItems` 产品。 |
| [productListOpens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | 可选 | 将创建新产品列表。 （例如，新购物车已创建。） |
| [productListRemoves](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | 强烈建议 | 产品从产品列表中删除。 |
| [productListReopens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | 可选 | 产品列表由用户重新激活。 这种情况经常发生在再营销活动。 |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | 强烈建议 | 查看列表产品。 |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | 强烈建议 | 产品视图。 请务必在中设置已查看的产品 `productListItems`。 |
| [购买](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | 强烈建议 | 接受命令。 必须具有产品列表。 |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | 可选 | 产品已保存以供将来使用。 |

以下是如何在SDK中设置这 `Measures` 些内容的示例。

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

商务对象还具有一个特殊字段，用于收集名为的订单详细信息 `order`。

| **订单** | **选项** | **推荐** | **描述** |
|---|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | 订 [单合计](https://en.wikipedia.org/wiki/ISO_4217) 的ISO 4217货币。 |
| [payments[paymentItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | 订单的付款列表。 paymentItem [包含](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) 以下各项。 |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | 可选 | 此支 [付方法的](https://en.wikipedia.org/wiki/ISO_4217) ISO 4217货币。 |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | 强烈建议 | 以指定的币种代码表示的付款值。 |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | 强烈建议 | 付款类型(例如， `credit_card`、 `gift_card`、 `paypal`)。 有关详细信息，请 [参阅已知值](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values) 的列表。 |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | 可选 | 此付款交易的唯一ID。 |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | 强烈建议 | 已应用所有折扣和税后此订单的合计。 |
| [purchaseID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseid) |  | 强烈推荐 | 卖家为此购买分配的唯一标识符。 |
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

## 列表产品

产品列表会指示与相应操作相关的产品。 它是productListItems [的列表](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md)。 每个产品都有许多可选字段。

| **字段** | **推荐** | **描述** |
|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | 可选 | 产 [品的ISO](https://en.wikipedia.org/wiki/ISO_4217) 4217货币。 仅当您可以拥有具有不同货币代码的产品并且产品适用时，此功能才有用。 例如，当有购买或添加到购物车时。 |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | 强烈建议 | 应仅在适用时进行设置。 例如，可能无法设置为开，因 `productView` 为不同的产品变体可能具有不同的价格，但是对于 `productListAdds`。 |
| [产品](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | 强烈建议 | 产品的XDM ID。 |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | 强烈建议 | 用于向列表添加产品项目的访客。 通过度 `productListAdds` 量进行设置，并且仅当将产品添加到列表时才应使用。 示例 `add to cart button`包括 `quick add`、和 `upsell`。 |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | 强烈建议 | 它设置为产品的显示名称或用户可读名称。 |
| [数量](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | 强烈建议 | 客户表示他们需要产品的套数。 应该设置 `productListAdds`、 `productListRemoves`、 `purchases`、 `saveForLaters`等等。 |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | 强烈建议 | 存储保持单元。 它是产品的唯一标识符。 |

## 示例

`productView` 事件

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

`productView` 事件

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

`checkout` 事件

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

`purchase` 事件

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
