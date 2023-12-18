---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；设备；数据类型；数据类型；货币；
solution: Experience Platform
title: 货币数据类型
description: 了解货币XDM数据类型。
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 5%

---

# [!UICONTROL 货币] 数据类型

[!UICONTROL 货币] 是一个标准的XDM数据类型，用于描述货币量，包括货币类型和兑换日期。

![](../images/data-types/currency.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `amount` | 双精度 | 由定义的货币金额 `currencyCode`. |
| `conversionDate` | 日期时间 | 进行货币转换的时间戳。 |
| `currencyCode` | 字符串 | 指示满足以下条件的货币类型的ISO 4217代码 `amount` 表示。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
