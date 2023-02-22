---
keywords: Experience Platform；主页；热门主题；查询编辑器；查询编辑器；查询服务；查询服务；
solution: Experience Platform
title: 查询编辑器UI指南
description: 查询编辑器是Adobe Experience Platform查询服务提供的一个交互式工具，允许您在Experience Platform用户界面中编写、验证和运行客户体验数据查询。 查询编辑器支持开发用于分析和数据探索的查询，并且允许您运行交互式查询以用于开发目的，以及非交互式查询以填充Experience Platform中的数据集。
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: 90829713e85e930e4fd6a32b0dbd38aeb837b84e
workflow-type: tm+mt
source-wordcount: '1696'
ht-degree: 0%

---

# [!DNL Query Editor] UI指南

[!DNL Query Editor] 是Adobe Experience Platform提供的交互式工具 [!DNL Query Service]，允许您在 [!DNL Experience Platform] 用户界面。 [!DNL Query Editor] 支持开发用于分析和数据探索的查询，并且允许您为开发目的运行交互式查询，以及用于填充 [!DNL Experience Platform].

有关 [!DNL Query Service]，请参阅 [查询服务概述](../home.md). 要详细了解如何在 [!DNL Platform]，请参阅 [查询服务UI概述](./overview.md).

## 快速入门 {#getting-started}

[!DNL Query Editor] 通过连接到 [!DNL Query Service]、和查询将仅在此连接处于活动状态时运行。

### 连接到 [!DNL Query Service] {#connecting-to-query-service}

[!DNL Query Editor] 需要几秒钟时间才能初始化并连接到 [!DNL Query Service] 打开时。 控制台会告知您何时连接，如下所示。 如果在编辑器连接之前尝试运行查询，则会延迟执行，直到连接完成为止。

![初始连接时查询编辑器的控制台输出。](../images/ui/query-editor/connect.png)

### 如何从中运行查询 [!DNL Query Editor] {#run-a-query}

从执行的查询 [!DNL Query Editor] 以交互方式运行。 这意味着，如果您关闭浏览器或导航离开，则查询将被取消。 对于通过查询输出生成数据集而进行的查询，也是如此。

## 使用进行查询创作 [!DNL Query Editor] {#query-authoring}

使用 [!DNL Query Editor]，您可以编写、执行和保存客户体验数据查询。 执行或保存在中的所有查询 [!DNL Query Editor] 可供贵组织中具有 [!DNL Query Service].

### 访问 [!DNL Query Editor] {#accessing-query-editor}

在 [!DNL Experience Platform] UI，选择 **[!UICONTROL 查询]** 在左侧导航菜单中，打开 [!DNL Query Service] 工作区。 接下来，选择 **[!UICONTROL 创建查询]** 来开始编写查询。 此链接可从 [!DNL Query Service] 工作区。

![“查询”工作区“概述”选项卡，其中突出显示了“创建查询”。](../images/ui/query-editor/create-query.png)

### 编写查询 {#writing-queries}

[!UICONTROL 查询编辑器] 组织以尽可能简单地编写查询。 以下屏幕截图显示了编辑器在UI中的显示方式，以及SQL条目字段和 **播放** 突出显示。

![突出显示SQL输入字段和播放的查询编辑器。](../images/ui/query-editor/editor.png)

为了最大程度地缩短开发时间，建议您开发查询，并对返回的行进行限制。 例如：`SELECT fields FROM table WHERE conditions LIMIT number_of_rows`。验证查询是否生成预期输出后，请删除限制并使用 `CREATE TABLE tablename AS SELECT` 生成包含输出的数据集。

### 在中编写工具 [!DNL Query Editor] {#writing-tools}

- **自动语法突出显示：** 使读取和组织SQL更加容易。

![查询编辑器中的SQL语句，用于演示语法颜色突出显示。](../images/ui/query-editor/syntax-highlight.png)

- **SQL关键字自动完成：** 开始键入查询，然后使用箭头键导航到所需的搜索词并按 **输入**.

