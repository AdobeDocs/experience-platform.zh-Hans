---
keywords: Experience Platform；主页；热门主题；查询编辑器；查询编辑器；查询服务；查询服务；
solution: Experience Platform
title: 查询编辑器UI指南
description: 查询编辑器是Adobe Experience Platform查询服务提供的交互式工具，允许您在Experience Platform用户界面中编写、验证和运行客户体验数据查询。 查询编辑器支持开发查询以进行分析和数据探索，并允许您运行交互式查询以进行开发，以及运行非交互式查询以填充Experience Platform中的数据集。
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: ff4b528a0456f46d8c99e5921cfc99b197956ba6
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 0%

---

# [!DNL Query Editor] UI指南

[!DNL Query Editor] 是Adobe Experience Platform提供的交互式工具 [!DNL Query Service]，允许您在中编写、验证和运行客户体验数据查询 [!DNL Experience Platform] 用户界面。 [!DNL Query Editor] 支持开发用于分析和数据探索的查询，并允许您运行交互式查询以进行开发，以及运行非交互式查询来填充数据集 [!DNL Experience Platform].

有关概念和功能的更多信息 [!DNL Query Service]，请参见 [查询服务概述](../home.md). 要了解有关如何导航查询服务用户界面的更多信息，请访问 [!DNL Platform]，请参见 [查询服务UI概述](./overview.md).

## 快速入门 {#getting-started}

[!DNL Query Editor] 通过连接到 [!DNL Query Service]和查询将仅在此连接处于活动状态时运行。

### 正在连接到 [!DNL Query Service] {#connecting-to-query-service}

[!DNL Query Editor] 需要几秒钟才能初始化并连接到 [!DNL Query Service] 打开时。 控制台将告诉您连接的时机，如下所示。 如果在编辑器连接之前尝试运行查询，则会在连接完成之前延迟执行。

![初始连接时查询编辑器的控制台输出。](../images/ui/query-editor/connect.png)

### 如何从运行查询 [!DNL Query Editor] {#run-a-query}

查询执行自 [!DNL Query Editor] 交互运行。 这意味着如果关闭浏览器或离开浏览器，查询将被取消。 对于为了从查询输出生成数据集而进行的查询，也是如此。

## 查询创作，使用 [!DNL Query Editor] {#query-authoring}

使用 [!DNL Query Editor]，您可以编写、执行和保存客户体验数据查询。 执行或保存的所有查询 [!DNL Query Editor] 可供贵组织中的所有用户访问 [!DNL Query Service].

### 访问 [!DNL Query Editor] {#accessing-query-editor}

在 [!DNL Experience Platform] UI，选择 **[!UICONTROL 查询]** 在左侧导航菜单中打开 [!DNL Query Service] 工作区。 接下来，选择 **[!UICONTROL 创建查询]** 开始编写查询。 此链接可从 [!DNL Query Service] 工作区。

![突出显示了“创建查询”的“查询”工作区概述选项卡。](../images/ui/query-editor/create-query.png)

### 编写查询 {#writing-queries}

[!UICONTROL 查询编辑器] 经过整理，以便尽可能轻松编写查询。 下面的屏幕截图显示了编辑器在UI中的显示方式，包括SQL输入字段和 **播放** 突出显示。

![高亮显示SQL输入字段和播放的查询编辑器。](../images/ui/query-editor/editor.png)

为了最大限度地缩短开发时间，建议您使用对返回行的限制来开发查询。 例如：`SELECT fields FROM table WHERE conditions LIMIT number_of_rows`。验证查询生成预期输出后，删除限制并使用运行查询 `CREATE TABLE tablename AS SELECT` 以使用输出生成数据集。

### 在中编写工具 [!DNL Query Editor] {#writing-tools}

- **自动语法突出显示：** 使读取和组织SQL更容易。

![查询编辑器中的SQL语句，用于演示语法颜色突出显示。](../images/ui/query-editor/syntax-highlight.png)

- **SQL关键字自动完成：** 开始键入您的查询，然后使用箭头键导航到所需的搜索词并按 **输入**.

