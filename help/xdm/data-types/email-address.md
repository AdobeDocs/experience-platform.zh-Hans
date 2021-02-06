---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式;emailAddress;xdm:emailAddress;email;email address;datatype;datatype;datatype;
solution: Experience Platform
title: 电子邮件地址数据类型
topic: overview
description: 此文档概述了电子邮件地址XDM数据类型。
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 1%

---


# [!UICONTROL 电子邮件] 地址数据类型

[!UICONTROL 电子] 邮件地址是一种标准XDM数据类型，用于描述电子邮件地址的详细信息。

<img src="../images/data-types/email-address.png" width="450" /><br />

| 属性 | 描述 |
| --- | --- |
| `address` | RFC2822和后续标准中通常定义的电子邮件技术地址（例如`name@domain.com`）。 |
| `label` | 可能提供的其他显示信息。 例如，如果电子邮件的Microsoft Outlook富地址显示为`John Smith smithjr@company.uk`，则`John Smith`将被放置在此字段中。 |
| `primary` | 指示这是否是个人的主要电子邮件地址。 用户档案在给定时间点只能有一个`primary`电子邮件地址。 |
| `status` | 指示当前是否可以使用电子邮件地址 |
| `statusReason` | 当前`status`的说明。 |
| `type` | 帐户与人员的关系（如`work`或`personal`）。 |


有关电子邮件地址数据类型的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.schema.json)