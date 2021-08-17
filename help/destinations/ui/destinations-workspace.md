---
keywords: 平台；目标；目标工作区；UI；目标UI；目录；目标目录
title: 目标工作区
description: “目标”工作区包含四个部分：“目录”、“浏览”、“帐户”和“系统视图”。 下面各节对这些参数进行了描述。
seo-description: 在Adobe Experience Platform中，从左侧导航栏中选择目标以访问目标工作区。
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: a619227de30513bb06a22ce7b4f2fc13847c1ab6
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 2%

---

# 目标工作区 {#destinations-workspace}

在Adobe Experience Platform中，从左侧导航栏中选择&#x200B;**[!UICONTROL 目标]**&#x200B;以访问[!UICONTROL 目标]工作区。

[!UICONTROL 目标]工作区由五个部分组成，分别是[!UICONTROL 概述]、[!UICONTROL 目录]、[!UICONTROL Browse]、[!UICONTROL 帐户]和[!UICONTROL 系统视图]，如以下各节所述。

![目标 — 概述](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL 概述] {#overview}

**[!UICONTROL 概述]**&#x200B;选项卡显示[!UICONTROL 目标]功能板，其中提供了与贵组织的目标数据相关的关键量度。 要了解更多信息，请访问[[!UICONTROL 目标]功能板指南](../../dashboards/guides/destinations.md)。

>[!NOTE]
>
>如果贵组织是新Experience Platform，并且还没有活动目标，则将不显示[!UICONTROL 目标]功能板和[!UICONTROL 概述]选项卡。 相反，从左侧导航中选择[!UICONTROL 目标]会显示[[!UICONTROL 目录]选项卡](#catalog)。

![](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catalog] {#catalog}

**[!UICONTROL Catalog]**&#x200B;选项卡显示[!DNL Platform]中所有可用目标的列表，您可以将数据发送到这些目标。

[!DNL Platform]用户界面在目标目录页面上提供了多个搜索和过滤选项：

* 使用页面上的搜索功能找到特定目标。
* 使用[!UICONTROL Categories]控件筛选目标。
* 在[!UICONTROL 所有目标]和[!UICONTROL 我的目标]之间切换。 选择&#x200B;**[!UICONTROL 所有目标]**&#x200B;后，将显示所有可用的[!DNL Platform]目标。 选择&#x200B;**[!UICONTROL My destinations]**&#x200B;后，您只能看到已建立连接的目标。
* 选择以查看&#x200B;**[!UICONTROL 连接]**&#x200B;和/或&#x200B;**[!UICONTROL 扩展]**。 要了解这两个类别之间的差异，请参阅[目标类型和类别](../destination-types.md)。

![目标筛选和搜索演示](../assets/ui/workspace/destinations-search-and-filter.gif)

目标卡包含&#x200B;**[!UICONTROL Configure]**&#x200B;或&#x200B;**[!UICONTROL Activate]**&#x200B;控件，以及可显示更多选项的辅助控件。 这些控件描述如下：

| 控制 | 描述 |
|---------|----------|
| [!UICONTROL 配置] | 用于创建与目标的连接。 |
| [!UICONTROL 激活] | 建立与目标的连接后，即可激活区段。 |
| [!UICONTROL 查看帐户] | 查看您为目标连接的帐户。 |
| [!UICONTROL 查看数据流] | 查看目标存在的数据激活流。 |
| [!UICONTROL 查看文档] | 打开指向该特定目标的文档页面的链接，以了解更多信息并帮助您进行设置。 |

{style=&quot;table-layout:auto&quot;}

![目标卡上的控件](../assets/ui/workspace/destination-card-options.png)

在目录中选择目标卡以打开右边栏。 在此，您可以看到目标的描述。 右边栏提供了上表中描述的相同控件，包括目标的描述，以及目标类别和类型的指示。

![目标目录选项](../assets/ui/workspace/destination-right-rail.png)

有关目标类别的更多信息以及有关每个目标的信息，请参阅[目标目录](../catalog/overview.md)和[目标类型和类别](../destination-types.md)。

## [!UICONTROL 帐户] {#accounts}

**[!UICONTROL Accounts]**&#x200B;选项卡显示了您已与各种目标建立的连接的详细信息，并允许您更新现有的连接详细信息。 有关详细说明，请参阅[更新帐户](update-accounts.md) 。

## [!UICONTROL 浏览] {#browse}

**[!UICONTROL Browse]**&#x200B;选项卡显示您已与之建立连接的目标。 已打开&#x200B;**[!UICONTROL 启用/禁用]**&#x200B;切换开关的目标，可分别将目标设置为活动或不活动。 您还可以通过选择&#x200B;**[!UICONTROL 区段]** > **[!UICONTROL 浏览]**&#x200B;并选择要检查的区段来查看数据流的目标。 有关“浏览”选项卡中为每个目标提供的所有信息，请参阅下表：

>[!TIP]
>
> * 使用&#x200B;**[!UICONTROL 名称]**&#x200B;列中的![添加区段按钮](../assets/ui/workspace/add-data-symbol.png)按钮将区段发送到该目标。
> * 使用&#x200B;**[!UICONTROL 名称]**&#x200B;列中的![删除目标按钮](../assets/ui/workspace/delete-destination-symbol.png)按钮，可以[删除](delete-destinations.md)与目标的现有连接。


![“浏览”选项卡](../assets/ui/workspace/browse-tab.png)

| 元素 | 描述 |
|---------|----------|
| 名称 | 您为激活流程提供到此目标的名称。 同一列包含两个控件：[!UICONTROL 激活]和[!UICONTROL 删除目标]。 |
| [!UICONTROL 上次流量运行状态] | 上次数据流运行的状态。 有关数据流运行的详细信息，请参阅[查看目标详细信息](destination-details-page.md) 。 |
| [!UICONTROL 上次流量运行日期] | 上次数据流运行发生的时间和日期。 有关数据流运行的详细信息，请参阅[查看目标详细信息](destination-details-page.md) 。 |
| [!UICONTROL 目标] | 您为激活流程选择的目标平台。 |
| [!UICONTROL 连接类型] | 表示与存储段或目标的连接类型。 <ul><li>对于电子邮件营销目标：可以是S3、FTP或[!DNL Azure Blob]。</li><li>对于实时广告目标：服务器到服务器。</li><li>对于流目标：可以是[!DNL Azure Event Hubs]或[!DNL Amazon Kinesis]。</li></ul> |
| [!UICONTROL 用户名] | 您为目标流程选择的帐户凭据。 |
| [!UICONTROL 激活数据] | 指示正在激活到此目标的区段数。 选择此控件可了解有关已激活区段的更多信息。 有关已激活区段的更多信息，请参阅目标详细信息页面中的[激活数据](/help/destinations/ui/destination-details-page.md#activation-data)。 |
| [!UICONTROL 已创建] | 创建到目标的激活流程的日期和UTC时间。 |
| [!UICONTROL 状态] | `Active` 或 `Inactive`. 指示数据是否正在激活到此目标。 |

单击目标行可在右边栏中显示有关目标的更多信息。

![单击目标行](../assets/ui/workspace/click-destination-row.png)

选择目标名称可查看有关激活到此目标的区段的信息。 单击&#x200B;**[!UICONTROL 编辑激活]**&#x200B;以修改或添加到发送到此目标的区段。

## [!UICONTROL 系统视图] {#system-view}

**[!UICONTROL 系统视图]**&#x200B;选项卡显示您在Adobe Experience Platform中设置的激活流的图形表示形式。

![数据流1](../assets/ui/workspace/data-flows1.png)

选择页面上显示的任意目标，然后单击&#x200B;**[!UICONTROL 查看流]**&#x200B;以查看您为每个目标设置的所有连接的信息。

![数据流2](../assets/ui/workspace/data-flows2.png)
