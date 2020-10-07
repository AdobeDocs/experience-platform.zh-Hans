---
keywords: RTCDP;rtcdp
title: 目标工作区
seo-title: 目标工作区
description: “目标”工作区由四个部分组成，即目录、浏览、帐户和系统视图，这些部分在以下各节中有介绍。
seo-description: 在Adobe实时客户数据平台中，从左侧导航栏中选择目标以访问目标工作区。
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 2%

---


# 目标工作区 {#destinations-workspace}

在Adobe实时数据平台中，从左侧 **[!UICONTROL 导航栏]** 中选择目标以访问 [!UICONTROL 目标] 工作区。

工 [!UICONTROL 作区] 由四个部分组成： [!UICONTROL Catalog]、 Browse Accounts [!UICONTROL 、 Accounts]Destinations System视图, 下面几节介绍了这些部分。

![目标——概述](/help/rtcdp/destinations/assets/destinations-overview.png)

## [!UICONTROL 目录] {#catalog}

“目 **[!UICONTROL 录]** ”选项卡显示Adobe实时CDP中所有可用目标的列表，您可以将数据发送到这些目标。

Adobe实时CDP用户界面在目标目录页面上提供了许多搜索和筛选选项：

* 使用页面上的搜索功能查找特定目标。
* 使用类别控件 [!UICONTROL 筛选目] 标。
* 在所有目 [!UICONTROL 标和我的] 目 [!UICONTROL 标之间切换]。 选择 **[!UICONTROL 所有目标]** 后，将显示所有可用的Adobe实时CDP目标。 选择 **[!UICONTROL 我的目]** 标后，您只能看到已建立连接的目标。
* 选择以视图 **[!UICONTROL 连接]** 和／或 **[!UICONTROL 扩展]**。 要了解两个类别之间的差异，请参 [阅目标类型和类别](/help/rtcdp/destinations/destination-types.md)。

![目标过滤和搜索演示](/help/rtcdp/destinations/assets/destinations-search-and-filter.gif)

目标卡包含Configure **** （配置） **[!UICONTROL 或Activate]** （激活）控件，以及可显示更多选项的辅助控件。 这些内容均描述如下：

| 控制 | 描述 |
---------|----------
| [!UICONTROL 配置] | 允许您创建到目标的连接。 |
| [!UICONTROL 激活] | 建立到目标的连接后，即可激活区段。 |
| [!UICONTROL 视图帐户] | 视图您为目标连接的帐户。 |
| [!UICONTROL 视图数据流] | 视图目标的激活流。 |
| [!UICONTROL 视图文档] | 打开指向该特定目标的文档页面的链接，以了解更多信息并帮助您设置它。 |

![目标卡上的控件](/help/rtcdp/destinations/assets/destination-card-options.png)

在目录中选择目标卡以打开右边栏。  此处，您可以看到目标的描述。 右边栏提供了上表中描述的相同控件，以及目标的描述，以及目标类别和类型的指示。

![目标目录选项](/help/rtcdp/destinations/assets/destination-right-rail.png)

有关目标类别和每个目标的信息，请参阅目 [标目录](/help/rtcdp/destinations/destinations-catalog.md) 、 [目标类型和类别](/help/rtcdp/destinations/destination-types.md)。

## [!UICONTROL 帐户] {#accounts}

在“帐 **[!UICONTROL 户]** ”选项卡中，您可以进一步了解您与各种目标建立的连接。 请参阅下表，了解您可以在每个目标上获取的所有信息：

>[!TIP]
>
>使用“ ![平台](/help/rtcdp/destinations/assets/add-data-symbol.png) ”列中的“添 **[!UICONTROL 加数据]** ”按钮为该帐户创建新的目标连接。

![“帐户”选项卡](/help/rtcdp/destinations/assets/accounts-tab.png)

| 元素 | 描述 |
---------|----------
| [!UICONTROL 平台] | 您为其设置连接的目标。 |
| [!UICONTROL 连接类型] | 表示到存储存储段或目标的连接类型。 <ul><li>对于电子邮件营销目标：可以是S3或FTP。</li><li>对于实时广告目标：服务器到服务器</li><li>对于AmazonS3云存储目标：访问密钥 </li><li>对于SFTP云存储目标：SFTP的基本身份验证</li></ul> |
| [!UICONTROL 用户名] | 在连接目标向导中选 [择的用户名](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination)。 |
| [!UICONTROL 目标] | 表示通过为目标创建的基本信息连接的唯一成功目标流的数量。 |
| [!UICONTROL 已授权] | 到此目标的连接被授权的日期。 |

## [!UICONTROL 浏览] {#browse}

“浏 **[!UICONTROL 览]** ”选项卡显示您已建立连接的目标。 启用“启 **[!UICONTROL 用]** ”切换的目标将目标设置为活动，反之亦然。 您还可以通过选择“区段”>“浏览”并选择要检 **[!UICONTROL 查的区段]** ，来 **[!UICONTROL 视图您拥]** 有数据流动的目标。 有关在“浏览”选项卡中为每个目标提供的所有信息，请参阅下表：

>[!TIP]
>
>使用“ ![名称](/help/rtcdp/destinations/assets/add-data-symbol.png) ”列中的“添 **[!UICONTROL 加数据”按]** 钮，可将其他区段激活到该目标。

![浏览选项卡](/help/rtcdp/destinations/assets/browse-tab.png)

| 元素 | 描述 |
---------|----------
| 名称 | 您为激活流提供到此目标的名称。 |
| [!UICONTROL 目标] | 您为激活流选择的目标平台。 |
| [!UICONTROL 连接类型] | 表示到存储存储段或目标的连接类型。 <ul><li>对于电子邮件营销目标：可以是S3或FTP。</li><li>对于实时广告目标：服务器到服务器</li></ul> |
| [!UICONTROL 用户名] | 您为目标流选择的帐户凭据。 |
| [!UICONTROL 区段] | 正在激活到此目标的区段数。 |
| [!UICONTROL 已创建] | 创建到目标的激活流的日期和UTC时间。 |
| [!UICONTROL 状态] | `Active` 或 `Inactive`. 指示数据当前是否正在激活到此目标。 要编辑状态，请参阅禁 [用激活](/help/rtcdp/destinations/activate-destinations.md#disable-activation)。 |

单击目标行以在右边栏中显示有关目标的更多信息。

![单击目标行](/help/rtcdp/destinations/assets/click-destination-row.png)

选择目标名称可查看有关激活到此目标的区段的信息。 单 **[!UICONTROL 击编辑激活]** ，以修改或添加要发送到此目标的区段。

## [!UICONTROL 系统视图] {#system-view}

“ **[!UICONTROL 系统视图]** ”选项卡显示您在实时客户数据平台中设置的激活流的图形表示。

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

选择页面上显示的任意目标，并按 **[!UICONTROL 视图流]** ，查看您为每个目标设置的所有连接的相关信息。

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)