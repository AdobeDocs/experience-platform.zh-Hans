---
title: 身份优化算法
description: 了解Identity Service中的身份优化算法。
hide: true
hidefromtoc: true
badge: Alpha
source-git-commit: 8f99dc633c87fa36cc0c5413d23b97b4fce7dbc3
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 2%

---

# 身份优化算法

>[!IMPORTANT]
>
>身份优化算法Alpha。 该功能和文档可能会发生更改。

身份优化算法是一种规则，有助于确保身份图代表单个人员，从而防止在Real-time Customer Profile上不需要的身份合并。

## 输入参数

单个合并的用户档案及其对应的身份图应表示单个个人（人员实体）。 通常单个人员由CRM ID和/或登录ID表示。 预计不会将两个个人(CRM ID)合并到单个配置文件或图表中。

您必须使用身份优化算法指定哪些命名空间代表Identity Service中的人员实体。 例如，如果CRM数据库定义了一个要与单个CRM ID和单个电子邮件地址关联的用户帐户，则此沙盒的标识设置将如下所示：

* CRM ID命名空间=唯一
* 电子邮件命名空间=唯一

声明为唯一的命名空间会自动配置为在给定身份图内最多有一个。 例如，如果您声明CRM ID命名空间是唯一的，则标识图只能有一个包含CRM ID命名空间的标识。

>[!NOTE]
>
>* 目前，算法仅支持使用单个登录标识符（一个登录命名空间）。 目前不支持多个登录标识符（用于登录的多个身份命名空间）、家庭实体图和层次图结构。
>
>* 作为人员标识符并且在沙盒中用于生成身份图的所有命名空间必须标记为唯一的命名空间。 否则，您可能会看到不希望出现的链接结果。

## 过程

在摄取新身份时，Identity Service会检查新身份及其对应的命名空间是否会导致超过配置的限制。 如果未超出限制，则将继续摄取新身份，并且这些身份将链接到图表。 但是，如果超过限制，身份优化算法将更新图形，以便记录最新的时间戳，并删除优先级较低的命名空间的最旧链接。

## 身份优化算法的示例场景

以下部分概述了在共享设备或摄取具有相同时间戳的数据等场景中，身份优化算法的行为。

### 共享设备

共享设备是指由多个用户使用的设备。 例如，共享设备可以是您与合作伙伴或家庭成员共享的笔记本电脑或平板电脑、库计算机或公共信息亭。

>[!BEGINTABS]

>[!TAB 示例1]

| 命名空间 | 限制 |
| --- | --- |
| CRM ID | 1 |
| 电子邮件 | 1 |
| ECID | 不适用 |

在此示例中，CRM ID和电子邮件都被指定为唯一的命名空间。 在 `timestamp=0`，则一个CRM记录数据集被摄取，并由于限制配置而创建两个不同的图。 每个图形都包含一个CRM ID和一个电子邮件命名空间。

* `timestamp=1`： Jane使用笔记本电脑登录到您的电子商务网站。 Jane由她的CRM ID和电子邮件代表，而她使用的笔记本电脑上的Web浏览器由一个ECID代表。
* `timestamp=2`： John使用相同的笔记本电脑登录到您的电子商务网站。 John由他的CRM ID和电子邮件代表，而他使用的Web浏览器已由ECID代表。 由于同一个ECID链接到两个不同的图形，因此Identity Service能够知道此设备（笔记本电脑）是共享设备。
* 但是，由于限制配置（每个图形最多设置一个CRM ID命名空间和一个电子邮件命名空间），身份优化算法随后将图形拆分为两个。
   * 最后，由于John是最后一个经过身份验证的用户，因此表示笔记本电脑的ECID仍与他的图表关联，而不是Jane&#39;s的图表。

![共享设备案例一](../images/identity-settings/shared-device-case-one.png)

>[!TAB 示例2]

| 命名空间 | 限制 |
| --- | --- |
| CRM ID | 1 |
| ECID | 不适用 |

在此示例中，CRM ID命名空间被指定为唯一的命名空间。

