---
keywords: 平台；目标；目标工作区；UI；目标UI；目录；目标目录
title: 目标工作区
description: “目标”工作区包含四个部分：“目录”、“浏览”、“帐户”和“系统视图”。 下面各节对这些参数进行了描述。
seo-description: In Adobe Experience Platform, select Destinations from the left navigation bar to access the destinations workspace.
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: 2d944c7bd237efbbd4a770b3a6dd03c4133bc901
workflow-type: tm+mt
source-wordcount: '1101'
ht-degree: 2%

---

# 目标工作区 {#destinations-workspace}

在Adobe Experience Platform中，选择 **[!UICONTROL 目标]** 从左侧导航栏访问 [!UICONTROL 目标] 工作区。

的 [!UICONTROL 目标] 工作区包含五个部分， [!UICONTROL 概述], [!UICONTROL 目录], [!UICONTROL 浏览], [!UICONTROL 帐户]和 [!UICONTROL 系统视图]，如以下部分中所述。

![目标 — 概述](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL 概述] {#overview}

的 **[!UICONTROL 概述]** 选项卡 [!UICONTROL 目标] 功能板，提供与贵组织的目标数据相关的关键量度。 要了解更多信息，请访问 [[!UICONTROL 目标] 仪表板指南](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>如果贵组织是新Experience Platform，并且还没有活动目标，则 [!UICONTROL 目标] 功能板和 [!UICONTROL 概述] 选项卡。 而是选择 [!UICONTROL 目标] 在左侧导航中， [[!UICONTROL 目录] 选项卡](#catalog).

![](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catalog] {#catalog}

的 **[!UICONTROL 目录]** 选项卡会显示 [!DNL Platform]，以将数据发送到。

的 [!DNL Platform] 用户界面在目标目录页面上提供了多个搜索和过滤选项：

* 使用页面上的搜索功能找到特定目标。
* 使用 [!UICONTROL 类别] 控制。
* 在之间切换 [!UICONTROL 所有目标] 和 [!UICONTROL 我的目标]. 选择 **[!UICONTROL 所有目标]**，全部可用 [!DNL Platform] 目标。 选择 **[!UICONTROL 我的目标]**，则只能查看已建立连接的目标。
* 选择以查看 **[!UICONTROL 连接]** 和/或 **[!UICONTROL 扩展]**. 要了解这两个类别之间的差异，请参阅 [目标类型和类别](../destination-types.md).

![目录](../assets/ui/workspace/catalog.png)

目标卡包含 **[!UICONTROL 设置]** 或 **[!UICONTROL 激活区段]** 控件，以及可显示更多选项的辅助控件。 这些控件描述如下：

| 控制 | 描述 |
|---------|----------|
| [!UICONTROL 设置] | 用于创建与目标的连接。 |
| [!UICONTROL 激活区段] | 建立与目标的连接后，即可激活区段。 |
| [!UICONTROL 查看帐户] | 查看您为目标连接的帐户。 |
| [!UICONTROL 查看数据流] | 查看目标存在的数据激活流。 |
| [!UICONTROL 查看文档] | 打开指向该特定目标的文档页面的链接，以了解更多信息并帮助您进行设置。 |

{style=&quot;table-layout:auto&quot;}

![目标卡上的控件](../assets/ui/workspace/destination-card-options.png)

在目录中选择目标卡以打开右边栏。 在此，您可以看到目标的描述。 右边栏提供了上表中描述的相同控件，包括目标的描述，以及目标类别和类型的指示。

![目标目录选项](../assets/ui/workspace/destination-right-rail.png)

有关目标类别的更多信息以及有关每个目标的信息，请参阅 [目标目录](../catalog/overview.md) 和 [目标类型和类别](../destination-types.md).

## [!UICONTROL 帐户] {#accounts}

的 **[!UICONTROL 帐户]** 选项卡显示有关您已与各种目标建立的连接的详细信息，并允许您更新或删除现有帐户详细信息。 有关每个目标帐户可获取的所有信息，请参阅下表。

>[!TIP]
>
> * 选择 [!UICONTROL 平台] 列，并使用 ![“激活区段”按钮](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL 激活区段&#x200B;]**按钮将区段发送到该目标。
> * 选择 [!UICONTROL 平台] 列，并使用 ![“编辑详细信息”按钮](../assets/ui/workspace/pencil-icon.png)**[!UICONTROL 编辑详细信息&#x200B;]**按钮 [更新](update-accounts.md) 现有目标帐户的详细信息。
> * 选择 [!UICONTROL 平台] 列，并使用 ![“删除”按钮](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL 删除&#x200B;]**按钮 [删除](delete-destination-account.md) 现有目标帐户。


![“帐户”选项卡](../assets/ui/workspace/destination-account-options.png)

| 元素 | 描述 |
|---|---|
| [!UICONTROL 平台] | 您为其设置连接的目标。 |
| [!UICONTROL 连接类型] | 表示到存储段或目标的帐户连接类型。 身份验证选项取决于目标： <ul><li>对于电子邮件营销目标：可以是S3、FTP或Azure Blob。</li><li>对于实时广告目标：服务器到服务器</li><li>对于Amazon S3云存储目标：访问密钥 </li><li>对于SFTP云存储目标：SFTP的基本身份验证</li><li>OAuth 1或OAuth 2身份验证</li><li>承载令牌身份验证</li></ul> |
| [!UICONTROL 用户名] | 您在 [连接目标向导](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL 目标] | 表示通过为目标创建的基本信息连接的唯一成功目标数据流的数量。 |
| [!UICONTROL 已授权] | 授权与此目标的连接的日期。 |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL 浏览] {#browse}

的 **[!UICONTROL 浏览]** 选项卡会显示您已建立连接的目标。 目标 **[!UICONTROL 已启用/已禁用]** 打开切换开关，分别将目标设置为活动或不活动。 您还可以通过选择 **[!UICONTROL 区段]** > **[!UICONTROL 浏览]** 并选择要检查的区段。 请参阅下表，以了解 [!UICONTROL 浏览] 选项卡：

>[!TIP]
>
> * 选择 [!UICONTROL 名称] 列，并使用 ![“激活区段”按钮](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL 激活区段&#x200B;]**按钮将区段发送到该目标。
> * 选择 [!UICONTROL 名称] 列，并使用 ![“删除”按钮](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL 删除&#x200B;]**按钮 [删除](delete-destinations.md) 到目标的现有连接。
> * 选择 [!UICONTROL 名称] 列，并使用 ![“在监视中查看”按钮](../assets/ui/workspace/monitoring-icon.png)**[!UICONTROL 在监控中查看&#x200B;]**按钮，以在 [监控仪表板](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard).


![“浏览”选项卡](../assets/ui/workspace/browse-tab.png)

| 元素 | 描述 |
|---------|----------|
| 名称 | 您为激活流程提供到此目标的名称。 同一列包含两个控件： [!UICONTROL 激活 ] 和 [!UICONTROL 删除目标]. |
| [!UICONTROL 上次流量运行状态] | 上次数据流运行的状态。 请参阅 [查看目标详细信息](destination-details-page.md) 有关数据流运行的详细信息。 |
| [!UICONTROL 上次流量运行日期] | 上次数据流运行发生的时间和日期。 请参阅 [查看目标详细信息](destination-details-page.md) 有关数据流运行的详细信息。 |
| [!UICONTROL 目标] | 您为激活流程选择的目标平台。 |
| [!UICONTROL 连接类型] | 表示与存储段或目标的连接类型。 <ul><li>对于电子邮件营销目标：可以是S3、FTP或 [!DNL Azure Blob].</li><li>对于实时广告目标：服务器到服务器。</li><li>对于流目标：可以 [!DNL Azure Event Hubs] 或 [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL 用户名] | 您为目标流程选择的帐户凭据。 |
| [!UICONTROL 激活数据] | 指示正在激活到此目标的区段数。 选择此控件可了解有关已激活区段的更多信息。 请参阅 [激活数据](/help/destinations/ui/destination-details-page.md#activation-data) 在目标详细信息页面中，了解有关已激活区段的更多信息。 |
| [!UICONTROL 已创建] | 创建到目标的激活流程的日期和UTC时间。 选择向上/向下箭头符号，按最新、最早或最早的优先顺序对激活流程进行排序。 |
| [!UICONTROL 状态] | `Enabled` 或 `Disabled`. 指示数据是否正在激活到此目标。 |

单击目标行可在右边栏中显示有关目标的更多信息。

![单击目标行](../assets/ui/workspace/click-destination-row.png)

选择目标名称可查看有关激活到此目标的区段的信息。 单击 **[!UICONTROL 编辑激活]** 修改或添加到发送到此目标的区段。

## [!UICONTROL 系统视图] {#system-view}

的 **[!UICONTROL 系统视图]** 选项卡显示您在Adobe Experience Platform中设置的激活流的图形表示形式。

![数据流1](../assets/ui/workspace/data-flows1.png)

选择页面上显示的任意目标，然后单击 **[!UICONTROL 查看数据流]** 查看您为每个目标设置的所有连接的信息。

![数据流2](../assets/ui/workspace/data-flows2.png)
