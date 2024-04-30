---
title: 在UI中过滤源对象
description: 了解如何在Experience PlatformUI中导航浏览源对象，例如帐户和数据流。
hide: true
hidefromtoc: true
exl-id: 59c200cc-1be7-45a8-9d7a-55e6f11dbcf2
source-git-commit: ca17854830edabaf2bd74265258d6f0096f2888e
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 1%

---

# 在UI中过滤源对象

使用Adobe Experience Platform用户界面中的筛选、搜索和内联操作工具，简化您在以下位置的工作流： [!UICONTROL 源] 工作区

* 使用筛选和搜索功能在组织中的源帐户和数据流中导航。
* 使用内联操作修改应用于数据流的配置设置并改进组织工作流。 您可以使用内联操作来应用标记、设置警报或根据需要创建引入作业。

## 快速入门

在使用源工作区中的对象导航Experience Platform之前，了解以下工具功能和概念会很有帮助：

* [源](../../home.md)：在Experience Platform中使用源从Adobe应用程序或第三方数据源中摄取数据。
* [管理标记](../../../administrative-tags/overview.md)：使用管理标记将元数据关键字应用于对象，并允许搜索以在Experience Platform生态系统中查找该对象。
* [警报](../../../observability/home.md)：使用警报接收通知，这些通知提供对象（如源数据流）状态的更新。
* [数据流](../../../dataflows/home.md)：数据流是跨Experience Platform移动数据的数据作业的表示形式。 您可以使用源工作区创建数据流，以将数据从给定源摄取到Experience Platform。
* [数据集](../../../catalog/datasets/user-guide.md)：数据集是用于数据集合的存储和管理结构，通常是表，包含架构（列）和字段（行）。
* [沙盒](../../../sandboxes/home.md)：在Experience Platform中使用沙盒在Experience Platform实例之间创建虚拟分区，并创建专用于开发或生产的环境。

## 筛选源数据流 {#filter-sources-dataflows}

在Experience PlatformUI中，选择 **[!UICONTROL 源]** 在左侧导航中，然后选择 **[!UICONTROL 数据流]** 从顶部标题中。

![源工作区中的“数据流”页面](../../images/tutorials/filter/dataflows-page.png)

默认情况下，过滤器菜单显示在界面的左侧。 要隐藏菜单，请选择 **[!UICONTROL 隐藏筛选器]**.

![已选择隐藏筛选器选项。](../../images/tutorials/filter/hide-filters.png)

您可以按以下参数筛选源数据流：

