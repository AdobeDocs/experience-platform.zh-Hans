---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；RStudio；rstudio；连接到查询服务；
solution: Experience Platform
title: 将RStudio连接到查询服务
description: 本文档介绍了将R Studio与Adobe Experience Platform查询服务连接的步骤。
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# 将[!DNL RStudio]连接到查询服务

本文档逐步介绍将[!DNL RStudio]与Adobe Experience Platform [!DNL Query Service]连接的步骤。

>[!NOTE]
>
> [!DNL RStudio]现已更名为[!DNL Posit]。 [!DNL RStudio]产品已重命名为[!DNL Posit Connect]、[!DNL Posit Workbench]、[!DNL Posit Package]经理、[!DNL Posit Cloud]和[!DNL Posit Academy]。
>
> 本指南假定您已经有权访问[!DNL RStudio]并熟悉其使用方法。 有关[!DNL RStudio]的详细信息，请参阅[官方 [!DNL RStudio] 文档](https://rstudio.com/products/rstudio/)。
> 
> 此外，要将[!DNL RStudio]与查询服务结合使用，您需要安装[!DNL PostgreSQL] JDBC 4.2驱动程序。 您可以从[[!DNL PostgreSQL] 官方网站](https://jdbc.postgresql.org/download/)下载JDBC驱动程序。

## 在[!DNL RStudio]界面中创建[!DNL Query Service]连接

安装[!DNL RStudio]后，您需要安装RJDBC包。 有关如何通过命令行[连接数据库](https://solutions.posit.co/connections/db/best-practices/drivers/#connecting-to-a-database-in-r)的说明，请参阅官方的Post文档。

如果使用Mac OS，您可以从菜单栏选择&#x200B;**[!UICONTROL 工具]**，然后从下拉菜单中选择&#x200B;**[!UICONTROL 安装包]**。 或者，从RStudio UI中选择&#x200B;**[!DNL Packages]**&#x200B;选项卡，然后选择&#x200B;**[!DNL Install]**。

此时会出现一个弹出窗口，显示&#x200B;**[!DNL Install Packages]**&#x200B;屏幕。 确保为&#x200B;**[!DNL Install from]**&#x200B;部分选择&#x200B;**[!DNL Repository (CRAN)]**。 **[!DNL Packages]**&#x200B;的值应为`RJDBC`。 确保已选择&#x200B;**[!DNL Install dependencies]**。 确认所有值均正确后，选择&#x200B;**[!DNL Install]**&#x200B;以安装包。 现在已安装RJDBC包，请重新启动[!DNL RStudio]以完成安装过程。

在[!DNL RStudio]重新启动后，您现在可以连接到查询服务。 在&#x200B;**[!DNL Packages]**&#x200B;窗格中选择&#x200B;**[!DNL RJDBC]**&#x200B;包，然后在控制台中输入以下命令：

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

其中`{PATH TO THE POSTGRESQL JDBC JAR}`表示计算机上安装的[!DNL PostgreSQL] JDBC JAR的路径。

现在，您可以创建与查询服务的连接。 在控制台中输入以下命令：

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!IMPORTANT]
>
>请参阅[[!DNL Query Service] SSL文档](./ssl-modes.md)，了解对Adobe Experience Platform查询服务的第三方连接的SSL支持，以及如何使用`verify-full` SSL模式连接。

有关查找数据库名称、主机、端口和登录凭据的详细信息，请阅读[凭据指南](../ui/credentials.md)。 若要查找凭据，请登录到[!DNL Experience Platform]，然后选择&#x200B;**[!UICONTROL 查询]**，然后选择&#x200B;**[!UICONTROL 凭据]**。

控制台输出中将显示一条消息，确认与查询服务的连接。

## 编写查询

现在您已连接到[!DNL Query Service]，您可以编写查询以执行并编辑SQL语句。 例如，您可以使用`dbGetQuery(con, sql)`执行查询，其中`sql`是要运行的SQL查询。

以下查询使用包含[体验事件](../../xdm/classes/experienceevent.md)的数据集，并根据设备的屏幕高度创建网站的页面查看直方图。

```sql
df_pageviews <- dbGetQuery(con,
"SELECT t.range AS buckets, 
 Count(*) AS pageviews 
FROM (SELECT CASE 
 WHEN device.screenheight BETWEEN 0 AND 99 THEN '0 - 99' 
 WHEN device.screenheight BETWEEN 100 AND 199 THEN '100-199' 
 WHEN device.screenheight BETWEEN 200 AND 299 THEN '200-299' 
 WHEN device.screenheight BETWEEN 300 AND 399 THEN '300-399' 
 WHEN device.screenheight BETWEEN 400 AND 499 THEN '400-499' 
 WHEN device.screenheight BETWEEN 500 AND 599 THEN '500-599' 
 ELSE '600-699' 
 end AS range 
 FROM aa_post_vals_3) t 
GROUP BY t.range 
ORDER BY buckets 
LIMIT 1000000")
```

成功的响应将返回查询的结果：

```r
df_pageviews
 buckets pageviews
1 0 - 99 198985
2 500-599 67138
3 300-399 2147
4 200-299 354
5 400-499 6947
6 100-199 4415
7 600-699 3097040
```

## 后续步骤

有关如何编写和运行查询的详细信息，请阅读有关[运行查询](../best-practices/writing-queries.md)的指南。
