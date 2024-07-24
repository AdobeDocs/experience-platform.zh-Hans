---
title: 配置示例
description: 使用图形模拟工具了解配置的示例。
badge: Beta 版
source-git-commit: 536770d0c3e7e93921fe40887dafa5c76e851f5e
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 10%

---

# 示例图形配置

>[!AVAILABILITY]
>
>标识图链接规则当前处于测试阶段。 有关参与标准的信息，请与您的Adobe客户团队联系。 该功能和文档可能会发生更改。

>[!NOTE]
>
>* “CRMID”和“loginID”是自定义命名空间。 在本文档中，“CRMID”是人员标识符，“loginID”是与给定人员关联的登录标识符。
>* 要模拟本文档中概述的示例图形场景，您必须首先创建两个自定义命名空间，一个具有身份符号“CRMID”，另一个具有身份符号“loginID”。 标识符号区分大小写。

本文档概述了在处理身份数据时可能遇到的常见场景的示例图形配置。

## 仅限CRMID

这是一个简单的实施方案示例，其中摄取在线事件（CRMID和ECID），并仅针对CRMID存储离线事件（配置文件记录）。

**实现：**

| 使用的命名空间 | Web行为收集方法 |
| --- | --- |
| CRMID、ECID | Web SDK |

**事件：**

您可以通过将以下事件复制到文本模式，在图形模拟中创建此方案：

* CRMID：Tom，ECID：111

**算法配置：**

您可以通过为算法配置以下设置，在图形模拟中创建此方案：

| 优先级 | 显示名称 | 标识类型 | 每个图唯一 |
| ---| --- | --- | --- |
| 1 | CRMID | 跨设备 | 是 |
| 2 | ECID | COOKIE | 否 |

实时客户个人资料的&#x200B;**主身份选择：**

在此配置的上下文中，主标识的定义如下所示：

| 身份验证状态 | 事件中的命名空间 | 主要标识 |
| --- | --- | --- |
| Authenticated | CRMID、ECID | CRMID |
| 未验证 | ECID | ECID |

>[!BEGINTABS]

>[!TAB 理想的单人图方案]

下面是一个理想的单人图示例，其中CRMID是唯一的，并且被赋予最高优先级。

![理想单人图的模拟示例，其中CRMID是唯一的，并且被赋予最高优先级。](../images/graph-examples/crmid_only_single.png)

>[!TAB 多人图表方案]

以下是多人图的一个示例。 此示例显示了“共享设备”方案，其中存在两个CRMID，并且已删除具有已建立旧链接的一个CRMID。

![多人图形的模拟示例。 此示例显示了一个共享设备方案，其中存在两个CRMID，并且旧的已建立链接被删除。](../images/graph-examples/crmid_only_multi.png)

>[!ENDTABS]

## 使用哈希电子邮件的CRMID

在此方案中，CRMID是摄取的，表示在线（体验事件）和离线（配置文件记录）数据。 此方案还涉及引入哈希电子邮件，该电子邮件表示在CRM记录数据集中与CRMID一起发送的其他命名空间。

**实现：**

| 使用的命名空间 | Web行为收集方法 |
| --- | --- |
| CRMID、Email_LC_SHA256、ECID | Web SDK |

**事件：**

您可以通过将以下事件复制到文本模式，在图形模拟中创建此方案：

* CRMID： Tom， Email_LC_SHA256： tom<span>@acme.com
* CRMID：Tom，ECID：111
* CRMID： Summer， Email_LC_SHA256： summer<span>@acme.com
* CRMID：夏天，ECID：222

**算法配置：**

您可以通过为算法配置以下设置，在图形模拟中创建此方案：

| 优先级 | 显示名称 | 标识类型 | 每个图唯一 |
| ---| --- | --- | --- |
| 1 | CRMID | 跨设备 | 是 |
| 2 | 电子邮件（SHA256，小写） | 电子邮件 | 否 |
| 3 | ECID | COOKIE | 否 |

**个人资料的主要身份选择：**

在此配置的上下文中，主标识的定义如下所示：

| 身份验证状态 | 事件中的命名空间 | 主要标识 |
| --- | --- | --- |
| Authenticated | CRMID、ECID | CRMID |
| 未验证 | ECID | ECID |

>[!BEGINTABS]

>[!TAB 理想的单人图方案]

![在此示例中，生成了两个单独的图形，每个图形表示一个单独的实体。](../images/graph-examples/crmid_hashed_single.png)

>[!TAB 多人图表：共享设备]

![在此示例中，模拟图形显示“共享设备”方案，因为Tom和Summer都与同一ECID相关联。](../images/graph-examples/crmid_hashed_shared_device.png)

>[!TAB 多人图表：非唯一电子邮件]

![此方案类似于“共享设备”方案。 但是，人员实体不是共享ECID，而是与同一电子邮件帐户关联。](../images/graph-examples/crmid_hashed_nonunique_email.png)

>[!ENDTABS]

## CRMID，带有哈希电子邮件、哈希手机、GAID和IDFA

此方案与上一个方案类似。 但是，在此方案中，经过哈希处理的电子邮件和手机将标记为身份，以便在区段匹配中使用。

