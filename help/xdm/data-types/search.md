---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；搜索；数据类型；数据类型；
solution: Experience Platform
title: 搜索数据类型
description: 了解搜索体验数据模型(XDM)数据类型。
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 11%

---

# [!UICONTROL 搜索]数据类型

[!UICONTROL 搜索]是包含Web搜索活动信息的标准体验数据模型(XDM)数据类型。

<img src="../images/data-types/search.PNG" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `isPaid` | 布尔值 | 用于指示搜索是否付费。 |
| `keywords` | 字符串 | 搜索关键词。 |
| `pageDepth` | 整数 | 搜索结果中的页面深度。 |
| `position` | 整数 | 在搜索结果页面中列出的位置或排名。 |
| `searchEngine` | 字符串 | 搜索所使用的搜索引擎。 |
| `searchEngineID` | 字符串 | 用于标识搜索引擎的应用程序特定标识符。 |
| `slot` | 字符串 | 显示搜索结果的页面的命名部分。 此属性的值必须等于您定义的已知枚举值之一，如`top`、`side`或`bottom`。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
