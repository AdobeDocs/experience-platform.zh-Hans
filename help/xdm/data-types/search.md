---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；搜索；数据类型；数据类型；
solution: Experience Platform
title: 搜索数据类型
description: 本文档概述了搜索体验数据模型(XDM)数据类型。
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 6%

---

# [!UICONTROL 搜索] 数据类型

[!UICONTROL 搜索] 是一种标准的体验数据模型(XDM)数据类型，其中包含有关Web搜索活动的信息。

<img src="../images/data-types/search.PNG" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `isPaid` | 布尔型 | 用于指示搜索是否已付费。 |
| `keywords` | 字符串 | 搜索的关键词。 |
| `pageDepth` | 整数 | 搜索结果中的页面深度。 |
| `position` | 整数 | 列表在搜索结果页面中的位置或排名。 |
| `searchEngine` | 字符串 | 搜索使用的搜索引擎。 |
| `searchEngineID` | 字符串 | 用于标识搜索引擎的应用程序特定标识符。 |
| `slot` | 字符串 | 显示搜索结果的页面的命名部分。 此属性的值必须等于您定义的已知枚举值之一，例如 `top`, `side`或 `bottom`. |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
