---
title: 数据元素
description: 数据元素是数据字典（或数据映射）的构建块。使用数据元素可跨市场营销和广告技术收集、组织和交付数据。
exl-id: 1e7b03cc-5a54-403d-bf8d-dbc206cfeb2d
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '1622'
ht-degree: 74%

---

# 数据元素

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

数据元素是数据字典（或数据映射）的构建块。使用数据元素可跨市场营销和广告技术收集、组织和交付数据。

单个数据元素是一个变量，其值可以映射到查询字符串、URL、Cookie 值、JavaScript 变量等。您可以在Adobe Experience Platform中透過變數名稱參照此值。 此数据元素集合将成为可用于构建规则（事件、条件和操作）的已定义数据的字典。此資料字典會在標籤之間共用，以搭配您新增至屬性的任何擴充功能使用。

>[!IMPORTANT]
>
>所做的更改在[发布](../publishing/overview.md)之后才会生效。

在创建规则的整个过程中，要尽可能广泛地使用数据元素，以统一动态数据的定义，并提高标记过程的效率。您只需定义数据规则一次，以后便可以在多个位置使用。

可重用数据元素的概念非常强大，您应该将它们作为最佳实践使用。

例如，如果您有特定方式來參考頁面名稱或產品ID，或從附屬機構行銷連結的查詢字串引數或來源抓取資訊 [!DNL AdWords]依此類推，您可以從資料字典的來源取得資訊，然後在各種標籤規則中使用此資料，藉此建立資料字典（資料元素）。

使用页面名称为例，假设您通过引用数据层、`document.title` 元素或网站中的标题标记来使用特定的页面名称模式。Adobe Experience Platform中的標籤可讓您將資料元素建立為該特定資料點的單一參考點。 之后，您可以在需要引用该页面名称的任意规则中使用此数据元素。如果在未来出于某些原因，您决定更改引用页面名称的方式（例如，您已经引用了 `document.title`，但现在希望引用某个特定数据层），那么要更改该引用，您无需编辑多个不同的规则。只需在数据元素中更改引用一次，引用该数据元素的所有规则都会自动更新。

>[!NOTE]
>
>如果某个数据元素没有在规则中引用，则它不会在任何页面上加载，除非在自定义脚本中被专门调用。

数据元素在规则中使用或在脚本中手动调用时会填充数据。在高级别时，您可以：

