---
keywords: Experience Platform；主页；热门主题；查询编辑器；查询编辑器；查询服务；查询服务；
solution: Experience Platform
title: 查询编辑器UI指南
topic-legacy: query editor
description: 查询编辑器是Adobe Experience Platform查询服务提供的一个交互式工具，允许您在Experience Platform用户界面中编写、验证和运行客户体验数据查询。 查询编辑器支持开发用于分析和数据探索的查询，并且允许您运行交互式查询以用于开发目的，以及非交互式查询以填充Experience Platform中的数据集。
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: aa61cb696d647c5f039283ce5926d5fa1e901a13
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 1%

---

# [!DNL Query Editor] UI指南

[!DNL Query Editor] 是Adobe Experience Platform提供的交互式工具 [!DNL Query Service]，允许您在 [!DNL Experience Platform] 用户界面。 [!DNL Query Editor] 支持开发用于分析和数据探索的查询，并且允许您为开发目的运行交互式查询，以及用于填充 [!DNL Experience Platform].

有关 [!DNL Query Service]，请参阅 [查询服务概述](../home.md). 要详细了解如何在 [!DNL Platform]，请参阅 [查询服务UI概述](./overview.md).

## 快速入门 {#getting-started}

[!DNL Query Editor] 通过连接到 [!DNL Query Service]、和查询将仅在此连接处于活动状态时运行。

### 连接到 [!DNL Query Service] {#connecting-to-query-service}

[!DNL Query Editor] 需要几秒钟时间才能初始化并连接到 [!DNL Query Service] 打开时。 控制台会告知您何时连接，如下所示。 如果在编辑器连接之前尝试运行查询，则会延迟执行，直到连接完成为止。

![图像](../images/ui/query-editor/connect.png)

### 如何从中运行查询 [!DNL Query Editor] {#run-a-query}

从执行的查询 [!DNL Query Editor] 以交互方式运行。 这意味着，如果您关闭浏览器或导航离开，则查询将被取消。 对于通过查询输出生成数据集而进行的查询，也是如此。

## 使用进行查询创作 [!DNL Query Editor] {#query-authoring}

使用 [!DNL Query Editor]，您可以编写、执行和保存客户体验数据查询。 执行或保存在中的所有查询 [!DNL Query Editor] 可供贵组织中具有 [!DNL Query Service].

### 访问 [!DNL Query Editor] {#accessing-query-editor}

在 [!DNL Experience Platform] UI，选择 **[!UICONTROL 查询]** 在左侧导航菜单中，打开 [!DNL Query Service] 工作区。 接下来，选择 **[!UICONTROL 创建查询]** 来开始编写查询。 此链接可从 [!DNL Query Service] 工作区。

![图像](../images/ui/query-editor/create-query.png)

### 编写查询 {#writing-queries}

[!UICONTROL 查询编辑器] 组织以尽可能简单地编写查询。 以下屏幕截图显示编辑器在UI中的显示方式，其中 **播放** 按钮和SQL条目字段突出显示。

![图像](../images/ui/query-editor/editor.png)

为了最大程度地缩短开发时间，建议您开发查询，并对返回的行进行限制。 例如：`SELECT fields FROM table WHERE conditions LIMIT number_of_rows`。验证查询是否生成预期输出后，请删除限制并使用 `CREATE TABLE tablename AS SELECT` 生成包含输出的数据集。

### 在中编写工具 [!DNL Query Editor] {#writing-tools}

- **自动语法突出显示：** 使读取和组织SQL更加容易。

![图像](../images/ui/query-editor/syntax-highlight.png)

- **SQL关键字自动完成：** 开始键入查询，然后使用箭头键导航到所需的搜索词并按 **输入**.

![图像](../images/ui/query-editor/syntax-auto.png)

- **表和字段自动完成：** 开始键入要输入的表名 `SELECT` 从，然后使用箭头键导航到要查找的表，然后按 **输入**. 选择表后，自动完成将识别该表中的字段。

![图像](../images/ui/query-editor/tables-auto.png)

### 错误检测 {#error-detection}

[!DNL Query Editor] 在您编写查询时自动验证查询，提供通用SQL验证和特定执行验证。 如果查询的下方显示红色下划线（如下图所示），则表示查询中存在错误。

![图像](../images/ui/query-editor/syntax-error-highlight.png)

当检测到错误时，您可以通过将鼠标悬停在SQL代码上来查看特定的错误消息。

![图像](../images/ui/query-editor/linting-error.png)

### 查询详细信息 {#query-details}

在中查看查询时 [!DNL Query Editor], **[!UICONTROL 查询详细信息]** 面板提供了用于管理所选查询的工具。

![图像](../images/ui/query-editor/query-details.png)

利用此面板，可直接从UI中生成输出数据集、删除或命名显示的查询，以及向查询添加计划。

此面板还显示有用的元数据，例如上次修改查询的时间以及修改查询的人员（如果适用）。 要生成数据集，请选择 **[!UICONTROL 输出数据集]**. 的 **[!UICONTROL 输出数据集]** 对话框。 输入名称和描述，然后选择 **[!UICONTROL 运行查询]**. 新数据集显示在 **[!UICONTROL 数据集]** 选项卡 [!DNL Query Service] 用户界面开启 [!DNL Platform].

### 计划查询 {#scheduled-queries}

>[!IMPORTANT]
>
>以下是使用查询编辑器时计划查询的限制列表。 它们不适用于 [!DNL Query Service] API:<br/>您只能向已创建、保存和运行的查询添加计划。<br/>您 **无法** 向参数化查询添加计划。<br/>计划查询 **无法** 包含匿名块。