![自动完成下拉菜单中提供了查询编辑器选项的SQL的几个字符。](../images/ui/query-editor/syntax-auto.png)

- **表和字段自动完成：** 开始键入要输入的表名 `SELECT` 从，然后使用箭头键导航到要查找的表，然后按 **输入**. 选择表后，自动完成将识别该表中的字段。

![显示下拉表名称建议的查询编辑器输入。](../images/ui/query-editor/tables-auto.png)

### 自动完成UI配置切换 {#auto-complete}

的 [!DNL Query Editor] 在编写查询时，会自动建议潜在的SQL关键字以及表或列的详细信息。 自动完成功能默认处于启用状态，并且可以通过选择 [!UICONTROL 语法自动完成] 切换到查询编辑器的右上角。

自动完成配置设置是按用户进行的，并在连续登录时记住该设置。

![语法自动完成切换的查询编辑器高亮显示。](../images/ui/query-editor/auto-complete-toggle.png)

禁用此功能会阻止处理多个元数据命令，并提供在编辑查询时通常有助于提高创作速度的推荐。

使用切换开关启用自动完成功能时，对于表和列名称以及SQL关键字的推荐建议会在短暂暂停后变得可用。 控制台中查询编辑器下方的成功消息表示该功能处于活动状态。

如果禁用自动完成功能，则需要刷新页面才能使该功能生效。 在禁用 [!UICONTROL 语法自动完成] 切换：

- [!UICONTROL 取消]
- [!UICONTROL 保存更改并刷新]
- [!UICONTROL 刷新而不保存更改]

>[!IMPORTANT]
>
>如果您在禁用此功能时正在编写或编辑查询，则必须在刷新页面之前保存对查询所做的任何更改，否则所有进度都将丢失。

![用于禁用自动完成功能的确认对话框。](../images/ui/query-editor/confirmation-dialog.png)

选择相应的选项以禁用自动完成功能。

### 错误检测 {#error-detection}

[!DNL Query Editor] 在您编写查询时自动验证查询，提供通用SQL验证和特定执行验证。 如果查询的下方显示红色下划线（如下图所示），则表示查询中存在错误。

![查询编辑器输入，以红色带下划线的方式显示SQL，以指示错误。](../images/ui/query-editor/syntax-error-highlight.png)

当检测到错误时，您可以通过将鼠标悬停在SQL代码上来查看特定的错误消息。

![出现错误消息的对话框。](../images/ui/query-editor/linting-error.png)

### 查询详细信息 {#query-details}

从 [!UICONTROL 模板] 选项卡，以在查询编辑器中查看。 “查询详细信息”面板提供了用于管理所选查询的更多信息和工具。

![突出显示了查询详细信息面板的查询编辑器。](../images/ui/query-editor/query-details.png)

利用此面板，可直接从UI中生成输出数据集、删除或命名显示的查询，以及向查询添加计划。

此面板还显示有用的元数据，例如上次修改查询的时间以及修改查询的人员（如果适用）。 要生成数据集，请选择 **[!UICONTROL 输出数据集]**. 的 **[!UICONTROL 输出数据集]** 对话框。 输入名称和描述，然后选择 **[!UICONTROL 运行查询]**. 新数据集显示在 **[!UICONTROL 数据集]** 选项卡 [!DNL Query Service] 用户界面开启 [!DNL Platform].

### 计划查询 {#scheduled-queries}

可以从查询编辑器中计划已另存为模板的查询。 这允许您在自定义频率上自动运行查询。 您可以根据频度、日期和时间计划查询，还可以根据需要为结果选择一个输出数据集。 还可以通过UI禁用或删除查询计划。

计划是通过查询编辑器设置的。 以下是使用查询编辑器时计划查询的限制列表。 它们不适用于 [!DNL Query Service] API:

- 您只能向已创建、保存和运行的查询添加计划。
- 您 **无法** 向参数化查询添加计划。
- 计划查询 **无法** 包含匿名块。

