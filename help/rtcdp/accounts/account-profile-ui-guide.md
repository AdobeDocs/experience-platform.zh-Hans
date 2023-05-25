---
keywords: rtcdp配置文件；配置文件rtcdp；rtcdp身份；rtcdp合并策略；实时客户配置文件
title: 帐户配置文件UI指南
description: 通过使用帐户配置文件，Adobe Real-time Customer Data Platform B2B版本使您能够统一来自多个来源的帐户信息。 本指南提供了有关在Adobe Experience Platform用户界面中与“帐户配置文件”交互的详细信息。
exl-id: a05e8b84-026e-4482-a288-aa25b441bd69
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1625'
ht-degree: 0%

---

# 帐户配置文件UI指南

>[!NOTE]
>
>帐户配置文件仅适用于Real-time Customer Data Platform B2B Edition客户。 要了解有关Real-Time CDP的更多信息（包括每种许可证类型可用的特性和功能），请首先阅读 [Real-Time CDP概述](../overview.md).

通过帐户配置文件，可统一来自多个来源的帐户信息。 这种统一的帐户视图将来自您的多个营销渠道以及贵组织当前用于存储客户帐户信息的各种系统的数据整合在一起。 本文档提供了使用Adobe Experience Platform用户界面(UI)中提供的Real-Time CDP B2B版功能与帐户配置文件进行交互的指南。

要详细了解如何在B2B工作流中创建帐户配置文件，请参阅 [端到端教程](../b2b-tutorial.md).

## 帐户配置文件概述 {#account-profiles-overview}

选择 **[!UICONTROL 配置文件]** 下 [!UICONTROL 帐户] 在左侧导航中，查看帐户配置文件的概述。 在 [!UICONTROL 概述] 选项卡中，仪表板在单个入口点中显示一个图形或图表，其中显示了小组件。

![显示小组件的“概述”选项卡](images/b2b-account-profile-overview.png)

请参阅有关以下内容的文档： [[!UICONTROL 帐户配置文件]](../../dashboards/guides/account-profiles.md) 仪表板以了解详情。

## 配置潜在客户与帐户匹配 {#configure-lead-to-account-matching}

>[!IMPORTANT]
>
> 只有B2B AI管理员可以启用、禁用和配置商机到帐户的匹配服务。 禁用服务后，将在24小时内删除匹配的结果。

要配置潜在客户与帐户匹配，请选择 **[!UICONTROL 配置文件]** 下 [!UICONTROL 帐户] 左侧导航栏中。 在 **[!UICONTROL 概述]** 选项卡，选择 **[!UICONTROL 设置]** 右上角。

![选择设置](images/b2b-configuring-accounts-profile.png)

此 **[!UICONTROL 帐户设置]** 对话框打开。 从此处选择 **[!UICONTROL 启用商机帐户匹配]** 切换以启用该功能。 使用下拉菜单进行选择 **[!UICONTROL 每日]** 对于 **[!UICONTROL 匹配节奏]** 设置。 最后，选择相关的 **[!UICONTROL 匹配条件]** 选项后接 **[!UICONTROL 保存]** 以确认您的设置并返回到 **[!UICONTROL 帐户配置文件]** 屏幕。

>[!NOTE]
>
> 地址不能用作唯一的匹配条件。 必须选择一个或多个其他匹配条件。

![配置帐户设置](images/b2b-configuring-account-settings.png)

要了解有关潜在客户与帐户匹配的更多信息，请参阅 [Real-Time CDP B2B中的商机帐户匹配概述](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md).

## 浏览帐户配置文件 {#browse-account-profiles}

要浏览帐户配置文件，请从选择 **[!UICONTROL 配置文件]** 下 [!UICONTROL 帐户] 左侧导航栏中。

在 **[!UICONTROL 浏览]** 选项卡，您可以使用连接的企业源中的帐户ID或通过直接输入源详细信息来浏览帐户配置文件。

![使用帐户ID浏览配置文件](images/b2b-account-browse-by.png)

