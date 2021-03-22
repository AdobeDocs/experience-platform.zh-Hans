---
keywords: 平台；目标；目标工作区；工作区；ui；目标ui；目录；目标目录；
title: 目标工作区
description: “目标”工作区由四个部分组成，即“目录”、“浏览”、“帐户”和“系统视图”，这些部分在以下各节中有介绍。
seo-description: 在Adobe Experience Platform中，从左侧导航栏中选择目标以访问目标工作区。
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 1%

---


# 目标工作区{#destinations-workspace}

## 概述 {#overview}

在Adobe Experience Platform中，从左侧导航栏中选择&#x200B;**[!UICONTROL Destinations]**&#x200B;以访问[!UICONTROL Destinations]工作区。

[!UICONTROL Destinations]工作区由四个部分组成，分别为[!UICONTROL Catalog]、[!UICONTROL Browse]、[!UICONTROL Accounts]和[!UICONTROL System View]，下面各节对它们进行了说明。

![目标 — 概述](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Catalog] {#catalog}

**[!UICONTROL Catalog]**&#x200B;选项卡显示平台中所有可用目标的列表，您可以将数据发送到该目标。

平台用户界面在目标目录页面上提供了许多搜索和筛选选项：

* 使用页面上的搜索功能查找特定目标。
* 使用[!UICONTROL Categories]控件过滤目标。
* 在[!UICONTROL All destinations]和[!UICONTROL My destinations]之间切换。 选择&#x200B;**[!UICONTROL All destinations]**&#x200B;时，将显示所有可用的平台目标。 选择&#x200B;**[!UICONTROL My destinations]**&#x200B;时，您只能看到已建立连接的目标。
* 选择视图&#x200B;**[!UICONTROL Connections]**&#x200B;和/或&#x200B;**[!UICONTROL Extensions]**。 要了解两个类别之间的差异，请参阅[目标类型和类别](../destination-types.md)。

![目标过滤和搜索演示](../assets/ui/workspace/destinations-search-and-filter.gif)

目标卡包含&#x200B;**[!UICONTROL Configure]**&#x200B;或&#x200B;**[!UICONTROL Activate]**&#x200B;控件，以及可显示更多选项的辅助控件。 这些内容均描述如下：

| 控制 | 描述 |
---------|----------
| [!UICONTROL Configure] | 允许您创建到目标的连接。 |
| [!UICONTROL Activate] | 建立到目标的连接后，即可激活区段。 |
| [!UICONTROL View account] | 视图您为目标连接的帐户。 |
| [!UICONTROL View dataflows] | 视图目标的激活流。 |
| [!UICONTROL View documentation] | 打开指向该特定目标的文档页面的链接，了解详细信息并帮助您设置它。 |

![目标卡上的控件](../assets/ui/workspace/destination-card-options.png)

在目录中选择目标卡以打开右边栏。  此处，您可以看到目标的描述。 右边栏提供了上表中描述的相同控件，以及目标的描述，以及目标类别和类型的指示。

![目标目录选项](../assets/ui/workspace/destination-right-rail.png)

有关目标类别和每个目标信息的详细信息，请参阅[目标目录](../catalog/overview.md)和[目标类型和类别](../destination-types.md)。

## [!UICONTROL Accounts] {#accounts}

在&#x200B;**[!UICONTROL Accounts]**&#x200B;选项卡中，您可以进一步了解您与各种目标建立的连接。 有关您可以获取的每个目标上的所有信息，请参阅下表：

>[!TIP]
>
>使用&#x200B;**[!UICONTROL Platform]**&#x200B;列中的![添加数据按钮](../assets/ui/workspace/add-data-symbol.png)按钮为该帐户创建新的目标连接。

![“帐户”选项卡](../assets/ui/workspace/edit-account-destinations.png)

| 元素 | 描述 |
---------|----------
| [!UICONTROL Platform] | 您为其设置连接的目标。 |
| [!UICONTROL Connection Type] | 表示到存储存储段或目标的连接类型。 <ul><li>对于电子邮件营销目标：可以是S3或FTP。</li><li>对于实时广告目标：服务器到服务器</li><li>对于Amazon S3云存储目标：访问密钥 </li><li>对于SFTP云存储目标：SFTP的基本身份验证</li></ul> |
| [!UICONTROL Username] | 您在[连接目标向导](../catalog/email-marketing/overview.md#connect-destination)中选择的用户名。 |
| [!UICONTROL Destinations] | 表示与为目标创建的基本信息连接的唯一成功目标流的数量。 |
| [!UICONTROL Authorized] | 到此目标的连接被授权的日期。 |

此外，您还可以编辑或更新帐户信息。 在&#x200B;**[!UICONTROL Platform]**&#x200B;列中选择![编辑帐户按钮](../assets/ui/workspace/pencil-icon.png)以编辑帐户信息。

对于使用`OAuth2`连接类型的帐户，可以选择&#x200B;**[!UICONTROL Reconnect OAuth]**&#x200B;来续订帐户凭据。

![Oauth图像](../assets/ui/workspace/reconnect-oauth.png)

对于使用`Access Key`或`ConnectionString`连接类型的帐户，您可以编辑帐户身份验证信息，包括访问ID、密钥或连接字符串等信息。

![帐户信息图像](../assets/ui/workspace/edit-account-details.png)

编辑完帐户详细信息后，选择&#x200B;**[!UICONTROL Save]**&#x200B;以完成更新。

## [!UICONTROL Browse] {#browse}

**[!UICONTROL Browse]**&#x200B;选项卡显示您已与之建立连接的目标。 打开&#x200B;**[!UICONTROL Enabled]**&#x200B;切换的目标将目标设置为活动，反之亦然。 您还可以通过选择&#x200B;**[!UICONTROL Segments]** > **[!UICONTROL Browse]**&#x200B;并选择要检查的区段来视图数据流动的目标。 有关在“浏览”选项卡中为每个目标提供的所有信息，请参阅下表：

>[!TIP]
>
> * 使用&#x200B;**[!UICONTROL Name]**&#x200B;列中的![添加区段按钮](../assets/ui/workspace/add-data-symbol.png)按钮可将其他区段激活到该目标。
> * 使用&#x200B;**[!UICONTROL Name]**&#x200B;列中的![删除目标按钮](../assets/ui/workspace/delete-destination-symbol.png)按钮可删除到目标的现有连接。


![浏览选项卡](../assets/ui/workspace/browse-tab.png)

| 元素 | 描述 |
---------|----------
| 名称 | 您为激活流提供到此目标的名称。 同一列包含两个控件：[!UICONTROL Activate ]和[!UICONTROL Delete destination]。 |
| 上次流运行状态 | 上次数据流运行的状态。 有关数据流运行的详细信息，请参阅[视图目标详细信息](destination-details-page.md)。 |
| 上次流运行日期 | 上次数据流运行的时间和日期。 有关数据流运行的详细信息，请参阅[视图目标详细信息](destination-details-page.md)。 |
| [!UICONTROL Destination] | 您为激活流选择的目标平台。 |
| [!UICONTROL Connection Type] | 表示到存储存储段或目标的连接类型。 <ul><li>对于电子邮件营销目标：可以是S3、FTP或[!DNL Azure Blob]。</li><li>对于实时广告目标：服务器到服务器。</li><li>对于流目标：可以是[!DNL Azure Event Hubs]或[!DNL Amazon Kinesis]。</li></ul> |
| [!UICONTROL Username] | 您为目标流选择的帐户凭据。 |
| [!UICONTROL Activation Data] | 指示要激活到此目标的区段数。 选择此控件可进一步了解已激活的区段。 有关已激活区段的详细信息，请参阅目标详细信息页中的[激活数据](/help/destinations/ui/destination-details-page.md#activation-data)。 |
| [!UICONTROL Created] | 创建到目标的激活流的日期和UTC时间。 |
| [!UICONTROL Status] | `Active` 或 `Inactive`. 指示数据当前是否正在激活到此目标。 要编辑状态，请参阅[禁用激活](./activate-destinations.md#disable-activation)。 |

单击目标行可在右边栏中显示有关目标的详细信息。

![单击目标行](../assets/ui/workspace/click-destination-row.png)

选择目标名称可查看有关已激活到此目标的区段的信息。 单击&#x200B;**[!UICONTROL Edit activation]**&#x200B;可修改或添加到要发送到此目标的区段。

## [!UICONTROL System View] {#system-view}

**[!UICONTROL System View]**&#x200B;选项卡显示您在Adobe Experience Platform中设置的激活流的图形表示形式。

![数据流1](../assets/ui/workspace/data-flows1.png)

选择页面上显示的任何目标，然后单击&#x200B;**[!UICONTROL View flows]**&#x200B;以查看您为每个目标设置的所有连接的相关信息。

![数据流2](../assets/ui/workspace/data-flows2.png)