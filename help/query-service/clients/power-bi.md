---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；Power BI；power bi；连接到查询服务；
solution: Experience Platform
title: 将Power BI连接到查询服务
description: 本文档介绍了将Power BI与Adobe Experience Platform查询服务连接的步骤。
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 0%

---

# 将[!DNL Power BI]连接到查询服务

本文档介绍了将[!DNL Power BI]桌面与Adobe Experience Platform查询服务连接的步骤。

## 快速入门

本指南要求您已具有对[!DNL Power BI]桌面应用程序的访问权限，并且熟悉如何导航其界面。 要下载[!DNL Power BI]桌面或了解更多信息，请参阅[官方 [!DNL Power BI] 文档](https://docs.microsoft.com/en-us/power-bi/)。

>[!IMPORTANT]
>
> [!DNL Power BI]桌面应用程序仅&#x200B;**在Windows设备上可用**。

要获取将[!DNL Power BI]连接到Experience Platform所需的凭据，您必须有权访问Experience Platform UI中的查询工作区。 如果您当前无权访问查询工作区，请联系您的组织管理员。

## 将[!DNL Power BI]连接到查询服务 {#connect-power-bi}

要将[!DNL Power BI]连接到查询服务，请打开[!DNL Power BI]并在顶部菜单功能区中选择&#x200B;**[!DNL Get Data]**。 接下来，在搜索栏中输入“[!DNL PostgreSQL]”以缩小数据源列表。 从显示的结果中，依次选择&#x200B;**[!DNL PostgreSQL database]**&#x200B;和&#x200B;**[!DNL Connect]**。

出现[!DNL PostgreSQL]数据库对话框，请求服务器和数据库的值。 有关如何从Power Query Desktop[&#128279;](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-to-a-postgresql-database-from-power-query-desktop)中连接到PostgreSQL数据库的其他说明，请参阅官方的[!DNL PowerBI]文档。

这些必需的值获取自您的Adobe Experience Platform凭据。 若要查找凭据，请登录到Experience Platform UI，然后从左侧导航中选择&#x200B;**[!UICONTROL 查询]**，然后选择&#x200B;**[!UICONTROL 凭据]**。 有关查找数据库名称、主机、端口和登录凭据的详细信息，请阅读[凭据指南](../ui/credentials.md)。

>[!IMPORTANT]
>
>作为Power BI或Tableau用户，您可以通过查询服务凭据选项卡将Customer Journey Analytics连接到您的BI工具。 有关如何[将您的BI工具](../ui/credentials.md#connect-to-customer-journey-analytics)连接到Customer Journey Analytics的说明，请参阅凭据文档。

![突出显示了“凭据”选项卡和“过期凭据”的Experience Platform查询工作区。](../images/clients/power-bi/query-service-credentials-page.png)

在[!DNL PostgreSQL database]对话框的&#x200B;**[!DNL Server]**&#x200B;字段中，输入在查询服务[!UICONTROL 凭据]部分中找到的主机的值。 对于生产，请将端口`:80`添加到主机字符串的末尾。 例如：`made-up.platform-query.adobe.io:80`。

**[!DNL Database]**&#x200B;字段可以是“all”或数据集表名称。 例如：`prod:all`。

>[!IMPORTANT]
>
>第三方BI工具中的嵌套数据结构可以扁平化，以提高其可用性并减少检索、分析、转换和报告数据所需的工作量。 有关在连接到数据库时如何激活此设置的说明，请参阅有关[`FLATTEN`功能](../key-concepts/flatten-nested-data.md)的文档。

### 数据连接模式 {#data-connectivity-mode}

接下来，您可以选择您的&#x200B;**[!DNL Data Connectivity mode]**。 在[!DNL PostgreSQL database]对话框中，选择&#x200B;**[!DNL Import]**&#x200B;后跟&#x200B;**[!DNL OK]**&#x200B;以显示所有可用表的列表，或选择&#x200B;**[!DNL DirectQuery]**&#x200B;直接查询数据源，而不将数据直接导入或复制到[!DNL Power BI]。

若要了解有关&#x200B;**[!DNL Import]**&#x200B;模式的详细信息，请阅读有关[导入表](#import)的部分。 要了解有关&#x200B;**[!DNL DirectQuery]**&#x200B;模式的更多信息，请阅读有关[查询数据集而不导入数据](#direct-query)的部分。

确认数据库详细信息后，选择&#x200B;**[!DNL OK]**。

### 身份验证 {#authentication}

确认数据连接模式后，会出现提示询问您的用户名、密码和应用程序设置。 在此示例中，用户名是您的组织ID，密码是您的身份验证令牌。 两者都可以在“查询服务凭据”页面上找到。

填写这些详细信息，然后选择&#x200B;**[!DNL Connect]**&#x200B;以继续下一步。

## 导入表 {#import}

通过选择&#x200B;**[!DNL Import]** [!DNL Data Connectivity mode]，将导入完整数据集，这样您就可以按原样使用[!DNL Power BI]桌面应用程序中的选定表和列。

>[!IMPORTANT]
>
>要查看自初始导入以来发生的数据更改，您必须通过再次导入完整数据集刷新[!DNL Power BI]内的数据。

要导入表，请输入服务器和数据库详细信息[（如上所述）](#connect-power-bi)，并选择&#x200B;**[!DNL Import]** [!DNL Data Connectivity mode]，然后选择&#x200B;**[!DNL OK]**。 此时将显示[!DNL Navigator]对话框，其中显示所有可用表的列表。 选择要预览的表，然后选择&#x200B;**[!DNL Load]**&#x200B;以将该数据集导入Power BI。 该表现在已导入到[!DNL Power BI]中。

[有关连接到PowerBi桌面应用程序中的数据的一般信息](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-quickstart-connect-to-data#connect-to-data)可在官方文档中找到。

### 使用自定义SQL导入表

[!DNL Power BI]和其他第三方工具（如[!DNL Tableau]）当前不允许用户导入嵌套对象，如Experience Platform中的XDM对象。 为此，[!DNL Power BI]允许您使用自定义SQL访问这些嵌套字段并创建数据的平面化视图。 然后，[!DNL Power BI]将以前嵌套数据的此平面化视图作为普通表加载。

从[!DNL PostgreSQL database]对话框中，选择&#x200B;**[!DNL Advanced options]**&#x200B;以在&#x200B;**[!DNL SQL statement]**&#x200B;部分中输入自定义SQL查询。 此自定义查询应该用于将您的JSON名称 — 值对拼合为表格式。 官方文档还提供了有关如何使用高级选项[&#128279;](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-using-advanced-options)中的SQL语句连接PowerBI的信息。

输入自定义查询后，选择&#x200B;**[!DNL OK]**&#x200B;以继续连接数据库。 有关从工作流的此部分连接数据库的指导，请参阅上面的[身份验证](#authentication)部分。

身份验证完成后，平面化数据的预览将作为表显示在[!DNL Power BI]桌面仪表板中。 服务器和数据库名称列在对话框的顶部。 选择&#x200B;**[!DNL Load]**&#x200B;以完成导入过程。

可视化图表现在可从[!DNL Power BI]桌面应用程序编辑和导出。

## 在不导入数据的情况下查询数据集 {#direct-query}

**[!DNL DirectQuery]** [!DNL Data Connectivity mode]直接查询数据源，而不将数据导入或复制到[!DNL Power BI]桌面。 使用此连接模式，可以通过UI使用当前数据刷新所有可视化图表。 但是，生成或刷新可视化所需的时间将因基础数据源的性能而异。

有关[使用 [!DNL DirectQuery]](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-use-directquery)的详细信息，以及有关其[连接选项、用例和限制](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-directquery-about)的全面讨论，可在官方的[!DNL PowerBI]文档中找到。

若要使用此[!DNL Data Connectivity mode]，请选择&#x200B;**[!DNL DirectQuery]**&#x200B;切换，然后选择&#x200B;**[!DNL Advanced options]**&#x200B;以在&#x200B;**[!DNL SQL statement]**&#x200B;分区中输入自定义SQL查询。 确保已选择&#x200B;**[!DNL Include relationship columns]**。 完成查询后，请选择&#x200B;**[!DNL OK]**&#x200B;以继续。

此时会出现查询的预览。 选择&#x200B;**[!DNL Load]**&#x200B;以查看查询的结果。

## 后续步骤

通过阅读本文档，您现在应该了解如何连接到[!DNL Power BI]桌面应用程序以及可用的不同数据连接模式。 有关如何编写和运行查询的详细信息，请参阅查询执行的[指南](../best-practices/writing-queries.md)。
