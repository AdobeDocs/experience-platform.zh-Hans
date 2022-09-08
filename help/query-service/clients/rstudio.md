---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；RStudio;rstudio；连接到查询服务；
solution: Experience Platform
title: 将RStudio连接到查询服务
topic-legacy: connect
description: 本文档将介绍将R Studio与Adobe Experience Platform查询服务连接的步骤。
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
source-git-commit: 9ab3d69553dee9fdb97472edfa3f812133ee1bb1
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# 连接 [!DNL RStudio] 查询服务

本文档将介绍连接的步骤 [!DNL RStudio] 与Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> 本指南假定您已拥有 [!DNL RStudio] 并熟悉如何使用它。 有关 [!DNL RStudio] 可在 [官方 [!DNL RStudio] 文档](https://rstudio.com/products/rstudio/).
> 
> 此外，要将RStudio与查询服务一起使用，您需要安装PostgreSQL JDBC 4.2驱动程序。 可以从下载JDBC驱动程序 [PostgreSQL官方站点](https://jdbc.postgresql.org/download/).

## 创建 [!DNL Query Service] 连接 [!DNL RStudio] 界面

安装后 [!DNL RStudio]，则需要安装RJDBC包。 转到 **[!DNL Packages]** 窗格，然后选择 **[!DNL Install]**.

![](../images/clients/rstudio/install-package.png)

此时会出现一个弹出窗口，其中显示了 **[!DNL Install Packages]** 屏幕。 确保 **[!DNL Repository (CRAN)]** 的 **[!DNL Install from]** 中。 的值 **[!DNL Packages]** 应该 `RJDBC`. 确保 **[!DNL Install dependencies]** 中。 确认所有值均正确后，选择 **[!DNL Install]** 来安装包。

![](../images/clients/rstudio/install-jrdbc.png)

现在，已安装RJDBC包，请重新启动RStudio以完成安装过程。

重新启动RStudio后，您现在可以连接到查询服务。 选择 **[!DNL RJDBC]** 包 **[!DNL Packages]** ，然后在控制台中输入以下命令：

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

其中{PATH TO THE POSTGRESQL JDBC JAR}表示安装在您计算机上的PostgreSQL JDBC JAR的路径。

现在，您可以通过在控制台中输入以下命令来创建与查询服务的连接：

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!IMPORTANT]
>
>请参阅 [[!DNL Query Service] SSL文档](./ssl-modes.md) 了解对与Adobe Experience Platform查询服务的第三方连接的SSL支持，以及如何使用 `verify-full` SSL模式。

有关查找数据库名称、主机、端口和登录凭据的详细信息，请阅读 [凭据指南](../ui/credentials.md). 要查找您的凭据，请登录到 [!DNL Platform]，然后选择 **[!UICONTROL 查询]**，后跟 **[!UICONTROL 凭据]**.

![](../images/clients/rstudio/connection-rjdbc.png)

## 编写查询

现在，您已连接到 [!DNL Query Service]，则可以编写查询以执行和编辑SQL语句。 例如，您可以使用 `dbGetQuery(con, sql)` 执行查询，其中 `sql` 是要运行的SQL查询。

以下查询使用包含 [体验事件](../sample-queries/experience-event.md) 并根据设备的屏幕高度创建网站页面查看次数的直方图。

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

成功的响应会返回查询的结果：

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

有关如何编写和运行查询的详细信息，请阅读 [运行查询](../best-practices/writing-queries.md).
