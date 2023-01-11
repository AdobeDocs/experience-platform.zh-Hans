---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；地理；数据类型；数据类型；
solution: Experience Platform
title: 地域数据类型
description: 本文档概述了Geo XDM数据类型。
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 5%

---

# [!UICONTROL 地域] 数据类型

[!UICONTROL 地域] 是一种标准的XDM数据类型，用于描述观察到事件的地理区域。

<img src="../images/data-types/geo.png" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_schema` | [[!UICONTROL 地理坐标]](./geo-coordinates.md) | 描述位置的地理坐标。 |
| `_id` | 字符串 | 坐标的唯一、系统生成的ID。 |
| `city` | 字符串 | 城市的名称。 |
| `countryCode` | 字符串 | 两个字符 <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> 国家/地区代码。 |
| `dmaID` | 整数 | 尼尔森媒体研究指定了市场区域。 |
| `msaID` | 整数 | 观察发生地的美国大都市统计区。 |
| `postalCode` | 字符串 | 位置的邮政编码。 邮政编码并非适用于所有国家/地区。 在某些国家/地区，此代码将仅包含部分邮政编码。 |
| `stateProvince` | 字符串 | 观察的州或省份。 格式遵循 [ISO 3166-2（国家/地区和分区）](https://www.unece.org/cefact/locode/subdivisions.html) 标准。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.schema.json)
