---
title: 帐户详细信息数据类型
description: 了解帐户详细信息Experience Data Model (XDM)数据类型。
exl-id: 17254393-263e-4000-9bd2-815a9e842533
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 11%

---

# [!UICONTROL 帐户详细信息]数据类型

[!UICONTROL 帐户详细信息]是标准体验数据模型(XDM)数据类型，用于描述与业务组织相关的详细信息。

![数据类型结构](../images/data-types/account-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `annualRevenue` | [[!UICONTROL 货币]](./currency.md) | 估计的组织年收入金额。 |
| `DUNSNumber` | 字符串 | 组织的Dun &amp; Bradstreet D-U-N-S编号。 这是分配给Dun &amp; Bradstreet数据库中每个营业地点的非指示性九位数编号，具有唯一、单独和独特的操作，并由Dun &amp; Bradstreet独家维护。 |
| `NAICSCode` | 字符串 | 该组织在北美行业分类系统中的分类。 |
| `NAICSDescription` | 字符串 | 对组织业务线的简要描述（基于其NAICS代码）。 |
| `SICCode` | 字符串 | 组织的标准行业分类(SIC)代码。 这是一个四位数的代码，根据公司的业务活动对公司所属的行业进行分类。 |
| `SICDescription` | 字符串 | 对组织业务线的简要描述（基于其SIC代码）。 |
| `companyProductAndServices` | 字符串 | 组织正在交易或开展业务的产品和服务。 |
| `facebookPageUrl` | 字符串 | 指向组织的Facebook帐户的网站链接。 |
| `industry` | 字符串 | 该组织所属的行业。 这是自由格式字段，建议在查询中使用结构化值或使用`xdm:classifier`属性。 |
| `jigsaw` | 字符串 | 组织的Data.com键。 |
| `linkedinPageUrl` | 字符串 | 指向组织的LinkedIn帐户的网站链接。 |
| `logoUrl` | 字符串 | 要与Salesforce实例的URL（例如`https://yourInstance.salesforce.com/`）组合的路径，用于生成URL以请求与组织关联的社交网络个人资料图像。 生成的URL会返回指向组织的社交网络个人资料图像的HTTP重定向（代码302）。 |
| `marketSegment` | 字符串 | 组织参与的指定市场受众。 这是自由格式字段，建议在查询中使用结构化值或使用`xdm:identifier`属性。 |
| `numberOfEmployees` | 整数 | 组织内的员工数。 |
| `organizationType` | 字符串 | 描述组织类型的标签。 |
| `primaryEmailDomain` | 字符串 | 组织用于其人员的主要电子邮件域。 |
| `rating` | 两次 | 此组织的计算得分或星级。 `1`表示可能的最大评分，`0`表示可能的最小评分。 |
| `tickerSymbol` | 字符串 | 此帐户的股市符号。最多 20 个字符。 |
| `twitterHandleUrl` | 字符串 | 指向组织的twitter句柄的网站链接。 |
| `website` | 字符串 | 组织网站的 URL。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.schema.json)
