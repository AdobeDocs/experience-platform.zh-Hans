---
title: 使用Adobe Experience Platform Web SDK收集商务和产品信息
description: 了解如何使用Adobe Experience Platform Web SDK添加与产品或购物车相关的数据。
keywords: products;commerce;measure;order;cartAndons；结帐；productListAdds;productListOpens;productListReopens;productListViews;productViews;purchases;saveForLaters;currencyCode;paymentAmount;paymentType;transactionIDpriceTotal;purchaseID;purchaseOrderNumber;
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
translation-type: tm+mt
source-git-commit: 7d7502b238f96eda1a15b622ba10bbccc289b725
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 6%

---

# 收集商务和产品信息

如果您的网站上有产品，则这是您可能希望发送的默认内容集，以启用Adobe中的最大功能。 尽管这是一个建议，但它提供了一套非常强大的开始数据。

此文档使用[ExperienceEvent商务详细信息](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md)模式字段组。 `commerce`字段组分为两部分：`commerce`对象和`productListItems`数组。 通过`commerce`对象，可以指示正在对`productListItems`数组执行哪些操作。

>[!TIP]
>
>如果您熟悉Adobe Analytics，则`commerce`与`events`变量最密切相关。 `productListItems`与`products`变量更加密切相关。

## 与产品相关的操作

以下是`commerce`对象中可用的`measures`列表。

>[!TIP]
>
>度量包含两个字段：`id`和`value`。 大多数情况下，您只使用`value`字段（例如`'value':1`）。 `id`字段允许您设置唯一标识符，用于跟踪发送度量的时间。 请参阅[Measure](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md)的XDM文档。

| **度量** | **推荐** | **描述** |
|---|---|---|
| [购物车放弃](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | 可选 | 购物车不再由用户访问或购买。 |
| [结帐](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | 强烈建议 | 用户不再浏览产品，但正在购买产品。 |
| [productListAdds](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | 强烈建议 | 产品已添加到列表。 请务必同时在`productListItems`中设置产品。 |
| [productListOpens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | 可选 | 将创建新产品列表。 （例如，新购物车已创建。） |
| [productListRemults](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | 强烈建议 | 产品从产品列表中删除。 |
| [productListReopens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | 可选 | 产品列表由用户重新激活。 这种情况经常发生在再营销活动。 |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | 强烈建议 | 查看产品列表。 |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | 强烈建议 | 产品视图。 请务必设置在`productListItems`中查看的产品。 |
| [购买](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | 强烈建议 | 接受命令。 必须具有产品列表。 |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | 可选 | 产品已保存以供将来使用。 |

下面是如何在SDK中设置这些`Measures`的示例。

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

商务对象还具有一个特殊字段，用于收集名为`order`的订单详细信息。

| **订单** | **选项** | **推荐** | **描述** |
|---|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | 订单合计的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币。 |
| [payments[paymentItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | 订单付款的列表。 [paymentItem](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema)包含以下内容。 |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | 可选 | 此付款方法的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币。 |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | 强烈建议 | 以指定的币种代码表示的付款值。 |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | 强烈建议 | 付款类型（例如，`credit_card`、`gift_card`、`paypal`）。 有关详细信息，请参阅[已知值](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values)的列表。 |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | 可选 | 此付款交易记录的唯一ID。 |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | 强烈建议 | 已应用所有折扣和税后此订单的合计。 |
| [purchaseID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseid) |  | 强烈推荐 | 卖家为此购买分配的唯一标识符。 |
| [purchaseOrderNumber](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseordernumber) |  | 可选 | 由购买者为此购买分配的唯一标识符。 |

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

产品列表会指示与相应操作相关的产品。 它是[productListItems](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md)的列表。 每个产品都有许多可选字段。

| **字段** | **推荐** | **描述** |
|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | 可选 | 产品的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币。 仅当您可以拥有具有不同货币代码的产品并且产品适用时，此功能才有用。 例如，当有购买或添加到购物车时。 |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | 强烈建议 | 应仅在适用时设置。 例如，可能无法在`productView`上设置，因为产品的不同变体可能具有不同的价格，但在`productListAdds`上设置。 |
| [product](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | 强烈建议 | 产品的XDM ID。 |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | 强烈建议 | 访客用于向列表添加产品项的方法。 设置为`productListAdds`度量，并且仅应在将产品添加到列表时使用。 示例包括 `add to cart button`、`quick add` 和 `upsell`。 |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | 强烈建议 | 设置为产品的显示名称或用户可读名称。 |
| [数量](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | 强烈建议 | 客户表示他们需要产品的套数。 应设置在`productListAdds`、`productListRemoves`、`purchases`、`saveForLaters`等上。 |
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
