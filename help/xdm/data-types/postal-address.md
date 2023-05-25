---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；地址；xdm：地址；数据类型；数据类型；
solution: Experience Platform
title: 邮政地址数据类型
description: 本文档概述了邮政地址XDM数据类型。
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# [!UICONTROL 邮政地址] 数据类型

[!UICONTROL 邮政地址] 是描述邮寄地址详细信息的标准XDM数据类型。

<img src="../images/data-types/postal-address.png" width="450" /><br />

| 属性 | 描述 |
| --- | --- |
| `city` | 城市的名称。 |
| `country` | 政府管辖地区的名称。 这是一个自由格式的字段，可以包含任何语言的国家/地区名称。 |
| `countryCode` | 两个字符 <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> 国家/地区的代码。 |
| `createdByBatchID` | 创建地址记录的已摄取批处理文件的ID。 |
| `dmaID` | Nielsen媒体研究指定的市场区域。 |
| `label` | 自由格式的地址名称。 |
| `lastVerifiedDate` | 上次验证地址仍与该人员关联的日期。 |
| `modifiedByBatchID` | 上次修改记录的所摄取批处理文件的ID。 |
| `msaID` | 美国发生观测的大都市统计区。 |
| `postOfficeBox` | 地址的邮政信箱。 |
| `postalCode` | 位置的邮政编码。 并非所有国家/地区都提供邮政编码。 在一些国家/地区，这仅包含邮政编码的一部分。 |
| `primary` | 一个布尔值，指示这是否为个人的主地址。 配置文件只能有一个 `primary` 在给定时间点的地址。 |
| `region` | 地址的区域、县或区部分。 |
| `repositoryCreatedBy` | 创建记录的用户的ID。 |
| `repositoryLastModifiedBy` | 上次修改记录的用户的ID。 |
| `stateProvince` | 观察的省/市/自治区部分。 格式遵循 [ISO 3166-2（国家/地区和细分）](https://www.unece.org/cefact/locode/subdivisions.html) 标准。 |
| `status` | 指示地址当前是否可以使用。 |
| `statusReason` | 当前内容的描述 `status`. |
| `street1` — `street4` | 这四个字段用于包含主要街道级别信息、公寓号、街道号和街道名称。 `street2` 到 `street4` 是可选的。 |

{style="table-layout:auto"}

有关邮政地址数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.schema.json)
