---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；Power BI;power bi；连接到查询服务；
solution: Experience Platform
title: 将Power BI连接到查询服务
description: 本文档将介绍如何将Power BI与Adobe Experience Platform查询服务连接。
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 1af89160cbf5b689396921869fec6c30a5bcfff0
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 1%

---

# 连接 [!DNL Power BI] 查询服务

本文档介绍了连接的步骤 [!DNL Power BI] 具有Adobe Experience Platform查询服务的桌面。

## 快速入门

本指南要求您已拥有 [!DNL Power BI] 桌面应用程序，熟悉如何导航其界面。 下载 [!DNL Power BI] 桌面版或更多信息，请参阅 [官方 [!DNL Power BI] 文档](https://docs.microsoft.com/zh-cn/power-bi/).

>[!IMPORTANT]
>
> 的 [!DNL Power BI] 桌面应用程序 **仅** 在Windows设备上可用。

获取连接所需的凭据 [!DNL Power BI] 要Experience Platform，您必须有权访问平台UI中的“查询”工作区。 如果您当前无权访问查询工作区，请联系您的组织管理员。

安装后 [!DNL Power BI]，则需要安装 `Npgsql`，用于PostgreSQL的.NET驱动程序包。 有关Npgsql的更多信息，请参阅 [Npgsql文档](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>您必须下载v4.0.10或更低版本，因为较新版本会导致错误。

在“[!DNL Npgsql GAC Installation]“ ”（在自定义设置屏幕上），选择 **[!DNL Will be installed on local hard drive]**.

要确保Npgsql已正确安装，请先重新启动计算机，然后再继续执行后续步骤。

## 连接 [!DNL Power BI] 查询服务 {#connect-power-bi}

连接 [!DNL Power BI] 要查询服务，请打开 [!DNL Power BI] 选择 **[!DNL Get Data]** 中。 下一步，输入“[!DNL PostgreSQL]”来缩小数据源列表。 在显示的结果中，选择 **[!DNL PostgreSQL database]**，后跟 **[!DNL Connect]**.

的 [!DNL PostgreSQL] 出现“数据库”对话框，请求服务器和数据库的值。 关于如何操作的其他说明 [从Power Query Desktop连接到PostgreSQL数据库](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-to-a-postgresql-database-from-power-query-desktop) 可以在官员 [!DNL PowerBI] 文档。

这些必需值取自您的Adobe Experience Platform凭据。 要查找凭据，请登录到Platform UI并选择 **[!UICONTROL 查询]** 从左侧导航，然后是 **[!UICONTROL 凭据]**. 有关查找数据库名称、主机、端口和登录凭据的详细信息，请阅读 [凭据指南](../ui/credentials.md).

![Experience Platform查询工作区中突出显示了凭据选项卡和过期凭据。](../images/clients/power-bi/query-service-credentials-page.png)

在 **[!DNL Server]** 字段 [!DNL PostgreSQL database] 对话框中，输入在查询服务中找到的主机的值 [!UICONTROL 凭据] 中。 对于生产，请添加端口 `:80` 到主机字符串的结尾。 例如：`made-up.platform-query.adobe.io:80`。

的 **[!DNL Database]** 字段可以是“all”或数据集表名称。 例如：`prod:all`。

>[!IMPORTANT]
>
>可以对第三方BI工具中的嵌套数据结构进行扁平化处理，以提高其可用性，并减少检索、分析、转换和报告数据所需的工作量。 请参阅[`FLATTEN` 功能](../best-practices/flatten-nested-data.md) 有关在连接到数据库时如何激活此设置的说明。

### 数据连接模式 {#data-connectivity-mode}

接下来，您可以选择 **[!DNL Data Connectivity mode]**. 在 [!DNL PostgreSQL database] 对话框，选择 **[!DNL Import]** 后跟 **[!DNL OK]** 显示所有可用表的列表，或选择 **[!DNL DirectQuery]** 直接查询数据源，而无需将数据直接导入或复制到 [!DNL Power BI].

要进一步了解 **[!DNL Import]** 模式，请阅读 [导入表](#import). 详细了解 **[!DNL DirectQuery]** 模式，请阅读 [在不导入数据的情况下查询数据集](#direct-query).

选择 **[!DNL OK]** 确认数据库详细信息后。

### 身份验证 {#authentication}

确认数据连接模式后，会出现提示，要求输入您的用户名、密码和应用程序设置。 此例中的用户名是您的组织ID，密码是您的身份验证令牌。 在“查询服务”凭据页上可以找到这两个凭据。

填写这些详细信息，然后选择 **[!DNL Connect]** 继续下一步。

## 导入表 {#import}

通过选择 **[!DNL Import]** [!DNL Data Connectivity mode]，则会导入完整数据集，以便在 [!DNL Power BI] 桌面应用程序原样。

>[!IMPORTANT]
>
>要查看自首次导入以来发生的数据更改，您必须刷新 [!DNL Power BI] 重新导入完整数据集。

要导入表，请输入服务器和数据库详细信息 [如上所述](#connect-power-bi) ，然后选择 **[!DNL Import]** [!DNL Data Connectivity mode]，后跟 **[!DNL OK]**. 的 [!DNL Navigator] 对话框，显示所有可用表的列表。 选择要预览的表，然后 **[!DNL Load]** 将数据集导入Power BI。 表格现已导入 [!DNL Power BI].

[有关在PowerBi桌面中连接到数据的一般信息](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-quickstart-connect-to-data#connect-to-data) 应用程序可在官方文档中找到。

### 使用自定义SQL导入表

[!DNL Power BI] 和其他第三方工具，如 [!DNL Tableau] 当前不允许用户导入嵌套对象，如平台中的XDM对象。 为了解决这个问题， [!DNL Power BI] 允许您使用自定义SQL访问这些嵌套字段并创建数据的扁平化视图。 [!DNL Power BI] 然后，将先前嵌套数据的此扁平化视图作为普通表加载。

从 [!DNL PostgreSQL database] 对话框，选择 **[!DNL Advanced options]** 在 **[!DNL SQL statement]** 中。 此自定义查询应用于将JSON名称值对拼合为表格格式。 官方文档还提供了有关如何 [使用高级选项中的SQL语句连接PowerBI](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-using-advanced-options).

输入自定义查询后，选择 **[!DNL OK]** 继续连接数据库。 请参阅 [身份验证](#authentication) 以上章节，以了解有关从工作流的此部分连接数据库的指导。

验证完成后，将在 [!DNL Power BI] 桌面功能板作为表。 服务器和数据库名称列在对话框顶部。 选择 **[!DNL Load]** 完成导入过程。

可视化图表现在可以从 [!DNL Power BI] 桌面应用程序。

## 在不导入数据的情况下查询数据集 {#direct-query}

的 **[!DNL DirectQuery]** [!DNL Data Connectivity mode] 直接查询数据源，而无需将数据导入或复制到 [!DNL Power BI] 台式机。 使用此连接模式，您可以通过UI使用当前数据刷新所有可视化图表。 但是，生成或刷新可视化所需的时间将因基础数据源的性能而异。

有关 [使用 [!DNL DirectQuery]](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-use-directquery) 以及对 [连接选项、用例和限制](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-directquery-about) 可以在官员 [!DNL PowerBI] 文档。

要使用此 [!DNL Data Connectivity mode]，选择 **[!DNL DirectQuery]** 切换 **[!DNL Advanced options]** 在 **[!DNL SQL statement]** 中。 确保 **[!DNL Include relationship columns]** 中。 完成查询后，选择 **[!DNL OK]** 继续。

此时将显示查询预览。 选择 **[!DNL Load]** 以查看查询结果。

## 后续步骤

通过阅读本文档，您现在应该了解如何连接到 [!DNL Power BI] 提供桌面应用程序和不同的数据连接模式。 有关如何编写和运行查询的详细信息，请参阅 [查询执行指南](../best-practices/writing-queries.md).
