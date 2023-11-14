---
keywords: 平台；目标；目标工作区；工作区；ui；目标ui；目录；目标目录；
title: 目标工作区
description: 目标工作区包括五个部分：“概述”、“目录”、“浏览”、“帐户”和“系统视图”。 以下各节对这些要求进行了说明。
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 2%

---

# 目标工作区 {#destinations-workspace}

在Adobe Experience Platform中，选择 **[!UICONTROL 目标]** 从左侧导航栏访问 [!UICONTROL 目标] 工作区。

此 [!UICONTROL 目标] 工作区由五个部分组成， [!UICONTROL 概述]， [!UICONTROL 目录]， [!UICONTROL 浏览]， [!UICONTROL 帐户]、和 [!UICONTROL 系统视图]，具体说明见以下部分。

![目标概述仪表板，显示三个小组件。](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL 概述] {#overview}

此 **[!UICONTROL 概述]** 选项卡显示 [!UICONTROL 目标] 仪表板，提供与贵组织的目标数据相关的关键量度。 要了解更多信息，请访问 [[!UICONTROL 目标] 仪表板指南](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>如果您的组织是初次使用Experience Platform，并且还没有有效的目标，则 [!UICONTROL 目标] 仪表板和 [!UICONTROL 概述] 选项卡不可见。 相反，选择 [!UICONTROL 目标] 从左侧导航栏显示 [[!UICONTROL 目录] 选项卡](#catalog).

![目标仪表板概述选项卡。](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catalog] {#catalog}

此 **[!UICONTROL 目录]** 选项卡显示中可用的所有目标列表 [!DNL Platform]，可将数据发送至。

此 [!DNL Platform] 用户界面在目标目录页面上提供了多个搜索和筛选选项：

* 使用页面上的搜索功能来查找特定目标。
* 使用过滤目标 [!UICONTROL 类别] 控制。
* 在之间切换 [!UICONTROL 所有目标] 和 [!UICONTROL 我的目标]. 当您选择时 **[!UICONTROL 所有目标]**，全部可用 [!DNL Platform] 将显示目标。 当您选择时 **[!UICONTROL 我的目标]**，则只能查看已建立连接的目标。
* 选择以查看 **[!UICONTROL 连接]** 和/或 **[!UICONTROL 扩展]** 类型。 要了解这两种类别之间的区别，请阅读 [目标类型和类别](../destination-types.md).

![目标目录显示一些广告和云存储目标。](../assets/ui/workspace/catalog.png)

目标卡包含主要和次要控制选项。 主要控件包括 [!UICONTROL 设置]， [!UICONTROL 激活]， [!UICONTROL 激活受众]，或 [!UICONTROL 导出数据集]. 辅助控件允许查看选项。 这些控制如下所述：

| 控制 | 描述 |
|---------|----------|
| [!UICONTROL 设置] | 用于创建到目标的连接。 |
| [!UICONTROL 激活] | 建立与目标之间的连接后，您可以激活受众或将数据集导出到此目标。 |
| [!UICONTROL 激活受众] | 建立与目标的连接后，即可将受众激活到此目标。 |
| [!UICONTROL 导出数据集] | 建立与目标的连接后，即可将数据集导出到此目标。 |
| [!UICONTROL 查看帐户] | 查看您为目标连接的帐户。 |
| [!UICONTROL 查看数据流] | 查看目标存在的数据激活流。 |
| [!UICONTROL 查看文档] | 打开指向该特定目标的文档页面的链接，以获取更多信息并帮助您进行设置。 |

{style="table-layout:auto"}

![目标信息卡上的控件](../assets/ui/workspace/destination-card-options.png)

在目录中选择目标卡以打开右边栏。 在这里，您可以看到目标的描述。 右边栏提供了上表中描述的相同控件，包括目标的描述，以及目标类别和类型的指示。

![目标目录选项](../assets/ui/workspace/destination-right-rail.png)

有关目标类别和每个目标的详细信息，请参阅 [目标目录](../catalog/overview.md) 和 [目标类型和类别](../destination-types.md).

## [!UICONTROL 帐户] {#accounts}

此 **[!UICONTROL 帐户]** 选项卡显示有关您与各种目标建立的连接的详细信息，并允许您更新或删除现有帐户详细信息。 有关各个目标帐户的所有信息，请参阅下表。

>[!TIP]
>
> * 选择省略号(`...`) [!UICONTROL 平台] 列并使用 ![激活控制](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL 激活&#x200B;]**/**[!UICONTROL &#x200B;激活受众&#x200B;]**/**[!UICONTROL &#x200B;导出数据集&#x200B;]**控件，用于将受众或数据集导出到该目标。
> * 选择省略号(`...`) [!UICONTROL 平台] 列并使用 ![编辑详细信息控件](../assets/ui/workspace/pencil-icon.png)**[!UICONTROL 编辑详细信息&#x200B;]**控制对象 [更新](update-accounts.md) 现有目标帐户的详细信息。
> * 选择省略号(`...`) [!UICONTROL 平台] 列并使用 ![删除控件](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL 删除&#x200B;]**控制对象 [删除](delete-destination-account.md) 现有目标帐户。

![“帐户”选项卡](../assets/ui/workspace/destination-account-options.png)

| 元素 | 描述 |
|---|---|
| [!UICONTROL 平台] | 已为其设置连接的目标。 |
| [!UICONTROL 连接类型] | 表示与存储段或目标的帐户连接类型。 根据目标的不同，身份验证选项有： <ul><li>对于电子邮件营销目标：可以是S3、FTP或Azure Blob。</li><li>对于实时广告目标：服务器到服务器</li><li>对于Amazon S3云存储目标：访问密钥 </li><li>对于SFTP云存储目标：SFTP的基本身份验证</li><li>OAuth 1或OAuth 2身份验证</li><li>持有者令牌身份验证</li></ul> |
| [!UICONTROL 用户名] | 您在中选择的用户名 [连接目标向导](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL 目标] | 表示与为目标创建的基本信息连接的唯一成功目标数据流数。 |
| [!UICONTROL 已授权] | 授权连接到此目标的日期。 |

{style="table-layout:auto"}

## [!UICONTROL 浏览] {#browse}

此 **[!UICONTROL 浏览]** 选项卡显示您与之建立连接的目标。 具有的目标 **[!UICONTROL 已启用/已禁用]** 切换打开将目标分别设置为活动或非活动。 您还可以通过选择来查看数据流动的目标 **[!UICONTROL 受众]** > **[!UICONTROL 浏览]** 并选择要检查的受众。 请参阅下表，了解中为每个目标提供的所有信息 [!UICONTROL 浏览] 选项卡：

>[!TIP]
>
> * 选择省略号(`...`) [!UICONTROL 名称] 列并使用 ![激活受众控制](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL 激活&#x200B;]**控件，用于将受众或数据集导出到该目标。
> * 选择省略号(`...`) [!UICONTROL 名称] 列并使用 ![删除控件](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL 删除&#x200B;]**控制对象 [移除](delete-destinations.md) 到目标的现有连接。
> * 选择省略号(`...`) [!UICONTROL 名称] 列并使用 ![在监控控制中查看](../assets/ui/workspace/monitoring-icon.png)**[!UICONTROL 在监控中查看&#x200B;]**用于在中查看此目标的激活信息的控件 [监视仪表板](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard).
> * 选择省略号(`...`) [!UICONTROL 名称] 列并使用 ![订阅警报 ](../assets/ui/workspace/alerts-icon.png)**[!UICONTROL 订阅警报&#x200B;]**用于订阅目标数据流警报的控制。 您可以订阅警报，以接收有关流运行的状态、成功或失败的消息。 请参阅 [订阅上下文目标警报](alerts.md) 以了解有关目标数据流警报的详细信息。

![“浏览”选项卡](../assets/ui/workspace/browse-tab.png)

| 元素 | 描述 |
|---------|----------|
| 名称 | 您为此目标的激活流提供的名称。 同一列包含两个控件： [!UICONTROL 激活] 和 [!UICONTROL 删除目标]. |
| [!UICONTROL 上次流量运行状态] | 上次数据流运行的状态。 请参阅 [查看目标详细信息](destination-details-page.md) 以了解有关数据流运行的更多信息。 |
| [!UICONTROL 上次流量运行日期] | 上次数据流运行发生的时间和日期。 请参阅 [查看目标详细信息](destination-details-page.md) 以了解有关数据流运行的更多信息。 |
| [!UICONTROL 目标] | 您为激活流选择的目标平台。 |
| [!UICONTROL 连接类型] | 表示与存储段或目标的连接类型。 <ul><li>对于电子邮件营销目标：可以是S3、FTP或 [!DNL Azure Blob].</li><li>对于实时广告目标：服务器到服务器。</li><li>对于流目标：可以是 [!DNL Azure Event Hubs] 或 [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL 用户名] | 您为目标流选择的帐户凭据。 |
| [!UICONTROL 激活数据] | 指示正在激活到此目标的受众数量。 选择此控件可了解有关已激活受众的更多信息。 请参阅 [激活数据](/help/destinations/ui/destination-details-page.md#activation-data) 在目标详细信息页面中查看激活的受众的详细信息。 |
| [!UICONTROL 已创建] | 创建到目标的激活流的日期和UTC时间。 选择向上/向下箭头符号，按最新先或最旧先对激活流进行排序。 |
| [!UICONTROL 状态] | `Enabled` 或 `Disabled`. 指示是否正在将数据激活到此目标。 |

单击目标行可在右边栏中显示有关目标的更多信息。

![单击目标行](../assets/ui/workspace/click-destination-row.png)

选择目标名称可查看有关激活到此目标的受众的信息。 单击 **[!UICONTROL 编辑激活]** 修改或添加到要发送到此目标的受众。

## [!UICONTROL 系统视图] {#system-view}

此 **[!UICONTROL 系统视图]** 选项卡以图形方式呈现您在Adobe Experience Platform中设置的激活流程。

![Data-flows1](../assets/ui/workspace/data-flows1.png)

选择页面上显示的任何目标，然后单击 **[!UICONTROL 查看数据流]** 查看有关您为每个目标设置的所有连接的信息。

![Data-flows2](../assets/ui/workspace/data-flows2.png)
