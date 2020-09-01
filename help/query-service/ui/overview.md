---
keywords: Experience Platform;home;popular topics;query service;Query service;query;query editor;Query Editor;Query editor;
solution: Experience Platform
title: Adobe Experience Platform查询服务UI指南
topic: guide
description: Adobe Experience Platform查询服务提供一个用户界面，可用于编写和执行查询、视图先前执行的查询以及访问由IMS组织内的用户保存的查询。
translation-type: tm+mt
source-git-commit: d2f098cb9e4aaf5beaad02173a22a25a87a43756
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 2%

---


# [!DNL Query Service] 指南

Adobe Experience Platform [!DNL Query Service] 提供一个用户界面，可用于编写和执行查询、视图先前执行的查询以及访问由IMS组织内的用户保存的查询。 要在Adobe Experience Platform内访 [问UI][platform-ui]，请在 **[!UICONTROL 左侧导]** 航中选择“查询”。

## [!DNL Query Editor]

使 [!DNL Query Editor] 您无需使用外部客户端即可编写和执行查询。 单 **[!UICONTROL 击创建查询]** ，以打开 [!DNL Query Editor] 并创建新查询。 您还可以通过从“ [!DNL Query Editor] 日志”或“浏览”选 **[!UICONTROL 项卡中]** 选 **[!UICONTROL 择查询来访]** 问。 选择之前执行或保存的查询将打 [!DNL Query Editor] 开并显示所选查询的SQL。

![图像](../images/queries/ui-overview/overview.png)

[!DNL Query Editor] 提供编辑空间，您可以在此开始键入查询。 在键入时，编辑器会自动完成表中的SQL保留字、表和字段名称。 编写完查询后，单击“ **播放** ”按钮以运行查询。 编 **[!UICONTROL 辑器下]** 的“控制台”选项卡显示 [!DNL Query Service] 当前正在执行的操作，指示何时返回查询。 “结 **[!UICONTROL 果]** ”选项卡在控制台旁显示查询结果。 有关使用 [查询的详细信][query-editor] 息，请参阅编辑器指南 [!DNL Query Editor]。

![图像](../images/queries/ui-overview/query-editor.png)

## 浏览

“浏 **[!UICONTROL 览]** ”选项卡显示由单位中的用户保存的查询。 将这些视为查询项目是有用的，因为保存在这里的查询可能仍在建设中。 查询在“浏 **[!UICONTROL 览]** ”选项卡上显示，如果以前由执行，则在“ **[!UICONTROL 日志]** ”选项卡中也显示为运行查询 [!DNL Query Service]。

![图像](../images/queries/ui-overview/browse.png)

| 栏目 | 描述 |
| --- | --- |
| 名称 | 用户创建的查询名。 您可以单击该名称以在中打开查询 [!DNL Query Editor]。 您还可以使用搜索栏搜索查询的名称。 搜索区分大小写。 |
| SQL | SQL查询的前几个字符。 将指针悬停在代码上方会显示完整查询。 |
| 修改者 | 修改查询的最后一个用户。 您组织中有权访问的任何用户都 [!DNL Query Service] 可以修改查询。 |
| 上次修改时间 | 浏览器时区中查询的上次修改日期和时间。 |

## 日志

“日 **[!UICONTROL 志]** ”选项卡提供以前已执行的列表。 默认情况下，日志以逆序顺序列表查询。

![图像](../images/queries/ui-overview/log.png)

| 栏目 | 描述 |
| --- | --- |
| **[!UICONTROL 名称]** | 查询名称，由SQL查询的前几个字符组成。 单击该名称会打 [!DNL Query Editor]开查询，允许您编辑该名称。 您可以使用搜索栏搜索查询的名称。 搜索区分大小写。 |
| **[!UICONTROL 创建者]** | 创建查询的人的姓名。 |
| **[!UICONTROL 客户]** | 用于查询的客户端。 |
| **[!UICONTROL 数据集]** | 查询使用的输入数据集。 单击数据集可转到输入数据集详细信息屏幕。 |
| **[!UICONTROL 状态]** | 查询的当前状态。 |
| **[!UICONTROL 上次运行]** | 上次运行查询时。 单击此列上的箭头，可以按升序或降序对列表进行排序。 |
| **[!UICONTROL 运行时]** | 运行查询所花的时间。 |

## 凭据

“凭 **[!UICONTROL 据]** ”选项卡显示 [!DNL Postgres] 您的凭据。 单击任 **[!UICONTROL 意字段旁]** 的“复制”图标，将其内容存储在键盘缓冲区中。 有关如何使用这些凭据与外部客户端连接的更多信息，请阅读“与客 [户端连接”指南][connect-clients]。

![图像](../images/queries/ui-overview/credentials.png)

## 后续步骤

您熟悉上的用 [!DNL Query Service] 户界面 [!DNL Platform]后，可以访 [!DNL Query Editor] 问开始，创建自己的查询项目并与组织中的其他用户共享。 有关在中创作和运行查询的详 [!DNL Query Editor]细信息，请 [参阅查询编辑器用户指南][query-editor]。

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
