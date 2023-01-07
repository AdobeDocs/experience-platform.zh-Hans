---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；Power BI;power bi；连接到查询服务；
solution: Experience Platform
title: 将Power BI连接到查询服务
description: 本文档将介绍如何将Power BI与Adobe Experience Platform查询服务连接。
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 1%

---

# 连接 [!DNL Power BI] 查询服务

本文档介绍了连接的步骤 [!DNL Power BI] 具有Adobe Experience Platform查询服务的桌面。

## 快速入门

本指南要求您已拥有 [!DNL Power BI] 桌面应用程序，熟悉如何导航其界面。 下载 [!DNL Power BI] 桌面版或更多信息，请参阅 [官方 [!DNL Power BI] 文档](https://docs.microsoft.com/zh-cn/power-bi/).

>[!IMPORTANT]
>
> 的 [!DNL Power BI] 桌面应用程序 **仅** 在Windows设备上可用。

获取连接所需的凭据 [!DNL Power BI] 要Experience Platform，您必须有权访问平台UI中的“查询”工作区。 如果您当前无权访问“查询”工作区，请联系您的IMS组织管理员。

安装后 [!DNL Power BI]，则需要安装 `Npgsql`，用于PostgreSQL的.NET驱动程序包。 有关Npgsql的更多信息，请参阅 [Npgsql文档](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>您必须下载v4.0.10或更低版本，因为较新版本会导致错误。

在“[!DNL Npgsql GAC Installation]“ ”（在自定义设置屏幕上），选择 **[!DNL Will be installed on local hard drive]**.

要确保Npgsql已正确安装，请先重新启动计算机，然后再继续执行后续步骤。

## 连接 [!DNL Power BI] 查询服务 {#connect-power-bi}

连接 [!DNL Power BI] 要查询服务，请打开 [!DNL Power BI] 选择 **[!DNL Get Data]** 中。

![的 [!DNL Power BI] 功能板“主页”选项卡，其中突出显示数据。](../images/clients/power-bi/open-power-bi.png)

输入“[!DNL PostgreSQL]”来缩小数据源列表。 在显示的结果下，选择 **[!DNL PostgreSQL database]**，后跟 **[!DNL Connect]**.

![获取数据对话框 [!DNL PostgreSQL] 数据库和Connect高亮显示。](../images/clients/power-bi/get-data.png)

的 [!DNL PostgreSQL] 出现“数据库”对话框，请求服务器和数据库的值。 这些值取自您的Adobe Experience Platform凭据。 要查找凭据，请登录到Platform UI并选择 **[!UICONTROL 查询]** 从左侧导航，然后是 **[!UICONTROL 凭据]**. 有关查找数据库名称、主机、端口和登录凭据的详细信息，请阅读 [凭据指南](../ui/credentials.md).

![Experience Platform查询工作区中突出显示了凭据选项卡和过期凭据。](../images/clients/power-bi/query-service-credentials-page.png)

对于 **[!DNL Server]** 在“Power BI”字段中，输入“查询服务凭据”部分中找到的主机的值。 对于生产，请添加端口 `:80` 到主机字符串的结尾。 例如：`made-up.platform-query.adobe.io:80`。

的 **[!DNL Database]** 字段可以是“all”或数据集表名称。 例如：`prod:all`。

>[!IMPORTANT]
>
>可以对第三方BI工具中的嵌套数据结构进行扁平化处理，以提高其可用性，并减少检索、分析、转换和报告数据所需的工作量。 请参阅[`FLATTEN` 功能](../best-practices/flatten-nested-data.md) 有关在连接到数据库时如何激活此设置的说明。

![的 [!DNL Power BI] 功能板，其中突出显示了服务器和数据库输入字段。](../images/clients/power-bi/postgresql-database-dialog.png)

### 数据连接模式

接下来，您可以选择 **[!DNL Data Connectivity mode]**. 选择 **[!DNL Import]** 后跟 **[!DNL OK]** 显示所有可用表的列表，或选择 **[!DNL DirectQuery]** 直接查询数据源，而无需将数据直接导入或复制到 [!DNL Power BI].

详细了解 **[!DNL Import]** 模式，请阅读 [导入表](#import). 详细了解 **[!DNL DirectQuery]** 模式，请阅读 [在不导入数据的情况下查询数据集](#direct-query).

选择 **[!DNL OK]** 确认数据库详细信息后。

![的 [!DNL PostgreSQL] 数据库对话框，数据连接模式突出显示。](../images/clients/power-bi/connectivity-mode.png)

### 身份验证

出现提示，要求输入您的用户名、密码和应用程序设置。 此例中的用户名是您的组织ID，密码是您的身份验证令牌。 在“查询服务”凭据页上可以找到这两个凭据。

填写这些详细信息，然后选择 **[!DNL Connect]** 继续下一步。

![突出显示了“用户名”、“密码”和“应用程序设置”下拉菜单的数据库对话框。](../images/clients/power-bi/import-mode.png)

## 导入表 {#import}

通过选择 **[!DNL Import]** [!DNL Data Connectivity mode]，则会导入完整数据集，以便在 [!DNL Power BI] 桌面应用程序原样。

>[!IMPORTANT]
>
>要查看自首次导入以来发生的数据更改，您必须刷新 [!DNL Power BI] 重新导入完整数据集。

要导入表，请输入服务器和数据库详细信息 [如上所述](#connect-power-bi) ，然后选择 **[!DNL Import]** [!DNL Data Connectivity mode]，后跟 **[!DNL OK]**. 出现一个对话框，其中显示了所有可用表的列表。 选择要预览的表，然后 **[!DNL Load]** 将数据集导入Power BI。

![在“导航”(Navigator)对话框中，突出显示了表格和“加载”(Load)。](../images/clients/power-bi/preview-table.png)

表格现已导入 [!DNL Power BI].

![的 [!DNL Power BI] 功能板中突出显示了有关创建自定义可视化的说明。](../images/clients/power-bi/import-table.png)

### 使用自定义SQL导入表

[!DNL Power BI] 以及其他第三方工具（如Tableau）当前不允许用户导入嵌套对象，如平台中的XDM对象。 为了解决这个问题， [!DNL Power BI] 允许您使用自定义SQL访问这些嵌套字段并创建数据的扁平化视图。 [!DNL Power BI] 然后，将先前嵌套数据的此扁平化视图作为普通表加载。

从 [!DNL PostgreSQL] 数据库弹出窗口，选择 **[!DNL Advanced options]** 在 **[!DNL SQL statement]** 中。 此自定义查询应用于将JSON名称值对拼合为表格格式。

![的 [!DNL PostgreSQL] 数据库对话框中，数据连接模式高级选项突出显示。 利用这些语句可创建自定义SQL语句。](../images/clients/power-bi/custom-sql-statement.png)

输入自定义查询后，选择 **[!DNL OK]** 继续连接数据库。 请参阅 [身份验证](#authentication) 以上章节，以了解有关从工作流的此部分连接数据库的指导。

验证完成后，将在 [!DNL Power BI] 桌面功能板作为表。 服务器和数据库名称列在对话框顶部。 选择 **[!DNL Load]** 完成导入过程。

![在 [!DNL Power BI] 功能板。](../images/clients/power-bi/imported-table-preview.png)

可视化图表现在可以从 [!DNL Power BI] 桌面应用程序。

## 在不导入数据的情况下查询数据集 {#direct-query}

的 **[!DNL DirectQuery]** [!DNL Data Connectivity mode] 直接查询数据源，而无需将数据导入或复制到 [!DNL Power BI] 台式机。 使用此连接模式，您可以通过UI使用当前数据刷新所有可视化图表。 但是，生成或刷新可视化所需的时间将因基础数据源的性能而异。

要使用此 [!DNL Data Connectivity mode]，选择 **[!DNL DirectQuery]** 切换 **[!DNL Advanced options]** 在 **[!DNL SQL statement]** 中。 确保 **[!DNL Include relationship columns]** 中。 完成查询后，选择 **[!DNL OK]** 继续。

![的 [!DNL PostgreSQL] 数据库对话框，其中突出显示了使用数据连接模式所需的设置。](../images/clients/power-bi/direct-query-mode.png)

此时将显示查询预览。 选择 **[!DNL Load]** 以查看查询结果。

![示例查询中的表格化结果预览。](../images/clients/power-bi/preview-direct-query.png)

## 后续步骤

通过阅读本文档，您现在应该了解如何连接到 [!DNL Power BI] 提供桌面应用程序和不同的数据连接模式。 有关如何编写和运行查询的详细信息，请参阅 [查询执行指南](../best-practices/writing-queries.md).
