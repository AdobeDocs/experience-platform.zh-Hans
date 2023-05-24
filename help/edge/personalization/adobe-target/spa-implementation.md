---
title: Adobe Experience Platform Web SDK的單頁應用程式實作
description: 瞭解如何使用Adobe Target建立Adobe Experience Platform Web SDK的單頁應用程式(SPA)實作。
keywords: target；adobe target；xdm檢視；檢視；單頁應用程式；SPA；SPA生命週期；使用者端；AB測試；AB；體驗鎖定目標；XT；VEC
exl-id: cc48c375-36b9-433e-b45f-60e6c6ea4883
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 13%

---

# 實作單頁應用程式

Adobe Experience Platform Web SDK提供豐富的功能，讓貴公司能以新世代使用者端技術(例如單頁應用程式(SPA))為基礎進行個人化。

传统网站使用的是“页面到页面”导航模型，也称为多页应用程序，其中网站设计与 URL 紧密耦合，并且从一个网页转换到另一个网页时，需要页面加载。

現代Web應用程式（例如單頁應用程式）已改為採用可加快瀏覽器UI呈現的使用的模型，這通常與頁面重新載入無關。 這些體驗可由客戶互動觸發，例如捲動、點按和游標移動。 隨著現代網路範例的不斷發展，傳統的一般事件（例如頁面載入）與部署個人化和實驗不再具有相關性。

![](assets/spa-vs-traditional-lifecycle.png)

## 適用於SPA的Platform Web SDK的優點

以下是為單頁應用程式使用Adobe Experience Platform Web SDK的一些優點：

* 能够在页面加载时缓存所有选件，将多次服务器调用减少至一次服务器调用。
* 大幅改善網站上的使用者體驗，因為選件可透過快取立即顯示，而不會因傳統伺服器呼叫而延遲。
* 只要一行程式碼和一次性的開發人員設定，行銷人員就能在SPA上透過視覺化體驗撰寫器(VEC)建立及執行A/B和體驗鎖定目標(XT)活動。

## XDM檢視和單頁應用程式

適用於SPA的Adobe Target VEC充分利用稱為「檢視」的概念：視覺化元素的邏輯群組，共同構成SPA體驗。 因此，單頁應用程式可視為根據使用者互動轉換檢視，而不是URL。 “视图”通常可显示整个站点或某个站点中分组的可视化元素。

為了進一步說明什麼是檢視，以下範例使用在React中實作的假想線上電子商務網站來探索範例檢視。

導覽至首頁後，主圖影像會宣傳復活節特賣以及網站上提供的最新產品。 在這種情況下，可以為整個主畫面定義檢視。 此檢視可以簡單地稱為「home」。

![](assets/example-views.png)

當客戶對業務所銷售的產品越來越感興趣時，他們決定按一下 **產品** 連結。 与主页网站类似，可将整个产品站点定义为一个“视图”。此檢視可命名為「products-all」。

![](assets/example-products-all.png)

由於檢視可定義為整個網站或網站上的一組視覺元素，因此產品網站上顯示的四個產品可分組並視為檢視。 此檢視可命名為「products」。

![](assets/example-products.png)

當客戶決定按一下 **載入更多** 按鈕瀏覽網站上的更多產品，在此情況下，網站URL不會變更，但可在此處建立檢視，以僅代表顯示的第二列產品。 檢視名稱可以是&quot;products-page-2&quot;。

![](assets/example-load-more.png)

客戶決定從網站購買一些產品，然後進入結帳畫面。 在結帳地點上，客戶可以選擇正常交貨或快速交貨。 檢視可以是網站上的任何一組視覺元素，因此可以為傳遞偏好設定建立檢視，並將其稱為「傳遞偏好設定」。

![](assets/example-check-out.png)

檢視的概念可以進一步延伸。 以下只是可在網站上定義的一些檢視範例。

## 實作XDM檢視

在Adobe Target中可運用XDM檢視，讓行銷人員透過視覺化體驗撰寫器在SPA上執行A/B和XT測試。 若要完成一次性開發人員設定，需要執行下列步驟：

