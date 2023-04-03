---
title: 验证编辑器视图
description: 本指南详细介绍了Adobe Experience Platform Assurance中的验证编辑器视图。
source-git-commit: 5778d4db27d0f57281821dc8e042a31b69745514
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 3%

---


# 验证编辑器视图

通过验证编辑器，您可以快速轻松地管理JavaScript功能，以验证Adobe Experience Platform保证会话中的事件。 每个函数在保证会话中接收事件。 您可以编写函数来验证您的客户端配置、事件条件、测试和用例。

## 验证编辑器入门

之后 [设置保证](../tutorials/implement-assurance.md)，在 **[!UICONTROL 主页]** 视图，选择 **[!UICONTROL 验证编辑器]**.

![验证编辑器屏幕截图](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## 编写验证函数

此功能允许您为Adobe Experience Platform保证会话创建、编辑或删除验证功能。

1. 选择 **[!UICONTROL 创建新验证]**.
2. 输入 **name** 要识别验证，请提供 **类别** 和 **描述**.
3. 在编辑器中编辑代码，以验证贵机构保证会话的事件。

函数测试完成后，选择 **[!UICONTROL 发布]** 以保存验证。

### 事件定义

| 键 | 类型 | 描述 |
| :--- | :--- | :--- |
| `uuid` | 字符串 | 事件的通用唯一标识符。 |
| `timestamp` | 数值 | 将事件发送到保证时客户端的时间戳。 |
| `eventNumber` | 数值 | 用于对事件发送的时间进行排序。 当事件具有相同的时间戳时，此键很有用。 |
| `vendor` | 字符串 | 反向域名格式的供应商标识字符串（例如com.adobe.assurance）。 |
| `type` | 字符串 | 用于表示事件的类型。 |
| `payload` | 对象 | 定义事件的数据，并包含唯一和通用的属性。 一些常见属性包括 `ACPExtensionEventSource` 和 `ACPExtensionEventType`. |
| `annotations` | 数组 | 注释对象的数组。 |

### 注释定义

| 键 | 类型 | 描述 |
| :--- | :--- | :--- |
| `uuid` | 字符串 | 注释的通用唯一标识符。 |
| `type` | 字符串 | 用于表示注释的类型，通常是插件的名称（例如analytics）。 |
| `payload` | 对象 | 定义应补充事件的数据。 对于Adobe Analytics，这是包含后处理点击数据的位置。 |

### 验证结果

验证函数应返回包含以下项的对象：

| 键 | 类型 | 描述 |
| :--- | :--- | :--- |
| `message` | 字符串 | 要在摘要结果中显示的验证消息。 |
| `events` | 数组 | 要报告为匹配或不匹配的事件uuid数组。 |
| `links` | 数组 | 数组 `ValidationResultLink` 引用文档和其他资源的对象 `{( type: 'doc'|'product', url: String )}` |
| `result` | 字符串 | 这是验证结果，应为枚举字符串之一：&quot;matched&quot;、&quot;notmatched&quot;、&quot;unknown&quot; |

## 查看验证结果

函数的结果显示在代码编辑器下方的结果部分中。 如果验证结果为 `unknown` 或 `not matched` 和 `events` 阵列具有一个或多个 `uuids`，则事件将在时间轴中突出显示，且显示以下颜色：

* 绿色 — 匹配
* 橙色 — 未知
* 红色 — 不匹配

![时间 — 验证 — 高亮 — 屏幕截图](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## 故障排除

您可以添加 `console.log()` 在函数中将项目打印到开发人员控制台。 或者，也可以使用结果对象的消息属性将消息调试到结果面板。

如果JavaScript代码编辑器中发生错误，则会显示错误状态以及原因。

要了解有关验证的更多信息，请访问 [Adobe Experience Platform保证验证](https://github.com/adobe/griffon-validation-plugins) GitHub。 您将在此处找到Adobe拥有的验证示例。 请参阅 [维基](https://github.com/adobe/griffon-validation-plugins/wiki) 以了解验证的更多详细描述。
