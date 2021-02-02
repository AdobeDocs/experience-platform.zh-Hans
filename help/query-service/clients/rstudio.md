---
keywords: Experience Platform；主题；热门主题；查询服务；查询服务；RStudio;rstudio；与查询服务；
solution: Experience Platform
title: 与RStudio连接
topic: connect
description: 此文档通过步骤将R Studio与Adobe Experience Platform查询服务连接。
translation-type: tm+mt
source-git-commit: eac93f3465fa6ce4af7a6aa783cf5f8fb4ac9b9b
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 2%

---


# [!DNL RStudio]

此文档介绍将[!DNL RStudio]与Adobe Experience Platform[!DNL Query Service]连接的步骤。

>[!NOTE]
>
> 本指南假定您已经具有访问[!DNL RStudio]的权限，并且熟悉如何使用它。 有关[!DNL RStudio]的详细信息，请参阅[offical [!DNL RStudio] 文档](https://rstudio.com/products/rstudio/)。

## 将[!DNL RStudio]与[!DNL Query Service]连接

在出现的&#x200B;**[!DNL Console]**&#x200B;屏幕上安装[!DNL RStudio]后，您首先需要准备R脚本才能使用[!DNL PostgreSQL]。

```r
install.packages("RPostgreSQL")
install.packages("rstudioapi")
require("RPostgreSQL")
require("rstudioapi")
```

在您准备好使用[!DNL PostgreSQL]的R脚本后，现在可以通过加载[!DNL PostgreSQL]驱动程序将[!DNL RStudio]连接到[!DNL Query Service]。

```r
drv <- dbDriver("PostgreSQL")
con <- dbConnect(drv, 
 dbname = "{DATABASE_NAME}",
 host="{HOST_NUMBER}",
 port={PORT_NUMBER},
 user="{USERNAME}",
 password="{PASSWORD}")
```

| 属性 | 描述 |
| -------- | ----------- |
| `{DATABASE_NAME}` | 将使用的数据库的名称。 |
| `{HOST_NUMBER` 和 `{PORT_NUMBER}` | 主机端点及其查询服务端口。 |
| `{USERNAME}` 和 `{PASSWORD}` | 将使用的登录凭据。 用户名采用`ORG_ID@AdobeOrg`的形式。 |

>[!NOTE]
>
>有关查找数据库名称、主机、端口和登录凭据的详细信息，请访问Platform](https://platform.adobe.com/query/configuration)上的[凭据页。 要查找您的凭据，请登录[!DNL Platform]，然后选择&#x200B;**[!UICONTROL 查询]**，后跟&#x200B;**[!UICONTROL 凭据]**。

## 编写查询

现在您已连接到[!DNL Query Service]，您可以编写查询以执行和编辑SQL语句。 例如，可以使用`dbGetQuery(con, sql)`执行查询，其中`sql`是要运行的SQL查询。

以下查询使用包含[体验事件](../best-practices/experience-event-queries.md)的数据集，并根据设备的屏幕高度创建网站页面视图的直方图。

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