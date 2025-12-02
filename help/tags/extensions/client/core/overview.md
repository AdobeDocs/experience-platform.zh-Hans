---
title: 核心扩展概述
description: 了解Adobe Experience Platform中的核心标记扩展。
exl-id: 841f32ad-a6a8-49fb-a131-ef4faab47187
source-git-commit: c76b64e76229db8f9da544a79aed903a134f7351
workflow-type: tm+mt
source-wordcount: '5425'
ht-degree: 62%

---

# 核心扩展概述

>[!NOTE]
>
>经过品牌重塑，Adobe Experience Platform Launch 已变为 Adobe Experience Platform 中的一套数据收集技术。因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

核心标记扩展是随Adobe Experience Platform一起发布的默认扩展。

本文档提供了有关使用核心扩展构建规则时可用的选项的信息。

## 核心扩展事件类型 {#core-extension-event-types}

本主题介绍核心扩展中可用的事件类型。 有关可以为多个不同事件类型设置的选项的信息，请参阅[选项](#options)部分。

### 基于浏览器的事件

#### Tab Blur

当选项卡失去焦点时，选项卡模糊事件会触发该操作。 没有适用于此事件类型的设置。

#### Tab Focus

选项卡聚焦事件会在选项卡获得焦点时触发该操作。 没有适用于此事件类型的设置。

### 表单

#### Blur

当表单失去焦点时，模糊事件会触发该操作。 有关可自定义的事件设置的详细信息，请参阅[选项](#options)部分。

#### Focus

焦点事件会在表单获得焦点时触发该操作。 有关可自定义的事件设置的详细信息，请参阅[选项](#options)部分。

#### Submit

提交事件会在提交表单时触发该操作。 有关可自定义的事件设置的详细信息，请参阅[选项](#options)部分。

### 键盘控制事件

#### Key Press

按下某个键时会触发该事件。 有关可自定义的事件设置的详细信息，请参阅[选项](#options)部分。

### 基于媒体的事件

#### Media Ended

媒体结束时，将触发该事件。 有关可自定义的事件设置的详细信息，请参阅[选项](#options)部分。

#### Media-loaded Data

媒体加载数据时会触发该事件。 有关可自定义的事件设置的详细信息，请参阅[选项](#options)部分。

#### Media Pause

暂停媒体时会触发该事件。 有关可自定义的事件设置的详细信息，请参阅[选项](#options)部分。

#### Media Play

播放媒体时会触发该事件。 有关可自定义的事件设置的详细信息，请参阅[选项](#options)部分。

#### Media Stalled

媒体停止时会触发该事件。 有关可自定义的事件设置的详细信息，请参阅[选项](#options)部分。

#### Media-Time已播放

如果媒体已播放指定的时长，则会触发该事件。 您必须指定媒体必须播放的持续时间才能触发事件。 有关可自定义的事件设置的详细信息，请参阅[选项](#options)部分。


#### Media-Volume Changed

如果音量升高或降低，则会触发该事件。 有关可自定义的事件设置的详细信息，请参阅[选项](#options)部分。

### 面向移动设备的事件

#### Orientation Change

如果设备的方向发生更改，则会触发该事件。 您必须指定方向必须更改才能触发事件的持续时间。 没有适用于此事件类型的设置。

#### Zoom Change

如果用户执行放大或缩小操作，则会触发该事件。 没有适用于此事件类型的设置。

### 鼠标控制事件

#### Click

如果选择（单击）指定的元素，则会触发该事件。 （可选）您可以为元素指定在触发该事件之前必须为 true 的属性值。

如果元素是链接到内容的锚点标记(`<a>`)，则还可以指定是否将导航延迟一段时间。 如果您的规则需要额外的执行时间，并且在页面导航发生之前通常无法完成操作，则可以使用此选项。

>[!WARNING]
>
>使用此选项时应格外谨慎，因为如果使用不正确，它可能会对用户体验产生负面影响。

当您使用链接延迟时，Experience Platform实际上会阻止浏览器离开页面。 然后，在指定的超时后，它将执行JavaScript重定向到原始目标。 当页面标记具有`<a>`标记，且预期功能实际上未将用户导航到离开页面时，这尤其危险。 如果您无法以任何其他方式解决您的问题，则您应该极其准确地使用选择器定义，以便此事件将在您真正需要它的地方（而不是其他任何地方）触发。

默认的链接延迟值为100毫秒。 请注意，标记将始终等待指定的时间，不会以任何方式与规则操作的执行相关联。 延迟可能会强制用户等待的时间超过所需时间，也可能会延迟时间不足以成功完成规则的所有操作。 较长的延迟为规则执行提供了更多时间，但也加剧了用户体验。

要触发延迟，需要提供触发事件的选定元素以及触发事件之前的特定时间量。

有关高级选项，请参阅[选项](#options)部分以了解更多信息。

#### Hover

如果用户将鼠标悬停在指定的元素上，则会触发该事件。 您还必须配置规则是立即触发还是在指定的毫秒数之后触发。 有关可自定义的事件设置的详细信息，请参阅[选项](#options)部分。

### 其他事件

#### Custom Event

如果发生自定义事件类型，则会触发该事件。 在代码库中的其他位置定义的命名JavaScript函数可用作自定义事件类型。 必须指定自定义事件类型的名称并配置任何其他设置，如以下[选项](#options)部分中所述。

#### Data Element Changed

如果指定的数据元素发生更改，则会触发该事件。 必须提供数据元素的名称。 您可以在文本字段中键入数据元素的名称，或者选择文本字段右侧的数据元素图标，然后从显示的对话框中提供的列表中选择数据元素。

#### Direct Call {#direct-call-event}

直接调用事件绕过事件检测和查找系统。 直接调用规则最适合您希望准确告知系统当前发生事件的情况。 此外，它们还适用于系统无法检测到DOM中的事件的情况。

定义直接调用事件时，必须指定将用作此事件标识符的字符串。 如果触发了包含相同标识符的[触发直接调用操作](#direct-call-action)，则将运行任何侦听该标识符的直接调用事件规则。

![数据收集UI中直接调用事件的屏幕截图](../../../images/extensions/client/core/direct-call-event.png)

#### Element Exists

如果存在指定的元素，则会触发该事件。 有关可自定义的事件设置的详细信息，请参阅[选项](#options)部分。

#### Enters Viewport

如果用户进入指定的视区，则会触发该事件。 必须提供CSS选择器作为定位匹配元素的条件。 您还必须配置规则是立即触发还是在指定的毫秒数后触发，以及事件是应在每次事件发生时触发，还是只应在第一次发生时触发。

有关可自定义的事件设置的详细信息，请参阅[选项](#options)部分。

#### History Change

如果发生pushState或hashchange事件，则会触发该事件。 没有适用于此事件类型的设置。

#### 页面逗留时间

如果用户在页面上停留指定的秒数，则会触发该事件。 必须指定触发事件之前必须经过的秒数。

### 页面加载事件

#### DOM Ready

当DOM就绪时，将触发该事件，用户可以与页面进行交互。 没有适用于此事件类型的设置。

#### Library Loaded (Page Top) {#library-loaded-page-top}

加载标记库后，就会触发事件。 没有适用于此事件类型的设置。

#### Page Bottom {#page-bottom}

调用`_satellite.pageBottom();`后，将触发该事件。 异步加载标记库时，不应使用此事件类型。 没有适用于此事件类型的设置。

#### Window Loaded

当浏览器调用了onLoad并且页面加载完成时，会触发事件。 没有适用于此事件类型的设置。

### 选项 {#options}

每个表单事件类型都使用以下设置：

#### Specific Elements \| Any Element

* 如果选择 **[!UICONTROL Specific Elements]**，则会显示用于选择元素和属性值的选项。
* 如果选择 **[!UICONTROL Any Element]**，则无需显示其他选项来缩小元素范围。

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

此部分介绍核心扩展中可用的条件类型。 这些条件类型可以与常规或例外逻辑类型一起使用。

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
>自定义代码现在支持ES6+ JavaScript。 请注意，某些较旧的浏览器不支持ES6+。 要了解使用ES6+函数的影响，请针对所有应受支持的Web浏览器进行测试。

使用内置代码编辑器输入自定义代码：

1. 选择 **[!UICONTROL Open Editor]**。
1. 键入自定义代码。
1. 选择 **[!UICONTROL Save]**。

将自动提供一个名为 `event` 的变量，您可以从自定义代码中引用该变量。`event` 对象将包含有关触发规则的事件的有用信息。确定哪些事件数据可用的最简单方法是从自定义代码中将 `event` 记录到控制台：

```javascript
console.log(event);
return true;
```

在浏览器中运行规则，并在浏览器控制台中检查已记录的事件对象。了解了哪些信息可用后，您便可以将其用于自定义代码中的程序化决策。

*条件排序*

启用属性设置中的“按顺序运行规则组件”选项后，您可以在执行异步任务时，让后续规则组件等待。

当条件返回[承诺](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)时，直到返回的承诺得到解析后才会执行规则中的下一个条件。如果承诺被拒绝，标记会将该条件视为失败，且不会执行该规则的其他条件或操作。

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
>自定义代码现在支持ES6+ JavaScript。 请注意，某些较旧的浏览器不支持ES6+。 要了解使用ES6+函数的影响，请针对所有应受支持的Web浏览器进行测试。

提供在触发事件并评估条件后运行的代码。

1. 命名操作代码。
1. 选择用于定义操作的语言：
   * JavaScript
   * HTML
1. 选择是否要全局执行操作代码。
1. 选择 **[!UICONTROL Open Editor]**。
1. 编辑代码，然后选择 **[!UICONTROL Save]**。

选择 JavaScript 作为语言时，将自动提供一个名为 `event` 的变量，您可以从自定义代码中引用该变量。`event` 对象将包含有关触发规则的事件的有用信息。确定哪些事件数据可用的最简单方法是从自定义代码中将 `event` 记录到控制台：

```javascript
console.log(event);
```

在浏览器中运行规则，并在浏览器控制台中检查已记录的事件对象。了解哪些信息可用后，您便可以将其用于自定义代码中的程序化决策，将一段 `event` 对象发送到服务器等。

### Custom Code 操作处理

适用于所有Adobe Experience Platform用户的核心扩展包含用于执行用户提供的JavaScript或HTML的Custom Code操作。 通常，了解如何处理具有 Custom Code 操作的规则对用户很有用。

#### 使用 page top 或 page bottom 事件的规则

自定义操作的代码会嵌入在主标记库中。 该代码将使用 document.write 写入文档。如果规则具有多个 Custom Code 操作，则该代码将按规则中配置的顺序写入。

#### 使用除 page top 或 page bottom 以外的任何事件的规则

自定义操作的代码将从服务器加载并使用 [Postscribe](https://github.com/krux/postscribe) 写入文档。如果规则具有多个 Custom Code 操作，则该代码将从服务器并行加载，但会按照规则中配置的顺序写入。

虽然在加载页面后使用 document.write 通常会出现问题，但对于通过 Custom Code 操作提供的代码来说，这并不是问题。无论何时执行代码，您都可以在 Custom Code 操作中使用 document.write。

#### 自定义代码验证

标记代码编辑器中使用的验证器可识别开发人员编写的代码中存在的问题。 经过缩小的代码（例如从代码管理器中下载的 AppMeasurement.js 代码）可能会被 验证器错误地标记为存在问题，这通常可以忽略不计。

#### 操作排序

启用属性设置中的“按顺序运行规则组件”选项后，您可以在操作执行异步任务时，让后续规则组件等待。  对于 JavaScript 和 HTML 自定义代码，这项操作的原理有所不同。

*JavaScript*

创建 JavaScript 自定义代码操作时，您可以从操作返回[承诺](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)。规则中的下一项操作将仅在返回的承诺得到解析后才执行。如果承诺被拒绝，则不会执行规则中的后续操作。

>[!NOTE]
>
>仅当JavaScript未设置为全局执行时，这项操作才起作用。 如果您正在全局范围内执行自定义代码操作，标记会将承诺视为立即解析，并转到处理队列中的下一个项目。

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

创建 HTML 自定义代码操作时，可在自定义代码中使用名为 `onCustomCodeSuccess()` 的函数。您可以调用此函数来指示您的自定义代码已完成，并且标记可能会继续执行后续操作。 另一方面，如果您的自定义代码以某种方式失败，您可以调用 `onCustomCodeFailure()`。它会通知标记不要执行该规则中的后续操作。

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

### 触发直接调用 {#direct-call-action}

此操作会触发所有使用特定[直接调用事件](#direct-call-event)的规则。 在配置操作时，必须提供要触发的直接调用事件的标识符字符串。 或者，您也可以通过`detail`对象将数据传递到直接调用事件，该对象可以包含一组自定义的键值对。

![数据收集UI中触发器直接调用操作的屏幕截图](../../../images/extensions/client/core/direct-call-action.png)

此操作直接映射到[`_satellite.track()`](/help/collection/tags/track.md)。

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
>自定义代码现在支持ES6+ JavaScript。 请注意，某些较旧的浏览器不支持ES6+。 要了解使用ES6+函数的影响，请针对所有应受支持的Web浏览器进行测试。

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

标记数据元素可用于捕获标记的JavaScript变量或对象属性。 随后，您可以通过引用标记数据元素，在扩展或自定义规则中使用这些值。 如果数据源发生更改，则只需更新对该源的引用即可。

在以下示例中，标记包含一个名为`Page_Name`的JavaScript变量。

```markup
<script>
  //data layer
  var Page_Name = "Homepage"
</script>
```

在创建数据元素时，只需提供该变量的路径。

如果您使用数据收集器对象作为数据层的一部分，请在路径中使用点表示法来引用要捕获到数据元素中的对象和属性，如`_myData.pageName`或`digitalData.pageName`等。

#### 示例：

`window.document.title`

### 本地存储

在 Local Storage Item Name 字段中提供本地存储项目的名称。

本地存储允许浏览器将信息从一个页面存储到另一个页面 ([https://www.w3schools.com/html/html5\_webstorage.asp](https://www.w3schools.com/html/html5_webstorage.asp))。本地存储的工作方式与 Cookie 非常类似，只是其存储空间更大，存储方式更灵活。

使用提供的字段指定您为本地存储项目创建的值，例如 `lastProductViewed.`

### 合并的对象

选择多个数据元素，每个元素都会提供对象。 这些对象将深层（递归）地合并在一起，以生成一个新的对象。 将不会修改源对象。 如果在多个源对象的同一位置找到属性，则将使用后一个对象的值。 如果源属性值是`undefined`，则它不会覆盖先前源对象的值。 如果在多个源对象上的同一位置找到数组，则这些数组将连接在一起。

例如，假设您选择的数据元素提供了以下对象：

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

假定您还选择另一个提供以下对象的数据元素：

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

合并对象数据元素的结果会是以下对象：

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

在 Session Storage Item Name 字段中提供会话存储项目的名称。

会话存储类似于本地存储，不同之处在于，会话存储在会话结束后会丢弃数据，而本地存储或 Cookie 则可以保留数据。

### 访客行为

与页面信息类似，此数据元素使用常见行为类型来扩充规则和其他Experience Platform解决方案中的逻辑。

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
* 在 X 个会话计数后向访客显示新产品建议
* 如果访客是首次来访访客，则显示新闻稿注册页面

### 条件值

[Value Comparison](#value-comparison-value-comparison)条件的包装器。 根据比较的结果，将在表单中返回两个可用值之一。 因此可以处理“如果……那么……否则……”无需额外规则的情况。

### 运行时环境

允许您选择以下变量之一：

* 环境暂存 — 返回`_satellite.environment.stage`以区分开发/暂存/生产环境。
* 库生成日期 — 返回包含相同值（如`turbine.buildInfo.buildDate`）的`_satellite.buildInfo.buildDate`。
* 属性名称 — 返回`_satellite.property.name`以获取Launch属性的名称。
* 属性ID — 返回`_satellite.property.id`以获取Launch属性的ID
* 规则名称 — 返回包含已执行规则名称的`event.$rule.name`。
* 规则ID — 返回包含已执行规则ID的`event.$rule.id`。
* 事件类型 — 返回包含触发规则的事件类型的`event.$type`。
* 事件详细信息有效负载 — 返回包含自定义事件或直接调用规则有效负载的`event.detail`。
* 直接调用标识符 — 返回包含直接调用规则标识符的`event.identifier`。

### 设备属性

返回以下其中一个访客设备属性：

* 浏览器窗口大小
* 屏幕大小

### JavaScript Tools

它是常用JavaScript操作的包装器。 它接收数据元素作为输入。 它会返回数据元素值的以下转换之一的结果：

* 基本字符串操作（替换、子字符串、正则表达式匹配、第一个和最后一个索引、拆分、切片）
* 基本阵列操作（切片、连接、pop、shift）
* 基本通用操作（切片、长度）