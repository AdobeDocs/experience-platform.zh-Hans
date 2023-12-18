---
title: 邮政地址数据类型
description: 了解邮政地址体验数据模型(XDM)数据类型。
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 8%

---

# [!UICONTROL 邮政地址] 数据类型

[!UICONTROL 邮政地址] 是一个标准体验数据模型(XDM)数据类型，提供了地址详细信息。

![的图表 [!UICONTROL 邮政地址] 数据类型。](../images/data-types/postal-address.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|------------------------------------|------------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL 主要] | `primary` | 布尔 | 主要地址指示器。 配置文件只能有一个 `primary` 在给定时间点的地址。 |
| [!UICONTROL 标签] | `label` | 字符串 | 自由形式的地址名称。 |
| [!UICONTROL 街道1] | `street1` | 字符串 | 主要街道级别信息、公寓号、街道号和街道名称。 |
| [!UICONTROL 街道2] | `street2` | 字符串 | 可选街道信息第二行。 |
| [!UICONTROL 街道3] | `street3` | 字符串 | 可选街道信息第三行。 |
| [!UICONTROL 街道4] | `street4` | 字符串 | 可选街道信息第四行。 |
| [!UICONTROL 区域] | `region` | 字符串 | 地址的区域、县或区部分。 |
| [!UICONTROL 邮政信箱] | `postOfficeBox` | 字符串 | 地址的邮政信箱。 |
| [!UICONTROL 国家/地区] | `country` | 字符串 | 政府管辖地区的名称。 除 ``countryCode``，这是一个自由格式的字段，可以包含任何语言的国家/地区名称。 |
| [!UICONTROL 省/州] | `state` | 字符串 | 国家的名称。 这是自由格式字段。 |
| [!UICONTROL 状态] | `status` | 字符串 | 关于使用地址的能力的指示。 |
| [!UICONTROL 状态原因] | `statusReason` | 字符串 | 当前状态的描述。 |
| [!UICONTROL 上次验证日期] | `lastVerifiedDate` | 字符串 | 上次验证地址仍与该人员关联的日期。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅 [完整模式](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/address.schema.json) 在公共XDM存储库上：
