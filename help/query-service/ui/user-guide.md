---
keywords: Experience Platform；主页；热门主题；查询编辑器；查询编辑器；查询服务；查询服务；
solution: Experience Platform
title: 查询编辑器UI指南
topic-legacy: query editor
description: 查询编辑器是Adobe Experience Platform查询服务提供的一个交互式工具，允许您在Experience Platform用户界面中编写、验证和运行客户体验数据查询。 查询编辑器支持开发用于分析和数据探索的查询，并且允许您运行交互式查询以用于开发目的，以及非交互式查询以填充Experience Platform中的数据集。
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: 483bcea231ed5f25c76771d0acba7e0c62dfed16
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 1%

---

# [!DNL Query Editor] UI指南

[!DNL Query Editor] 是Adobe Experience Platform提供的一款交互式工 [!DNL Query Service]具，允许您在用户界面中编写、验证和运行客户体验数 [!DNL Experience Platform] 据查询。[!DNL Query Editor] 支持开发用于分析和数据探索的查询，并允许您为开发目的运行交互式查询，以及用于填充中数据集的非交互式查询 [!DNL Experience Platform]。

有关[!DNL Query Service]的概念和功能的更多信息，请参阅[查询服务概述](../home.md)。 要详细了解如何导航[!DNL Platform]上的查询服务用户界面，请参阅[查询服务UI概述](./overview.md)。

## 快速入门

[!DNL Query Editor] 通过连接提供查询的灵活执行， [!DNL Query Service]并且仅在此连接处于活动状态时才运行查询。

### 连接到[!DNL Query Service]

[!DNL Query Editor] 初始化并连接到（打开时） [!DNL Query Service] 需要几秒钟的时间。控制台会告知您何时连接该设备，如下所示。 如果在编辑器连接之前尝试运行查询，则会延迟执行，直到连接完成为止。

![图像](../images/ui/query-editor/connect.png)

### 如何从[!DNL Query Editor]运行查询

从[!DNL Query Editor]执行的查询以交互方式运行。 这意味着，如果您关闭浏览器或导航离开，则查询将被取消。 对于通过查询输出生成数据集而进行的查询，也是如此。

## 使用[!DNL Query Editor]进行查询创作

使用[!DNL Query Editor]，您可以编写、执行和保存客户体验数据的查询。 在[!DNL Query Editor]中执行或保存的所有查询都可供贵组织中具有[!DNL Query Service]访问权限的所有用户使用。

### 访问 [!DNL Query Editor]

在[!DNL Experience Platform] UI的左侧导航菜单中，选择&#x200B;**[!UICONTROL 查询]**&#x200B;以打开[!DNL Query Service]工作区。 接下来，选择屏幕右上方的&#x200B;**[!UICONTROL 创建查询]**&#x200B;以开始编写查询。 此链接可从[!DNL Query Service]工作区中的任意页面访问。

![图像](../images/ui/query-editor/create-query.png)

### 编写查询

[!UICONTROL 查询编] 辑器的组织方式，可尽可能轻松地编写查询。以下屏幕截图显示了编辑器在UI中的显示方式，其中&#x200B;**Play**&#x200B;按钮和SQL条目字段突出显示。

![图像](../images/ui/query-editor/editor.png)

为了最大程度地缩短开发时间，建议您开发查询，并对返回的行进行限制。 例如：`SELECT fields FROM table WHERE conditions LIMIT number_of_rows`。验证查询是否生成了预期的输出后，请删除限制并运行查询`CREATE TABLE tablename AS SELECT`以生成包含该输出的数据集。

### 在[!DNL Query Editor]中写入工具

- **自动语法突出显示：** 使读取和组织SQL变得更轻松。

![图像](../images/ui/query-editor/syntax-highlight.png)

- **SQL关键字自动完成：** 开始键入查询，然后使用箭头键导航到所需的术语并按 **Enter**。

![图像](../images/ui/query-editor/syntax-auto.png)

- **表和字段自动完成：** 开始键入要从中输入的表 `SELECT` 名称，然后使用箭头键导航到要查找的表，然后按 **Enter**。选择表后，自动完成将识别该表中的字段。

![图像](../images/ui/query-editor/tables-auto.png)

### 错误检测

[!DNL Query Editor] 在您编写查询时自动验证查询，提供通用SQL验证和特定执行验证。如果查询的下方显示红色下划线（如下图所示），则表示查询中存在错误。

