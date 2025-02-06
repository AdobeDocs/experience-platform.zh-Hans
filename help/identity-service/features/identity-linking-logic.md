---
title: 标识服务链接逻辑
description: 了解Identity Service如何链接不同的身份以创建客户的全面视图。
exl-id: 1c958c0e-0777-48db-862c-eb12b2e7a03c
source-git-commit: 048d915d33a19a9d50a4951e165b5ade1b9d9734
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 3%

---

# 身份标识服务链接逻辑 {#identity-service-linking-logic}

>[!CONTEXTUALHELP]
>id="platform_identities_simulatedgraph"
>title="模拟图形"
>abstract="当身份标识命名空间和身份标识值匹配时，就会将身份标识链接起来。"

当标识命名空间与标识值匹配时，将在两个标识之间建立链接。

有两种类型的标识会被关联：

* **配置文件记录**：这些标识通常来自CRM系统。
* **体验事件**：这些标识通常来自WebSDK实现或Adobe Analytics源。

## 建立链接的语义含义

标识表示真实世界的实体。 如果两个身份之间建立了链接，则意味着这两个身份相互关联。 以下是说明此概念的一些示例：

| 操作 | 已建立的链接 | 含义 |
| --- | --- | --- |
| 最终用户使用计算机登录。 | CRMID和ECID已链接在一起。 | 人员(CRMID)拥有带浏览器(ECID)的设备。 |
| 最终用户使用iPhone匿名浏览。 | IDFA与ECID关联。 | Apple硬件设备(IDFA)(如iPhone)与浏览器(ECID)相关联。 |
| 最终用户先使用Google Chrome登录，然后再使用Firefox登录。 | CRMID与两个不同的ECID相关联。 | 人员(CRMID)与2个Web浏览器相关联（**注意**：每个浏览器都有自己的ECID）。 |
| 数据工程师摄取CRM记录，该记录包括两个标记为身份的字段：CRMID和电子邮件。 | CRMID和电子邮件已链接。 | 人员(CRMID)与电子邮件地址关联。 |

## 了解身份标识服务链接逻辑

身份由身份命名空间和身份值组成。

* 身份命名空间是给定的身份值到的上下文。 身份命名空间的常见示例包括CRMID、电子邮件和电话。
* 标识值是表示实际实体的字符串。 例如：“julien<span>@acme.com”可以是电子邮件命名空间的身份值，555-555-1234可以是手机命名空间的相应身份值。

>[!TIP]
>
>身份命名空间非常重要，因为如果没有它，则身份值将丢失其上下文，并且没有足够的信息来成功匹配身份。

有关Identity Service链接逻辑的工作方式的可视表示形式，请参阅下图：

>[!BEGINTABS]

>[!TAB 现有图形]

假设您有一个具有三个链接身份的现有身份图：

* 电话：(555)-555-1234
* 电子邮件：julien<span>@acme.com
* CRMID：60013ABC

![现有图形](../images/identity-settings/existing-graph.png)

>[!TAB 传入数据]

一对标识已摄取到您的图形中，并且此对包含：

* CRMID：60013ABC
* ECID：100066526

![传入数据](../images/identity-settings/incoming-data.png)

>[!TAB 已更新图形]

Identity Service识别图形中已存在CRMID：60013ABC，因此仅链接新的ECID

![已更新图形](../images/identity-settings/updated-graph.png)

>[!ENDTABS]

## 客户方案

您是数据工程师，并且已将以下CRM数据集（配置文件记录）摄取到Experience Platform。

| CRMID** | 电话* | 电子邮件* | 名字 | 姓氏 |
| --- | --- | --- | --- | --- |
| 60013ABC | 555-555-1234 | julien<span>@acme.com | 朱利安 | Smith |
| 31260XYZ | 777-777-6890 | evan<span>@acme.com | Evan | Smith |

