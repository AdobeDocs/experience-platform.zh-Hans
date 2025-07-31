---
title: 使用Adobe Experience Platform Web SDK收集商务、产品和订单信息
description: 了解如何使用Adobe Experience Platform Web SDK添加与产品或购物车相关的数据。
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 2%

---

# 收集商业、产品和订单信息

如果贵组织销售产品或服务，则可以使用此页面作为如何跟踪这些产品和服务的指南。

此页使用XDM [Commerce架构](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md)字段组。

此字段组包含两个主要部分：

* `commerce`对象。 此对象允许您指示`productListItems`数组发生了哪些操作。
* `productListItems`数组。

>[!TIP]
>
>如果您熟悉Adobe Analytics，`commerce`对象在`events`变量中包含与商业事件类似的数据。 `productListItems`对象数组包含的数据与`products`变量类似。

## `commerce`对象 {#commerce-object}

本节介绍`commerce`对象中可用的字段。

>[!TIP]
>
>度量值有两个字段：`id`和`value`。 大多数情况下，您只使用`value`字段（例如，`'value':1`）。 `id`字段允许您在发送度量值时设置用于跟踪的唯一标识符。 有关详细信息，请参阅[度量值](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/measure.schema.md)的XDM文档。

| 测量 | 推荐 | 描述 |
|---|---|---|
| [`cartAbandons`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcartabandons) | 可选 | 用户无法再访问或购买购物车。 |
| [`checkouts`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcheckouts) | 强烈建议 | 用户不再浏览产品，而是正在购买产品。 |
| [`productListAdds`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistadds) | 强烈建议 | 将产品添加到列表。 请确保同时在`productListItems`中设置该产品。 |
| [`productListOpens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistopens) | 可选 | 将创建新的产品列表。 例如，创建一个新的购物车。 |
| [`productListRemovals`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistremovals) | 强烈建议 | 从产品列表中删除产品。 |
| [`productListReopens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistreopens) | 可选 | 用户重新激活产品列表。 此操作通常发生在再营销活动中。 |
| [`productListViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistviews) | 强烈建议 | 将查看产品列表。 |
| [`productViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductviews) | 强烈建议 | 产品视图发生了。 请确保设置在`productListItems`中查看的产品。 |
| [`purchases`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmpurchases) | 强烈建议 | 接受订单。 必须具有产品列表。 |
| [`saveForLaters`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmsaveforlaters) | 可选 | 保存产品以供将来使用。 |

{style="table-layout:auto"}

### `Commerce`对象示例

展开以下部分以查看使用`commerce`对象中的字段的Web SDK命令示例。

+++`productViews`

将`sendEvent`字段设置为`productViews`的基本Web SDK `1`调用：

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

## `order`对象 {#order-object}

`commerce`对象包含用于收集订单详细信息的专用对象。 这称为`order`对象。

本节介绍`order`对象支持的所有字段。

| 字段 | 选项 | 推荐 | 描述 |
|---|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmcurrencycode) |  |  | 订单总额的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币。 |
| [`payments[]`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpayments) |  |  | 订单上的付款清单。 [paymentItem](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md)包含以下内容。 |
|  | [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmcurrencycode) | 可选 | 此付款方式的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币。 |
|  | [`paymentAmount`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymentamount) | 强烈建议 | 以指定的货币代码表示的付款值。 |
|  | [`paymentType`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype) | 强烈建议 | 付款类型（例如，`credit_card`、`gift_card`、`paypal`）。 有关详细信息，请参阅[已知值](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype-known-values)的列表。 |
|  | [`transactionID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmtransactionid) | 可选 | 此付款交易的唯一ID。 |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpricetotal) |  | 强烈建议 | 应用所有折扣和税费后此订单的总额。 |
| [`purchaseID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseid) |  | 强烈建议 | 卖方为此购买分配的唯一标识符。 |
| [`purchaseOrderNumber`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseordernumber) |  | 可选 | 购买者为此购买分配的唯一标识符。 |

### 排序对象示例

展开以下部分以查看使用`commerce`对象的Web SDK命令的示例。

+++`Order`对象示例

Web SDK `sendEvent`调用设置适用于`order`数组中的多个产品的`productListItems`对象：

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

产品列表会指示哪些产品与相应的操作相关。 它是[productListItems](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md)的列表。 每个产品都有几个可选字段。

| 字段 | 推荐 | 描述 |
|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmcurrencycode) | 可选 | 产品的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币。 通常情况下，仅当产品列表中存在多个使用不同货币代码的产品时，此字段适用。 |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmpricetotal) | 强烈建议 | 仅在适用的情况下设置此字段。 例如，可能无法在`productView`事件上设置，因为产品的不同变体可能具有不同的价格，但在`productListAdds`事件上却可能不同。 |
| [`product`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproduct) | 强烈建议 | 产品的XDM ID。 |
| [`productAddMethod`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproductaddmethod) | 强烈建议 | 访客用来将产品项目添加到列表的方法。 通过`productListAdds`度量设置，并且仅在将产品添加到列表时使用。 示例包括`add to cart button`、`quick add`和`upsell`。 |
| [`productName`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmname) | 强烈建议 | 产品的显示名称或易于用户识别的名称。 |
| [`quantity`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmquantity) | 强烈建议 | 客户表明的产品需求单位数。 应在`productListAdds`、`productListRemoves`、`purchases`、`saveForLaters`等上设置。 |
| [`SKU`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmsku) | 强烈建议 | 商店保管单位。 它是产品的唯一标识符。 |

### 产品列表示例

展开以下部分以查看使用`productListItems`对象的Web SDK命令示例。

+++`productListItems`示例

Web SDK `sendEvent`调用为`productViews`数组中的多个产品设置`productListItems`：

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

+++`productListAdds`示例

Web SDK `sendEvent`调用为`productListAdds`数组中的多个产品设置`productListItems`事件：

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

+++`checkouts`示例

Web SDK `sendEvent`调用为`checkouts`数组中的多个产品设置`productListItems`事件：

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
