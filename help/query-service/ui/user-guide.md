---
keywords: Experience Platform；主页；热门主题；查询编辑器；查询编辑器；查询服务；查询服务；
solution: Experience Platform
title: 查询编辑器用户指南
topic: query editor
description: 查询编辑器是Adobe Experience Platform查询服务提供的交互式工具，它允许您在Experience Platform用户界面中为客户体验数据编写、验证和运行查询。 查询编辑器支持开发分析和数据的查询，并允许您运行交互式查询以用于开发目的，以及运行非交互式查询以填充Experience Platform集。
translation-type: tm+mt
source-git-commit: f35443046a3d2bc5101d0fa2a58d07f4b6a31151
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 1%

---


# [!DNL Query Editor] 用户指南

[!DNL Query Editor] 是Adobe Experience Platform提供的交互式 [!DNL Query Service]工具，它允许您在用户界面中编写、验证和运行查询以获取客 [!DNL Experience Platform] 户体验数据。[!DNL Query Editor] 支持开发查询以进行分析和数据探索，并允许您运行交互式查询以用于开发目的，以及使用非交互式查询来填充数据集 [!DNL Experience Platform]

有关[!DNL Query Service]的概念和功能的详细信息，请参阅[查询服务概述][query-service-overview]。 要进一步了解如何在[!DNL Platform]上导航查询服务用户界面，请参阅[查询服务UI概述][query-service-ui]。

## 入门指南

[!DNL Query Editor] 通过连接提供灵活的查询执 [!DNL Query Service]行，并且查询将仅在此连接处于活动状态时运行。

### 连接到[!DNL Query Service]

[!DNL Query Editor] 初始化并连接到打开 [!DNL Query Service] 时需要几秒钟。控制台会告诉您何时连接，如下所示。 如果尝试在编辑器连接之前运行查询，则会延迟执行，直到连接完成。

![图像](../images/queries/query-editor-overview/initializing-connection.png)

### 如何从[!DNL Query Editor]运行查询

从[!DNL Query Editor]执行的查询以交互方式运行。 这意味着，如果您关闭浏览器或导航离开，查询将被取消。 对于从查询输出生成数据集的查询，也是如此。

## 查询创作（使用[!DNL Query Editor]）

使用[!DNL Query Editor]，您可以编写、执行和保存查询以获得客户体验数据。 在[!DNL Query Editor]中执行或保存的所有查询对组织中有权访问[!DNL Query Service]的所有用户都可用。

### 访问 [!DNL Query Editor]

在[!DNL Experience Platform] UI中，单击左侧导航菜单中的&#x200B;**[!UICONTROL 查询]**&#x200B;以打开[!DNL Query Service]工作区。 接下来，单击屏幕右上方的&#x200B;**[!UICONTROL 创建查询]**&#x200B;以开始写入查询。 此链接可从[!DNL Query Service]工作区中的任何页面访问。

![图像](../images/queries/query-editor-overview/create-query.png)

### 编写查询

[!UICONTROL 查询] 编辑人员组织使编写查询尽可能简单。下面的屏幕截图显示了编辑器在UI中的显示方式，其中突出显示了&#x200B;**播放**&#x200B;按钮和SQL条目字段。

![图像](../images/queries/query-editor-overview/editor.png)

为最大限度地缩短开发时间，建议您开发具有返回行限制的查询。 例如：`SELECT fields FROM table WHERE conditions LIMIT number_of_rows`。验证查询生成预期输出后，请删除限制并运行带`CREATE TABLE tablename AS SELECT`的查询以生成带有输出的数据集。

### 在[!DNL Query Editor]中编写工具

- **自动语法高亮显** 示：使读取和组织SQL更简单。

![图像](../images/queries/query-editor-overview/syntax-highlight.png)

- **SQL关键字自动完成：** 开始键入查询，然后使用箭头键导航到所需词并按 **Enter**。

![图像](../images/queries/query-editor-overview/syntax-auto.png)

- **表和字段自动完** 成：开始键入要从 `SELECT` 的表名称，然后使用箭头键导航到要查找的表，并按 **Enter**。选择表后，自动完成将识别该表中的字段。

![图像](../images/queries/query-editor-overview/tables-auto.png)

### 错误检测

[!DNL Query Editor] 在编写查询时自动验证该数据，提供通用SQL验证和特定执行验证。如果查询下方显示红色下划线（如下图所示），则表示查询内有错误。