![带有自动完成下拉菜单的SQL的一些字符，提供查询编辑器中的选项。](../images/ui/query-editor/syntax-auto.png)

- **表和字段自动完成：** 开始键入所需的表名 `SELECT` 从中，然后使用箭头键导航到要查找的表，然后按 **输入**. 选择表后，自动完成将识别该表中的字段。

![查询编辑器输入显示下拉表名称建议。](../images/ui/query-editor/tables-auto.png)

### 自动完成UI配置切换 {#auto-complete}

此 [!DNL Query Editor] 在编写查询时，自动为查询建议潜在的SQL关键字以及表或列详细信息。 默认情况下，自动完成功能处于启用状态，可以通过选择 [!UICONTROL 语法自动完成] 切换到“查询编辑器”的右上方。

自动完成配置设置是每个用户设置的，并且在该用户连续登录时记住该设置。

![突出显示语法自动完成切换的查询编辑器。](../images/ui/query-editor/auto-complete-toggle.png)

禁用此功能会阻止处理多个元数据命令，并提供通常有助于作者在编辑查询时提高速度的推荐。

使用切换启用自动完成功能时，在短暂暂停后即可获得有关表和列名称以及SQL关键字的建议建议。 控制台中查询编辑器下方的成功消息指示该功能处于活动状态。

如果禁用自动完成功能，则需刷新页面才能使功能生效。 禁用时，将显示一个包含三个选项的确认对话框 [!UICONTROL 语法自动完成] 切换：

- [!UICONTROL 取消]
- [!UICONTROL 保存更改并刷新]
- [!UICONTROL 刷新而不保存更改]

>[!IMPORTANT]
>
>如果您在禁用此功能时正在编写或编辑查询，则必须在刷新页面之前保存对查询所做的任何更改，否则所有进度都将丢失。

![用于禁用自动完成功能的确认对话框。](../images/ui/query-editor/confirmation-dialog.png)

选择相应的选项以禁用自动完成功能。

### 错误检测 {#error-detection}

[!DNL Query Editor] 在编写查询时自动验证查询，提供通用SQL验证和特定执行验证。 如果查询下方出现红色下划线（如下图所示），则表示查询中存在错误。

![查询编辑器输入以红色下划线显示SQL以指示错误。](../images/ui/query-editor/syntax-error-highlight.png)

检测到错误时，可通过将鼠标悬停在SQL代码上来查看特定的错误消息。

![带有错误消息的对话框。](../images/ui/query-editor/linting-error.png)

### 查询详细信息 {#query-details}

从中选择任何已保存的模板 [!UICONTROL 模板] 选项卡，以在查询编辑器中查看它。 “查询详细信息”面板提供管理所选查询的更多信息和工具。

![高亮显示查询详细信息面板的查询编辑器。](../images/ui/query-editor/query-details.png)

此面板允许您直接从UI生成输出数据集、删除或命名显示的查询，以及向查询添加计划。

此面板还显示有用的元数据，例如上次修改查询的时间以及修改查询的人员（如果适用）。 要生成数据集，请选择 **[!UICONTROL 输出数据集]**. 此 **[!UICONTROL 输出数据集]** 对话框。 输入名称和说明，然后选择 **[!UICONTROL 运行查询]**. 新数据集将显示在 **[!UICONTROL 数据集]** 选项卡 [!DNL Query Service] 上的用户界面 [!DNL Platform].

### 计划的查询 {#scheduled-queries}

可以从“查询编辑器”安排已另存为模板的查询。 这允许您以自定义节奏自动运行查询。 您可以根据频率、日期和时间安排查询，还可以根据需要为结果选择输出数据集。 也可以通过UI禁用或删除查询计划。

在查询编辑器中设置计划。 使用查询编辑器时，您只能向已创建、保存和运行的查询添加计划。 这不适用于 [!DNL Query Service] API：

请参阅查询计划文档，了解如何 [在UI中创建查询计划](./query-schedules.md). 或者，要了解如何使用API添加计划，请阅读 [计划查询端点指南](../api/scheduled-queries.md).