要向查询添加计划，请选择 **[!UICONTROL 添加计划]**.

![图像](../images/ui/query-editor/add-schedule.png)

的 **[!UICONTROL 计划详细信息]** 页面。 在此页面上，您可以选择计划查询的频率、计划查询运行的日期以及要将查询导出到的数据集。

![图像](../images/ui/query-editor/schedule-details.png)

您可以为 **[!UICONTROL 频率]**:

- **[!UICONTROL 每小时]**:在您选择的日期期间，计划查询将每小时运行一次。
- **[!UICONTROL 每日]**:计划查询将在您选择的时间和日期期间每X天运行一次。 请注意，选择的时间在 **UTC**，而不是您的本地时区。
- **[!UICONTROL 每周]**:所选查询将在您选择的周、时间和日期期间的天数运行。 请注意，选择的时间在 **UTC**，而不是您的本地时区。
- **[!UICONTROL 每月]**:选定的查询将每月在您选择的日期、时间和日期期间运行。 请注意，选择的时间在 **UTC**，而不是您的本地时区。
- **[!UICONTROL 每年]**:选定的查询将每年在您选择的日期、月、时间和日期期间运行。 请注意，选择的时间在 **UTC**，而不是您的本地时区。

对于数据集，您可以选择使用现有数据集或创建新数据集。

>[!IMPORTANT]
>
> 由于您使用的是现有数据集或创建了新数据集，因此需要 **not** 需要包括 `INSERT INTO` 或 `CREATE TABLE AS SELECT` 作为查询的一部分，因为数据集已经设置。 包括 `INSERT INTO` 或 `CREATE TABLE AS SELECT` 作为计划查询的一部分，将导致错误。

确认所有这些详细信息后，选择 **[!UICONTROL 保存]** 创建计划。

此时将重新显示查询详细信息页面，并显示新创建计划的详细信息，包括计划ID、计划本身和计划的输出数据集。 您可以使用计划ID查找有关计划查询本身运行的更多信息。 要了解更多信息，请阅读 [计划查询运行端点指南](../api/runs-scheduled-queries.md).

>[!NOTE]
>
> 您只能计划 **one** 使用UI查询模板。 如果要向查询模板添加其他计划，则需要使用API。 如果已使用API添加计划，则您将 **not** 能够使用UI添加其他计划。 如果已将多个计划附加到查询模板，则只会显示最早的计划。 要了解如何使用API添加计划，请阅读 [计划查询终结点指南](../api/scheduled-queries.md).
>
> 此外，如果要确保所查看的计划具有最新状态，则应刷新页面。

#### 删除计划 {#delete-schedule}

您可以通过选择 **[!UICONTROL 删除计划]**.

![图像](../images/ui/query-editor/delete-schedule.png)

>[!IMPORTANT]
>
> 如果要删除查询的计划，必须先禁用该计划。

### 保存查询 {#saving-queries}

[!DNL Query Editor] 提供了保存函数，用于保存查询并稍后对其进行处理。 要保存查询，请选择 **[!UICONTROL 保存]** 的右上角 [!DNL Query Editor]. 在保存查询之前，必须使用 **[!UICONTROL 查询详细信息]** 的上界。

### 如何查找以前的查询 {#previous-queries}

执行的所有查询 [!DNL Query Editor] 在日志表中捕获。 您可以在 **[!UICONTROL 日志]** 选项卡来查找查询执行。 保存的查询列在 **[!UICONTROL 浏览]** 选项卡。

请参阅 [查询服务UI概述](./overview.md) 以了解更多信息。

>[!NOTE]
>
>日志不会保存未执行的查询。 为了使查询在 [!DNL Query Service]，则必须运行或保存在中 [!DNL Query Editor].

## 使用查询编辑器执行查询 {#executing-queries}

在中运行查询 [!DNL Query Editor]，则可以在编辑器中输入SQL或从 **[!UICONTROL 日志]** 或 **[!UICONTROL 浏览]** ，然后选择 **播放**. 查询执行的状态显示在 **[!UICONTROL 控制台]** 选项卡，并在 **[!UICONTROL 结果]** 选项卡。

### 控制台 {#console}

控制台提供有关 [!DNL Query Service]. 控制台将显示与 [!DNL Query Service]、正在执行的查询操作以及从这些查询产生的任何错误消息。

![图像](../images/ui/query-editor/console.png)

>[!NOTE]
>
>控制台仅显示执行查询所导致的错误。 在执行查询之前，不会显示查询验证错误。

### 查询结果 {#query-results}

完成查询后，结果将显示在 **[!UICONTROL 结果]** 选项卡 **[!UICONTROL 控制台]** 选项卡。 此视图以表格形式显示查询的输出，最多显示100行。 利用此视图，可验证查询是否生成预期的输出。 要使用查询生成数据集，请删除返回的行限制，然后使用 `CREATE TABLE tablename AS SELECT` 生成包含输出的数据集。 请参阅 [生成数据集教程](./create-datasets.md) 有关如何根据 [!DNL Query Editor].

![图像](../images/ui/query-editor/query-results.png)

## 运行查询 [!DNL Query Service] 教程视频 {#query-tutorial-video}

以下视频演示如何在Adobe Experience Platform界面和PSQL客户端中运行查询。 此外，还演示了如何在XDM对象中使用单个属性、使用Adobe定义的函数以及使用CREATE TABLE AS SELECT(CTAS)。

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## 后续步骤

现在，您已了解 [!DNL Query Editor] 以及如何导航应用程序，您可以直接在 [!DNL Platform]. 有关针对 [!DNL Data Lake]，请参阅 [运行查询](../best-practices/writing-queries.md).
