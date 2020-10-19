---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;address;xdm:address;datatype;data-type;data type;
solution: Experience Platform
title: 邮政地址数据类型
topic: overview
description: 此文档概述了邮政地址XDM数据类型。
translation-type: tm+mt
source-git-commit: 6a7967ac9e652c7e73fd713e89a9079287cf0ae5
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---


# [!UICONTROL 邮政地址] 数据类型

[!UICONTROL 邮政地址] 是一种标准XDM数据类型，用于描述邮寄地址的详细信息。

<img src="../images/data-types/postal-address.png" width="450" /><br />

| 属性 | 描述 |
| --- | --- |
| `city` | 城市的名字。 |
| `country` | 政府管理领土的名称。 这是一个自由表单字段，可以使用任何语言命名国家／地区名称。 |
| `countryCode` | 适用于该国 <a href="https://datahub.io/core/country-list">家／地区的双字符ISO 3166-</a> 1 alpha-2代码。 |
| `createdByBatchID` | 创建地址记录的所摄取的批处理文件的ID。 |
| `dmaID` | 尼尔森媒体研究指定的市场领域。 |
| `label` | 地址的自由格式名称。 |
| `lastVerifiedDate` | 上次验证地址时仍与人员关联的日期。 |
| `modifiedByBatchID` | 上次修改记录的所摄取的批处理文件的ID。 |
| `msaID` | 观察发生地美国的大都市统计区。 |
| `postOfficeBox` | 地址的邮局框。 |
| `postalCode` | 位置的邮政编码。 邮政编码不适用于所有国家／地区。 在一些国家，这将仅包含部分邮政编码。 |
| `primary` | 一个布尔值，它指示这是否是个人的主要地址。 用户档案在给定时 `primary` 间点只能有一个地址。 |
| `region` | 地址的地区、县或地区部分。 |
| `repositoryCreatedBy` | 创建记录的用户的ID。 |
| `repositoryLastModifiedBy` | 上次修改记录的用户的ID。 |
| `stateProvince` | 观察的州或省部分。 格式遵循ISO [3166-2（国家／地区和细分）标准](http://www.unece.org/cefact/locode/subdivisions.html) 。 |
| `status` | 指示地址当前是否可以使用。 |
| `statusReason` | 当前的描述 `status`。 |
| `street1` - `street4` | 这四个字段用于包含主要街道级别信息、公寓编号、街道编号和街道名称。 `street2` 为 `street4` 可选。 |

有关邮政地址数据类型的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/address.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/address.schema.json)