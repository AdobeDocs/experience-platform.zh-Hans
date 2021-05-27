---
keywords: Experience Platform；主页；热门主题；架构；XDM；字段；架构；架构；电子邮件地址；xdm:emailAddress；电子邮件地址；数据类型；数据类型；
solution: Experience Platform
title: 电子邮件地址数据类型
topic-legacy: overview
description: 本文档概述“电子邮件地址”XDM数据类型。
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 2%

---

# [!UICONTROL 电子邮件] 地址数据类型

[!UICONTROL 电子邮] 件地址是一种标准的XDM数据类型，用于描述电子邮件地址的详细信息。

<img src="../images/data-types/email-address.png" width="450" /><br />

| 属性 | 描述 |
| --- | --- |
| `address` | RFC2822及后续标准中通常定义的电子邮件技术地址（例如`name@domain.com`）。 |
| `label` | 其他可用的显示信息。 例如，如果电子邮件的Microsoft Outlook富地址显示为`John Smith smithjr@company.uk`，则`John Smith`将置于此字段中。 |
| `primary` | 指示这是否是个人的主要电子邮件地址。 在给定时间点，用户档案只能有一个`primary`电子邮件地址。 |
| `status` | 指示当前是否可以使用电子邮件地址 |
| `statusReason` | 当前`status`的描述。 |
| `type` | 帐户与人员的关联方式（如`work`或`personal`）。 |

{style=&quot;table-layout:auto&quot;}


有关电子邮件地址数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.schema.json)
