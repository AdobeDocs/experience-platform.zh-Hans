---
title: 展示数据类型
description: 本文档概述了“展示次数”XDM数据类型。
exl-id: 1e758043-a41e-45f7-ae8b-514990d0649e
source-git-commit: afdac5ce2ed967b4688d456a586c946bc2cf4179
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 4%

---

# [!UICONTROL 展示次数] 数据类型

[!UICONTROL 展示次数] 是描述营销印象的标准XDM数据类型，营销印象是用于量化一段内容（如广告、数字帖子或网页）的数字查看或参与次数的量度。

![](../images/data-types/impressions.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `ID` | 字符串 | 展示的唯一ID。 |
| `displays` | 整数 | 展示项目已向客户显示的次数。 |
| `selected` | 整数 | 选择或单击展示项目的次数。 |
| `type` | 字符串 | 印象的类型。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)
