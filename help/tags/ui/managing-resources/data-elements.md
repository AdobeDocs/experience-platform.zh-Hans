---
title: 数据元素
description: 数据元素是数据字典（或数据映射）的构建块。使用数据元素可跨市场营销和广告技术收集、组织和交付数据。
exl-id: 1e7b03cc-5a54-403d-bf8d-dbc206cfeb2d
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1549'
ht-degree: 75%

---

# 数据元素

数据元素是数据字典（或数据映射）的构建块。使用数据元素可跨市场营销和广告技术收集、组织和交付数据。

单个数据元素是一个变量，其值可以映射到查询字符串、URL、Cookie 值、JavaScript 变量等。您可以在整个Adobe Experience Platform中通过其变量名称引用此值。 此数据元素集合将成为可用于构建规则（事件、条件和操作）的已定义数据的字典。此数据字典可在标记之间共享，以便与您添加到资产中的任何扩展一起使用。

>[!IMPORTANT]
>
>所做的更改在[发布](../publishing/overview.md)之后才会生效。

在创建规则的整个过程中，要尽可能广泛地使用数据元素，以统一动态数据的定义，并提高标记过程的效率。您只需定义数据规则一次，以后便可以在多个位置使用。

可重用数据元素的概念非常强大，您应该将它们作为最佳实践使用。

例如，如果您通过特定方式引用页面名称或产品ID，或从联盟营销链接或[!DNL AdWords]中的查询字符串参数获取信息，等等，则可以通过以下方式创建数据字典（数据元素）：从其源中获取信息，然后在各种标记规则中使用该数据。

使用页面名称为例，假设您通过引用数据层、`document.title` 元素或网站中的标题标记来使用特定的页面名称架构。Adobe Experience Platform中的标记允许您将数据元素创建为该特定数据点的单一引用点。 之后，您可以在需要引用该页面名称的任意规则中使用此数据元素。如果在未来出于某些原因，您决定更改引用页面名称的方式（例如，您已经引用了 `document.title`，但现在希望引用某个特定数据层），那么要更改该引用，您无需编辑多个不同的规则。只需在数据元素中更改引用一次，引用该数据元素的所有规则都会自动更新。

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

1. 在资产页面中，打开 [!UICONTROL Data Elements] 选项卡，然后选择 **[!UICONTROL Create New Data Element]**。
1. 命名数据元素。
1. 选择扩展和类型。

   可用的数据元素类型由扩展决定。有关核心标记扩展可用类型的信息，请参阅[数据元素类型](data-elements.md#types-of-data-elements)。

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
      * 该值会无限期地存储在浏览器的本地存储中。

1. 选择 **[!UICONTROL Save]**。

创建或编辑元素后，您可以将其保存并生成到[活动库](../publishing/libraries.md#active-library)。这会立即将更改保存到库并执行生成操作。随即会显示生成操作的状态。您还可以从[!UICONTROL Active Library]下拉菜单中创建新库。

## 数据元素类型 {#types-of-data-elements}

>[!NOTE]
>
>数据元素类型由扩展决定。对于可创建的类型，没有任何限制。

以下部分介绍&#x200B;**核心扩展**&#x200B;中可用的数据元素类型。 其他扩展则使用其他数据元素类型。

### Cookie

可在“Cookie 名称”字段中提及任何可用的域 Cookie。

#### 示例：

`cookieName`

### 自定义代码

通过选择 [!UICONTROL Open Editor] 并将代码插入编辑器窗口，可以将自定义 JavaScript 输入到用户界面中。

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

自定义代码可以接受调用规则中的 `event` 对象作为参数。这将允许代码读取其中的值。

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

使用百分比(`%`)语法时，您只需指定数据元素名称。 而无需指定 `event`。

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

如果要收集标记中的JavaScript变量或对象属性并将它们与任何扩展或规则一起使用，则可以使用数据元素来捕获这些值。 这样，您就可以在整个规则中引用数据元素，并且如果数据源发生更改，您只需在一个位置更改对该源（数据元素）的引用即可。

例如，假定您的标记包含一个名为 `Page_Name` 的 JavaScript 变量，如下所示：

```markup
<script>
  //data layer
  var Page_Name = "Homepage"
</script>
```

在创建数据元素时，必须提供该变量的路径。

如果您使用数据收集器对象作为数据层的一部分，则只需在路径中使用点表示法来引用要捕获到数据元素中的对象和属性即可，如`_myData.pageName`或`digitalData.pageName`等。

#### 示例：

`window.document.title`

### 本地存储

在 [!UICONTROL Local Storage Item Name] 字段中提供本地存储项目的名称。

本地存储允许浏览器将信息从一个页面存储到另一个页面 ([https://www.w3schools.com/html/html5\_webstorage.asp](https://www.w3schools.com/html/html5_webstorage.asp))。本地存储的工作方式与Cookie非常相似，但更大也更加灵活。

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

在 [!UICONTROL URL Parameter] 字段中指定单个 URL 参数。

只有名称部分是必需提供的，并且应该忽略任何特殊标志符，例如“?”或“=”

#### 示例：

`contentType`

### 随机数

使用此数据元素可生成一个随机数。随机数通常用于对数据采样或创建ID，例如点击ID。 随机数也可用于对敏感数据进行模糊或加盐处理。一些示例可能包括：

* 生成点击 ID
* 将数字连接到用户令牌或时间戳以确保唯一性
* 对 PII 数据执行单向哈希处理
* 随机确定在网站上显示调查请求的时间

指定随机数的最小值和最大值。

**默认值：**

最小值：0

最大值：1000000000

### 会话存储

在 [!UICONTROL Session Storage Item Name] 字段中提供会话存储项目的名称。

会话存储类似于本地存储，不同之处在于，会话存储在会话结束后会丢弃数据，而本地存储或 Cookie 则可以保留数据。

### 访客行为

与页面信息类似，此数据元素使用常见行为类型来扩充规则或其他Experience Platform解决方案中的逻辑。

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
* 在 X 个会话计数后向访客显示新产品建议
* 如果访客是首次来访访客，则显示新闻稿注册

## 内置数据元素

如果您之前使用过以下任何数据元素，则必须创建其他自定义数据元素：

* URI
* 协议
* 主机名
