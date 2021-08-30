---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；RStudio;rstudio；连接到查询服务；
solution: Experience Platform
title: 将RStudio连接到查询服务
topic-legacy: connect
description: 本文档将介绍将R Studio与Adobe Experience Platform查询服务连接的步骤。
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
source-git-commit: 910a38ccb556ec427584d9b522e29f6877d1c987
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 将[!DNL RStudio]连接到查询服务

本文档将介绍将[!DNL RStudio]与Adobe Experience Platform [!DNL Query Service]连接的步骤。

>[!NOTE]
>
> 本指南假定您已经拥有[!DNL RStudio]的访问权限，并熟悉其使用方式。 有关[!DNL RStudio]的更多信息，请参阅[official [!DNL RStudio] 文档](https://rstudio.com/products/rstudio/)。
> 
> 此外，要将RStudio与查询服务一起使用，您需要安装PostgreSQL JDBC 4.2驱动程序。 可以从[PostgreSQL官方站点](https://jdbc.postgresql.org/download.html)下载JDBC驱动程序。

## 在[!DNL RStudio]接口中创建[!DNL Query Service]连接

安装[!DNL RStudio]后，需要安装RJDBC包。 转到&#x200B;**[!DNL Packages]**&#x200B;窗格，然后选择&#x200B;**[!DNL Install]**。

![](../images/clients/rstudio/install-package.png)

出现一个弹出窗口，显示&#x200B;**[!DNL Install Packages]**&#x200B;屏幕。 确保为&#x200B;**[!DNL Install from]**&#x200B;部分选择&#x200B;**[!DNL Repository (CRAN)]**。 **[!DNL Packages]**&#x200B;的值应为`RJDBC`。 确保已选择&#x200B;**[!DNL Install dependencies]**。 确认所有值均正确后，选择&#x200B;**[!DNL Install]**&#x200B;以安装软件包。

![](../images/clients/rstudio/install-jrdbc.png)

现在，已安装RJDBC包，请重新启动RStudio以完成安装过程。

重新启动RStudio后，您现在可以连接到查询服务。 在&#x200B;**[!DNL Packages]**&#x200B;窗格中选择&#x200B;**[!DNL RJDBC]**&#x200B;包，然后在控制台中输入以下命令：

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

其中{PATH TO THE POSTGRESQL JDBC JAR}表示安装在您计算机上的PostgreSQL JDBC JAR的路径。

现在，您可以通过在控制台中输入以下命令来创建与查询服务的连接：

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!NOTE]
>
>有关查找数据库名称、主机、端口和登录凭据的详细信息，请阅读[凭据指南](../ui/credentials.md)。 要查找凭据，请登录到[!DNL Platform]，然后选择&#x200B;**[!UICONTROL 查询]**，接着选择&#x200B;**[!UICONTROL 凭据]**。

![](../images/clients/rstudio/connection-rjdbc.png)

## 编写查询

现在，您已连接到[!DNL Query Service]，可以编写查询以执行和编辑SQL语句。 例如，您可以使用`dbGetQuery(con, sql)`执行查询，其中`sql`是要运行的SQL查询。

以下查询使用包含[体验事件](../best-practices/experience-event-queries.md)的数据集，并根据设备的屏幕高度创建网站页面查看次数直方图。

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

有关如何编写和运行查询的详细信息，请阅读[运行查询](../best-practices/writing-queries.md)的指南。
