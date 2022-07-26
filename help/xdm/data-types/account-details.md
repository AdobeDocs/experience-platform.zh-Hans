---
title: 帐户详细信息数据类型
description: 本文档概述了“帐户详细信息”体验数据模型(XDM)数据类型。
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 5%

---

# [!UICONTROL 帐户详细信息] 数据类型

[!UICONTROL 帐户详细信息] 是一种标准的体验数据模型(XDM)数据类型，用于描述与业务组织相关的详细信息。

![数据类型结构](../images/data-types/account-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `annualRevenue` | [[!UICONTROL 货币]](./currency.md) | 组织的年收入估计数。 |
| `DUNSNumber` | 字符串 | 该组织的Dun &amp; Bradstreet D-U-N-S号码。 这是一个非指示性的九位数字，分配给Dun &amp; Bradstreet数据库中每个业务位置，具有独特、单独和独特的操作，并且仅由Dun &amp; Bradstreet维护。 |
| `NAICSCode` | 字符串 | 组织在北美行业分类系统中的分类。 |
| `NAICSDescription` | 字符串 | 基于组织NAICS代码的组织业务线的简要描述。 |
| `SICCode` | 字符串 | 组织的标准行业分类(SIC)代码。 这是一个四位数的代码，用于根据公司的业务活动对所属行业进行分类。 |
| `SICDescription` | 字符串 | 基于组织SIC代码的业务线的简要描述。 |
| `companyProductAndServices` | 字符串 | 组织在中处理或开展业务的产品和服务。 |
| `facebookPageUrl` | 字符串 | 指向组织Facebook帐户的网站链接。 |
| `industry` | 字符串 | 此组织所属的行业。 这是一个自由格式字段，建议使用结构化值进行查询或使用 `xdm:classifier` 属性。 |
| `jigsaw` | 字符串 | 组织的Data.com密钥。 |
| `linkedinPageUrl` | 字符串 | 指向组织LinkedIn帐户的网站链接。 |
| `logoUrl` | 字符串 | 要与Salesforce实例的URL组合的路径(例如， `https://yourInstance.salesforce.com/`)以生成一个URL，以请求与组织关联的社交网络用户档案图像。 生成的URL将返回HTTP重定向（代码302）到组织的社交网络配置文件图像。 |
| `marketSegment` | 字符串 | 组织参与的已命名市场区段。 这是一个自由格式字段，建议使用结构化值进行查询或使用 `xdm:identifier` 属性。 |
| `numberOfEmployees` | 整数 | 组织中的员工数量。 |
| `organizationType` | 字符串 | 描述组织类型的标签。 |
| `primaryEmailDomain` | 字符串 | 组织为其人员使用的主要电子邮件域。 |
| `rating` | 双精度 | 此组织的计算得分或星级评级。 `1` 指示最大可能的评级，以及 `0` 是最低的评级。 |
| `tickerSymbol` | 字符串 | 此帐户的股市符号。 最多20个字符。 |
| `twitterHandleUrl` | 字符串 | 指向组织twitter句柄的网站链接。 |
| `website` | 字符串 | 组织网站的URL。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.schema.json)
