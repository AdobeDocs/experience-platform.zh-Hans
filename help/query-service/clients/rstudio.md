---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；RStudio;rstudio；与查询服务；
solution: Experience Platform
title: 将RStudio连接到查询服务
topic: connect
description: 此文档将逐步介绍将R Studio与Adobe Experience Platform 查询 Service连接的步骤。
translation-type: tm+mt
source-git-commit: f1b2fd7efd43f317a85c831cd64c09be29688f7a
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# 将[!DNL RStudio]连接到查询服务

此文档将逐步介绍将[!DNL RStudio]与Adobe Experience Platform [!DNL Query Service]连接的步骤。

>[!NOTE]
>
> 本指南假定您已经具有访问[!DNL RStudio]的权限，并熟悉如何使用它。 有关[!DNL RStudio]的详细信息，请参阅[official [!DNL RStudio] 文档](https://rstudio.com/products/rstudio/)。
> 
> 此外，要将RStudio与查询服务一起使用，您需要安装PostgreSQL JDBC 4.2驱动程序。 您可以从[PostgreSQL官方站点](https://jdbc.postgresql.org/download.html)下载JDBC驱动程序。

## 在[!DNL RStudio]接口中创建[!DNL Query Service]连接

安装[!DNL RStudio]后，需要安装RJDBC包。 转到&#x200B;**[!DNL Packages]**&#x200B;窗格，然后选择&#x200B;**[!DNL Install]**。

![](../images/clients/rstudio/install-package.png)

出现一个弹出窗口，显示&#x200B;**[!DNL Install Packages]**&#x200B;屏幕。 确保为&#x200B;**[!DNL Install from]**&#x200B;部分选择了&#x200B;**[!DNL Repository (CRAN)]**。 **[!DNL Packages]**&#x200B;的值应为`RJDBC`。 确保已选择&#x200B;**[!DNL Install dependencies]**。 确认所有值均正确后，选择&#x200B;**[!DNL Install]**&#x200B;安装软件包。

![](../images/clients/rstudio/install-jrdbc.png)

现在已安装RJDBC包，请重新启动RStudio以完成安装过程。

RStudio重新启动后，您现在可以连接到查询服务。 在&#x200B;**[!DNL Packages]**&#x200B;窗格中选择&#x200B;**[!DNL RJDBC]**&#x200B;包，然后在控制台中输入以下命令：

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

其中{PATH TO THE POSTGRESQL JDBC JAR}表示计算机上安装的PostgreSQL JDBC JAR的路径。

现在，您可以通过在控制台中输入以下命令来创建与查询服务的连接：

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!NOTE]
>
>有关查找数据库名称、主机、端口和登录凭据的详细信息，请访问Platform](https://platform.adobe.com/query/configuration)上的[凭据页。 要查找您的凭据，请登录[!DNL Platform]，然后选择&#x200B;**[!UICONTROL 查询]**，然后选择&#x200B;**[!UICONTROL 凭据]**。

![](../images/clients/rstudio/connection-rjdbc.png)

## 编写查询

现在您已连接到[!DNL Query Service]，可以编写查询以执行和编辑SQL语句。 例如，可以使用`dbGetQuery(con, sql)`执行查询，其中`sql`是要运行的SQL查询。

以下查询使用包含[Experience事件](../best-practices/experience-event-queries.md)的数据集，并根据设备的屏幕高度创建网站页面视图的直方图。

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