1. [创建一个数据元素](#create-a-data-element)（如果尚未创建）。
1. 在[规则](./rules.md)或自定义脚本中使用该数据元素。

## 使用数据元素

### 在规则中

您可以在规则编辑界面中通过使用搜索框查找数据元素的名称来使用数据元素。

### 在自定义脚本中

您可以在自定义脚本中通过使用 `_satellite` 对象语法来使用数据元素：

`_satellite.getVar('data element name');`

## 创建数据元素 {#create-a-data-element}

数据元素是规则的构建块。数据元素可用于创建页面上常用项目的数据字典（或数据映射），而无需考虑网站中所包含对象的项目源自何处（查询字符串、URL 或 Cookie 值）。

1. 從「屬性」頁面，開啟 [!UICONTROL 資料元素] 索引標籤，然後選取 **[!UICONTROL 建立新資料元素]**.
1. 命名数据元素。
1. 选择扩展和类型。

   可用的数据元素类型由扩展决定。如需核心標籤擴充功能可用型別的相關資訊，請參閱 [資料元素型別](data-elements.md#types-of-data-elements).

1. 在提供的字段中提供任何请求的有关所选类型的信息。
1. （可选）输入默认值。

   如果不选择此选项，则不存在默认值。大多数用户将其保留为默认状态。不同的系统处理空变量的方式各不相同。有些人选择输入“none”或“N/A”等内容，以便当数据元素不返回值时，创建内容一致的报表。

1. 选择是否强制使用小写值以及是否移除换行符和空格。
1. 选择持续时间。

   可用的选项包括：

   * None
      * 不会存储该值。
   * Page view
      * 该值会持续保留在 JavaScript 变量中，直到刷新页面或加载新页面为止。
      * 可以在脚本中使用 `_satellite` 对象语法进行创建和设置：

         `_satellite.setVar('data_element_name')`
   * Session
      * 该值会持续保留在浏览器的会话存储中，直到浏览器选项卡关闭为止。
      * 在整个站点访问期间均可用。
   * Visitor
      * 此值會無限期儲存在瀏覽器的本機儲存空間中。

1. 选择&#x200B;**[!UICONTROL 保存]**。

创建或编辑元素后，您可以将其保存并生成到[活动库](../publishing/libraries.md#active-library)。这会立即将更改保存到库并执行生成操作。随即会显示生成操作的状态。您也可以從以下專案建立新程式庫： [!UICONTROL 使用中程式庫] 下拉式清單。

## 数据元素类型 {#types-of-data-elements}

数据元素类型由扩展决定。对于可创建的类型，没有任何限制。

以下部分介绍核心扩展中可用的数据元素类型。其他扩展则使用其他数据元素类型。

### Cookie

可在“Cookie 名称”字段中提及任何可用的域 Cookie。

#### 示例：

`cookieName`

### 自定义代码

在UI中選取以下專案可輸入自訂JavaScript：  [!UICONTROL 開啟編輯器] 和將程式碼插入編輯器視窗中。

编辑器窗口中需要一个返回语句，以指示应该将什么值设置为数据元素值。如果不包含返回语句，数据元素则解析为 `undefined`。这会触发回退去查找存储的值，如果没有存储的值，则使用默认值。

**示例：**

```text
var pageType = $('div.page-wrapper').attr('class').split('')[1];
if (window.location.pathname == '/') {
  return 'homepage';
} else {
  return pageType;
}
```

自定义代码可以接受调用规则中的 `event` 对象作为参数。如此可讓程式碼讀取該處的值。

**示例：**

```text
// `event` is the default object provided by the rule
var eventType = event.$type;
return eventType; // if this data element is called from a "DOM Ready" event, then `core.dom-ready` is returned
```

然后，您可以在自定义脚本中通过使用 `_satellite` 对象语法来使用此数据元素：

```javascript
// event refers to the calling rule's event
var rule = _satellite.getVar('return event rule', event);
```

使用百分比(`%`)語法，您只需要指定資料元素名稱。 而无需指定 `event`。

```text
%data element name%
```

### DOM 属性

可以检索任何元素值，例如 div 或 H1 标记。

#### 示例：

CSS 选择器链：

`id#dc logo img`

获取以下元素的值：

`src`

### JavaScript 变量

可以使用路径字段引用任何可用的 JavaScript 对象或变量。

如果您想在標籤中收集JavaScript變數或物件屬性，並將它們與任何擴充功能或規則搭配使用，資料元素可用來擷取這些值。 這樣的話，您可以在全部規則中參照資料元素，而如果資料來源有所變更，您只需在一個位置變更來源的參照（資料元素）即可。

例如，假定您的标记包含一个名为 `Page_Name` 的 JavaScript 变量，如下所示：

```markup
<script>
  //data layer
  var Page_Name = "Homepage"
</script>
```

建立資料元素時，您必須提供該變數的路徑。

如果您使用数据收集器对象作为数据层的一部分，则只需在路径中使用点表示法来引用要捕获到数据元素中的对象和属性即可，如 `_myData.pageName` 或 `digitalData.pageName` 等。

#### 示例：

`window.document.title`

### 本地存储

在「 」中提供本機儲存專案的名稱 [!UICONTROL 本機儲存體專案名稱] 欄位。

本地存储允许浏览器将信息从一个页面存储到另一个页面 ([https://www.w3schools.com/html/html5\_webstorage.asp](https://www.w3schools.com/html/html5_webstorage.asp))。本機儲存的運作方式與Cookie非常類似，但更大也更有彈性。

使用提供的字段指定您为本地存储项目创建的值，例如 `lastProductViewed.`

### 页面信息

使用这些数据点捕获页面信息，以将其用在规则逻辑中，或者将信息发送到 [!DNL Analytics] 或外部跟踪系统。

您可以选择以下任一页面属性，以将其用在数据元素中：

* URL
* 主机名
* 路径名
* 协议
* 反向链接
* 标题

### 查询字符串参数

在中指定單一URL引數 [!UICONTROL URL引數] 欄位。

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

在「 」中提供您工作階段儲存專案的名稱 [!UICONTROL 工作階段儲存體專案名稱] 欄位。

会话存储类似于本地存储，不同之处在于，会话存储在会话结束后会丢弃数据，而本地存储或 Cookie 则可以保留数据。

### 访客行为

與「頁面資訊」類似，此資料元素會使用常見行為型別，在規則或其他Platform解決方案中擴充邏輯。

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
* 如果访问的是登陆页面，则填充 [!DNL Analytics] 量度
* 在 X 个会话计数后向访客显示新选件
* 如果這是首次訪客，則顯示電子報註冊

## 内置数据元素

如果您先前曾使用下列任何資料元素，則必須建立其他自訂資料元素：

* URI
* 协议
* 主机名