任何计划的查询都会添加到的列表 [!UICONTROL 计划的查询] 选项卡。 在该工作区中，您可以通过UI监控所有已计划查询作业的状态。 在 [!UICONTROL 计划的查询] 选项卡，您可以找到有关查询运行的重要信息并订阅警报。 可用信息包括运行失败时的状态、计划详细信息和错误消息/代码。 请参阅 [监视计划查询文档](./monitor-queries.md) 了解更多信息。

### 保存查询 {#saving-queries}

此 [!DNL Query Editor] 提供保存功能，允许您保存查询并稍后处理。 要保存查询，请选择 **[!UICONTROL 保存]** 在的右上角 [!DNL Query Editor]. 在保存查询之前，必须使用为查询提供一个名称 **[!UICONTROL 查询详细信息]** 面板。

>[!NOTE]
>
>使用查询编辑器在中命名和保存的查询可用作查询仪表板中的模板 [!UICONTROL 模板] 选项卡。 请参阅 [模板文档](./query-templates.md) 了解更多信息。

### 如何查找以前的查询 {#previous-queries}

从以下位置执行的所有查询 [!DNL Query Editor] 将在Log表中捕获。 您可以使用中的搜索功能 **[!UICONTROL 日志]** 选项卡查找查询执行。 已保存的查询列在 **[!UICONTROL 模板]** 选项卡。

如果计划了查询，则 [!UICONTROL 计划的查询] 选项卡提高了这些查询作业在UI中的可见性。 请参阅 [查询监控文档](./monitor-queries.md) 了解更多信息。

>[!NOTE]
>
>日志不保存未执行的查询。 为了使查询可用于 [!DNL Query Service]，它必须运行或保存在中 [!DNL Query Editor].

## 使用查询编辑器执行查询 {#executing-queries}

在中运行查询 [!DNL Query Editor]，您可以在编辑器中输入SQL或从以下位置加载上一个查询： **[!UICONTROL 日志]** 或 **[!UICONTROL 模板]** 选项卡，然后选择 **播放**. 查询执行的状态显示在 **[!UICONTROL 控制台]** 选项卡，并且输出数据显示在 **[!UICONTROL 结果]** 选项卡。

### 控制台 {#console}

控制台提供有关以下项目的状态和操作的信息 [!DNL Query Service]. 控制台显示与的连接状态 [!DNL Query Service]、正在执行的查询操作以及这些查询产生的任何错误消息。

![查询编辑器控制台的控制台选项卡。](../images/ui/query-editor/console.png)

>[!NOTE]
>
>控制台仅显示执行查询导致的错误。 它不会在执行查询之前显示查询验证错误。

### 查询结果 {#query-results}

查询完成后，结果将显示在 **[!UICONTROL 结果]** 选项卡，在 **[!UICONTROL 控制台]** 选项卡。 此视图显示查询的表格输出，最多显示100行。 利用此视图，可验证查询是否生成预期的输出。 要使用您的查询生成数据集，请删除对返回行的限制，然后运行查询 `CREATE TABLE tablename AS SELECT` 以使用输出生成数据集。 请参阅 [生成数据集教程](./create-datasets.md) 有关如何从中的查询结果生成数据集的说明 [!DNL Query Editor].

![查询编辑器控制台的“结果”选项卡显示查询运行的结果。](../images/ui/query-editor/query-results.png)

## 运行查询 [!DNL Query Service] 教程视频 {#query-tutorial-video}

以下视频说明如何在Adobe Experience Platform界面和PSQL客户端中运行查询。 此外，还演示了在XDM对象中使用单个属性、使用Adobe定义的函数以及使用CREATE TABLE AS SELECT (CTAS)等方法。

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## 后续步骤

现在您知道了中提供了哪些功能 [!DNL Query Editor] 以及如何导航应用程序，您可以直接在中开始创作自己的查询 [!DNL Platform]. 有关在中针对数据集运行SQL查询的详细信息 [!DNL Data Lake]，请参阅指南，网址为 [正在运行查询](../best-practices/writing-queries.md).
