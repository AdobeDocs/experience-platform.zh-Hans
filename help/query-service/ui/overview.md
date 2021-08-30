---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；查询编辑器；查询编辑器；查询编辑器；查询编辑器；
solution: Experience Platform
title: 查询服务UI指南
topic-legacy: guide
description: Adobe Experience Platform查询服务提供了一个用户界面，可用于编写和执行查询、查看以前执行的查询，以及访问由IMS组织内的用户保存的查询。
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: 30c3ca4aa3e8f42140566c8fdf9fbc855ec72e1b
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 3%

---

# [!DNL Query Service] 指南

Adobe Experience Platform [!DNL Query Service]提供了一个用户界面，可用于编写和执行查询、查看以前执行的查询，以及访问IMS组织内用户保存的查询。 要在[Adobe Experience Platform](https://platform.adobe.com)中访问UI，请在左侧导航中选择&#x200B;**[!UICONTROL 查询]**。

## [!DNL Query Editor]

使用[!DNL Query Editor]，您无需使用外部客户端即可写入和执行查询。 选择&#x200B;**[!UICONTROL 创建查询]**&#x200B;以打开[!DNL Query Editor]并创建新查询。 您还可以通过从&#x200B;**[!UICONTROL Log]**&#x200B;或&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡中选择查询来访问[!DNL Query Editor]。 选择之前执行或保存的查询将打开[!DNL Query Editor]并显示所选查询的SQL。

![图像](../images/ui/overview/overview.png)

[!DNL Query Editor] 提供了编辑空间，您可以在其中开始键入查询。键入时，编辑器会自动完成表中的SQL保留字、表和字段名称。 完成查询编写后，选择&#x200B;**Play**&#x200B;按钮以运行查询。 编辑器下方的&#x200B;**[!UICONTROL Console]**&#x200B;选项卡显示[!DNL Query Service]当前正在执行的操作，指示查询何时返回。 控制台旁的&#x200B;**[!UICONTROL Result]**&#x200B;选项卡显示查询结果。 有关使用[!DNL Query Editor]的详细信息，请参阅[查询编辑器指南](./user-guide.md)。

![图像](../images/ui/overview/query-editor.png)

## 浏览

**[!UICONTROL Browse]**&#x200B;选项卡显示组织中用户保存的查询。 将这些查询视为查询项目非常有用，因为此处保存的查询可能仍在构建中。 在&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡上显示的查询如果之前由[!DNL Query Service]执行，则在&#x200B;**[!UICONTROL Log]**&#x200B;选项卡中也会显示为运行查询。

![图像](../images/ui/overview/browse.png)

| 栏目 | 描述 |
| --- | --- |
| 名称 | 用户创建的查询名称。 您可以在名称上选择以在[!DNL Query Editor]中打开查询。 您还可以使用搜索栏搜索查询的名称。 搜索区分大小写。 |
| SQL | SQL查询的前几个字符。 将鼠标悬停在代码上会显示完整查询。 |
| 修改者 | 修改查询的最后一个用户。 贵组织中任何有权访问[!DNL Query Service]的用户都可以修改查询。 |
| 上次修改时间 | 浏览器时区中查询的上次修改日期和时间。 |

## 日志

**[!UICONTROL Log]**&#x200B;选项卡提供了以前执行的查询列表。 默认情况下，日志会以逆时代顺序列出查询。

![图像](../images/ui/overview/log.png)

| 栏目 | 描述 |
| --- | --- |
| **[!UICONTROL 名称]** | 查询名称，由SQL查询的前几个字符组成。 选择该名称会打开[!DNL Query Editor]，用于编辑查询。 您可以使用搜索栏搜索查询的名称。 搜索区分大小写。 |
| **[!UICONTROL 创建者]** | 创建查询的人员的姓名。 |
| **[!UICONTROL 客户端]** | 用于查询的客户端。 |
| **[!UICONTROL 数据集]** | 查询使用的输入数据集。 选择要转到输入数据集详细信息屏幕的数据集。 |
| **[!UICONTROL 状态]** | 查询的当前状态。 |
| **[!UICONTROL 上次运行]** | 上次运行查询时。 您可以通过选择此列上的箭头，对列表进行升序或降序排序。 |
| **[!UICONTROL 运行时间]** | 运行查询所花费的时间。 |

## 凭据

**[!UICONTROL 凭据]**&#x200B;选项卡同时显示即将过期和未过期的凭据。 有关如何使用这些凭据与外部客户端连接的更多信息，请阅读[凭据指南](../clients/overview.md)。

![图像](../images/ui/overview/credentials.png)

## 后续步骤

现在，您已熟悉[!DNL Platform]上的[!DNL Query Service]用户界面，接下来可以访问[!DNL Query Editor]以开始创建您自己的查询项目，以与组织中的其他用户共享。 有关在[!DNL Query Editor]中创作和运行查询的更多信息，请参阅[查询编辑器用户指南](./user-guide.md)。