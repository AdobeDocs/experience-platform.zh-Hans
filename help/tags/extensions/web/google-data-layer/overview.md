---
title: Google数据层扩展
description: 了解Adobe Experience Platform中的Google客户端数据层标记扩展。
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 0%

---

# Google Data Layer扩展（测试版）

>[!IMPORTANT]
>
>此扩展目前处于测试阶段，尚未在生产中经过充分测试。

Google数据层扩展允许您在标记实施中使用Google数据层。 该扩展可以单独或同时与Google解决方案和Google的开放源一起使用 [数据层助手库](https://github.com/google/data-layer-helper).

帮助程序库提供与Adobe客户端数据日期(ACDL)类似的事件驱动功能。 Google数据层扩展的数据元素、规则和操作提供了与 [ACDL扩展](../client-data-layer/overview.md).

## 期限

扩展的1.0.x版是测试版。 此扩展尚未在生产环境中经过完全测试。

## 安装

要安装该扩展，请导航到Experience PlatformUI或数据收集UI中的扩展目录，然后选择 **Google数据层**.

安装后，每次标记库加载到您的网站上时，该扩展都会创建或访问数据层。

## 扩展视图

配置扩展时(在安装扩展时或通过选择 **[!UICONTROL 配置]** 从扩展目录中)，您必须定义扩展使用的数据层名称。 如果在加载库时不存在具有已配置名称的数据层，则扩展将创建一个。

>[!NOTE]
>
>无论是先加载Google代码还是Adobe代码并创建数据层，都无关紧要。 两个系统都将创建数据层（如果不存在），或使用现有数据层。

默认情况下，数据层使用Google默认名称 `dataLayer`.

## 活动

扩展允许您监听数据层内的更改（事件）。 事件可以是以下任一事件：

* 标记事件（例如正在加载的库）
* JavaScript事件
* 通过 `event` 关键词。

了解 [`event` 关键词](https://developers.google.com/tag-platform/devguides/datalayer#use_a_data_layer_with_event_handlers) 将数据推送到Google数据层时，与Adobe客户端数据层类似。 的 `event` 关键字会更改Google数据层的行为，因此扩展的行为会相应地进行更新。

以下各节概述了扩展可侦听的不同事件类型。

### 监听所有向数据层推送的内容

如果选择此选项，扩展将侦听对数据层所做的任何更改。

### 监听排除事件的推送消息

如果选择此选项，扩展将侦听被推送到数据层的任何内容（不包括事件）。

监听程序将跟踪以下示例推送事件：

```js
dataLayer.push({"data":"something"})
```

监听器不会跟踪以下推送事件示例：

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### 侦听所有事件

如果选择此选项，则扩展将侦听推送到数据层的任何事件。

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

如果要侦听特定事件，请选择此选项，以便事件侦听器跟踪与特定字符串匹配的任何事件。

例如，设置 `myEvent` 使用此配置时，侦听器将只跟踪以下推送事件：

```js
dataLayer.push({"event":"myEvent"})
```

您还可以使用正则表达式字符串来匹配事件名称。 例如，设置 `myEvent\d` 将跟踪以 `myEvent` 后跟一个数字：

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## 操作

以下各节概述了扩展在包含在 [规则](../../../ui/managing-resources/rules.md).

### 推送到数据层 {#push-to-data-layer}

此操作可将JSON内容推送到数据层本身，从而可以直接在JSON负载中使用数据元素。 在提供的JSON编辑器中，您可以使用百分比表示法引用数据元素(例如， `%dataElementName%`)。

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

### Google DL重置为计算状态

>[!NOTE]
>
>此操作从v1.0.5开始可用。

此操作会重置数据层。 如果在处理Google数据层更改的规则中使用，则数据层将在触发规则时重置为数据层的计算状态。 如果在不处理Google数据层更改的规则中使用操作，则该操作会清空数据层。

## 数据元素

该扩展提供了一个使用键访问数据层的唯一数据元素(例如， `page.url` 在 [以上代码片段](#push-to-data-layer))。

数据元素可以提供以下任一内容：

* 数据层的特定值(例如， `page.url`)
* 整个数据层数组（空键字段）
* 使用键值(如果 `event` 关键词)
* 整个事件对象（空键字段）

扩展始终优先考虑事件信息。 如果数据层 `event` 会一直从该事件中读取值。 如果 `event` 不存在，则会从直接数据层读取值。

## 其他信息

有关其他信息，请参阅 [项目自述文件](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md) 和扩展的数据元素和事件对话框中的。
