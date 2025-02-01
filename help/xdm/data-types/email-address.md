---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；电子邮件地址；xdm：emailAddress；电子邮件；电子邮件地址；数据类型；数据类型；
solution: Experience Platform
title: 电子邮件地址数据类型
description: 了解电子邮件地址XDM数据类型。
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# [!UICONTROL 电子邮件地址]数据类型

[!UICONTROL 电子邮件地址]是描述电子邮件地址详细信息的标准体验数据模型(XDM)数据类型。

![](../images/data-types/email-address.png){width=450}

| 属性 | 描述 |
| --- | --- |
| `address` | RFC2822和后续标准中通常定义的电子邮件的技术地址（例如，`name@domain.com`）。<br><br>在XDM中，电子邮件地址必须包含有效的顶级域才能通过验证。 有关由Internet号码分配机构(IANA)定义的有效顶级域的完整列表，请参阅以下[文档](https://data.iana.org/TLD/tlds-alpha-by-domain.txt)。 |
| `label` | 可能提供的其他显示信息。 例如，如果电子邮件的Microsoft Outlook丰富地址显示为`John Smith smithjr@company.uk`，则会将`John Smith`置于此字段中。 |
| `primary` | 指示这是否是个人的主要电子邮件地址。 在给定的时间点，个人资料只能有一个`primary`电子邮件地址。 |
| `status` | 指示电子邮件地址当前是否可以使用 |
| `statusReason` | 当前`status`的说明。 |
| `type` | 帐户与人员的关联方式（如`work`或`personal`）。 |

{style="table-layout:auto"}


有关电子邮件地址数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
