---
title: Google資料層擴充功能
description: 瞭解Adobe Experience Platform中的Google Client Data Layer標籤擴充功能。
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: 9c608f69f6ba219f9cb4e938a77bd4838158d42c
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 1%

---

# Google資料層擴充功能

Google Data Layer擴充功能可讓您在標籤實作中使用Google資料層。 此擴充功能可單獨使用，或與Google解決方案及Google的開放原始碼同時使用 [資料層協助程式庫](https://github.com/google/data-layer-helper).

Helper Library提供與Adobe Client Data Dayer (ACDL)類似的事件導向功能。 Google Data Layer擴充功能的資料元素、規則和動作所提供的功能與 [ACDL擴充功能](../client-data-layer/overview.md).

## 成熟度

1.2.x版為最新測試版，現正用於生產環境。

## 安装

若要安裝擴充功能，請導覽至資料收集UI中的擴充功能目錄，然後選取 **[!UICONTROL Google資料層]**.

安裝後，擴充功能就會在每次載入Adobe Experience Platform Tags資料庫時，建立或存取資料層。

## 擴充功能檢視

擴充功能組態可用來定義擴充功能使用的資料層名稱。 載入Adobe Experience Platform Tags時，如果沒有任何資料層具有已設定的名稱，擴充功能會建立一個資料層。

資料層名稱預設為Google預設名稱 `dataLayer`.

>[!NOTE]
>
>Google或Adobe程式碼會先載入並建立資料層並不重要。 兩個系統的行為相同 — 如果資料層不存在或使用現有的資料層，請建立資料層。

## 事件

>[!NOTE]
>
>單字 _事件_ 在Adobe Experience Platform Tags中使用事件導向的資料層時，會多載。 _事件_ 可以是：
> - Adobe Experience Platform Tags事件（Library Loaded等）。
> - JavaScript事件。
> - 使用推送至資料層的資料 _事件_ 關鍵字。


擴充功能可讓您接聽資料層上的變更。

>[!NOTE]
>
>請務必瞭解如何使用 _事件_ 關鍵字(類似於Adobe使用者端資料層)將資料推送至Google資料層時。 此 _事件_ 關鍵字會變更Google資料層的行為，進而變更此擴充功能。\
> 請閱讀Google檔案，或如果對此點不確定，請進行研究。

### 聆聽資料層的所有推送

如果您選取此選項，事件接聽程式會接聽資料層所做的任何變更。

### 接聽排除事件的推送

如果您選取此選項，事件接聽程式會接聽任何資料推送到資料層的動作，但不包括事件。

監聽器會追蹤下列範例推送事件：

```js
dataLayer.push({"data":"something"})
```

監聽器不會追蹤下列範例推送事件：

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### 接聽所有事件

如果您選取此選項，事件接聽程式會接聽推播至資料層的任何事件。

監聽器會追蹤下列範例推送事件：

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

監聽器不會追蹤下列範例推送事件：

```js
dataLayer.push({"data":"something"})
```

### 接聽特定事件

如果您指定事件，則事件接聽程式會追蹤符合特定字串的任何事件。

例如，設定 `myEvent` 使用此設定時，監聽器只會追蹤下列推播事件：

```js
dataLayer.push({"event":"myEvent"})
```

可以使用(ECMAScript / JavaScript)規則運算式來比對事件名稱。

例如，設定&#39;myEvent\d&#39;將追蹤 `myEvent` 加上數字(\d)：

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## 操作

### 推送至資料層 {#push-to-data-layer}

擴充功能提供您兩個將JSON推送至資料層的動作；一個是自由文字欄位，可手動建立要推送的JSON；另一個是從1.2.0版啟動的「索引鍵值多欄位」對話方塊。

#### 自由文字JSON

自由文字動作可讓您直接在JSON中使用資料元素。 在JSON編輯器中，應使用百分比標籤法參考資料元素。 例如：`%dataElementName%`。

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

#### 索引鍵 — 值多欄位

較新的索引鍵值多欄位對話方塊是更好記的介面，可讓您設定推送，而不需手動寫入JSON。

### Google DL重設為計算狀態

擴充功能提供您重設資料層的動作。 若用於處理Google資料層變更的規則中，資料層會重設為觸發規則時資料層的計算狀態。 如果動作用於不會處理Google資料層變更的規則中，該動作會清空資料層。

## 数据元素

提供的資料元素可用於執行Google資料層變更（推送事件）所觸發的規則，或用於不相關的規則，例如Library Loaded。 在前一種情況下，資料元素會傳回資料層變更時從計算狀態取得的值。 在後一種情況下，會使用規則執行時的計算狀態。

切換開關可讓您選擇資料元素是應該從整個計算狀態傳回值，還是隻從事件資訊傳回值（如果用於由資料層變更觸發的規則中）。

因此，資料元素可以傳回：

- 空白欄位：資料層計算狀態。
- 具有索引鍵的欄位（例如上述範例中的page.previous_url）：事件物件或計算狀態中的索引鍵值。

## 其他信息

擴充功能的資料元素和事件對話方塊包含詳細的使用資訊和範例。

其他一般資訊請參閱 [專案讀我檔案](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md)
