---
title: 目标工作区
seo-title: 目标工作区
description: 在Adobe实时客户数据平台中，从左侧导航栏中选择目标以访问目标工作区。
seo-description: 在Adobe实时客户数据平台中，从左侧导航栏中选择目标以访问目标工作区。
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# 目标工作区 {#destinations-workspace}

在Adobe实时客户数据平台中，从左 **[!UICONTROL Destinations]** 侧导航栏中进行选择以访问工 [!UICONTROL Destinations] 作区。

工 [!UICONTROL Destinations] 作区由四个部分组成， **[!UICONTROL Catalog]**&#x200B;分别 **[!UICONTROL Browse]**&#x200B;是、 **[!UICONTROL Accounts]**&#x200B;和 **[!UICONTROL System View]**，这些部分在以下各节中进行了介绍。

![目标——概述](/help/rtcdp/destinations/assets/destinations-overview.png)

## [!UICONTROL Catalog] {#catalog}

该选 **[!UICONTROL Catalog]** 项卡显示Adobe提供的所有目标的列表，您可以将数据发送到该目标。

使用页面上的搜索功能可定位特定目标或使用控件筛选目标 **[!UICONTROL Categories]** 。

在目录中选择一个目标以打开右边栏。 在此，您可以设置到目标(**[!UICONTROL Connect destination]**)的连接，视图现有目标连接(**[!UICONTROL Browse destinations]**)，或通过查看文档(**[!UICONTROL View documentation]**)了解有关每个目标的更多详细信息。

![目标目录选项](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

有关目标类别的详细信息以及每个目标的相关信息，请参 [阅目标目录](/help/rtcdp/destinations/destinations-catalog.md)。

## [!UICONTROL Browse] {#browse}

该选 **[!UICONTROL Browse]** 项卡显示您已与之建立连接的目标。 打开切换 **[!UICONTROL enabled]** 的目标将目标设置为活动，反之亦然。 您还可以通过选择和选择要检查的区段，视图 **[!UICONTROL Segments > Browse]** 有数据流动的目标。 请参阅下表，了解在“浏览”选项卡中为每个目标提供的所有信息：

![浏览选项卡](/help/rtcdp/destinations/assets/browse-tab.png)

| 元素 | 描述 |
---------|----------
| 名称 | 您为激活流提供到此目标的名称。 |
| [!UICONTROL Destination] | 您为激活流选择的目标平台。 |
| [!UICONTROL Connection Type] | 表示到存储存储段或目标的连接类型。 <ul><li>对于电子邮件营销目标：可以是S3或FTP。</li><li>对于实时广告目标：服务器到服务器</li></ul> |
| [!UICONTROL Username] | 您为目标流选择的帐户凭据。 |
| [!UICONTROL Segments] | 要激活到此目标的区段数。 |
| [!UICONTROL Created] | 创建到目标的激活流的日期和UTC时间。 |
| [!UICONTROL Status] | `Active` 或 `Inactive`. 指示数据当前是否正在激活到此目标。 要编辑状态，请参阅禁 [用激活](/help/rtcdp/destinations/activate-destinations.md#disable-activation)。 |

单击目标行可在右边栏中显示有关目标的更多信息。

![单击目标行](/help/rtcdp/destinations/assets/click-destination-row.png)

选择目标名称可查看有关激活到此目标的区段的信息。 单 **[!UICONTROL Edit activation]** 击可修改或添加到要发送到此目标的区段。

## [!UICONTROL Accounts] {#accounts}

在选项卡 **[!UICONTROL Accounts]** 中，您可以进一步了解您与各种目标建立的连接。 请参阅下表，了解您可以获取的每个目标的所有信息：

![“帐户”选项卡](/help/rtcdp/destinations/assets/accounts-tab.png)

| 元素 | 描述 |
---------|----------
| [!UICONTROL Platform] | 您为其设置连接的目标。 |
| [!UICONTROL Connection Type] | 表示到存储存储段或目标的连接类型。 <ul><li>对于电子邮件营销目标：可以是S3或FTP。</li><li>对于实时广告目标：服务器到服务器</li><li>对于Amazon S3云存储目标：访问密钥 </li><li>对于SFTP云存储目标：SFTP的基本身份验证</li></ul> |
| [!UICONTROL Username] | 您在连接目标向导中选 [择的用户名](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination)。 |
| [!UICONTROL Data Flows] | 表示与为目标创建的基本信息连接的唯一成功目标流的数量。 |
| [!UICONTROL Authorized] | 到此目标的连接被授权的日期。 |
| [!UICONTROL Status] | `Active` 或 `Inactive`. 指示数据当前是否正在激活到此目标。 要编辑状态，请参阅禁 [用激活](/help/rtcdp/destinations/activate-destinations.md#disable-activation)。 |

## [!UICONTROL System View] {#system-view}

该 **[!UICONTROL System View]** 选项卡显示您在实时客户数据平台中设置的激活流的图形表示形式。

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

选择页面上显示的任意目标，然后按 **[!UICONTROL View flows]** 键查看您为每个目标设置的所有连接的相关信息。

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)