* `timestamp=1`： Jane使用笔记本电脑登录到您的电子商务网站。 她由CRM ID代表，笔记本电脑上的Web浏览器由ECID代表。
* `timestamp=2`： John使用相同的笔记本电脑登录到您的电子商务网站。 他由他的CRM ID表示，他所使用的Web浏览器由相同的ECID表示。
   * 此事件将两个独立的CRM ID链接到同一ECID，该ECID已超过配置的一个CRM ID限制。
   * 因此，身份优化算法会删除旧链接，在本例中，该链接是链接在Jane的CRM ID `timestamp=1`.
   * 但是，尽管Jane的CRM ID不再作为Identity Service上的图形存在，但仍将作为Real-time Customer Profile上的个人资料保留。 这是因为标识图必须至少包含两个链接的标识，并且在删除链接后，Jane的CRM ID将不再具有要链接到的其他标识。

![shared-device-case-2](../images/identity-settings/shared-device-case-two.png)

>[!ENDTABS]

### 错误电子邮件

在某些情况下，用户可能会为其电子邮件和/或电话号码输入错误的值。

| 命名空间 | 限制 |
| --- | --- |
| CRM ID | 1 |
| 电子邮件 | 1 |
| ECID | 不适用 |

在此示例中，CRM ID和电子邮件命名空间指定为唯一。 考虑Jane和John使用错误的电子邮件值（例如，测试）注册您的电子商务网站的情况<span>@test.com)。

* `timestamp=1`： Jane在其iPhone上使用Safari登录到您的电子商务网站，并建立其CRM ID（登录信息）和ECID（浏览器）。
* `timestamp=2`： John在其iPhone上使用Google Chrome登录到您的电子商务网站，并建立其CRM ID（登录信息）和ECID（浏览器）。
* `timestamp=3`：您的数据工程师摄取Jane的CRM记录，这会导致她的CRM ID与错误电子邮件关联。
* `timestamp=4`：您的数据工程师摄取John的CRM记录，这会导致其CRM ID链接到错误的电子邮件。
   * 然后，这将违反配置的限制，因为它将创建具有两个CRM ID命名空间的单个图形。
   * 因此，身份优化算法会删除较旧的链接，在本例中，该链接是Jane的具有CRM ID命名空间的身份与具有测试的身份之间的链接<span>@test。

使用身份优化算法，错误的身份值（如虚假电子邮件或电话号码）不会在多个不同的身份图上传播。

![错误电子邮件](../images/identity-settings/bad-email.png)

### 匿名事件关联

ECID存储未经身份验证的（匿名）事件，而CRM ID存储经过身份验证的事件。 在共享设备的情况下，ECID（未验证事件的载体）与 **上次验证用户**.

查看下图以更好地了解匿名事件关联的工作方式：

* 凯文和诺拉共享平板电脑。
   * `timestamp=1`：Kevin使用自己的帐户登录到电子商务网站，从而建立自己的CRM ID（登录信息）和ECID（浏览器）。 登录时，Kevin现在被视为最后经过身份验证的用户。
   * `timestamp=2`： Nora使用她的帐户登录到电子商务网站，从而建立她的CRM ID（登录信息）和相同的ECID。 登录时，Nora现在被视为最后经过身份验证的用户。
   * `timestamp=3`：Kevin使用平板电脑浏览电子商务网站，但不会使用其帐户登录。 之后，Kevin的浏览活动存储在ECID中，ECID又与Nora相关联，因为她是最后一个经过身份验证的用户。 此时，Nora拥有匿名活动。
      * 在Kevin再次登录之前，Nora的合并配置文件将与针对ECID存储的所有未经身份验证的事件相关联（其中ECID是主要身份）。
   * `timestamp=4`：Kevin第二次登录。 此时，他再次成为最后一个经过身份验证的用户，并且现在拥有未经身份验证的事件：
      * 首次登录之前 `timestamp=1`；和
      * 他或Nora在凯文首次登录和第二次登录之间匿名浏览时所做的任何活动。

![非事件关联](../images/identity-settings/anon-event-association.png)


## 后续步骤

有关身份图链接规则的更多信息，请阅读以下文档：

* [身份图链接规则概述](./overview.md)
* [配置身份图链接规则的示例场景](./example-scenarios.md)
* [身份链接逻辑](./identity-linking-logic.md)
* [Identity Service和实时客户资料](identity-and-profile.md)