1. 安裝 [Adobe Experience Platform Web SDK](../../fundamentals/installing-the-sdk.md)
2. 決定您要個人化的單頁應用程式中的所有XDM檢視。
3. 定義XDM檢視後，為了傳送AB或XT VEC活動，請實作 `sendEvent()` 函式為 `renderDecisions` 設定為 `true` 以及單頁應用程式中對應的XDM檢視。 XDM檢視必須傳入 `xdm.web.webPageDetails.viewName`. 此步驟可讓行銷人員運用視覺化體驗撰寫器，針對這些XDM啟動A/B和XT測試。

   ```javascript
   alloy("sendEvent", { 
     "renderDecisions": true, 
     "xdm": { 
       "web": { 
         "webPageDetails": { 
         "viewName":"home" 
         }
       } 
     } 
   });
   ```

>[!NOTE]
>
>在第一個 `sendEvent()` 呼叫，將會擷取並快取應呈現給使用者的所有XDM檢視。 後續 `sendEvent()` 含有傳入的XDM檢視的呼叫將會從快取中讀取並轉譯，而不需要伺服器呼叫。

## `sendEvent()` 函式範例

本節概述三個範例，說明如何叫用 `sendEvent()` 函式於React中，適用於假定的電子商務SPA。

### 範例1：A/B測試首頁

行銷團隊想要在整個首頁上執行A/B測試。

![](assets/use-case-1.png)

若要在整個主網站上執行A/B測試， `sendEvent()` 必須透過XDM叫用 `viewName` 設定為 `home`：

```jsx
function onViewChange() { 
  
  var viewName = window.location.hash; // or use window.location.pathName if router works on path and not hash 

  viewName = viewName || 'home'; // view name cannot be empty 

  // Sanitize viewName to get rid of any trailing symbols derived from URL 

  if (viewName.startsWith('#') || viewName.startsWith('/')) { 
    viewName = viewName.substr(1); 
  }
   
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName":"home" 
        } 
      } 
    }
  }); 
} 

// react router v4 

const history = syncHistoryWithStore(createBrowserHistory(), store); 

history.listen(onViewChange); 

// react router v3 

<Router history={hashHistory} onUpdate={onViewChange} > 
```

### 範例2：個人化產品

行銷團隊想要在使用者點按後，將價格標籤顏色變更為紅色，以個人化第二列產品 **載入更多**.

![](assets/use-case-2.png)

```jsx
function onViewChange(viewName) { 

  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName
        }
      } 
    } 
  }); 
} 

class Products extends Component { 
  
  render() { 
    return ( 
      <button type="button" onClick={this.handleLoadMoreClicked}>Load more</button> 
    ); 
  } 

  handleLoadMoreClicked() { 
    var page = this.state.page + 1; // assuming page number is derived from component’s state 
    this.setState({page: page}); 
    onViewChange('PRODUCTS-PAGE-' + page); 
  } 

} 
```

### 範例3：A/B測試傳遞偏好設定

行銷團隊想要執行A/B測試，以檢視按鈕的顏色何時從藍色變更為紅色 **快遞** 選取可以提高轉換率（與讓兩個傳送選項的按鈕顏色保持藍色相反）。

![](assets/use-case-3.png)

若要根據選取的傳送偏好設定個人化網站內容，可針對每個傳送偏好設定建立檢視。 時間 **正常傳遞** ，則可將檢視命名為「checkout-normal」。 若 **快遞** ，則可將檢視命名為「checkout-express」。

```jsx
function onViewChange(viewName) { 
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName 
        }
      }
    }
  }); 
} 

class Checkout extends Component { 

  render() { 
    return ( 
      <div onChange={this.onDeliveryPreferenceChanged}> 
        <label> 
          <input type="radio" id="normal" name="deliveryPreference" value={"Normal Delivery"} defaultChecked={true}/> 
          <span> Normal Delivery (7-10 business days)</span> 
        </label> 
        <label> 
          <input type="radio" id="express" name="deliveryPreference" value={"Express Delivery"}/> 
          <span> Express Delivery* (2-3 business days)</span> 
        </label> 
      </div> 
    ); 
  } 

  onDeliveryPreferenceChanged(evt) { 
    var selectedPreferenceValue = evt.target.value; 
    onViewChange(selectedPreferenceValue); 
  } 

} 
```

## 使用SPA的視覺化體驗撰寫器

