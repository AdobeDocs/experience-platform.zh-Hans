---
title: Google数据层扩展
description: 了解Adobe Experience Platform中的Google客户端数据层标记扩展。
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: 9c608f69f6ba219f9cb4e938a77bd4838158d42c
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 1%

---

# Google数据层扩展

Google数据层扩展允许您在标记实施中使用Google数据层。 该扩展可以单独或同时与Google解决方案和Google的开放源一起使用 [数据层助手库](https://github.com/google/data-layer-helper).

帮助程序库提供与Adobe客户端数据日期(ACDL)类似的事件驱动功能。 Google数据层扩展的数据元素、规则和操作提供了与 [ACDL扩展](../client-data-layer/overview.md).

## 期限

版本1.2.x是一个较晚的测试版，正在生产中使用。

## 安装

要安装该扩展，请在数据收集UI中导航到扩展目录，然后选择 **[!UICONTROL Google数据层]**.

安装后，该扩展会在每次加载Adobe Experience Platform标记库时创建或访问数据层。

## 扩展视图

扩展配置可用于定义扩展所使用的数据层名称。 如果在加载Adobe Experience Platform标记时不存在具有已配置名称的数据层，则扩展将创建一个数据层。

数据层名称默认为Google默认名称 `dataLayer`.

>[!NOTE]
>
>无论是先加载Google代码还是Adobe代码并创建数据层，都无关紧要。 两个系统的行为都相同 — 如果数据层不存在，则创建数据层，或者使用现有数据层。

## 事件

>[!NOTE]
>
>词 _事件_ 在Adobe Experience Platform标记中使用事件驱动的数据层时，会过载。 _事件_ 可以是：
> - Adobe Experience Platform标记事件（已加载库等）。
> - JavaScript事件。
> - 通过 _事件_ 关键词。


利用扩展，可以侦听数据层上的更改。

>[!NOTE]
>
>了解 _事件_ 关键字。 的 _事件_ 关键字会更改Google数据层的行为，因此也会更改此扩展。\
> 如果您不确定此点，请阅读Google文档或进行研究。

### 监听所有向数据层推送的内容

如果选择此选项，则事件侦听器将侦听对数据层所做的任何更改。

### 监听排除事件的推送消息

如果选择此选项，则事件侦听器将侦听向数据层的任何数据推送，不包括事件。

监听器将跟踪以下推送事件示例：

```js
dataLayer.push({"data":"something"})
```

监听器不会跟踪以下推送事件示例：

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### 侦听所有事件

如果选择此选项，则事件侦听器将侦听推送到数据层的任何事件。

监听器将跟踪以下推送事件示例：

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

监听程序不会跟踪以下示例推送事件：

```js
dataLayer.push({"data":"something"})
```

### 侦听特定事件

在指定事件的情况下，事件侦听器会跟踪与特定字符串匹配的任何事件。

例如，设置 `myEvent` 使用此配置时，侦听器将只跟踪以下推送事件：

```js
dataLayer.push({"event":"myEvent"})
```

(ECMAScript / JavaScript)正则表达式可用于匹配事件名称。

例如，设置“myEvent\d”将跟踪 `myEvent` 带数字(\d):

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## 操作

### 推送到数据层 {#push-to-data-layer}

该扩展提供了两个操作来将JSON推送到数据层；用于手动创建要推送的JSON的自由文本字段，以及从版本1.2.0开始的键值多字段对话框。

#### 自由文本JSON

利用自由文本操作，可以直接在JSON中使用数据元素。 在JSON编辑器中，数据元素应使用百分比表示法引用。 例如：`%dataElementName%`。

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

较新的键值多字段对话框是一个更加用户友好的界面，它允许无需手动编写JSON即可配置推送。

### Google DL重置为计算状态

扩展为您提供了用于重置数据层的操作。 如果在处理Google数据层更改的规则中使用，则数据层将在触发规则时重置为数据层的计算状态。 如果在不处理Google数据层更改的规则中使用操作，则该操作会清空数据层。

## 数据元素

提供的数据元素可在执行由Google数据层更改（推送事件）触发的规则期间使用，也可在不相关的规则（如Library Loaded）中使用。 在前一种情况下，数据元素返回在数据层发生更改时从计算状态获取的值。 在后一种情况下，使用规则执行时的计算状态。

切换开关允许您选择数据元素应从整个计算状态返回值，还是仅从事件信息返回值（如果在由数据层更改触发的规则中使用）。

因此，数据元素可以返回：

- 空字段：数据层计算状态。
- 具有键的字段（例如上面示例中的page.previous_url）：事件对象或计算状态中键的值。

## 其他信息

扩展的数据元素和事件对话框包含详细的使用信息和示例。

其他常规信息位于 [项目自述文件](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md)
