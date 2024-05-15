---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；Power BI；power bi；连接到查询服务；
solution: Experience Platform
title: 将Power BI连接到查询服务
description: 本文档介绍了将Power BI连接到Adobe Experience Platform查询服务的步骤。
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 26f0725f0f239707bd719ed46929648f8d557155
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 0%

---

# 连接 [!DNL Power BI] 查询服务

本文档介绍了连接的步骤 [!DNL Power BI] 带有Adobe Experience Platform查询服务的桌面。

## 快速入门

本指南要求您已经有权访问 [!DNL Power BI] 并熟悉如何导航其界面。 下载 [!DNL Power BI] 桌面版或有关详细信息，请参见 [官方 [!DNL Power BI] 文档](https://docs.microsoft.com/en-us/power-bi/).

>[!IMPORTANT]
>
> 此 [!DNL Power BI] 桌面应用程序是 **仅限** 在Windows设备上可用。

获取进行连接所需的凭据 [!DNL Power BI] 要Experience Platform，您必须有权访问Platform UI中的查询工作区。 如果您当前无权访问查询工作区，请联系您的组织管理员。

安装后 [!DNL Power BI]，您需要安装 `Npgsql`，用于PostgreSQL的.NET驱动程序包。 有关Npgsql的详细信息，请参见 [Npgsql文档](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>您必须下载v4.0.10或更低版本，因为较新版本会导致错误。

在&quot;[!DNL Npgsql GAC Installation]”在自定义设置屏幕上，选择 **[!DNL Will be installed on local hard drive]**.

要确保已正确安装Npgsql，请重新启动计算机，然后再继续后续步骤。

## 连接 [!DNL Power BI] 查询服务 {#connect-power-bi}

连接 [!DNL Power BI] 要查询服务，请打开 [!DNL Power BI] 并选择 **[!DNL Get Data]** 在顶部菜单功能区中。 接下来，输入&#39;&#39;[!DNL PostgreSQL]”来缩小数据源列表。 从显示的结果中，选择 **[!DNL PostgreSQL database]**，后接 **[!DNL Connect]**.

此 [!DNL PostgreSQL] 此时将显示“数据库”对话框，请求服务器和数据库的值。 有关如何执行操作的附加说明 [从Power Query桌面连接到PostgreSQL数据库](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-to-a-postgresql-database-from-power-query-desktop) 详情请见官方网站 [!DNL PowerBI] 文档。

这些必需的值获取自您的Adobe Experience Platform凭据。 要查找凭据，请登录Platform UI并选择 **[!UICONTROL 查询]** 从左侧导航中，后面是 **[!UICONTROL 凭据]**. 有关查找数据库名称、主机、端口和登录凭据的详细信息，请阅读 [凭据指南](../ui/credentials.md).

>[!IMPORTANT]
>
>作为Power BI或Tableau用户，您可以从“查询服务凭据”选项卡将Customer Journey Analytics连接到BI工具。 有关如何执行操作的说明，请参阅凭据文档 [将您的BI工具连接到Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics).

![突出显示了“凭据”选项卡和“过期凭据”的“Experience Platform查询”工作区。](../images/clients/power-bi/query-service-credentials-page.png)

在 **[!DNL Server]** 字段 [!DNL PostgreSQL database] 对话框，输入在查询服务中找到的主机的值 [!UICONTROL 凭据] 部分。 对于生产，请添加端口 `:80` 到主机字符串的结尾。 例如：`made-up.platform-query.adobe.io:80`。

此 **[!DNL Database]** 字段可以是“all”或数据集表名称。 例如：`prod:all`。

>[!IMPORTANT]
>
>第三方BI工具中的嵌套数据结构可以扁平化，以提高其可用性并减少检索、分析、转换和报告数据所需的工作量。 请参阅有关以下内容的文档[`FLATTEN` 特征](../key-concepts/flatten-nested-data.md) 以获取有关在连接到数据库时如何激活此设置的说明。

### 数据连接模式 {#data-connectivity-mode}

接下来，您可以选择您的 **[!DNL Data Connectivity mode]**. 在 [!DNL PostgreSQL database] 对话框，选择 **[!DNL Import]** 后接 **[!DNL OK]** 显示所有可用表的列表，或选择 **[!DNL DirectQuery]** 直接查询数据源，而无需将数据直接导入或复制到中 [!DNL Power BI].

要了解有关 **[!DNL Import]** 模式，请阅读以下部分： [导入表](#import). 要了解有关 **[!DNL DirectQuery]** 模式，请阅读以下部分： [查询数据集而不导入数据](#direct-query).

选择 **[!DNL OK]** 确认数据库详细信息后。

### 身份验证 {#authentication}

确认数据连接模式后，会出现提示询问您的用户名、密码和应用程序设置。 在此示例中，用户名是您的组织ID，密码是您的身份验证令牌。 两者都可以在“查询服务凭据”页面上找到。

填写这些详细信息，然后选择 **[!DNL Connect]** 以继续执行下一步。

## 导入表 {#import}

通过选择 **[!DNL Import]** [!DNL Data Connectivity mode]，则会导入完整数据集，这样您就可以在中使用所选表和列 [!DNL Power BI] 桌面应用程序的现状。

>[!IMPORTANT]
>
>要查看自初始导入以来发生的数据更改，您必须刷新以下范围内的数据： [!DNL Power BI] 以再次导入完整数据集。

要导入表，请输入服务器和数据库的详细信息 [如上所述](#connect-power-bi) 并选择 **[!DNL Import]** [!DNL Data Connectivity mode]，后接 **[!DNL OK]**. 此 [!DNL Navigator] 对话框出现，其中显示所有可用表的列表。 选择要预览的表，然后 **[!DNL Load]** 将数据集导入Power BI。 该表现在导入到 [!DNL Power BI].

[有关连接到PowerBi桌面设备中的数据的一般信息](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-quickstart-connect-to-data#connect-to-data) 应用程序可在官方文档中找到。

### 使用自定义SQL导入表

[!DNL Power BI] 和其他第三方工具，例如 [!DNL Tableau] 当前不允许用户导入嵌套对象，如Platform中的XDM对象。 为了说明这一点， [!DNL Power BI] 允许您使用自定义SQL访问这些嵌套字段并创建数据的平面化视图。 [!DNL Power BI] 然后将以前嵌套数据的此平面化视图作为普通表加载。

从 [!DNL PostgreSQL database] 对话框，选择 **[!DNL Advanced options]** 要在以下位置输入自定义SQL查询 **[!DNL SQL statement]** 部分。 此自定义查询应该用于将您的JSON名称 — 值对拼合为表格式。 官方文档还提供了有关如何执行此操作的信息： [使用高级选项中的SQL语句连接PowerBI](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-using-advanced-options).

输入自定义查询后，选择 **[!DNL OK]** 以继续连接数据库。 请参阅 [身份验证](#authentication) 部分，以获取有关从工作流的此部分连接数据库的指导。

身份验证完成后，拼合数据的预览将显示在 [!DNL Power BI] 将桌面仪表板作为表格。 服务器和数据库名称列在对话框的顶部。 选择 **[!DNL Load]** 以完成导入过程。

现在，可以从编辑和导出可视化图表 [!DNL Power BI] 桌面应用程序。

## 在不导入数据的情况下查询数据集 {#direct-query}

此 **[!DNL DirectQuery]** [!DNL Data Connectivity mode] 直接查询数据源，而无需将数据导入或复制到中 [!DNL Power BI] 桌面。 使用此连接模式，可以通过UI使用当前数据刷新所有可视化图表。 但是，生成或刷新可视化所需的时间将因基础数据源的性能而异。

有关的更多信息 [使用 [!DNL DirectQuery]](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-use-directquery) 以及全面讨论其 [连接选项、使用案例和限制](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-directquery-about) 详情请见官方网站 [!DNL PowerBI] 文档。

使用此 [!DNL Data Connectivity mode]，选择 **[!DNL DirectQuery]** 切换然后 **[!DNL Advanced options]** 要在以下位置输入自定义SQL查询 **[!DNL SQL statement]** 部分。 确保 **[!DNL Include relationship columns]** 已选中。 完成查询后，选择 **[!DNL OK]** 以继续。

此时会出现查询的预览。 选择 **[!DNL Load]** 以查看查询的结果。

## 后续步骤

通过阅读本文档，您现在应该了解如何连接到 [!DNL Power BI] 桌面应用程序和不同的数据连接模式可用。 有关如何编写和运行查询的详细信息，请参阅 [查询执行指南](../best-practices/writing-queries.md).
