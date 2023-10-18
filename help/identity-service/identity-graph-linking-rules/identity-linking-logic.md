---
title: 标识服务链接逻辑
description: 了解Identity Service如何链接不同的身份以创建客户的全面视图。
hide: true
hidefromtoc: true
badge: Alpha
source-git-commit: 03e4cd440f8627ad837a31e1c017d0b824cafb04
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 3%

---

# 标识服务链接逻辑

>[!IMPORTANT]
>
>标识图链接规则当前处于Alpha状态。 该功能和文档可能会发生更改。

当标识命名空间与标识值匹配时，将在两个标识之间建立链接。

有两种类型的标识会被关联：

* **配置文件记录**：这些身份通常来自CRM系统。
* **体验事件**：这些标识通常来自WebSDK实施或Adobe Analytics源。

## 了解Identity Service关联逻辑

身份由身份命名空间和身份值组成。

* 身份命名空间是给定的身份值到的上下文。 常见的身份命名空间示例包括CRM ID、电子邮件和电话。
* 标识值是表示实际实体的字符串。 例如：“julien”<span>“@acme.com”可以是电子邮件命名空间的身份值，555-555-1234可以是手机命名空间的相应身份值。

>[!TIP]
>
>身份命名空间非常重要，因为如果没有它，则身份值将丢失其上下文，并且没有足够的信息来成功匹配身份。

有关Identity Service链接逻辑的工作方式的可视表示形式，请参阅下图：

>[!BEGINTABS]

>[!TAB 现有图表]

假设您有一个具有三个链接身份的现有身份图：

* 电话：(555)-555-1234
* 电子邮件：julien<span>@acme.com
* CRM ID：60013ABC

![现有图](../images/identity-settings/existing-graph.png)

>[!TAB 传入数据]

一对标识已摄取到您的图形中，并且此对包含：

* CRM ID：60013ABC
* ECID：100066526

![传入数据](../images/identity-settings/incoming-data.png)

>[!TAB 更新的图表]

Identity Service识别您的图形中已存在CRM ID：60013ABC，因此仅链接新的ECID

![更新的图表](../images/identity-settings/updated-graph.png)

>[!ENDTABS]

## 客户方案

您是数据工程师，并且已将以下CRM数据集（配置文件记录）摄取到Experience Platform。

| CRM ID** | Phone* | 电子邮件* | 名字 | 姓氏 |
| --- | --- | --- | --- | --- |
| 60013ABC | 555-555-1234 | 朱利安<span>@acme.com | 朱利安 | Smith |
| 31260XYZ | 777-777-6890 | evan<span>@acme.com | Evan | Smith |

>[!NOTE]
>
>* `**`  — 表示标记为主标识的字段。
>* `*`  — 表示标记为辅助标识的字段。
>
>Identity Service不区分主标识和辅助标识。 只要字段被标记为身份，它就会被摄取到Identity Service。

您还实施了WebSDK，并摄取了包含以下数据表的WebSDK数据集（体验事件）：

| 时间戳 | 事件中的身份* | 活动 |
| --- | --- | --- |
| `t=1` | ECID：38652 | 查看主页 |
| `t=2` | ECID：38652， CRM ID：31260XYZ | 搜索鞋子 |
| `t=3` | ECID：44675 | 查看主页 |
| `t=4` | ECID：44675，CRM ID： 31260XYZ | 查看购买历史记录 |

>[!NOTE]
>
>* `*`  — 表示标记为身份的字段，其中ECID标记为主。
>* 默认情况下，人员标识符（在本例中为CRM ID）被指定为主要身份。 如果人员标识符不存在，则Cookie标识符（在本例中为ECID）将成为主标识。

在此示例中：

* `t=1`，使用台式计算机(ECID：38652)并匿名查看主页。
* `t=2`，使用同一台台式计算机，登录(CRM ID：31260XYZ)，然后搜索鞋子。
   * 用户登录后，事件会将ECID和CRM ID发送到Identity Service。
* `t=3`，使用笔记本电脑(ECID：44675)并匿名浏览。
* `t=4`，使用同一台笔记本电脑，登录(CRM ID：31260XYZ)，然后查看购买历史记录。


>[!BEGINTABS]

>[!TAB timestamp=0]

在 `timestamp=0`，则您有两个适用于两个不同客户的标识图。 他们两人分别由三个关联的身份表示。

| | CRM ID | 电子邮件 | Phone |
| --- | --- | --- | --- |
| Customer one | 60013ABC | 朱利安<span>@acme.com | 555-555-1234 |
| 客户二 | 31260XYZ | evan<span>@acme.com | 777-777-6890 |

![timestamp-0](../images/identity-settings/timestamp-zero.png)

>[!TAB timestamp=1]

在 `timestamp=1`，客户使用笔记本电脑访问您的电子商务网站、查看您的主页并匿名浏览。 此匿名浏览事件标识为ECID：38652。 由于Identity Service仅存储具有至少两个标识的事件，因此不会存储此信息。

![timestamp-one](../images/identity-settings/timestamp-one.png)

>[!TAB timestamp=2]

在 `timestamp=2`，客户使用同一台笔记本电脑访问您的电子商务网站。 他们使用用户名和密码组合登录，并浏览查找鞋子。 Identity Service在客户登录时识别他们的帐户，因为它与其CRM ID 31260XYZ相对应。 此外，Identity Service将ECID：38562与CRM ID：31260XYZ关联，因为它们在同一设备上使用相同的浏览器。

![timestamp-2](../images/identity-settings/timestamp-two.png)

>[!TAB timestamp=3]

在 `timestamp=3` 客户使用平板电脑访问您的电子商务网站并匿名浏览。 此匿名浏览事件标识为ECID：44675。 由于Identity Service仅存储具有至少两个标识的事件，因此不会存储此信息。

![timestamp-3](../images/identity-settings/timestamp-three.png)

>[!TAB timestamp=4]

在 `timestamp=4`，客户使用同一台平板电脑，登录其帐户(CRM ID：31260XYZ)并查看其购买历史记录。 此事件将他们的CRM ID：31260XYZ链接到分配给匿名浏览活动的Cookie标识符、ECID：44675，并将ECID：44675链接到客户2的标识图。

![timestamp-4](../images/identity-settings/timestamp-four.png)

>[!ENDTABS]

## 后续步骤

有关身份图链接规则的更多信息，请阅读以下文档：

* [身份图链接规则概述](./overview.md)
* [配置身份图链接规则的示例场景](./example-scenarios.md)
* [Identity Service和实时客户资料](identity-and-profile.md)
