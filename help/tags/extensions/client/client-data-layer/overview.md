---
title: Adobe使用者端資料層擴充功能
description: 瞭解Adobe Experience Platform中的Adobe Client Data Layer標籤擴充功能。
exl-id: c4d1b4d3-4b51-4701-be2e-31b08e109bf6
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---

# Adobe使用者端資料層擴充功能

本檔案提供如何使用Adobe Client Data Layer擴充功能的範例和最佳作法。

<!-- (Missing document?)
If you would like to have more details on development consideration, [please reach this page](./dev.md). -->

## 安装

若要安裝擴充功能，請導覽至Experience PlatformUI或資料收集UI中的擴充功能目錄，然後選取「Adobe使用者端資料層」。

![目錄中的ACDL擴充功能檢視](./images/catalog.png)

<!-- (GitHub link?)
There is also the possibility to fork this project. You can download this github project, realize the change that you deem required for your specific use-case and re-upload it on your Organization as a private extension.
This installation will not be supported on our end.<br>
>[!NOTE]
>
> _Consider renaming the extension name in the extension.json file_ -->

## 擴充功能檢視

根據預設，ACDL指令碼會以變數名稱建立新的資料層 `adobeDataLayer`. 擴充功能檢視可讓您視需要變更此名稱。 載入標籤時，您設定的名稱將會具現化。

>[!NOTE]
>
>變更物件名稱時，原始物件 `adobeDataLayer` 物件仍在具現化，然後複製到您選取的新變數名稱。

## 事件

擴充功能可讓您接聽Data Layer上的事件。 可使用下列事件：

### 接聽所有資料變更

如果您選取此選項，事件接聽程式會接聽資料層所做的任何變更。

>[!IMPORTANT]
>
>推播事件不會變更資料層本身。

監聽器會追蹤下列範例推送事件：

* ` adobeDataLayer.push({"data":"something"})`
* ` adobeDataLayer.push({"event":"myevent","data":"something"})`

監聽器不會追蹤下列範例推送事件：

* ` adobeDataLayer.push({"event":"myevent"})`

### 聆聽所有事件

如果您選取此選項，事件接聽程式會接聽推播至資料層的任何事件。

監聽器會追蹤下列範例推送事件：

* ` adobeDataLayer.push({"event":"myevent"})`
* ` adobeDataLayer.push({"event":"myevent","data":"something"})`

監聽器不會追蹤下列範例推送事件：

* ` adobeDataLayer.push({"data":"something"}) `

### 接聽特定事件

如果您指定事件，則事件接聽程式會追蹤符合特定字串的任何事件。

例如，設定 `myEvent` 使用此設定時，監聽器只會追蹤下列推播事件：

* `adobeDataLayer.push({"event":"myEvent"})`

您也可以變更事件接聽程式的範圍。 不同選項概述如下：

* `all`：這是預設選項，會在您選取的上述條件過去曾經符合，或未來會推送時觸發規則。 如果您使用非同步實施，這是最安全的選項。
* `future`：只有將符合您條件的新推送事件傳送至Data Layer時，此選項才會觸發規則。
* `past`：此選項只會針對符合您條件的舊推送事件觸發規則。 符合您條件的新推播會遭忽略，且不再觸發規則。

## 操作

以下各節概述擴充功能支援的動作。

### 重設資料層

擴充功能提供重設資料層長度的方法，可協助您將單頁應用程式(SPA)的大小維持在有限範圍內。

不過，目前不可能完全移除先前在推送方法期間設定的資訊。

此 **重設和設定計算狀態** 動作會複製上次計算狀態、清空資料層物件，並重新推送上次狀態。

### 推送至資料層

擴充功能提供將JSON內容推送至資料層本身的動作。此動作讓直接在JSON中使用資料元素成為可能。 在JSON編輯器中，應使用百分比標籤法參考資料元素(例如 `%dataElementName%`)。

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

## 数据元素

以下各節說明擴充功能所提供的獨特資料元素型別。

### 計算狀態

根據您的設定方式，「資料層計算狀態」資料元素可以傳回下列兩個專案之一：

* 完整的資料層狀態：依預設，會傳回完整的資料層計算狀態。
* 特定路徑：您可以指定要在資料層中傳回的路徑。 路徑是使用點標籤法來指定(例如， `data.foo`)。

### 資料層大小

此資料元素會傳回資料層的大小。 資料層的大小是以已推送至此物件的元素數量表示。

在下列推送事件清單中，此資料元素會傳回整數 `2`：

```js
adobeDataLayer.push({"event":"myEvent"})
adobeDataLayer.push({"data":{"foo":"bar"}})
```
