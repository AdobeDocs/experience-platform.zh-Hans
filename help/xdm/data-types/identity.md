---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；身份；数据类型；数据类型；
solution: Experience Platform
title: 身份数据类型
topic-legacy: overview
description: 本文档概述了Identity XDM数据类型。
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 4%

---

#  Identitydata类型

 Identity是一种标准的XDM数据类型，用于明确区分与数字体验进行交互的人员。标识由标识提供程序建立，该提供程序本身在`namespace`属性中引用。 在每个`namespace`内，标识是唯一的。

<img src="../images/data-types/identity.png" width="550" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `namespace` | 对象 | 包含单个字符串字段(`code`)的对象，该字段指示与提供的`id`属性关联的命名空间。 |
| `authenticatedState` | 字符串 | 观察到的体验事件时此身份的已验证状态。 有关已接受的值和定义，请参阅[附录](#authenticatedState)。 |
| `id` | 字符串 | 相关命名空间中消费者的标识。 |
| `primary` | 布尔值 | 指示这是否是个人的主标识。 每个人只能有一个主标识。 |
| `xid` | 字符串 | 如果存在，则此值表示跨命名空间标识符，该标识符在所有命名空间中所有命名空间范围内的标识符都是唯一的。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## 附录

以下部分包含有关[!UICONTROL Identity]数据类型的其他信息。

## 已接受的authenticatedState值 {#authenticatedState}

下表概述了`authenticatedState`的已接受值及其相关含义：

| 值 | 描述 |
| --- | --- |
| `ambiguous` | 身份验证状态不明确。 |
| `authenticated` | 用户是通过在事件观察时有效的登录或类似操作来识别的。 |
| `loggedOut` | 用户是在以前某个时间点通过登录操作识别的，但在事件观察时未登录。 |
