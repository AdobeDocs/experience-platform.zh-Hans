---
keywords: Experience Platform；主页；热门主题；架构；XDM；字段；架构；架构；电子邮件地址；xdm:emailAddress；电子邮件地址；数据类型；数据类型；
solution: Experience Platform
title: 电子邮件地址数据类型
description: 本文档概述“电子邮件地址”XDM数据类型。
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 2%

---

# [!UICONTROL 电子邮件地址] 数据类型

[!UICONTROL 电子邮件地址] 是一种标准的体验数据模型(XDM)数据类型，用于描述电子邮件地址的详细信息。

<img src="../images/data-types/email-address.png" width="450" /><br />

| 属性 | 描述 |
| --- | --- |
| `address` | RFC2822及后续标准中通常定义的电子邮件的技术地址(例如， `name@domain.com`)。<br><br>在XDM中，电子邮件地址必须包含有效的顶级域名，才能通过验证。 请参阅以下内容 [文档](https://data.iana.org/TLD/tlds-alpha-by-domain.txt) 有效顶级域的完整列表，由Internet分配的号码管理局(IANA)定义。 |
| `label` | 其他可用的显示信息。 例如，如果电子邮件的Microsoft Outlook富地址显示为 `John Smith smithjr@company.uk`, `John Smith` 将被置于此字段中。 |
| `primary` | 指示这是否是个人的主要电子邮件地址。 用户档案只能具有一个 `primary` 指定时间点的电子邮件地址。 |
| `status` | 指示当前是否可以使用电子邮件地址 |
| `statusReason` | 当前的描述 `status`. |
| `type` | 帐户与人员的关联方式(例如 `work` 或 `personal`)。 |

{style=&quot;table-layout:auto&quot;}


有关电子邮件地址数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
