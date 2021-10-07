---
title: 展示次数数据类型
description: 本文档概述了展示次数XDM数据类型。
source-git-commit: 7fc16546176d196582a3cdfcee51f799eeef9788
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 6%

---

#  Impressions数据类型

 展示是一种标准的XDM数据类型，用于描述营销展示，该量度用于量化某段内容（如广告、数字帖子或网页）的数字查看次数或参与次数。

![](../images/data-types/impressions.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `ID` | 字符串 | 展示的唯一ID。 |
| `displays` | 整数 | 向客户显示展示项目的次数。 |
| `selected` | 整数 | 选择或点击展示项目的次数。 |
| `type` | 字符串 | 展示类型。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)