| 过滤器 | 描述 |
| --- | --- |
| [源平台](#filter-dataflows-by-source-platform) | 根据使用创建的数据流的源筛选数据流。 |
| [标记](#filter-dataflows-by-tags) | 根据应用于数据流的标记筛选数据流。 |
| [状态](#filter-dataflows-by-status) | 根据数据流的当前状态筛选数据流。 |
| [目标数据集](#filter-dataflows-by-target-dataset) | 根据使用创建的数据流的目标数据集筛选数据流。 |
| [帐户名称](#filter-dataflows-by-account-name) | 根据数据流对应的帐户名称筛选数据流。 |
| [创建者](#filter-dataflows-by-user) | 根据创建者筛选数据流。 |
| [创建日期](#filter-dataflows-by-creation-date) | 根据数据流的创建日期筛选数据流。 |
| [修改日期](#filter-dataflows-by-modification-date) | 根据上次更新日期筛选数据流。 |

### 按源平台筛选数据流 {#filter-dataflows-by-source-platform}

使用 [!UICONTROL 源平台] 用于按源类型筛选数据流的面板。 您可以键入特定源，也可以使用下拉菜单查看目录中的源列表。 您还可以为给定查询筛选多个不同的源。 例如，您可以选择 [!DNL Amazon S3]， [!DNL Azure Data Lake Storage Gen2]、和 [!DNL Google Cloud Storage] 更新目录并仅显示使用所选源创建的数据流。

### 按标记筛选数据流 {#filter-dataflows-by-tags}

使用标记面板按其各自的标记筛选数据流。

选择 **[!UICONTROL 具有任何标记]** 然后使用下拉菜单选择要过滤的标记。 使用此设置筛选具有任何所选标记的数据流。

![用于按任何标记筛选数据流的查询。](../../images/tutorials/filter/has-any-tag.png)

选择 **[!UICONTROL 具有所有标记]** 然后使用下拉菜单选择要过滤的标记。 使用此设置筛选具有您选择的所有标记的数据流。

![按所有标记筛选数据流的查询。](../../images/tutorials/filter/has-all-tags.png)

### 按状态筛选数据流 {#filter-dataflows-by-status}

您可以使用以下工具按状态过滤 [!UICONTROL 状态] 面板。

| 状态 | 描述 |
| --- | --- |
| 已启用 | 选择 **[!UICONTROL 已启用]** 以筛选视图并仅显示活动数据流。 |
| 已禁用 | 选择 **[!UICONTROL 已禁用]** 以筛选视图并仅显示已停用的数据流。 |
| 草稿 | 选择 **[!UICONTROL 草稿]** 以筛选视图并仅显示处于草稿模式的数据流。 |

### 按目标数据集筛选数据流 {#filter-dataflows-by-target-dataset}

选择 **[!UICONTROL 目标数据集]** 以访问所有目标数据集的下拉菜单。 然后，选择一个目标数据集以筛选视图，并仅显示使用指定的目标数据集创建的数据流。

### 按帐户名称筛选数据流 {#filter-dataflows-by-account-name}

选择 **[!UICONTROL 帐户名称]** 以访问包含所有帐户的下拉菜单。 然后，选择一个帐户以筛选视图并显示由您选定帐户创建的数据流。

### 按用户筛选数据流 {#filter-dataflows-by-user}

使用 [!UICONTROL 创建者] 用于按创建或上次更新数据流的用户筛选数据流的面板。 选择下拉列表，然后选择用于筛选数据流的用户名。

### 按创建日期筛选数据流 {#filter-dataflows-by-creation-date}

您可以按数据流创建日期筛选数据流。 在 [!UICONTROL 创建日期] 面板，配置开始日期和结束日期以创建时间范围窗口，并筛选视图以仅显示在该窗口创建的数据流。

您可以通过输入开始日期和结束日期来配置时间范围。 或者，选择日历图标并使用日历配置日期。

您也可以执行相同的步骤，但需按数据流的最后修改日期（而不是其创建日期）筛选数据流。

### 按修改日期筛选数据流 {#filter-dataflows-by-modification-date}

同样，您可以应用相同的原则并按数据流的修改日期筛选数据流。 使用 **[!UICONTROL 修改日期]** 以配置特定时间范围并筛选视图，从而仅显示在该时间段内修改的数据流。

### 组合过滤器 {#combine-filters}

您可以组合不同的筛选器以扩大或缩小搜索范围。 在下面的示例中，将应用过滤器来搜索：

* 使用创建的数据流 [!DNL Amazon S3] 源。
* 包含 **[!DNL ACME]** 标记之前。
* 当前启用的数据流。
* 使用创建的数据流 [!DNL Loyalty Dataset B2C] 数据集。
* 在2024年4月1日至2024年4月19日期间创建的数据流。

![显示所有已应用过滤器的下拉窗口。](../../images/tutorials/filter/combine-filters.png)

要删除所有筛选器，请选择 **[!UICONTROL 全部清除]**.

![已选择“全部清除”选项。](../../images/tutorials/filter/clear-all.png)

## 筛选源帐户 {#filter-sources-accounts}

在Experience PlatformUI中，选择 [!UICONTROL 源] 在左侧导航中，然后选择 **[!UICONTROL 帐户]** 从顶部标题中。 您可以根据创建源帐户的来源或创建源帐户的用户来筛选源帐户。

![源工作区中的“帐户”页面](../../images/tutorials/filter/accounts.png)

## 搜索帐户和数据流 {#search-for-accounts-and-dataflows}

您可以使用搜索栏立即导航到特定帐户或数据流，从而提高效率。

>[!BEGINTABS]

>[!TAB 搜索数据流]

使用中的搜索栏 [!UICONTROL 数据流] 页面查找特定数据流。 您可以使用数据流的名称或描述来搜索数据流。

![ACME数据流的搜索查询](../../images/tutorials/filter/search-dataflow.png)

>[!TAB 搜索帐户]

使用中的搜索栏 [!UICONTROL 帐户] 页面查找特定帐户。 您可以使用帐户的名称或描述来搜索帐户。

![4月帐户的搜索查询](../../images/tutorials/filter/search-account.png)

>[!ENDTABS]

## 源数据流的内联操作 {#inline-actions-for-sources-dataflows}

选择省略号(`...`)作为内联操作列表的数据流名称，您可以使用这些操作修改数据流。

![可为给定数据流选择的内联操作选项。](../../images/tutorials/filter/inline-actions.png)

| 内联操作 | 描述 |
| --- | --- |
| [!UICONTROL 编辑计划] | 选择 **[!UICONTROL 编辑计划]** 以更新数据流的摄取计划。 无法编辑已设置为一次性摄取的数据流。 |
| [!UICONTROL 禁用数据流] | 选择 **[!UICONTROL 禁用数据流]** 以停用数据流运行。 此选项不会删除您的数据流。 |
| [!UICONTROL 在监控中查看] | 选择 **[!UICONTROL 在监控中查看]** 在监视功能板中查看数据流的指标和状态。 有关详细信息，请阅读上的指南 [监控源数据流](../../../dataflows/ui/monitor-sources.md). |
| [!UICONTROL 删除] | 选择 **[!UICONTROL 删除]** 以删除您的数据流。 |
| [!UICONTROL 按需运行] | 选择 **[!UICONTROL 按需运行]** 以触发数据流运行的单个迭代。 有关详细信息，请阅读上的指南 [创建按需数据流运行](../ui/on-demand-ingestion.md). |
| [!UICONTROL 订阅警报] | 选择 **[!UICONTROL 订阅警报]** 要查看可订阅的警报弹出窗口，请执行以下操作： <ul><li>源数据流运行开始：选择此警报可在按需数据流运行开始时接收通知。</li><li>源数据流运行成功：选择此警报可在按需数据流运行成功完成时接收通知。</li><li>源数据流运行失败：当您的按需数据流运行由于错误而失败时，选择此警报。</li></ul> 有关详细信息，请阅读上的指南 [订阅源数据流的警报](../ui/alerts.md). |
| [!UICONTROL 添加到包] | 选择 **[!UICONTROL 添加到包]** 将数据流添加到包并将其导出以用于其他沙盒。 在此步骤中，您可以创建新资源包，也可以将数据流添加到现有资源包。 有关信息，请阅读以下指南： [沙盒工具](../../../sandboxes/ui/sandbox-tooling.md). |
| [!UICONTROL 管理标记] | 选择 **[!UICONTROL 管理标记]** 以向数据流添加标记或从数据流中删除标记。 使用标记管理元数据分类并分类业务对象，以便更轻松地发现和分类。 有关详细信息，请阅读上的指南 [管理标记](../../../administrative-tags/ui/managing-tags.md). |

## 后续步骤

通过阅读本文档，您已了解如何在源帐户和数据流页面中导航。 欲知关于来源的更多信息，请阅读 [源概述](../../home.md).
