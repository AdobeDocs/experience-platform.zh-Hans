---
title: 目标工作区
seo-title: 目标工作区
description: 在Adobe实时客户数据平台中，从左侧导航栏中选择目标以访问目标工作区。
seo-description: 在Adobe实时客户数据平台中，从左侧导航栏中选择目标以访问目标工作区。
translation-type: tm+mt
source-git-commit: 132bc9787a86045adba559c769b02927a6045b17

---


# 目标工作区 {#destinations-workspace}

在Adobe实时客户数据平台中，从左侧导航栏 **中选择** “目标”以访问“目标”工作区。

“目标”工作区由四个部分组成： **目录**、浏 **览、帐**&#x200B;户 **、数据流，******&#x200B;这些部分在以下各节中介绍。

![目标——概述](/help/rtcdp/destinations/assets/destinations-overview.png)

## Catalog {#catalog}

该选 **[!UICONTROL Catalog]** 项卡显示Adobe提供的所有目标列表，您可以将数据发送到这些目标。 在目录中选择一个目标以打开右边栏。 在此，您可以设置到目标(**Connect目标**)的连接，或通过查看文档（查看文档）了解有关每个目标的更&#x200B;**多详细信息**。

![目标目录选项](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

有关目标类别的详细信息以及有关每个目标的信息，请参阅 [目标目录](/help/rtcdp/destinations/destinations-catalog.md)。

## 浏览 {#browse}

该选 **[!UICONTROL Browse]** 项卡显示您已与之建立连接的目标。 启用切换的目标将目标设置为活动，反之亦然。 您还可以通过选择区段>浏览并选择要检查的区 **段** ，来查看有数据流动的目标。 请参阅下表，了解在“浏览”选项卡中为每个目标提供的所有信息：

![浏览选项卡](/help/rtcdp/destinations/assets/browse-tab.png)

| 元素 | 描述 |
---------|----------
| 目标名称 | 您为激活流程提供到此目标的名称。 |
| 目标 | 您为激活流程选择的目标平台。 |
| 已创建 | 创建到目标的激活流程的日期和UTC时间。 |
| 连接类型 | *仅适用于电子邮件营销目标*。 表示到存储存储桶的连接类型。 可以是S3或FTP。 |
| 用户名 | 您为目标流选择的帐户凭据。 |
| 区段 | 要激活到此目标的区段数。 |
| 状态 | `Active` 或 `Inactive`. 指示数据当前是否正在激活到此目标。 要编辑状态，请参阅停 [用激活](/help/rtcdp/destinations/activate-destinations.md#disable-activation)。 |

单击目标行可在右边栏中显示有关目标的更多信息。

![单击目标行](/help/rtcdp/destinations/assets/click-destination-row.png)

选择目标名称可查看有关激活到此目标的区段的信息。 单 **[!UICONTROL Edit activation]** 击可修改或添加到要发送到此目标的区段。

## 帐户 {#accounts}

在选项卡 **[!UICONTROL Accounts]** 中，您可以进一步了解您与各种目标建立的连接。 请参阅下表，了解您可以获取的每个目标的所有信息：

![“帐户”选项卡](/help/rtcdp/destinations/assets/accounts-tab.png)

| 元素 | 描述 |
---------|----------
| 平台 | 您为其设置连接的目标。 |
| 用户名 | 您在连接目标向导中选 [择的用户名](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination)。 |
| 流 | 表示与为目标创建的基本信息连接的唯一成功目标流的数量。 |
| 已授权 | 到此目标的连接被授权的日期。 |

## 数据流 {#data-flows}

该 **[!UICONTROL Data flows]** 选项卡显示您在实时客户数据平台中设置的激活流程的图形表示。

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

选择页面上显示的任意目标，然后按 **[!UICONTROL View flows]** 键查看您为每个目标设置的所有数据流的信息。

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)