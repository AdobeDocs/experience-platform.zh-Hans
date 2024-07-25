---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；查询；查询编辑器；查询编辑器；查询编辑器；
solution: Experience Platform
title: 查询服务UI指南
description: Adobe Experience Platform查询服务提供了一个用户界面，可用于编写和执行查询、查看先前执行的查询以及访问由您组织内的用户保存的查询。
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 1%

---

# [!DNL Query Service]用户界面指南

Adobe Experience Platform [!DNL Query Service]提供了一个用户界面，可用于编写和执行查询、查看以前执行的查询以及访问由您组织内的用户保存的查询。 要在[Adobe Experience Platform](https://platform.adobe.com)中访问UI，请在左侧导航中选择&#x200B;**[!UICONTROL 查询]**。

## [!DNL Query Editor]

[!DNL Query Editor]使您能够在不使用外部客户端的情况下编写和执行查询。 选择&#x200B;**[!UICONTROL 创建查询]**&#x200B;以打开[!DNL Query Editor]并创建新查询。 您还可以通过从&#x200B;**[!UICONTROL 日志]**&#x200B;或&#x200B;**[!UICONTROL 模板]**&#x200B;选项卡中选择查询来访问[!DNL Query Editor]。 选择以前执行或保存的查询将打开[!DNL Query Editor]并显示所选查询的SQL。

![已突出显示“创建查询”的查询仪表板。](../images/ui/overview/overview.png)

[!DNL Query Editor]提供了编辑空间，您可以在其中开始键入查询。 键入时，编辑器会自动完成表中的SQL保留字、表和字段名。 完成查询编写后，选择&#x200B;**播放**&#x200B;按钮以运行查询。 编辑器下方的&#x200B;**[!UICONTROL 控制台]**&#x200B;选项卡显示[!DNL Query Service]当前正在执行的操作，指示何时返回查询。 控制台旁边的&#x200B;**[!UICONTROL 结果]**&#x200B;选项卡显示查询结果。 有关使用[!DNL Query Editor]的详细信息，请参阅[查询编辑器指南](./user-guide.md)。

![A已缩放查看[!DNL Query Editor]。](../images/ui/overview/query-editor.png)

## 计划的查询 {#scheduled-queries}

已另存为模板的查询可以计划为定期运行。 在计划查询时，您可以选择运行频率、开始和结束日期、计划查询在一周中运行的日期以及要将查询导出到的数据集。 使用查询编辑器设置查询计划。

要了解如何通过UI计划查询，请参阅[计划查询指南](./user-guide.md#scheduled-queries)。 要了解如何使用API添加计划，请参阅[计划查询端点指南](../api/scheduled-queries.md)。

一旦安排了一个查询，它就会出现在[!UICONTROL 已安排的查询]选项卡上的已安排的查询列表中。 从列表中选择计划查询，即可找到有关查询、运行、创建者和时间的完整详细信息。

![带有“计划查询”选项卡的查询工作区突出显示，并显示查询计划的行。](../images/ui/overview/scheduled-queries.png)

| 列 | 描述 |
| --- | --- |
| **[!UICONTROL 名称]** | 名称字段是模板名称或SQL查询的前几个字符。 使用查询编辑器通过UI创建的任何查询都会在开始时命名。 如果查询是通过API创建的，则查询的名称是用于创建查询的初始SQL的片段。 |
| **[!UICONTROL 模板]** | 查询的模板名称。 选择模板名称以导航到查询编辑器。 为方便起见，查询模板会显示在查询编辑器中。 如果没有模板名称，该行将标有连字符，并且无法重定向到查询编辑器以查看查询。 |
| **[!UICONTROL SQL]** | SQL查询的片段。 |
| **[!UICONTROL 运行频率]** | 这是您的查询设置为运行的节奏。 可用值为`Run once`和`Scheduled`。 可以根据查询的运行频率对其进行筛选。 |
| **[!UICONTROL 创建者]** | 创建查询的用户的名称。 |
| **[!UICONTROL 已创建]** | 创建查询时的时间戳（UTC格式）。 |
| **[!UICONTROL 上次运行时间戳]** | 运行查询时的最新时间戳。 此列突出显示查询是否已根据其当前计划执行。 |
| **[!UICONTROL 上次运行状态]** | 最近查询执行的状态。 三个状态值为： `successful` `failed`或`in progress`。 |

有关如何通过查询服务UI[监视查询的详细信息，请参阅文档](./monitor-queries.md)。

## 模板 {#browse}

**[!UICONTROL 模板]**&#x200B;选项卡显示由您组织中的用户保存的查询。 将它们视为查询项目很有用，因为在此处保存的查询可能仍在构建中。 显示在&#x200B;**[!UICONTROL 模板]**&#x200B;选项卡上的查询在&#x200B;**[!UICONTROL 日志]**&#x200B;选项卡中也显示为运行查询（如果它们以前由[!DNL Query Service]执行）。

![A缩放为显示多个已保存查询的“查询仪表板模板”选项卡。](../images/ui/overview/templates.png)

| 列 | 描述 |
| --- | --- |
| **[!UICONTROL 名称]** | 名称字段是用户创建的查询名称或您的SQL查询的前几个字符。 使用查询编辑器通过UI创建的任何查询都会在开始时命名。 如果查询是通过API创建的，则查询的名称是用于创建查询的初始SQL的片段。 您可以选择查询名称以在[!DNL Query Editor]中打开查询。 您还可以使用搜索栏搜索查询的[!UICONTROL Name]。 搜索区分大小写。 |
| **[!UICONTROL SQL]** | sql查询的前几个字符。 将鼠标悬停在代码上会显示完整查询。 |
| **[!UICONTROL 修改者]** | 上次修改查询的用户。 您组织中任何有权访问[!DNL Query Service]的用户都可以修改查询。 |
| **[!UICONTROL 上次修改时间]** | 上次修改查询的日期和时间，以浏览器的时区表示。 |

有关Platform UI中模板的详细信息，请参阅[查询模板](./query-templates.md)文档。

## 日志 {#log}

**[!UICONTROL Log]**&#x200B;选项卡提供以前已执行的查询列表。 默认情况下，日志会按反向时间顺序列出查询。

![A缩放到“查询仪表板日志”选项卡，显示按逆时间顺序排列的查询列表。](../images/ui/overview/log.png)

| 列 | 描述 |
| --- | --- |
| **[!UICONTROL 名称]** | 查询名称，由SQL查询的前几个字符组成。 选择模板名称以打开该运行的[!UICONTROL 查询日志详细信息]视图。 您可以使用搜索栏搜索查询的名称。 搜索区分大小写。 |
| **[!UICONTROL 开始时间]** | 执行查询的时间。 |
| **[!UICONTROL 完成时间]** | 查询运行完成的时间。 |
| **[!UICONTROL 状态]** | 查询的当前状态。 |
| **[!UICONTROL 数据集]** | 查询使用的输入数据集。 选择数据集以转到输入数据集详细信息屏幕。 |
| **[!UICONTROL 客户端]** | 用于查询的客户端。 |
| **[!UICONTROL 创建者]** | 创建查询的人员姓名。 |

>
>
>选择铅笔图标(![A铅笔图标。](/help/images/icons/edit.png))，以导航到[!DNL Query Editor]。 为方便编辑，已预填充查询。

有关查询事件自动生成的日志文件的详细信息，请参阅[查询日志文档](./query-logs.md)。

## 凭据

**[!UICONTROL 凭据]**&#x200B;选项卡同时显示您的过期凭据和非过期凭据。 有关如何使用这些凭据与外部客户端连接的详细信息，请参阅[凭据指南](../clients/overview.md)。

![突出显示“凭据”选项卡的“查询”仪表板。](../images/ui/overview/credentials.png)

## 后续步骤

现在您已经熟悉[!DNL Platform]上的[!DNL Query Service]用户界面，您可以访问[!DNL Query Editor]以开始创建自己的查询项目并与组织中的其他用户共享。 有关在[!DNL Query Editor]中创作和运行查询的详细信息，请参阅[[!DNL Query Editor] 用户指南](./user-guide.md)。
