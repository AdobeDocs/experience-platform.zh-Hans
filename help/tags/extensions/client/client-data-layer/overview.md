---
title: Adobe客户端数据层扩展
description: 了解Adobe Experience Platform中的Adobe Client Data Layer标记扩展。
exl-id: c4d1b4d3-4b51-4701-be2e-31b08e109bf6
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---

# Adobe客户端数据层扩展

本文档提供了有关如何使用Adobe客户端数据层扩展的示例和最佳实践。

<!-- (Missing document?)
If you would like to have more details on development consideration, [please reach this page](./dev.md). -->

## 安装

要安装扩展，请导航到Experience Platform UI或数据收集UI中的扩展目录，然后选择Adobe Client Data Layer 。

目录![中的](./images/catalog.png)ACDL扩展视图

<!-- (GitHub link?)
There is also the possibility to fork this project. You can download this github project, realize the change that you deem required for your specific use-case and re-upload it on your Organization as a private extension.
This installation will not be supported on our end.<br>
>[!NOTE]
>
> _Consider renaming the extension name in the extension.json file_ -->

## 扩展视图

默认情况下，ACDL脚本使用变量名称`adobeDataLayer`创建新的数据层。 如果需要，扩展视图可让您更改此名称。 您设置的名称将在加载标记时实例化。

>[!NOTE]
>
>更改对象名称时，原始`adobeDataLayer`对象仍在实例化中，然后复制到您选择的新变量名称。

## 事件

通过扩展，您可以侦听Data Layer上的事件。 可以使用以下事件：

### 侦听所有数据更改

如果选择此选项，事件侦听器将侦听对数据层所做的任何更改。

>[!IMPORTANT]
>
>推送事件不会更改数据层本身。

监听程序将跟踪以下示例推送事件：

* `adobeDataLayer.push({"data":"something"})`
* `adobeDataLayer.push({"event":"myevent","data":"something"})`

监听程序将不会跟踪以下示例推送事件：

* `adobeDataLayer.push({"event":"myevent"})`

### 收听所有活动

如果选择此选项，事件侦听器将侦听推送到数据层的任何事件。

监听程序将跟踪以下示例推送事件：

* `adobeDataLayer.push({"event":"myevent"})`
* `adobeDataLayer.push({"event":"myevent","data":"something"})`

监听程序将不会跟踪以下示例推送事件：

* ` adobeDataLayer.push({"data":"something"}) `

### 收听特定事件

如果指定事件，则事件侦听器会跟踪与特定字符串匹配的任何事件。

例如，使用此配置时设置`myEvent`会导致侦听器仅跟踪以下推送事件：

* `adobeDataLayer.push({"event":"myEvent"})`

您还可以更改事件侦听器的范围。 不同选项概述如下：

* `all`：这是默认选项，当过去满足您以上选择的条件时，或将来会推送该条件时，就会触发规则。 如果您使用异步实施，这是最安全的选项。
* `future`：仅当将符合您条件的新推送事件发送到Data Layer时，此选项才会触发规则。
* `past`：此选项仅触发与您的条件匹配的旧推送事件的规则。 与您的条件匹配的新推送将被忽略，并且不再触发规则。

## 操作

以下部分概述了扩展支持的操作。

### 重置数据层

扩展提供了一种重置数据层长度的方法，可以帮助保持单页应用程序(SPA)的大小受限。

但是，当前不可能完全删除之前在推送方法期间设置的信息。

**重置和设置计算状态**&#x200B;操作将复制上次计算状态，清空数据层对象，并重新推送上次状态。

### 推送到Data Layer

扩展为您提供了一个将JSON内容推送到Data Layer本身的操作。通过此操作，可以在JSON中直接使用数据元素。 在JSON编辑器中，应使用百分比表示法引用数据元素（例如，`%dataElementName%`）。

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

以下各部分介绍了扩展提供的独特数据元素类型。

### 计算状态

根据配置方式， Data Layer Computed State数据元素可以返回以下两项之一：

* 完整的Data Layer状态：默认情况下，会返回完整的Data Layer Computed State。
* 特定路径：您可以指定要在Data Layer中返回的路径。 路径是使用点表示法指定的（例如，`data.foo`）。

### 数据层大小

此数据元素返回数据层的大小。 Data Layer的大小由已推送到此对象的元素数量表示。

给定以下推送事件列表，此数据元素将返回整数`2`：

```js
adobeDataLayer.push({"event":"myEvent"})
adobeDataLayer.push({"data":{"foo":"bar"}})
```
