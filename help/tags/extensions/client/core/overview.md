---
title: 核心擴充功能概觀
description: 瞭解Adobe Experience Platform中的核心標籤擴充功能。
exl-id: 841f32ad-a6a8-49fb-a131-ef4faab47187
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '5482'
ht-degree: 62%

---

# 核心擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

核心標籤擴充功能是隨Adobe Experience Platform發佈的預設擴充功能。

本檔案提供使用核心擴充功能建立規則時可用選項的相關資訊。

## 核心扩展事件类型 {#core-extension-event-types}

本主题介绍核心扩展中可用的事件类型。如需可針對多種不同事件型別設定的選項相關資訊，請參閱 [選項](#options) 區段。

### 瀏覽器型事件

#### Tab Blur

標籤失去焦點時，標籤模糊事件會觸發動作。 没有适用于此事件类型的设置。

#### Tab Focus

索引標籤獲得焦點時，索引標籤焦點事件會觸發動作。 没有适用于此事件类型的设置。

### 表单

#### Blur

表單失去焦點時，模糊事件會觸發動作。 請參閱 [選項](#options) 區段以取得可自訂事件設定的詳細資訊。

#### Focus

焦點事件會在表單獲得焦點時觸發動作。 請參閱 [選項](#options) 區段以取得可自訂事件設定的詳細資訊。

#### Submit

提交表單時，提交事件會觸發動作。 請參閱 [選項](#options) 區段以取得可自訂事件設定的詳細資訊。

### 鍵盤控制事件

#### Key Press

按下按鍵時觸發此事件。 請參閱 [選項](#options) 區段以取得可自訂事件設定的詳細資訊。

### 媒體型事件

#### Media Ended

媒體結束時觸發此事件。 請參閱 [選項](#options) 區段以取得可自訂事件設定的詳細資訊。

#### 媒體載入的資料

媒體載入資料時會觸發此事件。 請參閱 [選項](#options) 區段以取得可自訂事件設定的詳細資訊。

#### Media Pause

媒體暫停時會觸發此事件。 請參閱 [選項](#options) 區段以取得可自訂事件設定的詳細資訊。

#### Media Play

媒體播放時會觸發此事件。 請參閱 [選項](#options) 區段以取得可自訂事件設定的詳細資訊。

#### Media Stalled

媒體停止時會觸發此事件。 請參閱 [選項](#options) 區段以取得可自訂事件設定的詳細資訊。

#### Media-Time已播放

如果媒體播放了指定的時間長度，則會觸發此事件。 您必須指定媒體必須播放的持續時間，才能觸發事件。 請參閱 [選項](#options) 區段以取得可自訂事件設定的詳細資訊。


#### Media-Volume已變更

如果音量提高或降低，則會觸發此事件。 請參閱 [選項](#options) 區段以取得可自訂事件設定的詳細資訊。

### 行動裝置導向事件

#### Orientation Change

如果裝置的方向變更，則會觸發事件。 您必須指定方向必須變更的持續時間，才能觸發事件。 没有适用于此事件类型的设置。

#### Zoom Change

如果使用者放大或縮小，則會觸發此事件。 没有适用于此事件类型的设置。

### 滑鼠控制事件

#### Click

如果選取（按一下）指定的元素，則會觸發此事件。 （可选）您可以为元素指定在触发该事件之前必须为 true 的属性值。

如果元素是錨點標籤(`<a>`)至連結的內容，您也可以指定是否將導覽延遲一段時間。 如果您的規則需要額外的執行時間，而通常在頁面導覽發生之前無法完成，此功能會很有用。

>[!WARNING]
>
>使用此選項時請務必格外小心，因為如果使用不正確，可能會對使用者體驗產生負面影響。

當您使用連結延遲時，Platform實際上會防止瀏覽器導覽離開頁面。 然後在指定的逾時後，它會執行JavaScript重新導向至原始目的地。 當您的頁面標籤具有下列條件時，這會特別危險 `<a>` 預期功能實際上並未導覽使用者離開頁面的標籤。 如果您無法以任何其他方式解決問題，您應極為精確地使用選擇器定義，以便此事件將完全觸發您需要的位置，而不會觸發其他位置。

預設連結延遲值為100毫秒。 請注意，標籤一律會等待指定的時間量，且不會以任何方式連線到規則動作的執行。 延遲可能會強制使用者等候超過所需時間，而且延遲時間可能不足以讓所有規則動作成功完成。 較長的延遲可提供較多的規則執行時間，但也會惡化使用者體驗。

若要實施延遲，請提供觸發事件的所選元素，以及觸發事件之前的特定時間量。

如需進階選項，請參閱 [選項](#options) 區段以取得詳細資訊。

#### Hover

如果使用者將游標停留在指定的元素上，則會觸發事件。 您也必須設定規則是立即觸發還是在指定的毫秒數之後觸發。 請參閱 [選項](#options) 區段以取得可自訂事件設定的詳細資訊。

### 其他事件

#### Custom Event

如果發生自訂事件型別，則會觸發事件。 在程式碼基底中的其他地方定義的已命名JavaScript函式可以用作自訂事件型別。 您必須指定自訂事件型別的名稱，並依照中的說明進行任何其他設定 [選項](#options) 區段底下。

#### Data Element Changed

如果指定的資料元素變更，則會觸發此事件。 您必須提供資料元素的名稱。 您可以在文字欄位中輸入資料元素的名稱，或選取文字欄位右側的資料元素圖示，然後從出現的對話方塊內提供的清單中進行選擇，以選取資料元素。

#### Direct Call {#direct-call-event}

直接呼叫事件會略過事件偵測和查詢系統。 若要告訴系統確切發生的狀況，直接呼叫規則是理想的選擇。 此外，這類規則也非常適合系統無法偵測DOM中的事件。

定義直接呼叫事件時，您必須指定將當作此事件識別碼的字串。 若為 [觸發直接呼叫動作](#direct-call-action) 會觸發包含相同識別碼的任何直接呼叫事件規則，然後接聽該識別碼。

![資料收集UI中直接呼叫事件的熒幕擷圖](../../../images/extensions/client/core/direct-call-event.png)

#### Element Exists

如果指定的元素存在，則會觸發此事件。 請參閱 [選項](#options) 區段以取得可自訂事件設定的詳細資訊。

#### Enters Viewport

如果使用者進入指定的檢視區，則會觸發此事件。 您必須提供CSS選擇器作為目標符合元素的條件。 您也必須設定規則是立即觸發還是在指定的毫秒數後觸發，以及事件應該在每次事件發生時觸發，還是隻在第一次發生時觸發。

請參閱 [選項](#options) 區段以取得可自訂事件設定的詳細資訊。

#### History Change

如果發生pushState或hashchange事件，則會觸發此事件。 没有适用于此事件类型的设置。

#### 頁面逗留時間

如果使用者在頁面上停留指定的秒數，則會觸發事件。 您必須指定觸發事件之前必須經過的秒數。

### 頁面載入事件

#### DOM Ready

當DOM就緒且使用者可與頁面互動時，就會觸發事件。 没有适用于此事件类型的设置。

#### Library Loaded (Page Top) {#library-loaded-page-top}

載入標籤程式庫後，就會觸發事件。 没有适用于此事件类型的设置。

#### Page Bottom {#page-bottom}

事件觸發一次 `_satellite.pageBottom();` 已呼叫。 非同步載入標籤程式庫時，不應使用此事件型別。 没有适用于此事件类型的设置。

#### Window Loaded

當瀏覽器呼叫onLoad且頁面載入完成時，就會觸發事件。 没有适用于此事件类型的设置。

### 选项 {#options}

每个表单事件类型都使用以下设置：

#### Specific Elements \| Any Element

* 如果您選擇 **[!UICONTROL 特定元素]**，則會顯示選取元素和屬性值的選項。
* 如果您選擇 **[!UICONTROL 任何元素]**，則不需要進階選項來縮小元素。

#### Elements matching the CSS selector

输入用于标识将会触发事件的元素的 CSS 选择器。

#### And having certain property values

如果选择此选项，则以下参数将变为可用：

* `property=value`

   指定属性的值

* Regex

   如果 `property=value` 是正则表达式，则启用此选项。

* Add

   添加其他 `property=value` 对。

#### Advanced options (Bubbling)

* 即使事件源自子元素，也运行此规则
* 即使事件已触发针对子元素的规则，也允许运行此规则
* 此规则运行后，阻止事件触发针对父元素的规则

## 核心扩展条件类型

此部分介绍核心扩展中可用的条件类型。这些条件类型可以与常规或例外逻辑类型一起使用。

### 数据

#### Cookie

指定要使事件触发操作而必须存在的 Cookie 名称和值。

1. 指定 Cookie 名称。
1. 输入如果事件要触发操作，Cookie 中必须存在的值。
1. （可选）如果这是正则表达式，则启用 Regex。

#### 自定义代码

指定必须作为事件条件存在的任何自定义代码。

>[!NOTE]
>
>自訂程式碼現在支援ES6+ JavaScript。 請注意，有些舊版瀏覽器不支援ES6+。 若要瞭解使用ES6+函式的影響，請針對所有應受支援的網頁瀏覽器進行測試。

使用內建程式碼編輯器輸入自訂程式碼：

1. 選取 **[!UICONTROL 開啟編輯器]**.
1. 键入自定义代码。
1. 选择&#x200B;**[!UICONTROL 保存]**。

将自动提供一个名为 `event` 的变量，您可以从自定义代码中引用该变量。`event` 对象将包含有关触发规则的事件的有用信息。确定哪些事件数据可用的最简单方法是从自定义代码中将 `event` 记录到控制台：

```javascript
console.log(event);
return true;
```

在浏览器中运行规则，并在浏览器控制台中检查已记录的事件对象。了解了哪些信息可用后，您便可以将其用于自定义代码中的程序化决策。

*条件排序*

啟用屬性設定的「依序執行規則元件」選項時，您可以讓後續的規則元件等候，先由條件執行非同步工作。

当条件返回[承诺](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)时，直到返回的承诺得到解析后才会执行规则中的下一个条件。如果Promise遭拒，標籤會將該條件視為執行失敗，不會執行該規則的其他條件或動作。

返回承诺的条件的示例：

```javascript
return new Promise(function(resolve, reject) {
  setTimeout(function() {
    if (new Date().getDay() === 5) {
      resolve();
    } else {
      reject();
    }
  }, 1000);
});
```

#### Value Comparison {#value-comparison}

比较两个值以确定此条件是否返回 true。

假设您有一个包含多个条件的规则，此条件可能会返回 true，但是由于其他条件评估为 false 或其中一个例外评估为 true，因此该规则仍不会触发。

1. 提供一个值。
1. 选择运算符。有关更多详细信息，请参阅下面的值比较运算符列表。
1. （如果需要）选择比较是否应区分大小写。
1. 提供另一个要比较的值。

可以使用以下值比较运算符：

**Equal：**&#x200B;如果使用非严格比较后认为两个值相等，则该条件会返回 true（在 JavaScript 中，运算符为 ==）。值可以是任何类型。在值字段中输入 _true_、_false_、_null_ 或 _undefined_ 之类的词时，该词将作为字符串进行比较，而不会转换为其 JavaScript 等效字符。

**Does Not Equal：**&#x200B;如果使用非严格比较后认为两个值不相等，则该条件会返回 true（在 JavaScript 中，运算符为 !=）。值可以是任何类型。在值字段中输入 _true_、_false_、_null_ 或 _undefined_ 之类的词时，该词将作为字符串进行比较，而不会转换为其 JavaScript 等效字符。

**Contains：**&#x200B;如果第一个值包含第二个值，则该条件会返回 true。数字将转换为字符串。除数字或字符串之外的任何其他值都会导致该条件返回 false。

**Does Not Contain：**&#x200B;如果第一个值不包含第二个值，则该条件会返回 true。数字将转换为字符串。除数字或字符串之外的任何其他值都会导致该条件返回 true。

**Starts With：**&#x200B;如果第一个值以第二个值开头，则该条件会返回 true。数字将转换为字符串。除数字或字符串之外的任何其他值都会导致该条件返回 false。

**Does Not Start With：**&#x200B;如果第一个值不以第二个值开头，则该条件会返回 true。数字将转换为字符串。除数字或字符串之外的任何其他值都会导致该条件返回 true。

**Ends With：**&#x200B;如果第一个值以第二个值结尾，则该条件会返回 true。数字将转换为字符串。除数字或字符串之外的任何其他值都会导致该条件返回 false。

**Does Not End With：**&#x200B;如果第一个值不以第二个值结尾，则该条件会返回 true。数字将转换为字符串。除数字或字符串之外的任何其他值都会导致该条件返回 true。

**Matches Regex：**&#x200B;如果第一个值匹配正则表达式，则该条件会返回 true。数字将转换为字符串。除数字或字符串之外的任何其他值都会导致该条件返回 false。

**Does Not Match Regex：**&#x200B;如果第一个值不匹配正则表达式，则该条件会返回 true。数字将转换为字符串。除数字或字符串之外的任何其他值都会导致该条件返回 true。

**Is Less Than：**&#x200B;如果第一个值小于第二个值，则该条件会返回 true。表示数字的字符串将转换为数字。除数字或可转换字符串之外的任何其他值都会导致该条件返回 false。

**Is Less Than Or Equal To：**&#x200B;如果第一个值小于或等于第二个值，则该条件会返回 true。表示数字的字符串将转换为数字。除数字或可转换字符串之外的任何其他值都会导致该条件返回 false。

**Is Greater Than：**&#x200B;如果第一个值大于第二个值，则该条件会返回 true。表示数字的字符串将转换为数字。除数字或可转换字符串之外的任何其他值都会导致该条件返回 false。

**Is Greater Than Or Equal To：**&#x200B;如果第一个值大于或等于第二个值，则该条件会返回 true。表示数字的字符串将转换为数字。除数字或可转换字符串之外的任何其他值都会导致该条件返回 false。

**Is True：**&#x200B;如果提供的值是值为 true 的布尔值，则该条件会返回 true。如果您提供的值是任何其他类型，则不会将该值转换为布尔值。除值为 true 的布尔值之外的任何其他值都会导致该条件返回 false。

**Is Truthy：**&#x200B;如果提供的值在转换为布尔值后为 true，则该条件会返回 true。有关 truthy 值的示例，请参阅 [MDN 的 Truthy 文档](https://developer.mozilla.org/zh-CN/docs/Glossary/Truthy)。

**Is False：**&#x200B;如果提供的值是值为 false 的布尔值，则该条件会返回 true。如果您提供的值是任何其他类型，则不会将该值转换为布尔值。除值为 false 的布尔值之外的任何其他值都会导致该条件返回 false。

**Is Falsy：**&#x200B;如果提供的值在转换为布尔值后为 false，则该条件会返回 true。有关 falsy 值的示例，请参阅 [MDN 的 Falsy 文档](https://developer.mozilla.org/zh-CN/docs/Glossary/Falsy)。

#### Variable

指定要使事件触发操作而必须存在的 JavaScript 变量名称和值。

1. 指定 JavaScript 变量名称。
1. 指定必须作为事件条件存在的变量值。
1. （可选）如果这是正则表达式，则启用 Regex。

### 参与度

#### 登陆页面

指定用户必须登陆才能触发事件的页面。

1. 指定登陆页面。
1. （可选）如果这是正则表达式，则启用 Regex。

#### New/Returning Visitor

指定要使事件触发操作，访客应该是新访客还是回访访客。

选择下列选项之一：

* New Visitor
* Returning Visitor

#### Page Views

配置在触发操作之前访客必须查看页面的次数。

1. 选择页面查看次数是必须大于、等于还是小于指定的值。
1. 指定用于确定是否满足条件的页面查看次数。
1. 通过选择以下任一选项来配置何时计数页面查看次数：
   * Lifetime
   * Current Session

#### Sessions

如果用户的会话数满足指定的标准，则会触发操作。

1. 选择会话数是必须大于、等于还是小于指定的值。
1. 指定用于确定是否满足条件的会话数。

#### Time On Site

如果用户的会话数满足指定的标准，则会触发操作。

配置在触发操作之前访客必须在网站上停留的时长。

1. 选择访客在网站上停留的分钟数是必须大于、等于还是小于指定的值。
1. 指定用于确定是否满足条件的分钟数。

#### Traffic Source

如果用户的会话数满足指定的标准，则会触发操作。

指定要使操作能够触发，必须为 true 的访客流量源。

1. 指定流量源。
1. （可选）如果这是正则表达式，则启用 Regex。

### 技术

#### 浏览器

选择要使操作能够触发，访客必须使用的浏览器。

选择以下一种或多种浏览器：

* Chrome
* Firefox
* Internet Explorer/Edge
* Internet Explorer Mobile
* Mobile Safari
* OmniWeb
* Opera
* Opera Mini
* Opera Mobile
* Safari

#### Device Type

选择要使操作能够触发，访客必须使用的设备类型。

选择以下一种或多种设备类型：

* Android
* Blackberry
* 台式机
* iPad
* iPhone
* iPod
* Nokia
* Windows Phone

#### Operating System

选择要使操作能够触发，访客必须使用的操作系统。

选择以下一种或多种操作系统：

* Android
* Blackberry
* iOS
* Linux
* MacOS
* Maemo
* Symbian OS
* Unix
* Windows

#### Screen Resolution

选择要使操作能够触发，访客必须在其设备上使用的屏幕分辨率。

1. 选择访客设备的屏幕分辨率宽度是必须大于、等于还是小于指定的值。
1. 指定屏幕分辨率宽度所需的像素数。
1. 选择访客设备的屏幕分辨率高度是必须大于、等于还是小于指定的值。
1. 指定屏幕分辨率高度所需的像素数。

#### Window Size

选择要使操作能够触发，访客必须在其设备上使用的窗口大小。

1. 选择访客设备的窗口大小宽度是必须大于、等于还是小于指定的值。
1. 指定窗口大小宽度所需的像素数。
1. 选择访客设备的窗口大小高度是必须大于、等于还是小于指定的值。
1. 指定窗口大小高度所需的像素数。

### URL

#### Domain

指定访客的域。

#### Hash

指定 URL 中必须存在的一个或多个哈希模式。

>[!NOTE]
>
>使用 OR 连接多个哈希模式。

1. 指定哈希模式。
1. （可选）如果这是正则表达式，则启用 Regex。
1. 添加任何其他哈希模式。

#### 路径和查询字符串

指定 URL 中必须存在的一个或多个路径。这包括路径和查询字符串。

>[!NOTE]
>
>使用 OR 连接多个路径。

1. 指定路径。
1. （可选）如果这是正则表达式，则启用 Regex。
1. 添加任何其他路径。

#### 不含查询字符串的路径

指定 URL 中必须存在的一个或多个路径。这包括路径，但不包括查询字符串。

>[!NOTE]
>
>使用 OR 连接多个路径。

1. 指定路径。
1. （可选）如果这是正则表达式，则启用 Regex。
1. 添加任何其他路径。

#### 协议

指定 URL 中使用的协议。

选择下列选项之一：

* HTTP
* HTTPS

#### 查询字符串参数

指定 URL 中使用的 URL 参数。

1. 指定 URL 参数名称。
1. 指定用于 URL 参数的值。
1. （可选）如果这是正则表达式，则启用 Regex。

#### Subdomain

指定 URL 中必须存在的一个或多个子域。

>[!NOTE]
>
>使用 OR 连接多个子域。

1. 指定子域。
1. （可选）如果这是正则表达式，则启用 Regex。
1. 添加任何其他子域。

### 其他

#### Date Range

指定日期范围。选择发生事件的日期和时间范围以及时区。

#### Max Frequency

指定条件会返回 true 的最大次数。您可以从下列选项中进行选择：

* Page view
* Sessions
* Visitor
* Seconds
* Minutes
* Days
* Weeks
* Months

对于每个会话最大频率为 1 的条件，可将这两个 `localStorage` 项目进行比较。如果 `visitorTracking.sessionCount` 大于 `maxFrequency.session` 计数，则取样条件为 true。如果两者相等，则条件为 false。

`sessionCount` 是 `visitorTracking` 项目，因此必须启用访客 API 才能使取样条件正常工作。

#### Sampling

指定条件会返回 true 的次数百分比。

## 核心扩展操作类型

此部分介绍核心扩展中可用的操作类型。

### 自定义代码

>[!NOTE]
>
>自訂程式碼現在支援ES6+ JavaScript。 請注意，有些舊版瀏覽器不支援ES6+。 若要瞭解使用ES6+函式的影響，請針對所有應受支援的網頁瀏覽器進行測試。

提供在触发事件并评估条件后运行的代码。

1. 命名操作代码。
1. 选择用于定义操作的语言：
   * JavaScript
   * HTML
1. 选择是否要全局执行操作代码。
1. 選取 **[!UICONTROL 開啟編輯器]**.
1. 編輯程式碼，然後選取 **[!UICONTROL 儲存]**.

选择 JavaScript 作为语言时，将自动提供一个名为 `event` 的变量，您可以从自定义代码中引用该变量。`event` 对象将包含有关触发规则的事件的有用信息。确定哪些事件数据可用的最简单方法是从自定义代码中将 `event` 记录到控制台：

```javascript
console.log(event);
```

在浏览器中运行规则，并在浏览器控制台中检查已记录的事件对象。了解哪些信息可用后，您便可以将其用于自定义代码中的程序化决策，将一段 `event` 对象发送到服务器等。

### Custom Code 操作处理

核心擴充功能適用於所有Adobe Experience Platform使用者，其中包含執行使用者所提供JavaScript或HTML的自訂程式碼動作。 通常，了解如何处理具有 Custom Code 操作的规则对用户很有用。

#### 使用 page top 或 page bottom 事件的规则

自訂動作的程式碼內嵌在主標籤程式庫中。 该代码将使用 document.write 写入文档。如果规则具有多个 Custom Code 操作，则该代码将按规则中配置的顺序写入。

#### 使用除 page top 或 page bottom 以外的任何事件的规则

自定义操作的代码将从服务器加载并使用 [Postscribe](https://github.com/krux/postscribe) 写入文档。如果规则具有多个 Custom Code 操作，则该代码将从服务器并行加载，但会按照规则中配置的顺序写入。

虽然在加载页面后使用 document.write 通常会出现问题，但对于通过 Custom Code 操作提供的代码来说，这并不是问题。无论何时执行代码，您都可以在 Custom Code 操作中使用 document.write。

#### 自定义代码验证

標籤程式碼編輯器中使用的驗證器，專門用於識別開發人員所編寫程式碼的問題。 经过缩小的代码（例如从代码管理器中下载的 AppMeasurement.js 代码）可能会被 验证器错误地标记为存在问题，这通常可以忽略不计。

#### 操作排序

啟用屬性設定的「依序執行規則元件」選項時，您可以在動作執行非同步工作時，讓後續的規則元件等候。  对于 JavaScript 和 HTML 自定义代码，这项操作的原理有所不同。

*JavaScript*

创建 JavaScript 自定义代码操作时，您可以从操作返回[承诺](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)。规则中的下一项操作将仅在返回的承诺得到解析后才执行。如果承诺被拒绝，则不会执行规则中的后续操作。

>[!NOTE]
>
>唯有JavaScript未設定為全域執行時，才能使用此功能。 如果您正在全域範圍中執行自訂程式碼動作，標籤會將Promise視為立即解決，並移至處理佇列中的下一個專案。

返回承诺的 JavaScript 自定义代码操作的示例：

```javascript
return new Promise(function(resolve, reject) {
  setTimeout(function() {
    if (new Date().getDay() === 5) {
      resolve();
    } else {
      reject();
    }
  }, 1000);
});
```

*HTML*

创建 HTML 自定义代码操作时，可在自定义代码中使用名为 `onCustomCodeSuccess()` 的函数。您可以呼叫此函式來指出自訂程式碼已完成，且標籤可能會繼續執行後續動作。 另一方面，如果您的自定义代码以某种方式失败，您可以调用 `onCustomCodeFailure()`。這會通知標籤不要執行該規則的後續動作。

使用新回调的 HTML 自定义代码操作的示例：

```html
<script>
setTimeout(function() {
  if (new Date().getDay() === 5) {
    onCustomCodeSuccess();
  } else {
    onCustomCodeFailure();
  }
}, 1000);
</script>
```

### 觸發直接呼叫 {#direct-call-action}

此動作會觸發使用特定規則的所有規則 [直接呼叫事件](#direct-call-event). 設定動作時，您必須提供要觸發之直接呼叫事件的識別碼字串。 或者，您也可以透過將資料傳遞至直接呼叫事件 `detail` 物件，可包含一組自訂的索引鍵/值組。

![資料收集UI中觸發直接呼叫動作的熒幕擷圖](../../../images/extensions/client/core/direct-call-action.png)

該動作直接對應至 [`track` 方法](../../../ui/client-side/satellite-object.md?lang=en#track) 在 `satellite` 物件，可由使用者端程式碼存取。

## 核心扩展数据元素类型

数据元素类型由扩展决定。对于可创建的类型，没有任何限制。

以下部分介绍核心扩展中可用的数据元素类型。其他扩展则使用其他数据元素类型。

### Cookie

可在“Cookie 名称”字段中提及任何可用的域 Cookie。

#### 示例：

`cookieName`

### 常量

随后可在操作或条件中引用的任何常数字符串值。

#### 示例：

`string`

### 自定义代码

>[!NOTE]
>
>自訂程式碼現在支援ES6+ JavaScript。 請注意，有些舊版瀏覽器不支援ES6+。 若要瞭解使用ES6+函式的影響，請針對所有應受支援的網頁瀏覽器進行測試。

通过选择“打开编辑器”并将代码插入编辑器窗口，可以将自定义 JavaScript 输入到用户界面中。

编辑器窗口中需要一个返回语句，以指示应该将什么值用作数据元素值。如果不包括返回语句或返回了值 `null` 或 `undefined`，则将使用数据元素的默认值作为数据元素值。

**示例：**

```javascript
var pageType = $('div.page-wrapper').attr('class').split('')[1];
if (window.location.pathname == '/') {
  return 'homepage';
} else {
  return pageType;
}
```

如果在规则执行时检索自定义代码数据元素，则将自动提供一个名为 `event` 的变量，您可以从自定义代码中引用该变量。`event` 对象将包含有关触发规则的事件的有用信息。确定哪些事件数据可用的最简单方法是从自定义代码中将 `event` 记录到控制台：

```javascript
console.log(event);
return true;
```

在浏览器中运行规则，并在浏览器控制台中检查已记录的事件对象。了解可能使用您的数据元素的各种规则下哪些信息可用后，您便可以将其用于自定义代码中的程序化决策，或返回一段 `event` 对象作为数据元素的值。

### DOM 属性

可以检索任何元素值，例如 div 或 H1 标记。

#### 示例：

CSS 选择器链：

`id#dc logo img`

获取以下元素的值：

`src`

### JavaScript 变量

可以使用路径字段引用任何可用的 JavaScript 对象或变量。

標籤資料元素可用於擷取您的標籤JavaScript變數或物件屬性。 然後，您可以透過參考標籤資料元素，在擴充功能或自訂規則中使用這些值。 如果資料來源變更，則只需更新來源的參照即可。

在以下範例中，標籤包含稱為的JavaScript變數 `Page_Name`.

```markup
<script>
  //data layer
  var Page_Name = "Homepage"
</script>
```

建立資料元素時，只需提供該變數的路徑。

如果您使用資料收集器物件作為資料層的一部分，請在路徑中使用點記號來參照您要擷取到資料元素中的物件和屬性，例如 `_myData.pageName`，或 `digitalData.pageName`、等等。

#### 示例：

`window.document.title`

### 本地存储

在 Local Storage Item Name 字段中提供本地存储项目的名称。

本地存储允许浏览器将信息从一个页面存储到另一个页面 ([https://www.w3schools.com/html/html5\_webstorage.asp](https://www.w3schools.com/html/html5_webstorage.asp))。本地存储的工作方式与 Cookie 非常类似，只是其存储空间更大，存储方式更灵活。

使用提供的字段指定您为本地存储项目创建的值，例如 `lastProductViewed.`

### 合併的物件

選取每個都會提供物件的多個資料元素。 這些物件將深層（遞回）合併在一起，以產生新物件。 將不會修改來源物件。 如果在多個來源物件的相同位置找到屬性，將使用後一個物件的值。 如果來源屬性值是 `undefined`，不會覆寫先前來源物件的值。 如果在多個來源物件上的相同位置找到陣列，則會串連陣列。

例如，假設您選取的資料元素提供下列物件：

```
{
  "sport": {
    "name": "tennis"
  },
  "dessert": "ice cream",
  "fruits": [
    "apple",
    "banana"
  ]
}
```

假設您也選取另一個提供下列物件的資料元素：

```
{
  "sport": {
    "name": "volleyball"
  },
  "dessert": undefined,
  "pet": "dog",
  "instrument": undefined,
  "fruits": [
    "cherry",
    "duku"
  ]
}
```

「合併的物件」資料元素的結果會是下列物件：

```
{
  "sport": {
    "name": "volleyball"
  },
  "dessert": "ice cream",
  "pet": "dog",
  "instrument": undefined,
  "fruits": [
    "apple",
    "banana",
    "cherry",
    "duku"
  ]
}
```

### 页面信息

使用这些数据点捕获页面信息，以将其用在规则逻辑中，或者将信息发送到 Analytics 或外部跟踪系统。

您可以选择以下任一页面属性，以将其用在数据元素中：

* URL
* 主机名
* 路径名
* 协议
* 反向链接
* 标题

### 查询字符串参数

在 URL Parameter 字段中指定单个 URL 参数。

只有名称部分是必需提供的，并且应该忽略任何特殊标志符，例如“?”或“=”

#### 示例：

`contentType`

### 随机数

使用此数据元素可生成一个随机数。它通常用於取樣資料或建立ID，例如點選ID。 随机数也可用于对敏感数据进行模糊或加盐处理。一些示例可能包括：

* 生成点击 ID
* 将数字连接到用户令牌或时间戳以确保唯一性
* 对 PII 数据执行单向哈希处理
* 随机确定在网站上显示调查请求的时间

指定随机数的最小值和最大值。

**默认值：**

最小值：0

最大值：1000000000

### 会话存储

在 Session Storage Item Name 字段中提供会话存储项目的名称。

会话存储类似于本地存储，不同之处在于，会话存储在会话结束后会丢弃数据，而本地存储或 Cookie 则可以保留数据。

### 访客行为

與「頁面資訊」類似，此資料元素會使用常見行為型別，在規則和其他平台解決方案中擴充邏輯。

选择以下任一访客行为属性：

* 登陆页面
* 流量源
* 网站逗留分钟数
* 会话计数
* 会话页面查看计数
* 存留期页面查看计数
* 是新访客

一些常见用例包括：

* 当访客在网站上停留五分钟后，显示调查结果
* 如果访问的是登陆页面，则填充 Analytics 量度
* 在 X 个会话计数后向访客显示新选件
* 如果访客是首次来访访客，则显示新闻稿注册页面

### 條件值

的包裝函式 [值比較](#value-comparison-value-comparison) 條件。 根據比較的結果，將會傳回表單中兩個可用值之一。 因此可以處理「如果……然後……否則……」無需額外規則的情況。

### 執行階段環境

可讓您選取下列其中一個變數：

* 環境階段 — 回訪 `_satellite.environment.stage` 以區分開發/測試/生產環境。
* 程式庫建置日期 — 傳回 `turbine.buildInfo.buildDate` 包含相同值，例如 `_satellite.buildInfo.buildDate`.
* 屬性名稱 — 傳回 `_satellite.property.name` 以取得Launch屬性的名稱。
* 屬性ID — 傳回 `_satellite.property.id` 以取得Launch屬性的ID
* 規則名稱 — 傳回 `event.$rule.name` 包含已執行規則的名稱。
* 規則ID — 傳回 `event.$rule.id` 包含已執行規則的ID。
* 事件型別 — 傳回 `event.$type` 包含觸發規則之事件的型別。
* 事件詳細資料裝載 — 傳回 `event.detail` 包含自訂事件或直接呼叫規則的裝載。
* 直接呼叫識別碼 — 傳回 `event.identifier` 包含直接呼叫規則的識別碼。

### 裝置屬性

傳回下列其中一個訪客裝置屬性：

* 瀏覽器視窗大小
* 熒幕大小

### JavaScript工具

它是常見JavaScript作業的包裝函式。 它會接收資料元素作為輸入。 它會傳回資料元素值的下列其中一個轉換的結果：

* 基本字串操作（取代、子字串、規則運算式相符、第一個和最後一個索引、分割、切片）
* 基本陣列作業（切片、連線、彈出、移位）
* 基本通用作業（切片、長度）