---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;emailAddress;xdm:emailAddress;email;email address;datatype;data-type;data type;
solution: Experience Platform
title: 电子邮件地址数据类型
topic: overview
description: 此文档概述了电子邮件地址XDM数据类型。
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 1%

---


# [!UICONTROL 电子邮件地址] ，数据类型

[!UICONTROL 电子邮件地址] 是一种标准XDM数据类型，用于描述电子邮件地址的详细信息。

<img src="../images/data-types/email-address.png" width="450" /><br />

| 属性 | 描述 |
| --- | --- |
| `address` | RFC2822和后续标准中通常定义的电子邮件技术地址(例如 `name@domain.com`)。 |
| `label` | 可能提供的其他显示信息。 例如，如果电子邮件的Microsoft Outlook富地址显示 `John Smith smithjr@company.uk`, `John Smith` 则会放置在此字段中。 |
| `primary` | 指示这是否是个人的主要电子邮件地址。 用户档案在给定时间 `primary` 点只能有一个电子邮件地址。 |
| `status` | 指示当前是否可以使用电子邮件地址 |
| `statusReason` | 当前的描述 `status`。 |
| `type` | 帐户与人员（如或）的关 `work` 联方 `personal`式。 |


有关电子邮件地址数据类型的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.schema.json)