當您完成定義XDM檢視並實作時 `sendEvent()` 傳入這些XDM檢視後，VEC將能夠偵測這些檢視，並允許使用者建立A/B或XT活動的動作和修改。

>[!NOTE]
>
>若要將VEC用於您的SPA，您必須安裝並啟動 [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) 或 [鉻黃](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper擴充功能。

### “修改”面板

「修改」面板會擷取為特定檢視建立的動作。 「檢視」的所有動作會分組在「該檢視」下。

![](assets/modifications-panel.png)

### 操作

单击某个操作会突出显示将应用此操作的网站上的元素。在檢視下建立的每個VEC動作都有下列圖示： **資訊**， **編輯**， **原地複製**， **移動**、和 **刪除**. 下表會詳細說明這些圖示。

![](assets/action-icons.png)

| 图标 | 描述 |
|---|---|
| 信息 | 显示操作的详细信息。 |
| Edit | 允许您直接编辑操作的属性。 |
| 克隆 | 将操作克隆到位于“修改”面板上的一个或多个视图，或者您在 VEC 中浏览并导航到的一个或多个视图。该操作不一定存在于“修改”面板中。<br/><br/>**注意：** 執行原地復製作業後，您必須透過瀏覽導覽至VEC中的檢視，才能檢視該原地複製動作的作業是否有效。 如果该操作未应用到视图，您将看到一个错误。 |
| 移动 | 将操作移动到“页面加载事件”或修改面板中已存在的任何其他视图。<br/><br/>**頁面載入事件：** 任何對應至頁面載入事件的動作，都會套用到網頁應用程式的初始頁面載入上。 <br/><br/>**注意：** 執行移動作業後，您必須透過瀏覽導覽至VEC中的檢視，才能檢視該移動作業是否有效。 如果该操作未应用到视图，您将看到一个错误。 |
| Delete | 删除操作。 |

## 使用VEC進行SPA範例

本節概述三個使用視覺化體驗撰寫器建立A/B或XT活動之動作和修改的範例。

### 範例1：更新「首頁」檢視

在此檔案的先前部分，已針對整個首頁網站定義名為「home」的檢視。 現在，行銷團隊想要以下列方式更新「首頁」檢視：

* 變更 **加入購物車** 和 **按讚** 按鈕變淺為藍色。 這應在頁面載入期間發生，因為它涉及變更標頭的元件。
* 變更 **2019年最新產品** 標籤至 **2019年最暢銷產品** 並將文字顏色變更為紫色。

若要在VEC中進行這些更新，請選取 **撰寫** 並將這些變更套用至「首頁」檢視。

![](assets/vec-home.png)

### 範例2：變更產品標籤

針對「products-page-2」檢視，行銷團隊想要變更 **價格** 標籤至 **售價** 並將標籤顏色變更為紅色。

若要在VEC中進行這些更新，需執行下列步驟：

1. 選取 **瀏覽** 在VEC中。
2. 選取 **產品** 在網站頂端導覽列中。
3. 選取 **載入更多** 一次，即可檢視產品的第二列。
4. 選取 **撰寫** 在VEC中。
5. 套用動作以將文字標籤變更為 **售價** 和顏色變成紅色。

![](assets/vec-products-page-2.png)

### 範例3：個人化傳遞偏好設定樣式

檢視可以在精細層次進行定義，例如單選按鈕的狀態或選項。 在本檔案的前面部分，已針對傳遞偏好設定「checkout-normal」和「checkout-express」定義檢視。 行銷團隊想要將「checkout-express」檢視的按鈕顏色變更為紅色。

若要在VEC中進行這些更新，需執行下列步驟：

1. 選取 **瀏覽** 在VEC中。
2. 將產品新增至網站上的購物車。
3. 選取網站右上角的購物車圖示。
4. 選取 **結帳訂單**.
5. 選取 **快遞** 下的選項按鈕 **傳遞偏好設定**.
6. 選取 **撰寫** 在VEC中。
7. 變更 **付款** 按鈕顏色變成紅色。

>[!NOTE]
>
>「checkout-express」檢視要等到 **快遞** 選項按鈕已選取。 這是因為 `sendEvent()` 函式執行時機 **快遞** 選項按鈕已選取，因此，在選取選項按鈕之前，VEC不會察覺「checkout-express」檢視。

![](assets/vec-delivery-preference.png)
