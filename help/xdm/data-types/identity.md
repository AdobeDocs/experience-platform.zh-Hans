---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式；标识；数据类型；数据类型；
solution: Experience Platform
title: 身份数据类型
topic-legacy: overview
description: 本文档概述了Identity XDM数据类型。
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 3%

---

# [!UICONTROL Identity] 数据类型

[!UICONTROL Identity] 是一种标准的XDM数据类型，用于清晰区分与数字体验交互的人。标识由标识提供者建立，标识提供者本身在`namespace`属性中引用。 在每个`namespace`中，标识是唯一的。

<img src="../images/data-types/identity.png" width="550" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `namespace` | 对象 | 包含单个字符串字段(`code`)的对象，它指示与提供的`id`属性关联的命名空间。 |
| `authenticatedState` | 字符串 | 在观察到的体验事件时此标识的已验证状态。 有关已接受的值和定义，请参见[附录](#authenticatedState)。 |
| `id` | 字符串 | 相关命名空间中消费者的身份。 |
| `primary` | 布尔值 | 指示这是否为个人的主要身份。 每个人只能有一个主要身份。 |
| `xid` | 字符串 | 当存在时，此值表示跨命名空间标识符，该标识符在所有命名空间中所有命名空间范围标识符之间是唯一的。 |

有关数据类型的详细信息，请参阅公共XDM存储库：

* [已填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## 附录

以下部分包含有关[!UICONTROL Identity]数据类型的其他信息。

## authenticatedState {#authenticatedState}的已接受值

下表概述了`authenticatedState`的已接受值及其相关含义：

| 值 | 描述 |
| --- | --- |
| `ambiguous` | 已验证的状态不明确。 |
| `authenticated` | 用户由登录或在事件观察时有效的类似操作识别。 |
| `loggedOut` | 用户在以前某个时间点通过登录操作进行标识，但在事件观察时未登录。 |
