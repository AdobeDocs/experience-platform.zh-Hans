---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；电话号码；xdm：phoneNumber；数据类型；数据类型；
solution: Experience Platform
title: 电话号码数据类型
description: 本文档概述了电话号码XDM数据类型。
exl-id: b84e48f9-bbb4-4b8b-9476-4bc1c455ecfd
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# [!UICONTROL 电话号码] 数据类型

[!UICONTROL 电话号码] 是描述电话号码详细信息的标准XDM数据类型。

<img src="../images/data-types/phone-number.png" width="600" /><br />

| 属性 | 描述 |
| --- | --- |
| `extension` | 用于从专用交换机、接线员或总机呼叫的内部拨号号码。 |
| `number` | 电话号码。 请注意，电话号码是一个字符串，并且可能包含有意义的字符，如括号 `()`，连字符 `-`或字符来指示子拨号标识符，如扩展 `x` 例如， `1-353(0)18391111` 或 `+613 9403600x1234`. |
| `primary` | 一个布尔值，指示这是否为个人的主要电话号码。 与地址或电子邮件地址不同，可以有多个主要电话号码；每个通信渠道一个。 通信渠道由类型定义（由父属性的名称指示）： `textMessaging`， `mobile`， `phone`， `home`， `work`， `unknown`、和 `fax`. |
| `status` | 指示电话号码当前是否可以使用。 |
| `statusReason` | 当前状态的描述。 |
| `validity` | 电话号码的技术正确性级别。 |

{style="table-layout:auto"}

有关电话号码数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.schema.json)
