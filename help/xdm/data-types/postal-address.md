---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；地址；xdm:address；数据类型；数据类型；
solution: Experience Platform
title: 邮政地址数据类型
description: 本文档概述了邮政地址XDM数据类型。
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 1%

---

# [!UICONTROL 邮政地址] 数据类型

[!UICONTROL 邮政地址] 是描述邮寄地址详细信息的标准XDM数据类型。

<img src="../images/data-types/postal-address.png" width="450" /><br />

| 属性 | 描述 |
| --- | --- |
| `city` | 城市的名称。 |
| `country` | 政府管理领土的名称。 这是一个自由格式字段，可使用任何语言提供国家/地区名称。 |
| `countryCode` | 两个字符 <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> 国家/地区代码。 |
| `createdByBatchID` | 创建地址记录的所摄取批处理文件的ID。 |
| `dmaID` | 尼尔森媒体研究指定了市场区域。 |
| `label` | 地址的自由格式名称。 |
| `lastVerifiedDate` | 地址上次被验证为仍与人员关联的日期。 |
| `modifiedByBatchID` | 上次修改记录的摄取批处理文件的ID。 |
| `msaID` | 观察发生地的美国大都市统计区。 |
| `postOfficeBox` | 地址的邮局框。 |
| `postalCode` | 位置的邮政编码。 邮政编码并非适用于所有国家/地区。 在某些国家/地区，此代码将仅包含部分邮政编码。 |
| `primary` | 一个布尔值，用于指示这是否是个人的主地址。 用户档案只能具有一个 `primary` 地址。 |
| `region` | 地址的地区、县或地区部分。 |
| `repositoryCreatedBy` | 创建记录的用户的ID。 |
| `repositoryLastModifiedBy` | 上次修改记录的用户ID。 |
| `stateProvince` | 观察的州或省份。 格式遵循 [ISO 3166-2（国家/地区和分区）](https://www.unece.org/cefact/locode/subdivisions.html) 标准。 |
| `status` | 指示当前是否可以使用地址。 |
| `statusReason` | 当前的描述 `status`. |
| `street1` — `street4` | 这四个字段用于包含主要街道级别信息、公寓号、街道号和街道名称。 `street2` to `street4` 为可选项。 |

{style=&quot;table-layout:auto&quot;}

有关邮政地址数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.schema.json)
