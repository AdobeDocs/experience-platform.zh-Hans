---
title: 使用Adobe Experience Platform Web SDK收集商業和產品資訊
description: 瞭解如何使用Adobe Experience Platform Web SDK新增與產品或購物車相關的資料。
keywords: 產品；商務；測量；訂購；cartAbandons；結帳；productListAdds；productListOpens；productListRemovals；productListReopens；productListViews；productViews；購買；saveForLaters；currencyCode；付款；paymentAmount；paymentType；transactionID；priceTotal；purceID；purceOrderNumber；
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: 51a18ca3a9d0817eafeecea328900eb2f4d1d9a4
workflow-type: tm+mt
source-wordcount: '1326'
ht-degree: 6%

---

# 收集商業和產品資訊

如果您的網站上有產品，則這是您可能想要傳送以啟用Adobe中大部分功能的預設專案集。 雖然這是建議，但它從一開始就提供一組非常強大的資料。

本檔案使用 [ExperienceEvent商務詳細資料](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) 結構描述欄位群組。 此 `commerce` 欄位群組分為兩個部分： `commerce` 物件與 `productListItems` 陣列。 此 `commerce` 物件可讓您指出哪些動作正在發生 `productListItems` 陣列。

>[!TIP]
>
>如果您熟悉Adobe Analytics，請參閱 `commerce` 與以下專案關係最密切： `events` 變數。 此 `productListItems` 與 `products` 變數。

## 與產品相關的動作

以下是以下清單 `measures` 可在 `commerce` 物件。

>[!TIP]
>
>測量有兩個欄位： `id` 和 `value`. 大部分時間，您會使用 `value` 僅限欄位(例如， `'value':1`)。 此 `id` 欄位可讓您設定唯一識別碼，以便用於追蹤測量傳送的時間。 請參閱XDM檔案以瞭解 [測量](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md).

| **測量** | **推荐** | **描述** |
|---|---|---|
| [cartAbandons](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | 可选 | 使用者無法再存取或購買購物車。 |
| [結帳](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | 强烈建议 | 使用者不再瀏覽產品，而是正在購買產品。 |
| [productListAdds](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | 强烈建议 | 產品會新增至清單。 請務必在 `productListItems` 同時。 |
| [productListOpens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | 可选 | 已建立新的產品清單。 （例如，建立新的購物車。） |
| [productListRemovals](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | 强烈建议 | 產品會從產品清單中移除。 |
| [productListReopens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | 可选 | 使用者會重新啟用產品清單。 這通常發生在再行銷活動中。 |
| [productListView](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | 强烈建议 | 已檢視產品清單。 |
| [產品檢視](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | 强烈建议 | 產品檢視。 請務必設定在中檢視的產品 `productListItems`. |
| [購買](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | 强烈建议 | 已接受訂單。 必須有產品清單。 |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | 可选 | 儲存產品以供日後使用。 |

以下是如何設定這些專案的範例 `Measures` （在SDK中）。

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

商務物件也有收集訂單詳細資料的特殊欄位，稱為 `order`.

| **訂購** | **Option** | **推荐** | **描述** |
|---|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | 此 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 訂單總計的貨幣。 |
| [payments[paymentItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | 訂單上的付款清單。 A [paymentItem](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) 包含下列專案。 |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | 可选 | 此 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 此付款方式的貨幣。 |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | 强烈建议 | 以指定貨幣代碼表示的付款值。 |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | 强烈建议 | 付款型別(例如： `credit_card`， `gift_card`， `paypal`)。 檢視清單 [已知值](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values) 以取得詳細資訊。 |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | 可选 | 此付款交易的唯一識別碼。 |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | 强烈建议 | 此訂單套用所有折扣和稅金後的總計。 |
| [purchaseID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseid) |  | 強烈建議 | 賣家為此購買所指派的唯一識別碼。 |
| [purchaseOrderNumber](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseordernumber) |  | 可选 | 購買者為此購買所指派的唯一識別碼。 |

以下是SDK中典型購買的範例。

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

## 產品清單

產品清單會指出哪些產品與對應動作相關。 此清單包含 [productListItems](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md). 每個產品都有許多選用欄位。

| **字段** | **推荐** | **描述** |
|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | 可选 | 此 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 產品的貨幣。 只有在您可以擁有具有不同貨幣代碼的產品且套用時，此功能才有用。 例如，當有購買或加入購物車時。 |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | 强烈建议 | 應僅在適用時設定。 例如，可能無法將設定在 `productView` 事件，因為不同產品變數可能會有不同的價格，但 `productListAdds` 事件。 |
| [product](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | 强烈建议 | 產品的XDM ID。 |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | 强烈建议 | 訪客用來將產品專案新增至清單的方法。 設定方式 `productListAdds` 測量，且只應在將產品新增至清單時使用。 示例包括 `add to cart button`、`quick add` 和 `upsell`。 |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | 强烈建议 | 這會設定為產品的顯示名稱或人類看得懂的名稱。 |
| [數量](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | 强烈建议 | 客戶表示所需的產品單位數。 應設定於 `productListAdds`， `productListRemoves`， `purchases`， `saveForLaters`、等等。 |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | 强烈建议 | 存放區維護單位。 這是產品的唯一識別碼。 |

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
