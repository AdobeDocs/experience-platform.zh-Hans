---
keywords: Experience Platform；主页；热门主题；查询编辑器；查询编辑器；查询服务；查询服务；
solution: Experience Platform
title: 查询编辑器UI指南
description: 查询编辑器是Adobe Experience Platform查询服务提供的交互式工具，允许您在Experience Platform用户界面中编写、验证和运行客户体验数据查询。 查询编辑器支持开发用于分析和数据探索的查询，并允许您运行交互式查询以进行开发，以及运行非交互式查询以在Experience Platform中填充数据集。
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: 45eab8f894819eea36465ea0b8f3f3dd8f91fbe0
workflow-type: tm+mt
source-wordcount: '2432'
ht-degree: 0%

---

# 查询编辑器UI指南

>[!NOTE]
>
>旧版编辑器已于2024年5月24日弃用。 它不再可供使用。 您现在可以使用 [增强的查询编辑器](#enhanced-editor-toggle) 编写、验证和运行查询

查询编辑器是Adobe Experience Platform查询服务提供的交互式工具，允许您在中编写、验证和运行客户体验数据查询。 [!DNL Experience Platform] 用户界面。 查询编辑器支持开发用于分析和数据探索的查询，并允许您运行交互式查询以进行开发，以及运行非交互式查询以填充以下位置的数据集： [!DNL Experience Platform].

有关Query Service概念和功能的更多信息，请参见 [查询服务概述](../home.md). 要了解有关如何导航查询服务用户界面的更多信息，请访问 [!DNL Platform]，请参见 [查询服务UI概述](./overview.md).

## 快速入门 {#getting-started}

查询编辑器通过连接到查询服务来提供灵活的查询执行，并且查询仅在此连接处于活动状态时运行。

## 访问查询编辑器 {#accessing-query-editor}

在 [!DNL Experience Platform] UI，选择 **[!UICONTROL 查询]** 在左侧导航菜单中打开查询服务工作区。 接下来，要开始编写查询，请选择 **[!UICONTROL 创建查询]** 在屏幕的右上角。 此链接可从查询服务工作区中的任何页面使用。

![突出显示了“创建查询”的查询工作区概述选项卡。](../images/ui/query-editor/create-query.png)

### 正在连接到查询服务 {#connecting-to-query-service}

查询编辑器需要几秒钟才能初始化，并在打开时连接到查询服务。 控制台将告诉您连接时间，如下所示。 如果在编辑器连接之前尝试运行查询，则会延迟执行，直到连接完成。

![初次连接时查询编辑器的控制台输出。](../images/ui/query-editor/connect.png)

### 如何从查询编辑器运行查询 {#run-a-query}

从查询编辑器执行的查询以交互方式运行，这意味着如果关闭浏览器或离开浏览器，查询将被取消。 对于通过查询输出生成数据集的查询，也是如此。

## 使用增强型查询编辑器创作查询 {#query-authoring}

>[!NOTE]
>
>旧版编辑器已于2024年5月24日弃用。 它不再可供使用。 您现在可以使用增强型查询编辑器来编写、验证和运行查询。

使用查询编辑器，您可以编写、执行和保存客户体验数据的查询。 在查询编辑器中执行或保存的所有查询都可供贵组织中有权访问查询服务的所有用户使用。

### 设置 {#settings}

查询编辑器输入字段上方的设置图标包括用于启用/禁用深色主题或禁用/启用自动完成的选项。

>[!TIP]
>
>您可以 [!UICONTROL 禁用语法自动完成] 在创作查询时不会失去进度。

要启用深色或浅色主题，请选择设置图标(![设置图标。](../images/ui/query-editor/settings-icon.png))，然后显示下拉菜单中的选项。

![突出显示带有设置图标和启用深色主题下拉菜单选项的查询编辑器。](../images/ui/query-editor/query-editor-settings.png)

#### 自动完成 {#auto-complete}

查询编辑器会在您编写查询时，自动为查询建议潜在的SQL关键字以及表或列详细信息。 默认情况下，自动完成功能处于启用状态，可以随时从查询编辑器设置中禁用或启用该功能。

自动完成配置设置针对每个用户，并在该用户的连续登录中被记住。 禁用此功能会阻止处理多个元数据命令，并提供通常有利于作者在编辑查询时提高速度的建议。

<!-- Currently editing the auto complete setting info. -->



### 执行多个顺序查询 {#execute-multiple-sequential-queries}

使用增强型查询编辑器编写多个查询并按顺序执行所有查询。 按顺序执行多个查询，每个查询都会生成日志条目。 但是，查询编辑器控制台中只显示第一个查询的结果。 如果需要排除问题或确认已执行的查询，请查看查询日志。 请参阅 [查询日志文档](./query-logs.md) 以了解更多信息。

>[!NOTE]
> 
>如果在查询编辑器中的第一个查询之后执行CTAS查询，则仍会创建一个表，但查询编辑器控制台上没有输出。

### 执行选定的查询 {#execute-selected-query}

如果您已经编写了多个查询，但只需要执行一个查询，则可以突出显示所选的查询并选择
[!UICONTROL 运行选定的查询] 图标。 默认情况下，此图标处于禁用状态，直到您在编辑器中选择查询语法。

![具有的查询编辑器 [!UICONTROL 运行选定的查询] 图标高亮显示。](../images/ui/query-editor/run-selected-query.png)

### 取消查询编辑器会话 {#cancel-query}

通过取消长时间运行的查询来控制查询执行并提高生产效率。 此操作在查询运行时清除查询编辑器。 请注意，查询将继续在后台执行。 如果它是CTAS查询，仍会生成输出数据集。 要在编辑器中取消运行并继续编写SQL语句，请选择 **[!UICONTROL 取消查询]** 执行查询之后。

![使用的查询编辑器 [!UICONTROL 取消查询] 突出显示。](../images/ui/query-editor/cancel-query-run.png)

将显示确认对话框。 选择 **[!UICONTROL 确认]** 以取消查询运行。

![取消查询确认对话框突出显示“确认”。](../images/ui/query-editor/cancel-query-confirmation-dialog.png)

### 结果计数 {#result-count}

查询编辑器的行输出最多为50,000个。 您可以选择在查询编辑器控制台中一次显示的行数。 要更改控制台中显示的行数，请选择 **[!UICONTROL 结果计数]** 下拉菜单并从50、100、150、300和500选项中进行选择。

![突出显示结果计数下拉列表的查询编辑器。](../images/ui/query-editor/result-count.png)

## 编写查询 {#writing-queries}

[!UICONTROL 查询编辑器] 组织以尽可能方便编写查询。 下面的屏幕截图显示了编辑器在UI中的显示方式，其中包含SQL输入字段和 **播放** 突出显示。

![高亮显示SQL输入字段和“播放”的查询编辑器。](../images/ui/query-editor/editor.png)

为了最大限度地缩短开发时间，建议您开发对返回行数具有限制的查询。 例如：`SELECT fields FROM table WHERE conditions LIMIT number_of_rows`。验证查询是否生成预期输出后，删除限制并使用运行查询 `CREATE TABLE tablename AS SELECT` 以使用输出生成数据集。

## 在查询编辑器中编写工具 {#writing-tools}

- **自动语法突出显示：** 使读取和组织SQL更容易。

![查询编辑器中的SQL语句，用于演示语法颜色突出显示。](../images/ui/query-editor/syntax-highlight.png)

- **SQL关键字自动完成：** 开始键入您的查询，然后使用箭头键导航到所需术语并按 **输入**.

![带有自动完成下拉菜单的SQL的一些字符，该菜单提供来自查询编辑器的选项。](../images/ui/query-editor/syntax-auto.png)

- **表和字段自动完成：** 开始键入要使用的表名 `SELECT` ，然后使用箭头键导航到要查找的表，并按 **输入**. 选择表后，自动完成将识别该表中的字段。

![查询编辑器输入显示下拉表名称建议。](../images/ui/query-editor/tables-auto.png)

### 设置文本格式 {#format-text}

此 [!UICONTROL 设置文本格式] 功能通过添加标准化的语法样式使查询更易读取。 选择 **[!UICONTROL 设置文本格式]** 标准化查询编辑器中的所有文本。

>[!NOTE]
>
>此 [!UICONTROL 设置文本格式] 功能不适用于匿名块。 要了解如何按顺序链接一个或多个SQL语句，请参见 [匿名块文档](../key-concepts/anonymous-block.md).

![使用的查询编辑器 [!UICONTROL 设置文本格式] 和突出显示的SQL语句。](../images/ui/query-editor/format-text.png)

<!-- ### Undo text {#undo-text}

If you format your SQL in the Query Editor, you can undo the formatting applied by the [!UICONTROL Format text] feature. To return your SQL back to its original form, select **[!UICONTROL Undo text]**.

![The Query Editor with [!UICONTROL Undo text] and the SQL statements highlighted.](../images/ui/query-editor/undo-text.png) -->

### 复制 SQL {#copy-sql}

选择复制图标以将SQL从查询编辑器复制到剪贴板。 此复制功能可用于查询模板和查询编辑器中新创建的查询。

![查询工作区中有一个示例查询模板，该模板中高亮显示了复制图标。](../images/ui/query-editor/copy-sql.png)

### 查询详细信息 {#query-details}

要在查询编辑器中查看查询，请从中选择任何已保存的模板 [!UICONTROL 模板] 选项卡。 查询详细信息面板提供了更多信息和工具来管理所选查询。 它还显示有用的元数据，例如上次修改查询的时间以及修改查询的人员（如果适用）。

>[!NOTE]
>
>此 [!UICONTROL 查看计划]， [!UICONTROL 添加计划] 和 [!UICONTROL 删除查询] 仅当将查询另存为模板后，选项才可用。 此 [!UICONTROL 添加计划] 选项会将您直接从查询编辑器转到计划生成器。 此 [!UICONTROL 查看计划] 选项会将您直接转至该查询的计划库存。 请参阅查询计划文档，了解如何 [在UI中创建查询计划](./query-schedules.md#create-schedule).

![高亮显示查询详细信息面板的查询编辑器。](../images/ui/query-editor/query-details.png)

在详细信息面板中，您可以直接从UI生成输出数据集，删除或命名显示的查询，查看查询运行计划，并将查询添加到计划中。

要生成输出数据集，请选择 **[!UICONTROL 作为CTA运行]**. 此 **[!UICONTROL 输入输出数据集详细信息]** 出现对话框。 输入名称和说明，然后选择 **[!UICONTROL 作为CTA运行]**. 新数据集显示在中 **[!UICONTROL 数据集]** 浏览选项卡。 请参阅 [查看数据集文档](../../catalog/datasets/user-guide.md#view-datasets) 了解有关贵组织可用数据集的更多信息。

>[!NOTE]
>
>此 [!UICONTROL 作为CTA运行] 选项仅在查询具有 **非** 已计划。

![此 [!UICONTROL 输入输出数据集详细信息] 对话框。](../images/ui/query-editor/output-dataset-details.png)

在您执行 **[!UICONTROL 作为CTA运行]** 操作，此时会弹出一条确认消息，通知您操作成功。 此弹出消息包含一个链接，为导航到查询日志工作区提供了一种便捷的方式。 请参阅 [查询日志文档](./query-logs.md) 以了解有关查询日志的详细信息。

### 保存查询 {#saving-queries}

查询编辑器提供保存功能，允许您保存查询并稍后处理。 要保存查询，请选择 **[!UICONTROL 保存]** 位于查询编辑器的右上角。 在保存查询之前，必须使用为查询提供一个名称 **[!UICONTROL 查询详细信息]** 面板。

>[!NOTE]
>
>使用查询编辑器在中命名和保存的查询在查询仪表板中可用作模板 [!UICONTROL 模板] 选项卡。 请参阅 [模板文档](./query-templates.md) 以了解更多信息。

在查询编辑器中保存查询时，将会弹出一条确认消息，通知您操作成功。 此弹出消息包含一个链接，为导航到查询计划工作区提供了一种便捷的方法。 请参阅 [计划查询文档](./query-schedules.md) 以了解如何以自定义节奏运行查询。

### 计划的查询 {#scheduled-queries}

可以从“查询编辑器”安排已另存为模板的查询。 计划查询允许您以自定义节奏自动运行查询。 您可以根据频率、日期和时间安排查询，还可以在必要时为结果选择输出数据集。 也可以通过UI禁用或删除查询计划。

在查询编辑器中设置计划。 使用查询编辑器时，您只能将计划添加到已创建和保存的查询中。 该限制不适用于查询服务API。

>[!NOTE]
>
>连续十次运行失败的已计划查询将自动置于 [!UICONTROL 已隔离] 状态。 具有此状态的查询需要您的干预，然后才能进行任何进一步的执行。 请参阅 [隔离的查询](./monitor-queries.md#quarantined-queries) 文档，以了解更多详细信息。

请参阅查询计划文档，了解如何 [在UI中创建查询计划](./query-schedules.md). 或者，要了解如何使用API添加计划，请参阅 [计划查询端点指南](../api/scheduled-queries.md).

任何计划查询都会添加到的列表 [!UICONTROL 计划的查询] 选项卡。 在该工作区中，您可以通过UI监控所有已计划查询作业的状态。 在 [!UICONTROL 计划的查询] 选项卡，您可以找到有关查询运行的重要信息并订阅警报。 可用信息包括状态、计划详细信息和运行失败时的错误消息/代码。 请参阅 [监视计划查询文档](./monitor-queries.md) 以了解更多信息。


### 如何查找以前的查询 {#previous-queries}

从“查询编辑器”执行的所有查询都在“日志”表中捕获。 您可以使用中的搜索功能 **[!UICONTROL 日志]** 选项卡查找查询执行。 已保存的查询列在 **[!UICONTROL 模板]** 选项卡。

如果计划了查询，则 [!UICONTROL 计划的查询] 选项卡提高了这些查询作业在UI中的可见性。 请参阅 [查询监控文档](./monitor-queries.md) 以了解更多信息。

>[!NOTE]
>
>日志不会保存未执行的查询。 为了使查询在查询服务中可用，必须在查询编辑器中运行或保存查询。

## 使用查询编辑器执行查询 {#executing-queries}

要在查询编辑器中运行查询，您可以在编辑器中输入SQL或从以下位置加载上一个查询： **[!UICONTROL 日志]** 或 **[!UICONTROL 模板]** 选项卡，然后选择 **播放**. 查询执行的状态显示在 **[!UICONTROL 控制台]** 选项卡，并且输出数据显示在 **[!UICONTROL 结果]** 选项卡。

### 控制台 {#console}

控制台提供有关查询服务的状态和操作的信息。 控制台显示与查询服务的连接状态、正在执行的查询操作以及这些查询产生的任何错误消息。

![查询编辑器控制台的控制台选项卡。](../images/ui/query-editor/console.png)

>[!NOTE]
>
>控制台仅显示执行查询导致的错误。 它不显示查询执行前发生的查询验证错误。

### 查询结果 {#query-results}

查询完成后，结果将显示在 **[!UICONTROL 结果]** 选项卡，在 **[!UICONTROL 控制台]** 选项卡。 此视图显示查询的表格输出，根据您选择的结果显示50到500行结果 [结果计数](#result-count). 此视图允许您验证查询是否生成预期的输出。 要使用您的查询生成数据集，请删除对返回行的限制，然后运行查询 `CREATE TABLE tablename AS SELECT` 以使用输出生成数据集。 请参阅 [生成数据集教程](./create-datasets.md) 有关如何从查询编辑器中的查询结果生成数据集的说明。

![查询编辑器控制台的“结果”选项卡显示查询运行的结果。](../images/ui/query-editor/query-results.png)

## 用例 {#use-cases}

查询服务为跨行业和业务场景的各种用例提供解决方案。 这些实际示例展示了服务在满足各种需求方面的灵活性和影响。 至 [了解查询服务如何为您的特定业务需求带来价值](../use-cases/overview.md)中，了解用例文档的完整集合。 了解如何使用查询服务提供洞察信息和解决方案，以增强运营效率和业务成功。

<!-- This video is from 2019. The logic is sounds but the workflow is too outdated. -->

## 使用查询服务运行查询教程视频 {#query-tutorial-video}

以下视频介绍了如何在Adobe Experience Platform界面和PSQL客户端中运行查询。 此视频还演示了如何在XDM对象中使用单个属性、Adobe定义的函数，以及如何使用CREATE TABLE AS SELECT (CTAS)查询。

>[!NOTE]
>
>视频中描述的UI已过时，但在工作流中使用的逻辑保持不变。

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## 后续步骤

现在您已经知道查询编辑器中提供了哪些功能以及如何导航应用程序，您可以开始直接在中创作自己的查询 [!DNL Platform]. 有关在中针对数据集运行SQL查询的详细信息 [!DNL Data Lake]，请参阅指南，网址为 [正在运行查询](../best-practices/writing-queries.md).
