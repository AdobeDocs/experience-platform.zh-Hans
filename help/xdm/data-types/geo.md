---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式;geo;datatype；数据类型；
solution: Experience Platform
title: 地理数据类型
topic: overview
description: 此文档概述了Geo XDM数据类型。
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 4%

---


# [!UICONTROL 地] 理数据类型

[!UICONTROL Geois] 是一种标准XDM数据类型，用于描述观察事件的地理区域。

<img src="../images/data-types/geo.png" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_schema` | [[!UICONTROL 地理坐标]](./geo-coordinates.md) | 描述地理坐标。 |
| `_id` | 字符串 | 坐标的唯一、系统生成的ID。 |
| `city` | 字符串 | 城市的名字。 |
| `countryCode` | 字符串 | 国家／地区的双字符<a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a>代码。 |
| `dmaID` | 整数 | 尼尔森媒体研究指定的市场领域。 |
| `msaID` | 整数 | 观察发生地美国的大都市统计区。 |
| `postalCode` | 字符串 | 位置的邮政编码。 邮政编码不适用于所有国家／地区。 在一些国家，这将仅包含部分邮政编码。 |
| `stateProvince` | 字符串 | 观察的州或省部分。 格式遵循[ISO 3166-2（国家／地区和细分）](http://www.unece.org/cefact/locode/subdivisions.html)标准。 |

有关混音的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.schema.json)