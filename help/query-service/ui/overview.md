---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；查询编辑器；查询编辑器；查询编辑器；查询编辑器；
solution: Experience Platform
title: 查询服务UI指南
topic-legacy: guide
description: Adobe Experience Platform查询服务提供了一个用户界面，可用于编写和执行查询、查看以前执行的查询，以及访问由IMS组织内的用户保存的查询。
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: a085bac6b4ee825d534710ae91d6690fa076e873
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 2%

---

# [!DNL Query Service] UI指南

Adobe Experience Platform [!DNL Query Service] 提供了一个用户界面，可用于编写和执行查询、查看以前执行的查询，以及访问由IMS组织内的用户保存的查询。 要在 [Adobe Experience Platform](https://platform.adobe.com)，选择 **[!UICONTROL 查询]** 中。

## [!DNL Query Editor]

的 [!DNL Query Editor] 使您无需使用外部客户端即可编写和执行查询。 选择 **[!UICONTROL 创建查询]** 打开 [!DNL Query Editor] 并创建新查询。 您还可以访问 [!DNL Query Editor] 通过从 **[!UICONTROL 日志]** 或 **[!UICONTROL 模板]** 选项卡。 选择之前执行或保存的查询将打开 [!DNL Query Editor] 并显示所选查询的SQL。

![“查询”功能板中突出显示了“创建查询”。](../images/ui/overview/overview.png)

[!DNL Query Editor] 提供了编辑空间，您可以在其中开始键入查询。 键入时，编辑器会自动完成表中的SQL保留字、表和字段名称。 完成编写查询后，选择 **播放** 按钮以运行查询。 的 **[!UICONTROL 控制台]** 选项卡上，将显示 [!DNL Query Service] 当前正在执行，用于指示何时返回了查询。 的 **[!UICONTROL 结果]** 选项卡中，显示查询结果。 请参阅 [查询编辑器指南](./user-guide.md) 有关使用 [!DNL Query Editor].

![在 [!DNL Query Editor].](../images/ui/overview/query-editor.png)

## 模板 {#browse}

的 **[!UICONTROL 模板]** 选项卡中显示由组织中的用户保存的查询。 将这些查询视为查询项目非常有用，因为此处保存的查询可能仍在构建中。 查询在 **[!UICONTROL 模板]** 选项卡在 **[!UICONTROL 日志]** 选项卡 [!DNL Query Service].

![在“查询”功能板“模板”选项卡的视图中放大以显示多个保存的查询。](../images/ui/overview/templates.png)

| 栏目 | 描述 |
| --- | --- |
| **[!UICONTROL 名称]** | 名称字段是用户创建的查询名称或SQL查询的前几个字符。 任何通过具有查询编辑器的UI创建的查询，在开始时即会命名。 如果查询是通过API创建的，则查询的名称是用于创建查询的初始SQL的一个代码片段。 您可以选择查询名称，以在 [!DNL Query Editor]. 您还可以使用搜索栏搜索 [!UICONTROL 名称] 的次数。 搜索区分大小写。 |
| **[!UICONTROL SQL]** | SQL查询的前几个字符。 将鼠标悬停在代码上会显示完整查询。 |
| **[!UICONTROL 修改者]** | 修改查询的最后一个用户。 贵组织中有权访问 [!DNL Query Service] 可以修改查询。 |
| **[!UICONTROL 上次修改时间]** | 浏览器时区中查询的上次修改日期和时间。 |

## 日志

的 **[!UICONTROL 日志]** 选项卡提供了以前执行的查询列表。 默认情况下，日志会以逆时代顺序列出查询。

![在“查询”功能板“日志”选项卡的视图中放大，按时间顺序相反地显示查询列表。](../images/ui/overview/log.png)

| 栏目 | 描述 |
| --- | --- |
| **[!UICONTROL 名称]** | 查询名称，由SQL查询的前几个字符组成。 选择名称会打开 [!DNL Query Editor]，用于编辑查询。 您可以使用搜索栏搜索查询的名称。 搜索区分大小写。 |
| **[!UICONTROL 创建者]** | 创建查询的人员的姓名。 |
| **[!UICONTROL 客户端]** | 用于查询的客户端。 |
| **[!UICONTROL 数据集]** | 查询使用的输入数据集。 选择要转到输入数据集详细信息屏幕的数据集。 |
| **[!UICONTROL 状态]** | 查询的当前状态。 |
| **[!UICONTROL 上次运行]** | 上次运行查询时。 您可以通过选择此列上的箭头，对列表进行升序或降序排序。 |
| **[!UICONTROL 运行时间]** | 运行查询所花费的时间。 |

## 凭据

的 **[!UICONTROL 凭据]** 选项卡会同时显示过期和未过期的凭据。 有关如何使用这些凭据与外部客户端连接的更多信息，请阅读 [凭据指南](../clients/overview.md).

![突出显示了“凭据”选项卡的“查询”功能板。](../images/ui/overview/credentials.png)

## 后续步骤

现在你已经熟悉了 [!DNL Query Service] 用户界面开启 [!DNL Platform]，您可以访问 [!DNL Query Editor] 以开始创建您自己的查询项目，以与组织中的其他用户共享。 有关在中创作和运行查询的更多信息 [!DNL Query Editor]，请参阅 [[!DNL Query Editor] 用户指南](./user-guide.md).