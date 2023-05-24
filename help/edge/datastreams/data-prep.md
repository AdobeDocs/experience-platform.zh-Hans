---
title: 为数据收集准备数据
description: 瞭解在為Adobe Experience Platform Web和Mobile SDK設定資料流時，如何將您的資料對應到Experience Data Model (XDM)事件結構。
exl-id: 87a70d56-1093-445c-97a5-b8fa72a28ad0
source-git-commit: 3ab02646968222c0ad09c1d8ce8fda04de7aaac6
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 2%

---

# 为数据收集准备数据

「資料準備」是一項Adobe Experience Platform服務，可讓您對應、轉換及驗證來往資料 [體驗資料模型(XDM)](../../xdm/home.md). 設定啟用平台時 [資料串流](./overview.md)，則可在將來源資料傳送至Platform Edge Network時，使用「資料準備」功能將其對應至XDM。

>[!NOTE]
>
>如需所有「資料準備」功能的全面指引，包括計算欄位的轉換函式，請參閱下列檔案：
>
>* [資料準備總覽](../../data-prep/home.md)
>* [資料準備對應函式](../../data-prep/functions.md)
>* [使用「資料準備」處理資料格式](../../data-prep/data-handling.md)


本指南說明如何在UI中對應資料。 若要隨著步驟進行，請開始建立資料流的程式，直到（並包括） [基本設定步驟](./overview.md#create).

如需資料收集程式資料準備的快速示範，請參閱下列影片：

>[!VIDEO](https://video.tv.adobe.com/v/342120?quality=12&enable10seconds=on&speedcontrol=on)

## [!UICONTROL 选择数据] {#select-data}

選取 **[!UICONTROL 儲存並新增對應]** 完成資料串流的基本設定後，以及 **[!UICONTROL 選取資料]** 步驟隨即顯示。 從這裡，您必須提供範例JSON物件，代表您計畫傳送至Platform的資料結構。

若要直接從資料層擷取屬性，JSON物件必須具有單一根屬性 `data`. 的子屬性 `data` 物件之後應該以對應至您要擷取的資料層屬性的方式建構。 選取以下區段，檢視格式正確的JSON物件範例(包含 `data` 根。

+++範例JSON檔案，使用 `data` 根

```json
{
  "data": {
    "eventMergeId": "cce1b53c-571f-4f36-b3c1-153d85be6602",
    "eventType": "view:load",
    "timestamp": "2021-09-30T14:50:09.604Z",
    "web": {
      "webPageDetails": {
        "siteSection": "Product section",
        "server": "example.com",
        "name": "product home",
        "URL": "https://www.example.com"
      },
      "webReferrer": {
        "URL": "https://www.adobe.com/index2.html",
        "type": "external"
      }
    },
    "commerce": {
      "purchase": 1,
      "order": {
        "orderID": "1234"
      }
    },
    "product": [
      {
        "productInfo": {
          "productID": "123"
        }
      },
      {
        "productInfo": {
          "productID": "1234"
        }
      }
    ],
    "reservation": {
      "id": "anc45123xlm",
      "name": "Embassy Suits",
      "SKU": "12345-L",
      "skuVariant": "12345-LG-R",
      "priceTotal": "112.99",
      "currencyCode": "USD",
      "adults": 2,
      "children": 3,
      "productAddMethod": "PDP",
      "_namespace": {
        "test": 1,
        "priceTotal": "112.99",
        "category": "Overnight Stay"
      },
      "freeCancellation": false,
      "cancellationFee": 20,
      "refundable": true
    }
  }
}
```

+++

若要從XDM物件資料元素擷取屬性，相同的規則會套用至JSON物件，但根屬性必須輸入為 `xdm` 而非。 選取以下區段，檢視格式正確的JSON物件範例，其中包含 `xdm` 根。

+++範例JSON檔案，使用 `xdm` 根

```json
{
  "xdm": {
    "environment": {
      "type": "browser",
      "browserDetails": {
        "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_5) AppleWebkit/537.36 (KHTML, like Gecko) Chrome/49.0.2623.112 Safari/537.36",
        "javaScriptEnabled": true,
        "javaScriptVersion": "1.8.5",
        "cookiesEnabled": true,
        "viewportHeight": 900,
        "viewportWidth": 1680,
        "javaEnabled": true
      },
      "domain": "adobe.com",
      "colorDepth": 24,
      "viewportHeight": 1050,
      "viewportWidth": 1680
    },
    "device": {
      "screenHeight": 1050,
      "screenWidth": 1680
    }
  }
}
```

+++

您可以選取將物件上傳為檔案的選項，或將原始物件貼到提供的文字方塊中。 如果JSON有效，右側面板中會顯示預覽結構描述。 选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![預期傳入資料的JSON範例](../assets/datastreams/data-prep/select-data.png)

## [!UICONTROL 映射]

此 **[!UICONTROL 對應]** 步驟隨即顯示，可讓您將來源資料中的欄位對應到Platform中目標事件結構描述的欄位。 從這裡，您可以透過兩種方式設定對應：

* [建立新的對應規則](#create-mapping) 流執行手動程式時，才會使用此資料。
* [匯入對應規則](#import-mapping) 從現有資料串流。

### 建立新對應 {#create-mapping}

若要開始使用，請選取 **[!UICONTROL 新增對應]** 以建立新的對應列。

![新增對應](../assets/datastreams/data-prep/add-new-mapping.png)

選取來源圖示(![來源圖示](../assets/datastreams/data-prep/source-icon.png))，然後在出現的對話方塊中，選取您要在提供的畫布中對應的來源欄位。 選擇欄位後，請使用 **[!UICONTROL 選取]** 按鈕以繼續。

![選取要在來源結構描述中對應的欄位](../assets/datastreams/data-prep/source-mapping.png)

接下來，選取結構描述圖示(![結構描述圖示](../assets/datastreams/data-prep/schema-icon.png))以開啟目標事件結構描述的類似對話方塊。 在確認之前，選擇您要對應資料的欄位 **[!UICONTROL 選取]**.

![選取要在目標結構描述中對應的欄位](../assets/datastreams/data-prep/target-mapping.png)

對應頁面會重新出現，並顯示已完成的欄位對應。 此 **[!UICONTROL 對應進度]** 區段更新以反映已成功對應的欄位總數。

![欄位已成功對應，並反映進度](../assets/datastreams/data-prep/field-mapped.png)

>[!TIP]
>
>如果您想要將物件陣列（在來源欄位中）對應至不同物件陣列（在目標欄位中），請新增 `[*]` 在來源和目的地欄位路徑中的陣列名稱之後，如下所示。
>
>![陣列物件對應](../assets/datastreams/data-prep/array-object-mapping.png)

### 匯入現有的對應規則 {#import-mapping}

如果您先前已建立資料流，您可以針對新資料流重複使用其已設定的對應規則。

>[!WARNING]
>
>從其他資料流匯入對應規則將會覆寫您在匯入之前可能已新增的任何欄位對應。

若要開始，請選取 **[!UICONTROL 匯入對應]**.

![影像顯示 [!UICONTROL 匯入對應] 正在選取按鈕](../assets/datastreams/data-prep/import-mapping-button.png)

在出現的對話方塊中，選取您要匯入其對應規則的資料流。 選擇資料流後，選取 **[!UICONTROL 預覽]**.

![顯示正在選取的現有資料串流的影像](../assets/datastreams/data-prep/select-mapping-rules.png)

>[!NOTE]
>
>資料串流只能匯入相同內 [沙箱](../../sandboxes/home.md). 換言之，您無法將資料串流從一個沙箱匯入另一個沙箱。

下一個畫面會顯示所選資料串流的已儲存對應規則預覽。 確認顯示的對應符合您的預期，然後選取 **[!UICONTROL 匯入]** 以確認並將對應新增至新資料流。

![顯示要匯入之對應規則的影像](../assets/datastreams/data-prep/import-mapping-rules.png)

>[!NOTE]
>
>如果匯入的對應規則中有任何來源欄位未包含在您指定的JSON範例資料中 [先前提供](#select-data)，這些欄位對應將不會包含在匯入中。

### 完成對應

繼續上述步驟，將其餘欄位對應至目標結構描述。 雖然您不必對應所有可用的來源欄位，但是目標結構描述中設定為必要的任何欄位都必須對應，才能完成此步驟。 此 **[!UICONTROL 必填欄位]** counter指出目前設定中尚未對應多少必要欄位。

必填欄位計數達到零且對對應滿意後，請選擇 **[!UICONTROL 儲存]** 以完成變更。

![對應完成](../assets/datastreams/data-prep/mapping-complete.png)

## 后续步骤

本指南說明在UI中設定資料流時，如何將資料對應至XDM。 如果您正在遵循一般資料串流教學課程，您現在可以回到上的步驟 [檢視資料流詳細資料](./overview.md).
