---
title: 验证编辑器视图
description: 本指南详细介绍了有关Adobe Experience Platform Assurance中的验证编辑器视图的信息。
exl-id: 09be531c-8dc3-48b8-814f-b7a06adf1da3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 3%

---

# 验证编辑器视图

通过验证编辑器，您可以快速轻松地管理JavaScript功能，以验证Adobe Experience Platform保障会话中的事件。 每个函数都会在保证会话中接收事件。 您可以编写函数来验证客户端配置、事件条件、测试和用例。

## 验证编辑器入门

晚于 [设置Assurance](../tutorials/implement-assurance.md)，位于 **[!UICONTROL 主页]** 视图，选择 **[!UICONTROL 验证编辑器]**.

![Validation-Editor — 屏幕快照](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## 编写验证函数

此功能允许您创建、编辑或删除Adobe Experience Platform保障会话的验证功能。

1. 选择 **[!UICONTROL 创建新验证]**.
2. 输入 **name** 要标识验证，请提供 **类别** 和 **描述**.
3. 在编辑器中编辑代码以验证您的保障会话的事件。

完成功能测试后，选择 **[!UICONTROL Publish]** 以保存您的验证。

### 事件定义

| 键 | 类型 | 描述 |
| :--- | :--- | :--- |
| `uuid` | 字符串 | 事件的通用唯一标识符。 |
| `timestamp` | 数值 | 将事件发送到Assurance时客户端的时间戳。 |
| `eventNumber` | 数值 | 用于排序事件的发送时间。 当事件具有相同的时间戳时，此键非常有用。 |
| `vendor` | 字符串 | 采用反向域名格式的供应商标识字符串（例如，com.adobe.assurance）。 |
| `type` | 字符串 | 用于表示事件的类型。 |
| `payload` | 对象 | 为事件定义数据，并包含唯一属性和常用属性。 一些常见属性包括 `ACPExtensionEventSource` 和 `ACPExtensionEventType`. |
| `annotations` | 数组 | 批注对象的数组。 |

### 注释定义

| 键 | 类型 | 描述 |
| :--- | :--- | :--- |
| `uuid` | 字符串 | 注释的通用唯一标识符。 |
| `type` | 字符串 | 用于表示注释的类型，通常是插件的名称（例如analytics）。 |
| `payload` | 对象 | 定义应补充事件的数据。 对于Adobe Analytics，这是包含处理后点击数据的位置。 |

### 验证结果

验证函数应返回包含以下内容的对象：

| 键 | 类型 | 描述 |
| :--- | :--- | :--- |
| `message` | 字符串 | 要在摘要结果中显示的验证消息。 |
| `events` | 数组 | 要报告为匹配或不匹配的事件uuid数组。 |
| `links` | 数组 | 一个数组 `ValidationResultLink` 引用文档和其他资源的对象 `{( type: 'doc'|'product', url: String )}` |
| `result` | 字符串 | 这是验证结果，应是枚举字符串之一：“matched”、“not matched”、“unknown” |

## 查看验证结果

函数的结果显示在代码编辑器下的结果部分中。 如果验证结果为 `unknown` 或 `not matched` 和 `events` 数组有一个或多个 `uuids`时，事件将在时间轴中用以下颜色突出显示：

* 绿色 — 匹配
* 橙色 — 未知
* 红色 — 不匹配

![Timeling-Validation-Highlights-Screen-Shot](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## 故障排除

您可以添加 `console.log()` 以将项目打印到开发人员控制台的功能。 或者，您可以使用结果对象的message属性调试发送到结果面板的消息。

如果JavaScript代码编辑器中发生错误，则会显示错误状态以及原因。

要了解有关验证的更多信息，请访问 [Adobe Experience Platform保证验证](https://github.com/adobe/griffon-validation-plugins) GitHub。 您将在其中找到Adobe拥有的验证示例。 请参阅 [维客](https://github.com/adobe/griffon-validation-plugins/wiki) 以获取有关验证的更多详细说明。
