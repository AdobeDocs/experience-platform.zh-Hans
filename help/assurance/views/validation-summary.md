---
title: 验证编辑器视图
description: 本指南详细介绍了 Adobe Experience Platform Assurance 中的应用验证编辑器视图的信息。
exl-id: 09be531c-8dc3-48b8-814f-b7a06adf1da3
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 93%

---

# 验证编辑器视图

验证编辑器可让您快速轻松地管理 JavaScript 函数，以验证 Adobe Experience Platform Assurance 会话中的事件。每个功能都会在 Assurance 会话中接收事件。您可以编写函数来验证客户端配置、事件条件、测试和用例。

## 开始使用验证编辑器

在[设置Assurance](../tutorials/implement-assurance.md)后，在&#x200B;**[!UICONTROL Home]**&#x200B;视图中，选择&#x200B;**[!UICONTROL Validation Editor]**。

![Validation-Editor-Screen-Shot](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## 编写验证函数

此功能允许您为 Adobe Experience Platform Assurance 会话创建、编辑或删除验证功能。

1. 选择 **[!UICONTROL Create a New Validation]**。
2. 输入一个&#x200B;**名称**，以识别验证，然后提供一个&#x200B;**类别**&#x200B;和一个&#x200B;**描述**。
3. 在编辑器中编辑代码以验证 Assurance 会话的事件。

完成功能测试后，选择&#x200B;**[!UICONTROL Publish]**&#x200B;以保存验证。

### 事件定义

| 键 | 类型 | 描述 |
| :--- | :--- | :--- |
| `uuid` | 字符串 | 事件的通用唯一标识符。 |
| `timestamp` | 数值 | 事件发送至 Assurance 时客户端的时间戳。 |
| `eventNumber` | 数值 | 用于对事件发送的时间进行排序。当事件具有相同时间戳时，此键很有用。 |
| `vendor` | 字符串 | 反向域名格式的供应商标识字符串（例如 com.adobe.assurance）。 |
| `type` | 字符串 | 用于表示事件的类型。 |
| `payload` | 对象 | 定义事件的数据并包含唯一的通用属性。一些常见的属性包括 `ACPExtensionEventSource` 和 `ACPExtensionEventType`。 |
| `annotations` | 数组 | 注释对象的数组。 |

### 注释定义

| 键 | 类型 | 描述 |
| :--- | :--- | :--- |
| `uuid` | 字符串 | 注释的通用唯一标识符。 |
| `type` | 字符串 | 用于表示注释的类型，通常是插件的名称（例如，Analytics）。 |
| `payload` | 对象 | 定义应补充事件的数据。对于 Adobe Analytics，这是包含后处理的点击数据的位置。 |

### 验证结果

验证函数预计会返回一个包含以下内容的对象：

| 键 | 类型 | 描述 |
| :--- | :--- | :--- |
| `message` | 字符串 | 要在摘要结果中显示的验证消息。 |
| `events` | 数组 | 要报告为匹配或不匹配的事件 uuid 的数组。 |
| `links` | 数组 | `ValidationResultLink`对象的数组，用于引用文档和其他资源`{( type: 'doc'`&amp;amp；vert；`'product', url: String )}` |
| `result` | 字符串 | 这是验证结果，并且预计会是枚举字符串之一：&quot;matched&quot;, &quot;not matched&quot;, &quot;unknown&quot; |

## 查看验证结果

该函数的结果显示在代码编辑器下方的结果部分中。如果验证结果是 `unknown` 或者 `not matched`，并且 `events` 数组有一个或多个 `uuids`，则事件将会在时间线中用以下颜色突出显示：

* 绿色 - 匹配
* 橙色 - 未知
* 红色 - 不匹配

![Timeling-Validation-Highlights-Screen-Shot](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## 故障排除

您可以在函数中添加 `console.log()`，以将项目打印到 Developer Console。或者，您可以使用结果对象的信息属性将调试消息发送到结果面板。

如果 JavaScript 代码编辑器中发生错误，则会显示错误状态以及原因。

要了解有关验证的更多信息，请访问 [Adobe Experience Platform Assurance 验证](https://github.com/adobe/griffon-validation-plugins) GitHub。您可以在此处找到 Adobe 拥有的验证示例。请参阅[维基百科](https://github.com/adobe/griffon-validation-plugins/wiki)，了解有关验证的更详细说明。
