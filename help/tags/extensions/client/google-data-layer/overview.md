---
title: Google数据层扩展
description: 了解Adobe Experience Platform中的Google Client Data Layer标记扩展。
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: c61afdc2c3df98a0ef815d7cb034ba2907c52908
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 0%

---

# Google数据层扩展

Google数据层扩展允许您在标记实施中使用Google数据层。 该扩展可以独立使用，也可以与Google解决方案和Google的开源同时使用 [数据层帮助程序库](https://github.com/google/data-layer-helper).

帮助程序库提供了与Adobe客户端数据层(ACDL)类似的事件驱动功能。 Google数据层扩展的数据元素、规则和操作提供了与 [ACDL扩展](../client-data-layer/overview.md).

## 安装

要安装扩展，请导航到数据收集UI中的扩展目录，然后选择 **[!UICONTROL Google Data Layer]**.

安装后，扩展会在每次加载Adobe Experience Platform Tags库时创建或访问数据层。

## 扩展视图

扩展配置可用于定义扩展所使用的数据层的名称。 如果在加载Adobe Experience Platform Tags时不存在具有已配置名称的数据层，则扩展将创建一个数据层。

数据层名称默认为Google默认名称 `dataLayer`.

>[!NOTE]
>
>无论是Google还是Adobe代码先加载并创建数据层，这都无关紧要。 两个系统的行为相同 — 如果数据层不存在则创建数据层，或者使用现有的数据层。

## 活动

>[!NOTE]
>
>单词 _事件_ 在Adobe Experience Platform Tags中使用事件驱动的数据层时，将会过载。 _活动_ 可以是：
> - Adobe Experience Platform Tags事件（Library Loaded等）。
> - JavaScript事件。
> - 使用推送至数据层的数据 _事件_ 关键字。

通过扩展，您可以侦听数据层上的更改。

>[!NOTE]
>
>了解如何使用 _事件_ 关键字，这与将Adobe客户端数据层推送到Google数据层类似。 此 _事件_ 关键字会更改Google数据层的行为，因此也会更改此扩展。\
> 请阅读Google文档，如果不确定这一点，请做调查。

### Google事件类型

Google支持两种推送事件的方法：使用Google Tag Manager `push()` 方法和Google Analytics4，使用 `gtag()` 方法。

Google Data Layer 1.2.1之前的扩展版本仅支持由创建的事件 `push()`，如本页上的代码示例中所示。

版本1.2.1及更高版本支持使用创建的事件 `gtag()`.  这是可选操作，可以在扩展配置对话框中启用。

有关详情 `push()` 和 `gtag()` 事件，请参见 [Google文档](https://developers.google.com/analytics/devguides/collection/ga4/reference/events?client_type=gtag).  扩展的“配置”和“规则”对话框中也提供了相关信息。

### 侦听所有对数据层的推送

如果选择此选项，事件侦听器将侦听对数据层所做的任何更改。

### 监听不包括事件的推送

如果选择此选项，事件侦听器将侦听任何将数据推送到数据层的操作，不包括事件。

监听程序将跟踪以下示例推送事件：

```js
dataLayer.push({"data":"something"})
```

监听程序将不会跟踪以下示例推送事件：

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### 侦听所有事件

如果选择此选项，事件侦听器将侦听推送到数据层的任何事件。

监听程序将跟踪以下示例推送事件：

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

监听程序将不会跟踪以下示例推送事件：

```js
dataLayer.push({"data":"something"})
```

### 侦听特定事件

如果指定事件，则事件侦听器会跟踪与特定字符串匹配的任何事件。

例如，设置 `myEvent` 使用此配置时，会导致侦听器仅跟踪以下推送事件：

```js
dataLayer.push({"event":"myEvent"})
```

可以使用(ECMAScript / JavaScript)正则表达式来匹配事件名称。

例如，设置“myEvent\d”将跟踪 `myEvent` 带数字(\d)：

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## 操作

### 推送到Data Layer {#push-to-data-layer}

扩展提供了两个用于将JSON推送到数据层的操作：一个是自由文本字段，用于手动创建要推送的JSON；另一个是从1.2.0版推出的键值多字段对话框。

#### 自由文本JSON

利用自由文本操作，可以在JSON中直接使用数据元素。 在JSON编辑器中，应使用百分比表示法引用数据元素。 例如：`%dataElementName%`。

```json
{
  "page": {
    "url": "%url%",
    "previous_url": "%previous_url%",
    "concatenated_values": "static string %dataElement%"
  }
}
```

#### 键值多字段

较新的键值多字段对话框是一个更友好的界面，允许配置推送而不手动写入JSON。

### Google DL重置为已计算状态

扩展提供了重置数据层的操作。 如果在处理Google数据层更改的规则中使用，则数据层将重置为触发规则时数据层的计算状态。 如果操作在不处理Google数据层更改的规则中使用，则该操作会清空数据层。

## 数据元素

提供的数据元素可在执行Google数据层更改（推送事件）触发的规则期间或在不相关的规则（例如Library Loaded）中使用。 在前一种情况下，数据元素返回在数据层改变时从计算状态中取出的值。 在后一种情况下，使用规则执行时的计算状态。

切换开关允许您选择数据元素是应从整个计算状态返回值，还是仅从事件信息返回值（如果在由数据层更改触发的规则中使用）。

因此，数据元素可以返回：

- 空字段：数据层计算状态。
- 带键的字段（例如上面示例中的page.previous_url）：事件对象或计算状态中键的值。

## 其他信息

扩展的数据元素和事件对话框包含详细的使用信息和示例。

其他一般信息请参见 [项目自述文件](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md)
