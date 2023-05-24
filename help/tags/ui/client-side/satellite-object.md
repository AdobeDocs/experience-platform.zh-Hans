---
title: 衛星物件參考
description: 瞭解使用者端_satellite物件，以及您可以在標籤中執行的各種功能。
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 42%

---

# Satellite物件參考

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

本檔案可用作使用者端的參考 `_satellite` 物件以及您可以用它執行的各種功能。

## `track`

**代码**

```javascript
_satellite.track(identifier: string [, detail: *] )
```

**示例**

```javascript
_satellite.track('contact_submit', { name: 'John Doe' });
```

`track` 會使用已設定核心標籤擴充功能之指定識別碼的「直接呼叫」事件型別，觸發所有規則。 以上示例使用“直接调用”事件类型触发所有规则，其中配置的标识符为 `contact_submit`。此外，还会传递包含相关信息的可选对象。可以通过在条件或操作的文本字段中输入 `%event.detail%` 或者在“自定义代码”条件或操作的代码编辑器中输入 `event.detail` 来访问详细信息对象。

## `getVar`

**代码**

```javascript
_satellite.getVar(name: string) => *
```

**示例**

```javascript
var product = _satellite.getVar('product');
```

在提供的範例中，如果資料元素存在且具有相符名稱，則會傳回資料元素的值。 如果不存在匹配的数据元素，则将检查以前是否使用 `_satellite.setVar()` 设置了具有匹配名称的自定义变量。如果找到匹配的自定义变量，则将返回其值。

>[!NOTE]
>
>您可以使用百分比(`%`)語法來參考標籤實作中許多表單欄位的變數，減少呼叫的需求 `_satellite.getVar()`. 例如，使用 `%product%` 將存取產品資料元素或自訂變數的值。

當事件觸發規則時，您可以傳遞規則的對應專案 `event` 物件進入 `_satellite.getVar()` 如下所示：

```javascript
// event refers to the calling rule's event
var rule = _satellite.getVar('return event rule', event);
```

## `setVar`

**代码**

```javascript
_satellite.setVar(name: string, value: *)
```

**示例**

```javascript
_satellite.setVar('product', 'Circuit Pro');
```

`setVar()` 設定具有指定名稱和值的自訂變數。 之后可以使用 `_satellite.getVar()` 访问该变量的值。

您可以选择一次设置多个变量，方法是传递一个对象，其中键是变量名称，值是各自的变量值。

```javascript
_satellite.setVar({ 'product': 'Circuit Pro', 'category': 'hobby' });
```

## `getVisitorId`

**代码**

```javascript
_satellite.getVisitorId() => Object
```

**示例**

```javascript
var visitorIdInstance = _satellite.getVisitorId();
```

如果资产上安装了 [!DNL Adobe Experience Cloud ID] 扩展，此方法将返回访客 ID 实例。有关详细信息，请参阅 [Experience Cloud ID 服务文档](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=zh-Hans)。

## `logger`

**代码**

```javascript
_satellite.logger.log(message: string)
```

```javascript
_satellite.logger.info(message: string)
```

```javascript
_satellite.logger.warn(message: string)
```

```javascript
_satellite.logger.error(message: string)
```

**示例**

```javascript
_satellite.logger.error('No product ID found.');
```

此 `logger` 物件允許將訊息記錄到瀏覽器主控台。 只有在使用者已啟用標籤偵錯（透過呼叫）功能時，才會顯示訊息 `_satellite.setDebug(true)` 或使用適當的瀏覽器擴充功能)。

### 记录弃用警告

```javascript
_satellite.logger.deprecation(message: string)
```

**示例**

```javascript
_satellite.logger.deprecation('This method is no longer supported, please use [new example] instead.');
```

這會將警告記錄到瀏覽器主控台。 顯示使用者是否啟用標籤偵錯的訊息。

## `cookie` {#cookie}

