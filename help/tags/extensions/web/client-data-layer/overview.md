---
title: Adobe客户端数据层扩展
description: 了解Adobe Experience Platform中的Adobe客户端数据层标记扩展。
exl-id: c4d1b4d3-4b51-4701-be2e-31b08e109bf6
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 0%

---

# Adobe客户端数据层扩展

本文档提供了有关如何使用Adobe客户端数据层扩展的示例和最佳实践。

<!-- (Missing document?)
If you would like to have more details on development consideration, [please reach this page](./dev.md). -->

## 安装

要安装扩展，请导航到数据收集UI中的扩展目录，然后选择Adobe客户端数据层。

![目录中的ACDL扩展视图](./images/catalog.png)

<!-- (GitHub link?)
There is also the possibility to fork this project. You can download this github project, realize the change that you deem required for your specific use-case and re-upload it on your Organization as a private extension.
This installation will not be supported on our end.<br>
>[!NOTE]
>
> _Consider renaming the extension name in the extension.json file_ -->

## 扩展视图

默认情况下，ACDL脚本会使用变量名称创建新数据层 `adobeDataLayer`. 扩展视图可让您根据需要更改此名称。 加载标记后，您设置的名称将被实例化。

>[!NOTE]
>
>更改对象名称时，原始 `adobeDataLayer` 对象仍在实例化中，然后被复制到您选择的新变量名称中。

## 活动

利用扩展，可监听数据层上的事件。 以下事件可用：

### 监听所有数据更改

如果选择此选项，则事件侦听器将侦听对数据层所做的任何更改。

>[!IMPORTANT]
>
>推送事件不会更改数据层本身。

监听器将跟踪以下推送事件示例：

* ` adobeDataLayer.push({"data":"something"})`
* ` adobeDataLayer.push({"event":"myevent","data":"something"})`

监听程序不会跟踪以下示例推送事件：

* ` adobeDataLayer.push({"event":"myevent"})`

### 监听所有事件

如果选择此选项，则事件侦听器将侦听推送到数据层的任何事件。

监听器将跟踪以下推送事件示例：

* ` adobeDataLayer.push({"event":"myevent"})`
* ` adobeDataLayer.push({"event":"myevent","data":"something"})`

监听程序不会跟踪以下示例推送事件：

* ` adobeDataLayer.push({"data":"something"}) `

### 监听特定事件

在指定事件的情况下，事件侦听器会跟踪与特定字符串匹配的任何事件。

例如，设置 `myEvent` 使用此配置时，侦听器将只跟踪以下推送事件：

* `adobeDataLayer.push({"event":"myEvent"})`

您还可以更改事件侦听器的范围。 不同选项概述如下：

* `all`:这是默认选项，在过去满足您选择的上述条件或将来推送该条件时，都会触发规则。 如果您使用异步实施，则最安全的选项是。
* `future`:仅当将与您的条件匹配的新推送事件发送到数据层时，此选项才会触发规则。
* `past`:此选项仅针对与您的条件匹配的旧推送事件触发规则。 将忽略与您的条件匹配的新推送，并且不再触发规则。

## 操作

以下各节概述了扩展支持的操作。

### 重置数据层

扩展为您提供了一种重置数据层长度的方法，这有助于保持单页应用程序(SPA)的有限大小。

但是，当前不可能在推送方法期间完全删除以前设置的信息。

的 **重置和设置计算状态** 操作会复制最后一个计算状态，清空数据层对象，并重新推送最后一个状态。

### 推送到数据层

该扩展为您提供了一项操作，可将JSON内容推送到数据层本身。此操作可让您直接在JSON中使用数据元素。 在JSON编辑器中，数据元素应使用百分比表示法引用(例如， `%dataElementName%`)。

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

以下部分涵盖扩展提供的唯一数据元素类型。

### 计算状态

数据层计算状态数据元素可返回以下两项之一，具体取决于您配置它的方式：

* 完整的数据层状态：默认情况下，会返回完整的数据层计算状态。
* 特定路径：您可以指定要在数据层中返回的路径。 使用点表示法指定路径(例如， `data.foo`)。

### 数据层大小

此数据元素返回数据层的大小。 数据层的大小由已推送到此对象的元素数量表示。

根据以下推送事件列表，此数据元素将返回整数 `2`:

```js
adobeDataLayer.push({"event":"myEvent"})
adobeDataLayer.push({"data":{"foo":"bar"}})
```
