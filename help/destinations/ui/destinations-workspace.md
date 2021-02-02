---
keywords: 平台；目标；目标工作区；工作区；ui；目标ui；目录；目标目录；
title: 目标工作区
seo-title: 目标工作区
description: “目标”工作区由四个部分组成，即目录、浏览、帐户和系统视图，这些部分在以下各节中有介绍。
seo-description: 在Adobe Experience Platform，从左侧导航栏中选择目标以访问目标工作区。
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 2%

---


# 目标工作区{#destinations-workspace}

在Adobe Experience Platform，从左侧导航栏中选择&#x200B;**[!UICONTROL 目标]**&#x200B;以访问[!UICONTROL 目标]工作区。

[!UICONTROL 目标]工作区由四个部分组成，分别是[!UICONTROL 目录]、[!UICONTROL 浏览]、[!UICONTROL 帐户]和[!UICONTROL 系统视图]，具体说明请参阅以下各节。

![目标——概述](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL 目录] {#catalog}

**[!UICONTROL 目录]**&#x200B;选项卡显示平台中所有可用目标的列表，您可以将数据发送到该目标。

平台用户界面在目标目录页面上提供了许多搜索和筛选选项：

* 使用页面上的搜索功能查找特定目标。
* 使用[!UICONTROL 类别]控件过滤目标。
* 在[!UICONTROL 所有目标]和[!UICONTROL 我的目标]之间切换。 选择&#x200B;**[!UICONTROL 所有目标]**&#x200B;后，将显示所有可用的平台目标。 选择&#x200B;**[!UICONTROL 我的目标]**&#x200B;后，您只能看到已建立连接的目标。
* 选择以视图&#x200B;**[!UICONTROL 连接]**&#x200B;和／或&#x200B;**[!UICONTROL 扩展]**。 要了解两个类别之间的差异，请参阅[目标类型和类别](../destination-types.md)。

![目标过滤和搜索演示](../assets/ui/workspace/destinations-search-and-filter.gif)

目标卡包含&#x200B;**[!UICONTROL 配置]**&#x200B;或&#x200B;**[!UICONTROL 激活]**&#x200B;控件，以及带有更多选项的辅助控件。 这些内容均描述如下：

| 控制 | 描述 |
---------|----------
| [!UICONTROL 配置] | 允许您创建到目标的连接。 |
| [!UICONTROL 激活] | 建立到目标的连接后，即可激活区段。 |
| [!UICONTROL 视图帐户] | 视图您为目标连接的帐户。 |
| [!UICONTROL 视图数据流] | 视图目标的激活流。 |
| [!UICONTROL 视图文档] | 打开指向该特定目标的文档页面的链接，以了解更多信息并帮助您设置它。 |

![目标卡上的控件](../assets/ui/workspace/destination-card-options.png)

在目录中选择目标卡以打开右边栏。  此处，您可以看到目标的描述。 右边栏提供了上表中描述的相同控件，以及目标的描述，以及目标类别和类型的指示。

![目标目录选项](../assets/ui/workspace/destination-right-rail.png)

有关目标类别和每个目标类别的详细信息，请参阅[目标目录](../catalog/overview.md)和[目标类型和目标](../destination-types.md)。

## [!UICONTROL 帐户] {#accounts}

在&#x200B;**[!UICONTROL 帐户]**&#x200B;选项卡中，您可以进一步了解您与各种目标建立的连接。 请参阅下表，了解您可以在每个目标上获取的所有信息：

>[!TIP]
>
>使用&#x200B;**[!UICONTROL Platform]**&#x200B;列中的![添加数据按钮](../assets/ui/workspace/add-data-symbol.png)按钮为该帐户创建新的目标连接。

![“帐户”选项卡](../assets/ui/workspace/edit-account-destinations.png)

| 元素 | 描述 |
---------|----------
| [!UICONTROL 平台] | 您为其设置连接的目标。 |
| [!UICONTROL 连接类型] | 表示到存储存储段或目标的连接类型。 <ul><li>对于电子邮件营销目标：可以是S3或FTP。</li><li>对于实时广告目标：服务器到服务器</li><li>对于AmazonS3云存储目标：访问密钥 </li><li>对于SFTP云存储目标：SFTP的基本身份验证</li></ul> |
| [!UICONTROL 用户名] | 您在[连接目标向导](../catalog/email-marketing/overview.md#connect-destination)中选择的用户名。 |
| [!UICONTROL 目标] | 表示通过为目标创建的基本信息连接的唯一成功目标流的数量。 |
| [!UICONTROL 已授权] | 到此目标的连接被授权的日期。 |

此外，您还可以编辑或更新帐户信息。 在&#x200B;**[!UICONTROL 平台]**&#x200B;列中选择![编辑帐户按钮](../assets/ui/workspace/pencil-icon.png)以编辑帐户信息。

对于使用`OAuth2`连接类型的帐户，可选择&#x200B;**[!UICONTROL 重新连接OAuth]**&#x200B;以续订帐户凭据。

![Oauth图像](../assets/ui/workspace/reconnect-oauth.png)

对于使用`Access Key`或`ConnectionString`连接类型的帐户，您可以编辑帐户身份验证信息，包括访问ID、密钥或连接字符串等信息。

![帐户信息图像](../assets/ui/workspace/edit-account-details.png)

编辑完帐户详细信息后，选择&#x200B;**[!UICONTROL 保存]**&#x200B;以完成更新。

## [!UICONTROL 浏览] {#browse}

**[!UICONTROL 浏览]**&#x200B;选项卡显示您已建立连接的目标。 启用&#x200B;**[!UICONTROL 已启用]**&#x200B;切换的目标将目标设置为活动，反之亦然。 您还可以通过选择&#x200B;**[!UICONTROL 区段]** > **[!UICONTROL 浏览]**&#x200B;并选择要检查的区段，来视图数据流动的目标。 有关在“浏览”选项卡中为每个目标提供的所有信息，请参阅下表：

>[!TIP]
>
>使用&#x200B;**[!UICONTROL 名称]**&#x200B;列中的![添加数据按钮](../assets/ui/workspace/add-data-symbol.png)按钮可将其他段激活到该目标。

![浏览选项卡](../assets/ui/workspace/browse-tab.png)

| 元素 | 描述 |
---------|----------
| 名称 | 您为激活流提供到此目标的名称。 |
| [!UICONTROL 目标] | 您为激活流选择的目标平台。 |
| [!UICONTROL 连接类型] | 表示到存储存储段或目标的连接类型。 <ul><li>对于电子邮件营销目标：可以是S3或FTP。</li><li>对于实时广告目标：服务器到服务器</li></ul> |
| [!UICONTROL 用户名] | 您为目标流选择的帐户凭据。 |
| [!UICONTROL 区段] | 正在激活到此目标的区段数。 |
| [!UICONTROL 已创建] | 创建到目标的激活流的日期和UTC时间。 |
| [!UICONTROL 状态] | `Active` 或 `Inactive`. 指示数据当前是否正在激活到此目标。 要编辑状态，请参阅[禁用激活](./activate-destinations.md#disable-activation)。 |

单击目标行以在右边栏中显示有关目标的更多信息。

![单击目标行](../assets/ui/workspace/click-destination-row.png)

选择目标名称可查看有关激活到此目标的区段的信息。 单击&#x200B;**[!UICONTROL 编辑激活]**&#x200B;可修改或添加到要发送到此目标的区段。

## [!UICONTROL 系统视图] {#system-view}

**[!UICONTROL 系统视图]**&#x200B;选项卡显示您在Adobe Experience Platform设置的激活流的图形表示。

![数据流1](../assets/ui/workspace/data-flows1.png)

选择页面上显示的任何目标，并按&#x200B;**[!UICONTROL 视图流]**&#x200B;查看您为每个目标设置的所有连接的相关信息。

![数据流2](../assets/ui/workspace/data-flows2.png)