`_satellite.cookie` 包含讀取和寫入Cookie的函式。 它是公開第三方程式庫js-cookie的副本。 如需此程式庫更進階用法的詳細資訊，請檢閱 [js-cookie檔案](https://www.npmjs.com/package/js-cookie#basic-usage).

### 設定Cookie {#cookie-set}

若要設定Cookie，請使用 `_satellite.cookie.set()`.

**代码**

```javascript
_satellite.cookie.set(name: string, value: string[, attributes: Object])
```

>[!NOTE]
>
>舊版 [`setCookie`](#setCookie) 設定Cookie的方法中，此函式呼叫的第三個（選用）引數是整數，指出Cookie的過期時間（以天為單位）。 在這個新方法中，「attributes」物件會改為被接受為第三個引數。 若要使用新方法設定Cookie的有效期，您必須提供 `expires` 屬性物件中的屬性，並將其設定為所需的值。 以下範例說明此方法。

**示例**

以下函式呼叫所寫入的Cookie會在一週後過期。

```javascript
_satellite.cookie.set('product', 'Circuit Pro', { expires: 7 });
```

### 擷取Cookie {#cookie-get}

若要擷取Cookie，請使用 `_satellite.cookie.get()`.

**代码**

```javascript
_satellite.cookie.get(name: string) => string
```

**示例**

以下函式呼叫會讀取先前設定的Cookie。

```javascript
var product = _satellite.cookie.get('product');
```

### 移除Cookie {#cookie-remove}

若要移除Cookie，請使用 `_satellite.cookie.remove()`.

**代码**

```javascript
_satellite.cookie.remove(name: string)
```

**示例**

以下函式呼叫會移除先前設定的Cookie。

```javascript
_satellite.cookie.remove('product');
```

## `buildInfo`

**代码**

```javascript
_satellite.buildInfo
```

此物件包含目前標籤執行階段程式庫組建的相關資訊。 该对象包含以下属性：

### `turbineVersion`

如此可提供 [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) 目前程式庫內使用的版本。

### `turbineBuildDate`

生成容器内使用的 [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) 版本的 ISO 8601 日期。

### `buildDate`

生成当前库的 ISO 8601 日期。

以下示例展示了对象值：

```javascript
{
  turbineVersion: "14.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z"
}
```

## `environment`

此物件包含部署目前標籤執行階段程式庫所在環境的相關資訊。

**代码**

```javascript
_satellite.environment
```

该对象包含以下属性：

```javascript
{
  id: "ENbe322acb4fc64dfdb603254ffe98b5d3",
  stage: "development"
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 環境的ID。 |
| `stage` | 生成此库的环境。可能的值包括 `development`， `staging`、和 `production`. |

## `notify`

>[!NOTE]
>
>此方法已弃用。请改用 `_satellite.logger.log()`。

**代码**

```javascript
_satellite.notify(message: string[, level: number])
```

**示例**

```javascript
_satellite.notify('Hello world!');
```

`notify` 將訊息記錄到瀏覽器主控台。 只有在使用者已啟用標籤偵錯（透過呼叫）功能時，才會顯示訊息 `_satellite.setDebug(true)` 或使用適當的瀏覽器擴充功能)。

可傳遞選用的記錄層級，這會影響所記錄訊息的樣式和篩選。 支持的级别包括：

3 - 信息性消息。

4 - 警告消息。

5 - 错误消息。

如果您未提供日志记录级别或未传递任何其他级别值，则消息将记录为常规消息。

## `setCookie` {#setCookie}

>[!IMPORTANT]
>
>此方法已弃用。请改用 [`_satellite.cookie.set()`](#cookie-set)。

**代码**

```javascript
_satellite.setCookie(name: string, value: string, days: number)
```

**示例**

```javascript
_satellite.setCookie('product', 'Circuit Pro', 3);
```

這會在使用者的瀏覽器中設定Cookie。 Cookie 将持续保留指定的天数。

## `readCookie`

>[!IMPORTANT]
>
>此方法已弃用。请改用 [`_satellite.cookie.get()`](#cookie-get)。

**代码**

```javascript
_satellite.readCookie(name: string) => string
```

**示例**

```javascript
var product = _satellite.readCookie('product');
```

這會從使用者的瀏覽器中讀取Cookie。

## `removeCookie`

>[!NOTE]
>
>此方法已弃用。请改用 [`_satellite.cookie.remove()`](#cookie-remove)。

**代码**

```javascript
_satellite.removeCookie(name: string)
```

**示例**

```javascript
_satellite.removeCookie('product');
```

這會從使用者的瀏覽器中移除Cookie。

## 调试函数

下列函式不應從生產程式碼中存取。 这些函数仅用于调试目的，并将根据需要随时间发生更改。

### `container`

**代码**

```javascript
_satellite._container
```

**示例**

>[!IMPORTANT]
>
>不應從生產程式碼存取此函式。 此函数仅用于调试目的，并将根据需要随时间发生更改。

### `monitor`

**代码**

```javascript
_satellite._monitors
```

**示例**

>[!IMPORTANT]
>
>不應從生產程式碼存取此函式。 此函数仅用于调试目的，并将根据需要随时间发生更改。

**样例**

在執行標籤庫的網頁上，將程式碼片段新增至HTML。 通常，程式碼會插入 `<head>` 元素之前的 `<script>` 載入標籤程式庫的元素。 這可讓監視器擷取標籤程式庫中發生的最早系統事件。 例如：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script>
    window._satellite = window._satellite || {};
    window._satellite._monitors = window._satellite._monitors || [];
    window._satellite._monitors.push({
      ruleTriggered: function (event) {
        console.log(
          'rule triggered',
          event.rule
        );
      },
      ruleCompleted: function (event) {
        console.log(
          'rule completed',
          event.rule
        );
      },
      ruleConditionFailed: function (event) {
        console.log(
          'rule condition failed',
          event.rule,
          event.condition
        );
      }
    });
  </script>
  <script src="//assets.adobedtm.com/launch-EN5bfa516febde4b22b3e7c6f96f6b439f.min.js"
          async></script>
</head>
<body>
  <h1>Click me!</h1>
</body>
</html>
```

在第一個指令碼元素中，由於標籤程式庫尚未載入，因此初始的 `_satellite` 已建立物件並在上建立陣列 `_satellite._monitors` 已初始化。 然后，此脚本将一个监视器对象添加到该数组。監視器物件可以指定下列方法，標籤程式庫稍後會呼叫這些方法：

### `ruleTriggered`

此函式會在事件觸發規則之後，但在處理規則的條件和動作之前呼叫。 传递给 `ruleTriggered` 的事件对象包含有关已触发的规则的信息。

### `ruleCompleted`

此函式會在完全處理規則後呼叫。 換言之，事件已發生、所有條件皆已傳遞，且所有動作皆已執行。 傳遞至的事件物件 `ruleCompleted` 包含已完成規則的相關資訊。

### `ruleConditionFailed`

觸發規則且其中一個條件失敗後，會呼叫此函式。 传递给 `ruleConditionFailed` 的事件对象包含有关已触发的规则和失败的条件的信息。

如果调用 `ruleTriggered`，则此后不久将调用 `ruleCompleted` 或 `ruleConditionFailed`。

>[!NOTE]
>
>监视器不必指定所有三种方法（`ruleTriggered`、`ruleCompleted` 和 `ruleConditionFailed`）。Adobe Experience Platform中的標籤可與監視器已提供的任何支援方法搭配使用。

### 测试监视器

上面的示例在监视器中指定了所有三种方法。当这些方法被调用时，监视器会记录相关信息。若要對此進行測試，請在標籤程式庫中設定兩個規則：

1. 具有一个点击事件和一个浏览器条件（仅当浏览器为 [!DNL Chrome] 时才传递）的规则。
1. 具有一个点击事件和一个浏览器条件（仅当浏览器为 [!DNL Firefox] 时才传递）的规则。

如果您在 [!DNL Chrome] 中打开页面，打开浏览器控制台，然后选择该页面，则控制台中会显示以下内容：

![](../../images/debug.png)

您可視需要將其他Hook或其他資訊新增到這些處理常式。
