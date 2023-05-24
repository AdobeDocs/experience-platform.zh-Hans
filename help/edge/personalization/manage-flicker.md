---
title: 使用Adobe Experience Platform Web SDK管理個人化體驗的閃爍
description: 瞭解如何使用Adobe Experience Platform Web SDK管理使用者體驗上的閃爍。
keywords: target；忽隱忽現；預先隱藏Style；非同步；非同步；
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: e5d279397cab30e997103496beda5265520dca77
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# 管理忽隱忽現情形

嘗試呈現個人化內容時，SDK必須確定沒有忽隱忽現的情形。 閃爍(也稱為FOOC (原始內容的Flash))是指在測試/個人化期間出現替代方案之前，先短暫顯示原始內容。 SDK會嘗試將CSS樣式套用至頁面的元素，以確保這些元素會隱藏，直到成功呈現個人化內容為止。

忽隱忽現的管理功能包含幾個階段：

1. 預先隱藏
1. 正在預先處理
1. 呈現

## 預先隱藏

在預先隱藏階段，SDK會使用 `prehidingStyle` 設定選項來建立HTML樣式標籤並將其附加至DOM，以確保隱藏頁面的大部分內容。 如果您不確定頁面的哪些部分將會個人化，建議設定 `prehidingStyle` 至 `body { opacity: 0 !important }`. 這可確保隱藏整個頁面。 但是，這也有不利的一面，可能會導致Lighthouse、網頁測試等工具報告的頁面轉譯效能不佳。 若要獲得最佳的頁面轉譯效能，建議設定 `prehidingStyle` 至包含將個人化之頁面部分的容器元素清單。

假設您有一個類似以下的HTML頁面，而且您只知道 `bar` 和 `bazz` 容器元素將永遠個人化：

```html
<html>
  <head>
  </head>
  <body>
    <div id="foo">
      Foo foo foo
    </div>

    <div id="bar">
      Bar bar bar
    </div>

    <div id="bazz">
      Bazz bazz bazz
    </div>
  </body>
</html>
```

然後 `prehidingStyle` 應該設定為類似以下的專案 `#bar, #bazz { opacity: 0 !important }`.

## 正在預先處理

一旦SDK收到來自伺服器的個人化內容，預先處理階段就會開始。 在此階段中，會預先處理回應，確保隱藏必須包含個人化內容的元素。 隱藏這些元素後，已根據以下專案建立的HTML樣式標籤： `prehidingStyle` 組態選項會移除，且會顯示HTML內文或隱藏的容器元素。

## 呈現

成功轉譯所有個人化內容後，或發生任何錯誤時，會顯示所有先前隱藏的元素，以確定頁面上沒有已被SDK隱藏的隱藏元素。

## 管理非同步載入SDK時的閃爍問題

建議一律非同步載入SDK，以獲得最佳頁面轉譯效能。 不過，這對個人化內容的呈現有一些影響。 非同步載入SDK時，必須使用預先隱藏程式碼片段。 必須在HTML頁面的SDK之前新增預先隱藏的程式碼片段。 以下是隱藏整個內文的範常式式碼片段：

```html
<script>
  !function(e,a,n,t){
    if (a) return;
    var i=e.head;if(i){
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
    setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

為了確保HTML本文或容器元素不會長時間隱藏，預先隱藏程式碼片段會使用計時器，依預設會移除之後的程式碼片段 `3000` 毫秒。 此 `3000` 毫秒是等待時間上限。 如果更快收到並處理來自伺服器的回應，則會儘快移除預先隱藏HTML樣式標籤。
