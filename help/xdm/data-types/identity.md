---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;identity;datatype;data-type;data type;
solution: Experience Platform
title: 身份数据类型
topic: overview
description: 此文档概述了Identity XDM数据类型。
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 2%

---


# [!UICONTROL 身份] 数据类型

[!UICONTROL 身份] 是一种标准的XDM数据类型，用于清晰区分与数字体验交互的用户。 标识由标识提供者建立，该提供者本身在属性中 `namespace` 引用。 在每个人 `namespace`中，身份都是独一无二的。

<img src="../images/data-types/identity.png" width="550" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `namespace` | 对象 | 包含单个字符串字段()`code`的对象，它指示与提供的属性关联的 `id` 命名空间。 |
| `authenticatedState` | 字符串 | 在观察到的体验事件时此标识的已验证状态。 有关已接 [受的值](#authenticatedState) 和定义，请参阅附录。 |
| `id` | 字符串 | 相关命名空间中消费者的身份。 |
| `primary` | 布尔值 | 指示这是否为个人的主要身份。 每个人只能有一个主身份。 |
| `xid` | 字符串 | 当存在时，此值表示跨命名空间标识符，该标识符在所有命名空间范围内的所有命名空间标识符中都是唯一的。 |

有关混音的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## 附录

以下部分包含有关Identity数据类 [!UICONTROL 型的] 其他信息。

## 已接受的authenticatedState值 {#authenticatedState}

下表概述了可接受的值及其 `authenticatedState` 相关含义：

| 值 | 描述 |
| --- | --- |
| `ambiguous` | 已验证的状态不明确。 |
| `authenticated` | 用户由登录名或在事件观察时有效的类似操作来标识。 |
| `loggedOut` | 用户在以前某个时间点通过登录操作进行标识，但在事件观察时未登录。 |