---
title: 使用Adobe Experience Platform Web SDK收集商务、产品和订单信息
description: 了解如何使用Adobe Experience Platform Web SDK添加与产品或购物车相关的数据。
source-git-commit: cb47f70fe75eb0dfe26fb3c3557658cf6cff5a17
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 2%

---


# 收集商业、产品和订单信息

如果贵组织销售产品或服务，则可以使用此页面作为如何跟踪这些产品和服务的指南。

此页面使用XDM [商业架构](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md) 字段组。

此字段组包含两个主要部分：

* 此 `commerce` 对象。 此对象允许您指示对 `productListItems` 数组。
* 此 `productListItems` 数组。

>[!TIP]
>
>如果您熟悉Adobe Analytics，请参阅 `commerce` 对象包含的数据与中的商务事件类似 `events` 变量。 此 `productListItems` 对象数组包含的数据与 `products` 变量。

## 此 `commerce` 对象 {#commerce-object}

此部分介绍 `commerce` 对象。

>[!TIP]
>
>度量值包含两个字段： `id` 和 `value`. 大多数情况下，您仅使用 `value` 字段(例如， `'value':1`)。 此 `id` 字段允许您设置唯一标识符以在发送度量值时进行跟踪。 请参阅XDM文档，了解 [衡量](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/measure.schema.md) 以了解更多信息。

| 衡量 | 推荐 | 描述 |
|---|---|---|
| [`cartAbandons`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcartabandons) | 可选 | 用户无法再访问或购买购物车。 |
| [`checkouts`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcheckouts) | 强烈建议 | 用户不再浏览产品，而是正在购买产品。 |
| [`productListAdds`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistadds) | 强烈建议 | 将产品添加到列表。 请确保将产品设置为 `productListItems` 同时。 |
| [`productListOpens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistopens) | 可选 | 将创建新的产品列表。 例如，创建一个新的购物车。 |
| [`productListRemovals`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistremovals) | 强烈建议 | 从产品列表中删除产品。 |
| [`productListReopens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistreopens) | 可选 | 用户重新激活产品列表。 此操作通常发生在再营销活动中。 |
| [`productListViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistviews) | 强烈建议 | 将查看产品列表。 |
| [`productViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductviews) | 强烈建议 | 产品视图发生了。 请务必设置在中查看的产品 `productListItems`. |
| [`purchases`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmpurchases) | 强烈建议 | 接受订单。 必须具有产品列表。 |
| [`saveForLaters`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmsaveforlaters) | 可选 | 保存产品以供将来使用。 |

{style="table-layout:auto"}

### `Commerce` 对象示例

展开以下部分，查看使用 `commerce` 对象。

+++`productViews`

基本Web SDK `sendEvent` 呼叫设置 `productViews` 字段至 `1`：

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

+++

## 此 `order` 对象 {#order-object}

此 `commerce` 对象包含用于收集订单详细信息的专用对象。 这称为 `order` 对象。

本节介绍 `order` 对象。

| 字段 | 选项 | 推荐 | 描述 |
|---|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmcurrencycode) |  |  | 此 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 订单总计的货币。 |
| [`payments[]`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpayments) |  |  | 订单上的付款清单。 A [paymentitem](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md) 包括以下内容。 |
|  | [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmcurrencycode) | 可选 | 此 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 此付款方式的币种。 |
|  | [`paymentAmount`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymentamount) | 强烈建议 | 以指定的货币代码表示的付款值。 |
|  | [`paymentType`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype) | 强烈建议 | 付款类型(例如， `credit_card`， `gift_card`， `paypal`)。 查看列表 [已知值](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype-known-values) 以了解详细信息。 |
|  | [`transactionID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmtransactionid) | 可选 | 此付款交易的唯一ID。 |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpricetotal) |  | 强烈建议 | 应用所有折扣和税费后此订单的总额。 |
| [`purchaseID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseid) |  | 强烈建议 | 卖方为此购买分配的唯一标识符。 |
| [`purchaseOrderNumber`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseordernumber) |  | 可选 | 购买者为此购买分配的唯一标识符。 |

### 排序对象示例

展开以下部分，查看使用的Web SDK命令示例。 `commerce` 对象。

+++`Order` 对象示例

Web SDK `sendEvent` 呼叫设置 `order` 应用于中多个产品的对象 `productListItems` 数组：

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

+++

## 产品列表对象 {#product-list-object}

产品列表会指示哪些产品与相应的操作相关。 它是一个 [productListItems](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md). 每个产品都有几个可选字段。

| 字段 | 推荐 | 描述 |
|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmcurrencycode) | 可选 | 此 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 产品的货币。 通常情况下，仅当产品列表中存在多个使用不同货币代码的产品时，此字段适用。 |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmpricetotal) | 强烈建议 | 仅在适用的情况下设置此字段。 例如，可能无法将设置为 `productView` 事件，因为产品不同的变体可能具有不同的价格，但 `productListAdds` 事件。 |
| [`product`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproduct) | 强烈建议 | 产品的XDM ID。 |
| [`productAddMethod`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproductaddmethod) | 强烈建议 | 访客用来将产品项目添加到列表的方法。 设置方式 `productListAdds` 度量并且仅在将产品添加到列表时使用。 示例包括 `add to cart button`、`quick add` 和 `upsell`。 |
| [`productName`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmname) | 强烈建议 | 产品的显示名称或易于用户识别的名称。 |
| [`quantity`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmquantity) | 强烈建议 | 客户表明的产品需求单位数。 应设置为 `productListAdds`， `productListRemoves`， `purchases`， `saveForLaters`，等等。 |
| [`SKU`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmsku) | 强烈建议 | 商店保管单位。 它是产品的唯一标识符。 |

### 产品列表示例

展开以下部分，查看使用的Web SDK命令示例 `productListItems` 对象。

+++`productListItems` 示例

Web SDK `sendEvent` 呼叫设置 `productViews` （对于中的多个产品） `productListItems` 数组：

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

+++

+++`productListAdds` 示例

Web SDK `sendEvent` 呼叫设置 `productListAdds` 中的多个产品的事件 `productListItems` 数组：

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

+++

+++`checkouts` 示例

Web SDK `sendEvent` 呼叫设置 `checkouts` 中的多个产品的事件 `productListItems` 数组：

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

+++