![图像](../images/queries/query-editor-overview/syntax-error-highlight.png)

检测到错误后，可以将鼠标悬停在SQL代码上，以视图特定的错误消息。

![图像](../images/queries/query-editor-overview/linting-error.png)

### 查询详细信息

当您在[!DNL Query Editor]中查看查询时，**[!UICONTROL 查询详细信息]**&#x200B;面板提供用于管理所选查询的工具。

![图像](../images/queries/query-editor-overview/query-details.png)

此面板允许您直接从UI生成输出数据集，删除或命名显示的查询，并在&#x200B;**[!UICONTROL SQL查询]**&#x200B;选项卡上以易于复制的格式视图SQL代码。 此面板还显示有用的元数据，如上次修改查询的时间以及修改者（如果适用）。 要生成数据集，请单击&#x200B;**[!UICONTROL 输出数据集]**。 将显示&#x200B;**[!UICONTROL 输出数据集]**&#x200B;对话框。 输入名称和说明，然后单击&#x200B;**[!UICONTROL 运行查询]**。 新数据集显示在[!DNL Platform]的[!DNL Query Service]用户界面的&#x200B;**[!UICONTROL 数据集]**&#x200B;选项卡中。

### 保存查询

[!DNL Query Editor] 提供保存功能，允许您保存查询并稍后处理。要保存查询，请单击[!DNL Query Editor]右上角的&#x200B;**[!UICONTROL 保存]**。 在保存查询之前，必须使用&#x200B;**[!UICONTROL 查询详细信息]**&#x200B;面板为查询提供名称。

### 如何查找以前的查询

从[!DNL Query Editor]执行的所有查询都捕获在日志表中。 您可以使用&#x200B;**[!UICONTROL 日志]**&#x200B;选项卡中的搜索功能来查找查询执行。 保存的查询列在&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡中。

有关详细信息，请参阅[查询服务UI概述][query-service-ui]。

>[!NOTE]
>
>未执行的查询不会由日志保存。 要使查询在[!DNL Query Service]中可用，它必须在[!DNL Query Editor]中运行或保存。

## 使用查询编辑器执行查询

要在[!DNL Query Editor]中运行查询，您可以在编辑器中输入SQL，或从&#x200B;**[!UICONTROL 日志]**&#x200B;或&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡加载以前的查询，然后单击&#x200B;**播放**。 查询执行状态显示在下面的&#x200B;**[!UICONTROL 控制台]**&#x200B;选项卡中，输出数据显示在&#x200B;**[!UICONTROL 结果]**&#x200B;选项卡中。

### 控制台

控制台提供有关[!DNL Query Service]的状态和操作的信息。 控制台将显示连接状态至[!DNL Query Service]、正在执行的查询操作以及这些查询产生的任何错误消息。

![图像](../images/queries/query-editor-overview/console.png)

>[!NOTE]
>
>该控制台仅显示因执行查询而导致的错误。 在执行查询之前，它不显示查询验证错误。

### 查询结果

完成查询后，结果显示在&#x200B;**[!UICONTROL 控制台]**&#x200B;选项卡旁的&#x200B;**[!UICONTROL 结果]**&#x200B;选项卡中。 此视图显示查询的表格输出，最多显示100行。 此视图允许您验证查询是否生成预期输出。 要使用查询生成数据集，请删除对返回行的限制，然后使用`CREATE TABLE tablename AS SELECT`运行查询以生成带有输出的数据集。 有关如何从[!DNL Query Editor]中的查询结果生成数据集的说明，请参见[生成数据集教程][query-service-create-datasets]。

![图像](../images/queries/query-editor-overview/query-results.png)

## 运行带有[!DNL Query Service]教程视频的查询

以下视频演示如何在Adobe Experience Platform接口和PSQL客户端中运行查询。 此外，还演示了在XDM对象中使用单个属性、使用Adobe定义函数以及使用CREATE TABLE AS SELECT(CTAS)。

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## 后续步骤

现在您已经知道[!DNL Query Editor]中提供哪些功能以及如何导航应用程序，您可以直接在[!DNL Platform]中开始创作您自己的查询。 有关针对[!DNL Data Lake]中的数据集运行SQL查询的详细信息，请参见[运行查询][query-service-running-queries]上的指南。

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../best-practices/writing-queries.md
[query-service-create-datasets]: ./create-datasets.md