![图像](../images/ui/query-editor/syntax-error-highlight.png)

当检测到错误时，您可以通过将鼠标悬停在SQL代码上来查看特定的错误消息。

![图像](../images/ui/query-editor/linting-error.png)

### 查询详细信息

在[!DNL Query Editor]中查看查询时，**[!UICONTROL 查询详细信息]**&#x200B;面板提供了用于管理所选查询的工具。

![图像](../images/ui/query-editor/query-details.png)

此面板允许您直接从UI中生成输出数据集、删除或命名显示的查询，并在&#x200B;**[!UICONTROL SQL查询]**&#x200B;选项卡上以易于复制的格式查看SQL代码。 此面板还显示有用的元数据，例如上次修改查询的时间以及修改查询的人员（如果适用）。 要生成数据集，请选择&#x200B;**[!UICONTROL 输出数据集]**。 出现&#x200B;**[!UICONTROL 输出数据集]**&#x200B;对话框。 输入名称和描述，然后选择&#x200B;**[!UICONTROL 运行查询]**。 新数据集显示在[!DNL Platform]用户界面的[!DNL Query Service]Datasets ]**选项卡中。**[!UICONTROL 

### 保存查询

[!DNL Query Editor] 提供了保存函数，用于保存查询并稍后对其进行处理。要保存查询，请选择[!DNL Query Editor]右上角的&#x200B;**[!UICONTROL Save]**。 在保存查询之前，必须使用&#x200B;**[!UICONTROL 查询详细信息]**&#x200B;面板为查询提供名称。

### 如何查找以前的查询

从[!DNL Query Editor]执行的所有查询都捕获在日志表中。 您可以使用&#x200B;**[!UICONTROL Log]**&#x200B;选项卡中的搜索功能来查找查询执行。 保存的查询列在&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡中。

有关更多信息，请参阅[查询服务UI概述](./overview.md) 。

>[!NOTE]
>
>日志不会保存未执行的查询。 要使查询在[!DNL Query Service]中可用，必须在[!DNL Query Editor]中运行或保存该查询。

## 使用查询编辑器执行查询

要在[!DNL Query Editor]中运行查询，可以在编辑器中输入SQL，或从&#x200B;**[!UICONTROL Log]**&#x200B;或&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡加载上一个查询，然后选择&#x200B;**Play**。 查询执行状态显示在下面的&#x200B;**[!UICONTROL Console]**&#x200B;选项卡中，输出数据显示在&#x200B;**[!UICONTROL Results]**&#x200B;选项卡中。

### 控制台

控制台提供有关[!DNL Query Service]的状态和操作的信息。 控制台将显示[!DNL Query Service]的连接状态、正在执行的查询操作以及这些查询产生的任何错误消息。

![图像](../images/ui/query-editor/console.png)

>[!NOTE]
>
>控制台仅显示执行查询所导致的错误。 在执行查询之前，不会显示查询验证错误。

### 查询结果

查询完成后，结果显示在&#x200B;**[!UICONTROL Console]**&#x200B;选项卡旁边的&#x200B;**[!UICONTROL Results]**&#x200B;选项卡中。 此视图以表格形式显示查询的输出，最多显示100行。 利用此视图，可验证查询是否生成预期的输出。 要使用您的查询生成数据集，请删除对返回行的限制，然后运行查询`CREATE TABLE tablename AS SELECT`以生成带有输出的数据集。 有关如何从[!DNL Query Editor]中的查询结果生成数据集的说明，请参阅[生成数据集教程](./create-datasets.md)。

![图像](../images/ui/query-editor/query-results.png)

## 使用[!DNL Query Service]教程视频运行查询

以下视频演示如何在Adobe Experience Platform界面和PSQL客户端中运行查询。 此外，还演示了如何在XDM对象中使用单个属性、使用Adobe定义的函数以及使用CREATE TABLE AS SELECT(CTAS)。

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## 后续步骤

现在，您已知道[!DNL Query Editor]中提供了哪些功能以及如何导航应用程序，接下来可以直接在[!DNL Platform]中开始创作您自己的查询。 有关针对[!DNL Data Lake]中的数据集运行SQL查询的详细信息，请参阅[运行查询](../best-practices/writing-queries.md)的指南。