### 浏览方式 [!UICONTROL 连接的企业源] {#browse-by-connected-enterprise-source}

要按连接的企业源浏览帐户配置文件，请选择 **[!UICONTROL 连接的企业源]** 从 **[!UICONTROL 浏览方式]** 下拉列表，然后使用 **[!UICONTROL 来源]** 字段。

![按连接的企业源浏览帐户配置文件](images/b2b-account-browse.png)

这将打开 **[!UICONTROL 选择源]** 对话框，您可以在此处根据组织已建立的连接选择源。

>[!NOTE]
>
>贵组织可能为同一服务提供程序配置了多个源(例如，Marketo)，因此请务必查看连接名称、源系统和源系统实例，以确保您按正确的源实例进行搜索。

要了解有关连接企业源的更多信息，请参阅 [源概述](../sources/sources-overview.md).

您可以通过选择连接名称旁边的单选按钮来选择源，然后使用 **[!UICONTROL 选择]** 以返回 [!UICONTROL 浏览] 选项卡。

![选择源工作流](images/b2b-account-select-source.png)

在选定源后，您现在必须输入 **[!UICONTROL 帐户ID]** 与源相关。 例如，选择Salesforce源需要您从Salesforce实例中输入帐户ID，以查看与该ID关联的帐户配置文件。

>[!NOTE]
>
>对于Marketo帐户ID，可能会引用两个帐户表，因此您必须使用特定语法以确保查看正确的帐户。
>
>最常见的标准语法是Marketo帐户ID，其后附加有 `.mkto_org` (例如， `1234567.mkto_org`)。 Marketo Account-Based Marketing客户可能具有其他值，这些值可使用附加了的Marketo帐户ID找到 `.mkto_account`. 如果您不确定要使用哪种语法，请咨询Marketo管理员。

![帐户ID选择](images/b2b-account-browse-id.png)

### 浏览方式 [!UICONTROL 其他] {#browse-by-others}

Real-Time CDP， B2B版本通过允许您输入 **[!UICONTROL 源名称]**， **[!UICONTROL 源实例]**、和 **[!UICONTROL 帐户ID]** ，以便查看帐户。 通过直接输入源名称和实例，您可以为Experience Platform提供搜索并显示正确帐户配置文件数据所需的上下文。

在无法与数据直接建立源连接的情况下，执行直接查找的功能非常有用。 例如，如果您的组织制定了数据治理策略，阻止直接连接到CRM，则您可以将该数据导出到云存储系统，然后将其摄取到Experience Platform。

另一个示例可能是，您正在对数据执行转换，转换时间介于数据离开系统并进入Platform之间。 您可以使用直接查找功能来提供数据的上下文(例如，指定它是Marketo数据，即使它来自Amazon S3存储桶)，以使系统知道在哪里查找以及如何正确渲染数据。

要开始直接查找，请选择 **[!UICONTROL 其他]** 从 **[!UICONTROL 浏览方式]** 下拉列表，然后输入 **[!UICONTROL 源名称]**， **[!UICONTROL 源实例]**、和 **[!UICONTROL 帐户ID]** 用于您要查看的帐户。

![按其他人浏览](images/b2b-account-browse-adhoc.png)

## 查看帐户配置文件详细信息 {#view-account-profile-details}

使用之后 **[!UICONTROL 浏览]** 选项卡以查找帐户配置文件，选择 **[!UICONTROL 配置文件ID]** 打开 **[!UICONTROL 详细信息]** 帐户配置文件的选项卡。 配置文件信息显示在 **[!UICONTROL 详细信息]** 选项卡已从多个配置文件片段合并在一起，以形成单个帐户的单个视图。 这包括帐户详细信息，例如基本属性和社交媒体数据。

显示的默认字段也可以在组织级别更改以显示首选帐户配置文件属性。

>[!NOTE]
>
>客户配置文件可使用类似功能，并且已创建分步指南，其中包含有关添加和删除属性、调整面板大小等说明。 请阅读 [配置文件详细信息自定义指南](../../profile/ui/profile-customization.md) 了解更多信息。

