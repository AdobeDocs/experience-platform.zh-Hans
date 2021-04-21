---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式；搜索；数据类型；数据类型；
solution: Experience Platform
title: 搜索数据类型
topic-legacy: overview
description: 本文档概述了搜索体验数据模型(XDM)数据类型。
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 4%

---

# [!UICONTROL Search] 数据类型

[!UICONTROL Search] 是一个标准的体验数据模型(XDM)数据类型，其中包含有关Web搜索活动的信息。

<img src="../images/data-types/search.PNG" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `isPaid` | 布尔值 | 用于指示是否已支付搜索。 |
| `keywords` | 字符串 | 搜索的关键字。 |
| `pageDepth` | 整数 | 搜索结果中的页面深度。 |
| `position` | 整数 | 列表在搜索结果页面中的位置或排名。 |
| `searchEngine` | 字符串 | 搜索使用的搜索引擎。 |
| `searchEngineID` | 字符串 | 用于标识搜索引擎的应用程序特定标识符。 |
| `slot` | 字符串 | 显示搜索结果的页面的命名部分。 此属性的值必须等于您定义的已知枚举值之一，如`top`、`side`或`bottom`。 |

有关数据类型的详细信息，请参阅公共XDM存储库：

* [已填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