>[!NOTE]
>
>* `**` — 表示标记为主标识的字段。
>* `*` — 表示标记为辅助标识的字段。
>
>Identity Service不区分主标识和辅助标识。 只要字段被标记为身份，它就会被摄取到Identity Service。

您还实施了WebSDK，并摄取了包含以下数据表的WebSDK数据集（体验事件）：

| 时间戳 | 事件中的身份* | 活动 |
| --- | --- | --- |
| `t=1` | ECID：38652 | 查看主页 |
| `t=2` | ECID：38652， CRMID：31260XYZ | 搜索鞋子 |
| `t=3` | ECID：44675 | 查看主页 |
| `t=4` | ECID：44675， CRMID： 31260XYZ | 查看购买历史记录 |

每个事件的主标识将根据[您配置数据元素类型](../../tags/extensions/client/web-sdk/data-element-types.md)的方式确定。

>[!NOTE]
>
>* 如果您选择CRMID作为主节点，则经过身份验证的事件（具有包含CRMID和ECID的标识映射的事件）将具有CRMID的主标识。 对于未经身份验证的事件（具有仅包含ECID的标识映射的事件），将具有ECID的主标识。 Adobe建议使用此选项。
>
>* 如果选择ECID作为主标识，则无论身份验证状态如何，ECID都将成为主标识。

在此示例中：

* `t=1`，使用台式计算机(ECID：38652)并匿名查看主页。
* `t=2`使用同一台台式计算机登录(CRMID：31260XYZ)，然后搜索鞋子。
   * 用户登录后，该事件会将ECID和CRMID发送到Identity Service。
* `t=3`，使用笔记本电脑(ECID：44675)并匿名浏览。
* `t=4`使用同一台膝上型计算机，登录(CRMID： 31260XYZ)，然后查看购买历史记录。


>[!BEGINTABS]

>[!TAB 时间戳=0]

在`timestamp=0`，您有两个适用于两个不同客户的身份图。 他们两人分别由三个关联的身份表示。

| | CRMID | 电子邮件 | 电话 |
| --- | --- | --- | --- |
| Customer one | 60013ABC | julien<span>@acme.com | 555-555-1234 |
| 客户二 | 31260XYZ | evan<span>@acme.com | 777-777-6890 |

![时间戳 — 零](../images/identity-settings/timestamp-zero.png)

>[!TAB 时间戳=1]

在`timestamp=1`，客户使用笔记本电脑访问您的电子商务网站、查看您的主页并匿名浏览。 此匿名浏览事件标识为ECID：38652。 由于Identity Service仅存储具有至少两个标识的事件，因此不会存储此信息。

![timestamp-one](../images/identity-settings/timestamp-one.png)

>[!TAB 时间戳=2]

在`timestamp=2`，客户使用同一台笔记本电脑访问您的电子商务网站。 他们使用用户名和密码组合登录，并浏览查找鞋子。 Identity Service在客户登录时识别他们的帐户，因为它与其CRMID： 31260XYZ相对应。 此外，Identity Service将ECID：38562与CRMID：31260XYZ关联起来，因为它们都在同一设备上使用相同的浏览器。

![时间戳 — 二](../images/identity-settings/timestamp-two.png)

>[!TAB 时间戳=3]

在`timestamp=3`，客户使用平板电脑访问您的电子商务网站并匿名浏览。 此匿名浏览事件标识为ECID：44675。 由于Identity Service仅存储具有至少两个标识的事件，因此不会存储此信息。

![时间戳 — 三](../images/identity-settings/timestamp-three.png)

>[!TAB 时间戳=4]

在`timestamp=4`，客户使用相同的平板电脑，登录到其帐户(CRMID：31260XYZ)并查看其购买历史记录。 此事件将他们的CRMID：31260XYZ链接到分配给匿名浏览活动的Cookie标识符ECID：44675，并将ECID：44675链接到客户2的标识图。

![时间戳–4](../images/identity-settings/timestamp-four.png)

>[!ENDTABS]
