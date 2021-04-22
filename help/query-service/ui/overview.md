---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；查询;查询编辑器；查询编辑器；查询编辑器；
solution: Experience Platform
title: 查询服务UI指南
topic-legacy: guide
description: Adobe Experience Platform 查询 Service提供一个用户界面，可用于写入和执行查询、视图以前执行的查询以及访问由IMS组织内的用户保存的查询。
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
translation-type: tm+mt
source-git-commit: d2f19cc97082f75e66cf38e54b5bdb89482930ed
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 2%

---

# [!DNL Query Service] 指南

Adobe Experience Platform [!DNL Query Service]提供了一个用户界面，可用于写入和执行查询、视图以前执行的查询以及访问由IMS组织内的用户保存的查询。 要访问[Adobe Experience Platform][platform-ui]中的UI，请在左侧导航中选择&#x200B;**[!UICONTROL Queries]**。

## [!DNL Query Editor]

使用[!DNL Query Editor]，您无需使用外部客户端即可编写和执行查询。 选择&#x200B;**[!UICONTROL Create Query]**&#x200B;以打开[!DNL Query Editor]并创建新查询。 您还可以通过从&#x200B;**[!UICONTROL Log]**&#x200B;或&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡中选择查询来访问[!DNL Query Editor]。 选择之前执行或保存的查询将打开[!DNL Query Editor]并显示所选查询的SQL。

![图像](../images/ui/overview/overview.png)

[!DNL Query Editor] 提供了编辑空间，您可以在其中开始键入查询。键入时，编辑器会自动在表内完成SQL保留字、表和字段名。 写入完查询后，选择&#x200B;**播放**&#x200B;按钮以运行查询。 编辑器下的&#x200B;**[!UICONTROL Console]**&#x200B;选项卡显示[!DNL Query Service]当前正在执行的操作，指示何时返回查询。 控制台旁的&#x200B;**[!UICONTROL Result]**&#x200B;选项卡显示查询结果。 有关使用[!DNL Query Editor]的详细信息，请参阅[查询编辑器指南][query-editor]。

![图像](../images/ui/overview/query-editor.png)

## 浏览

**[!UICONTROL Browse]**&#x200B;选项卡显示由单位中的用户保存的查询。 将这些项目视为查询项目是有用的，因为此处保存的查询可能仍在建设中。 **[!UICONTROL Browse]**&#x200B;选项卡上显示的查询如果以前已由[!DNL Query Service]执行，也会在&#x200B;**[!UICONTROL Log]**&#x200B;选项卡中显示为运行查询。

![图像](../images/ui/overview/browse.png)

| 栏目 | 描述 |
| --- | --- |
| 名称 | 由用户创建的查询名称。 可以在名称上选择以在[!DNL Query Editor]中打开查询。 您还可以使用搜索栏搜索查询的名称。 搜索区分大小写。 |
| SQL | SQL查询的前几个字符。 将指针悬停在代码上方会显示完整查询。 |
| 修改者 | 修改查询的最后一个用户。 您组织中有权访问[!DNL Query Service]的任何用户都可以修改查询。 |
| 上次修改时间 | 浏览器时区中查询的上次修改日期和时间。 |

## 日志

**[!UICONTROL Log]**&#x200B;选项卡提供先前已执行的查询的列表。 默认情况下，日志将列表反向编年表中的查询。

![图像](../images/ui/overview/log.png)

| 栏目 | 描述 |
| --- | --- |
| **[!UICONTROL Name]** | 查询名称，由SQL查询的前几个字符组成。 选择名称将打开[!DNL Query Editor]，允许您编辑查询。 您可以使用搜索栏搜索查询的名称。 搜索区分大小写。 |
| **[!UICONTROL Created By]** | 创建查询的人的姓名。 |
| **[!UICONTROL Client]** | 用于查询的客户端。 |
| **[!UICONTROL Dataset]** | 查询使用的输入数据集。 选择要转到输入数据集详细信息屏幕的数据集。 |
| **[!UICONTROL Status]** | 查询的当前状态。 |
| **[!UICONTROL Last Run]** | 上次运行查询时。 您可以通过选择此列上的箭头，按升序或降序对列表进行排序。 |
| **[!UICONTROL Run Time]** | 运行查询所花的时间。 |

## 凭据

**[!UICONTROL Credentials]**&#x200B;选项卡显示您的[!DNL Postgres]凭据。 选择任意字段旁边的&#x200B;**[!UICONTROL Copy]**&#x200B;图标，将其内容存储在键盘缓冲区中。 有关如何使用这些凭据与外部客户端连接的详细信息，请阅读[与客户端连接指南][connect-clients]。

![图像](../images/ui/overview/credentials.png)

## 后续步骤

现在，您已熟悉[!DNL Platform]上的[!DNL Query Service]用户界面，因此可以访问[!DNL Query Editor]以开始创建您自己的查询项目，以便与您组织中的其他用户共享。 有关在[!DNL Query Editor]中创作和运行查询的详细信息，请参阅[查询编辑器用户指南][query-editor]。

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