**实现：**

| 使用的命名空间 | Web行为收集方法 |
| --- | --- |
| CRMID、Email_LC_SHA256、Phone_SHA256、GAID、IDFA、ECID | Web SDK |

**事件：**

您可以通过将以下事件复制到文本模式，在图形模拟中创建此方案：

* CRMID：Tom，Email_LC_SHA256：aabbcc，Phone_SHA256:123-4567
* CRMID：Tom，ECID：111
* CRMID：Tom，ECID：222，IDFA：A-A-A
* CRMID：Summer，Email_LC_SHA256：deeff，Phone_SHA256:765-4321
* CRMID：夏天，ECID：333
* CRMID：Summer，ECID：444，GAID：B-B-B

**算法配置：**

您可以通过为算法配置以下设置，在图形模拟中创建此方案：

| 优先级 | 显示名称 | 标识类型 | 每个图唯一 |
| ---| --- | --- | --- |
| 1 | CRMID | 跨设备 | 是 |
| 2 | 电子邮件（SHA256，小写） | 电子邮件 | 否 |
| 3 | 手机 (SHA256) | 电话 | 否 |
| 4 | Google Ad ID (GAID) | 设备 | 否 |
| 5 | Apple IDFA(Apple的ID) | 设备 | 否 |
| 6 | ECID | COOKIE | 否 |

**个人资料的主要身份选择：**

在此配置的上下文中，主标识的定义如下所示：

| 身份验证状态 | 事件中的命名空间 | 主要标识 |
| --- | --- | --- |
| Authenticated | CRMID、IDFA、ECID | CRMID |
| Authenticated | CRMID、GAID、ECID | CRMID |
| Authenticated | CRMID、ECID | CRMID |
| 未验证 | GAID、ECID | GAID |
| 未验证 | IDFA、ECID | IDFA |
| 未验证 | ECID | ECID |

>[!BEGINTABS]

>[!TAB 理想的单人图方案]

![](../images/graph-examples/crmid_hashed_single_seg_match.png)

>[!ENDTABS]

<!-- 
## Single CRMID with multiple login IDs (simple)

In this scenario, there is a single CRMID that represents a person entity. However, a person entity may have multiple login identifiers:

* A given person entity can have different account account types (personal vs. business, account by state, account by brand, etc.)
* A given person entity may use different email addresses for any number of accounts.

Therefore, **it is crucial that the CRMID is always sent for every user**. Failure to do so may result in a "dangling" login ID scenario, where a single person entity is assumed to be sharing a device with another person.

**Implementation:**

| Namespaces used | Web behavior collection method |
| --- | --- |
| CRMID, loginID, ECID | Web SDK |

**Events:**

You can create this scenario in graph simulation by copying the following events to text mode:

* CRMID: John, loginID: ID_A
* CRMID: John, loginID: ID_B
* loginID: ID_A, ECID: 111
* CRMID: Jane, loginID: ID_C
* CRMID: Jane, loginID: ID_D
* loginID: ID_C, ECID: 222

**Algorithm configuration:**

You can create this scenario in graph simulation by configuring the following setup for your algorithm configuration:

| Priority | Display name | Identity symbol | Identity type | Unique per graph |
| ---| --- | --- | --- | --- |
| 1 | CRMID | CRMID | CROSS_DEVICE | Yes |
| 2 | loginID | loginID | CROSS_DEVICE | No |
| 3 | ECID | ECID | COOKIE | No |

## Single CRMID with multiple login IDs (complex)

In this scenario, there is a single CRMID that represents a person entity. However, a person entity may have multiple login identifiers:

* A given person entity can have different account account types (personal vs. business, account by state, account by brand, etc.)
* A given person entity may use different email addresses for any number of accounts.

The case of "dangling" loginID also applies for this scenario.

**Implementation:**

| Namespaces used | Web behavior collection method |
| --- | --- |
| CRMID, Email_LC_SHA256, Phone_SHA256, loginID, ECID, AAID | Adobe Analytics source connector |


**Events:**

You can create this scenario in graph simulation by copying the following events to text mode:

* CRMID: John, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* CRMID: John, loginID: ID_A
* CRMID: John, loginID: ID_B
* loginID:ID_A, ECID: 111, AAID: AAA
* CRMID: Jane, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* CRMID: Jane, loginID: ID_C
* CRMID: Jane, loginID: ID_D
* loginID: ID_C, ECID: 222, AAID: BBB

**Algorithm configuration:**

You can create this scenario in graph simulation by configuring the following setup for your algorithm configuration:

| Priority | Display name | Identity symbol | Identity type | Unique per graph |
| ---| --- | --- | --- | --- |
| 1 | CRMID | CRMID | CROSS_DEVICE | Yes |
| 2 | Email_LC_SHA256 | Email_LC_SHA256 | EMAIL | No |
| 3 | Phone_SHA256 | Phone_SHA256 | PHONE | No |
| 4 | loginID | loginID | CROSS_DEVICE | No |
| 5 | ECID | ECID | COOKIE | No |
| 6 | AAID | AAID | COOKIE | No |
 -->