请参阅查询计划文档，以了解如何 [在UI中创建查询计划](./query-schedules.md). 或者，要了解如何使用API添加计划，请阅读 [计划查询终结点指南](../api/scheduled-queries.md).

任何计划查询都将添加到 [!UICONTROL 计划查询] 选项卡。 在该工作区中，您可以通过UI监控所有计划查询作业的状态。 在 [!UICONTROL 计划查询] 选项卡，您可以找到有关查询运行和订阅警报的重要信息。 可用信息包括状态、计划详细信息以及运行失败时的错误消息/代码。 请参阅 [监视计划查询文档](./monitor-queries.md) 以了解更多信息。

### 保存查询 {#saving-queries}

的 [!DNL Query Editor] 提供了保存函数，用于保存查询并稍后对其进行处理。 要保存查询，请选择 **[!UICONTROL 保存]** 的右上角 [!DNL Query Editor]. 在保存查询之前，必须使用 **[!UICONTROL 查询详细信息]** 的上界。

>[!NOTE]
>
>使用查询编辑器命名和保存的查询可用作查询功能板中的模板 [!UICONTROL 模板] 选项卡。 请参阅 [模板文档](./query-templates.md) 以了解更多信息。

### 如何查找以前的查询 {#previous-queries}

执行的所有查询 [!DNL Query Editor] 在日志表中捕获。 您可以在 **[!UICONTROL 日志]** 选项卡来查找查询执行。 保存的查询列在 **[!UICONTROL 模板]** 选项卡。

如果已计划查询，则 [!UICONTROL 计划查询] 选项卡为这些查询作业提供了更好的UI可见性。 请参阅 [查询监控文档](./monitor-queries.md) 以了解更多信息。

>[!NOTE]
>
>日志不会保存未执行的查询。 为了使查询在 [!DNL Query Service]，则必须运行或保存在中 [!DNL Query Editor].

## 使用查询编辑器执行查询 {#executing-queries}

在中运行查询 [!DNL Query Editor]，则可以在编辑器中输入SQL或从 **[!UICONTROL 日志]** 或 **[!UICONTROL 模板]** ，然后选择 **播放**. 查询执行的状态显示在 **[!UICONTROL 控制台]** 选项卡，并在 **[!UICONTROL 结果]** 选项卡。

### 控制台 {#console}

控制台提供有关 [!DNL Query Service]. 控制台将显示与 [!DNL Query Service]、正在执行的查询操作以及从这些查询产生的任何错误消息。

![查询编辑器控制台的控制台选项卡。](../images/ui/query-editor/console.png)

>[!NOTE]
>
>控制台仅显示执行查询所导致的错误。 在执行查询之前，不会显示查询验证错误。

### 查询结果 {#query-results}

完成查询后，结果将显示在 **[!UICONTROL 结果]** 选项卡 **[!UICONTROL 控制台]** 选项卡。 此视图以表格形式显示查询的输出，最多显示100行。 利用此视图，可验证查询是否生成预期的输出。 要使用查询生成数据集，请删除返回的行限制，然后使用 `CREATE TABLE tablename AS SELECT` 生成包含输出的数据集。 请参阅 [生成数据集教程](./create-datasets.md) 有关如何根据 [!DNL Query Editor].

![查询编辑器控制台的“结果”选项卡显示查询运行的结果。](../images/ui/query-editor/query-results.png)

## 运行查询 [!DNL Query Service] 教程视频 {#query-tutorial-video}

以下视频演示如何在Adobe Experience Platform界面和PSQL客户端中运行查询。 此外，还演示了如何在XDM对象中使用单个属性、使用Adobe定义的函数以及使用CREATE TABLE AS SELECT(CTAS)。

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## 后续步骤

现在，您已了解 [!DNL Query Editor] 以及如何导航应用程序，您可以直接在 [!DNL Platform]. 有关针对 [!DNL Data Lake]，请参阅 [运行查询](../best-practices/writing-queries.md).