![查看帐户配置文件详细信息](images/b2b-account-details.png)

您可以通过选择其他可用选项卡，查看与帐户相关的其他详细信息。 这些标签页包括属性、人员和“业务机会”标签，这些标签页显示与整个企业系统中的帐户相关的未结和已结业务机会。 有关每个选项卡的更多信息，请参阅以下部分。

## “属性”选项卡 {#attributes-tab}

此 **[!UICONTROL 属性]** 选项卡列出了与帐户相关的所有记录信息。 这包括来自多个源的属性数据，这些数据已合并到一起，以形成帐户的单个视图。

除了可以查看列表中的数据之外，您还可以使用搜索栏搜索特定属性或以JSON格式查看记录数据。

![“属性”选项卡](images/b2b-account-attributes.png)

## “人员”选项卡 {#people-tab}

此 **[!UICONTROL 人员]** 选项卡提供与帐户关联的个人人员的列表。 这些人员可能是来自贵公司内不同团队管理的不同企业系统的联系人和潜在客户，但在Real-Time CDP B2B版中，他们以单个列表的形式呈现，使您能够更全面地查看客户联系人。

>[!NOTE]
>
>此 [!UICONTROL 人员] 选项卡显示与该帐户关联的最多25人的列表。 对于关联人员超过25人的客户，系统显示25条记录的随机抽样。

除了向您显示联系人的信息快照外，列出的每个人员还包含 **[!UICONTROL 配置文件ID]**，这是一个可单击的链接，允许您浏览该个人的Real-Time Customer Profile。 要了解有关查看与您的帐户相关的个人客户配置文件的更多信息，请访问指南 [在Real-Time CDP B2B版本中浏览配置文件](../profile/profile-browse.md).

![“人员”选项卡](images/b2b-account-people.png)

## “业务机会”选项卡 {#opportunities-tab}

此 **[!UICONTROL 机会]** 标签页提供与帐户相关的未结和已结业务机会的信息。 这些机会可能会从多个来源引入Experience Platform，但是Real-Time CDP， B2B版本使营销人员可以轻松地在一个位置一起查看所有这些机会。

>[!NOTE]
>
>此 [!UICONTROL 机会] 标签页显示与帐户关联的最多25个业务机会的列表。 对于关联业务机会超过25个的客户，系统显示25条记录的随机抽样。

每个机会都包括一些信息，如机会的名称、数量、阶段，以及机会是开放、关闭、成功还是失败。

![“客户机会”选项卡](images/b2b-account-opportunities.png)

## “相关帐户”选项卡 {#related-accounts-tab}

此 **[!UICONTROL 相关帐户]** 选项卡提供有关可能与您浏览的帐户相关的其他帐户的信息。 有关功能的详细信息，请阅读 [相关帐户概述](/help/rtcdp/b2b-ai-ml-services/related-accounts.md).

>[!NOTE]
>
>* 相关帐户组最多可以具有30个帐户配置文件。 如果发现超过30个帐户配置文件相关，则将其任意拆分为多个组，每个组的成员不超过30个。 帐户配置文件的“相关帐户”组始终包括自身。
>* 此 [!UICONTROL 相关帐户] 选项卡当前显示一个列表，其中包含最多25个与正在浏览的帐户相关联的相关帐户。 这是将在未来更新中解决的限制。 尽管有此UI限制，当您在区段定义中使用相关帐户时，对于30个相关帐户配置文件的组，所有配置文件都用于定位。


每个相关帐户包括帐户个人资料ID和名称、帐户源密钥，以及与主页、地址、父帐户、电话、行业和年收入相关的其他信息。

![“相关帐户”选项卡](images/b2b-account-related-accounts.png)

您可以使用此列表中的相关帐户进行分段。 查看 [分段示例](/help/rtcdp/segmentation/b2b.md#related-account) 以了解如何使用相关帐户来扩展您在区段定义中的访问范围。