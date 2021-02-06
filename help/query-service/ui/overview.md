---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；查询;查询编辑器；查询编辑器；查询编辑器；
solution: Experience Platform
title: 查询服务UI指南
topic: guide
description: Adobe Experience Platform查询服务提供一个用户界面，可用于编写和执行查询、视图先前执行的查询以及访问由IMS组织内的用户保存的查询。
translation-type: tm+mt
source-git-commit: 97dc0b5fb44f5345fd89f3f56bd7861668da9a6e
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 2%

---


# [!DNL Query Service] 指南

Adobe Experience Platform[!DNL Query Service]提供一个用户界面，可用于写入和执行查询、视图先前执行的查询以及访问由IMS组织内的用户保存的查询。 要访问[Adobe Experience Platform][platform-ui]中的UI，请在左侧导航中选择&#x200B;**[!UICONTROL 查询]**。

## [!DNL Query Editor]

使用[!DNL Query Editor]，您无需使用外部客户端即可编写和执行查询。 单击&#x200B;**[!UICONTROL 创建查询]**&#x200B;以打开[!DNL Query Editor]并创建新查询。 您还可以从&#x200B;**[!UICONTROL 日志]**&#x200B;或&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡中选择查询来访问[!DNL Query Editor]。 选择之前执行或保存的查询将打开[!DNL Query Editor]并显示所选查询的SQL。

![图像](../images/queries/ui-overview/overview.png)

[!DNL Query Editor] 提供编辑空间，您可以在此开始键入查询。在键入时，编辑器会自动完成表中的SQL保留字、表和字段名称。 编写完查询后，单击&#x200B;**播放**&#x200B;按钮以运行查询。 编辑器下的&#x200B;**[!UICONTROL 控制台]**&#x200B;选项卡显示[!DNL Query Service]当前正在执行的操作，指示何时返回查询。 控制台旁的&#x200B;**[!UICONTROL Result]**&#x200B;选项卡显示查询结果。 有关使用[!DNL Query Editor]的详细信息，请参阅[查询编辑器指南][query-editor]。

![图像](../images/queries/ui-overview/query-editor.png)

## 浏览

**[!UICONTROL 浏览]**&#x200B;选项卡显示组织中用户保存的查询。 将这些视为查询项目是有用的，因为保存在这里的查询可能仍在建设中。 **[!UICONTROL 浏览]**&#x200B;选项卡上显示的查询在&#x200B;**[!UICONTROL 日志]**&#x200B;选项卡中也显示为运行查询（如果之前已由[!DNL Query Service]执行）。

![图像](../images/queries/ui-overview/browse.png)

| 栏目 | 描述 |
| --- | --- |
| 名称 | 用户创建的查询名。 单击名称可打开[!DNL Query Editor]中的查询。 您还可以使用搜索栏搜索查询的名称。 搜索区分大小写。 |
| SQL | SQL查询的前几个字符。 将指针悬停在代码上方会显示完整查询。 |
| 修改者 | 修改查询的最后一个用户。 您组织中有权访问[!DNL Query Service]的任何用户都可以修改查询。 |
| 上次修改时间 | 浏览器时区中查询的上次修改日期和时间。 |

## 日志

**[!UICONTROL 日志]**&#x200B;选项卡提供以前已执行的列表。 默认情况下，日志以逆序顺序列表查询。

![图像](../images/queries/ui-overview/log.png)

| 栏目 | 描述 |
| --- | --- |
| **[!UICONTROL 名称]** | 查询名称，由SQL查询的前几个字符组成。 单击该名称可打开[!DNL Query Editor]，以便编辑查询。 您可以使用搜索栏搜索查询的名称。 搜索区分大小写。 |
| **[!UICONTROL 创建者]** | 创建查询的人的姓名。 |
| **[!UICONTROL 客户]** | 用于查询的客户端。 |
| **[!UICONTROL 数据集]** | 查询使用的输入数据集。 单击数据集可转到输入数据集详细信息屏幕。 |
| **[!UICONTROL 状态]** | 查询的当前状态。 |
| **[!UICONTROL 上次运行]** | 上次运行查询时。 单击此列上的箭头，可以按升序或降序对列表进行排序。 |
| **[!UICONTROL 运行时]** | 运行查询所花的时间。 |

## 凭据

**[!UICONTROL 凭据]**&#x200B;选项卡显示您的[!DNL Postgres]凭据。 单击任意字段旁的&#x200B;**[!UICONTROL 复制]**&#x200B;图标，将其内容存储在键盘缓冲区中。 有关如何使用这些凭据连接到外部客户端的详细信息，请阅读[与客户端连接指南][connect-clients]。

![图像](../images/queries/ui-overview/credentials.png)

## 后续步骤

您熟悉[!DNL Platform]上的[!DNL Query Service]用户界面后，可以访问[!DNL Query Editor]以创建您自己的开始项目并与组织中的其他用户共享。 有关在[!DNL Query Editor]中创作和运行查询的详细信息，请参阅[查询编辑器用户指南][query-editor]。

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
