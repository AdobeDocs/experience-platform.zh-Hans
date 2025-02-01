---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；地域；数据类型；数据类型；
solution: Experience Platform
title: 地理数据类型
description: 了解地域XDM数据类型。
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 34%

---

# [!UICONTROL 地域]数据类型

[!UICONTROL 地域]是一种标准XDM数据类型，它描述了观察到事件的地理区域。

![](../images/data-types/geo.png){width=400}

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_schema` | [[!UICONTROL 地理坐标]](./geo-coordinates.md) | 描述位置的地理坐标。 |
| `_id` | 字符串 | 系统生成的唯一坐标ID。 |
| `city` | 字符串 | 城市名。 |
| `countryCode` | 字符串 | 国家/地区的双字符<a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a>代码。 |
| `dmaID` | 整数 | Nielsen 媒体研究指定的市场区域。 |
| `msaID` | 整数 | 美国发生观测的大都市统计区。 |
| `postalCode` | 字符串 | 位置的邮政编码。并非所有国家/地区都有邮政编码。在某些国家/地区，这将仅包含邮政编码的一部分。 |
| `stateProvince` | 字符串 | 观察的省/市/自治区部分。 格式遵循[ISO 3166-2（国家/地区和细分）](https://www.unece.org/cefact/locode/subdivisions.html)标准。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.schema.json)
