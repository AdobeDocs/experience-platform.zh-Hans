---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 与RStudio连接
topic: connect
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 2%

---


# 连接 [!DNL RStudio]

此文档逐步介绍将R Studio与Adobe Experience Platform连接的步骤 [!DNL Query Service]。

安装 [!DNL RStudio]后，在显 *示的* “控制台”屏幕上，您首先需要准备要使用的R脚本 [!DNL PostgreSQL]。

```r
install.packages("RPostgreSQL")
install.packages("rstudioapi")
require("RPostgreSQL")
require("rstudioapi")
```

准备好R脚本使用后， [!DNL PostgreSQL]现在可以通过加 [!DNL RStudio] 载驱 [!DNL Query Service] 动程序连接到 [!DNL PostgreSQL] 。

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
| `{USERNAME}` 和 `{PASSWORD}` | 将使用的登录凭据。 用户名采用的形式 `ORG_ID@AdobeOrg`。 |

>[!NOTE]
>
>有关查找数据库名称、主机、端口和登录凭据的详细信息，请访 [问平台上的凭据页](https://platform.adobe.com/query/configuration)。 要查找凭据，请登录， [!DNL Platform]单击 **[!UICONTROL 查询]**，然后单 **[!UICONTROL 击凭据]**。

## 后续步骤

现在，您已连接 [!DNL Query Service]到，可以编写查询以执行和编辑SQL语句。 例如，您可以使 `dbGetQuery(con, sql)` 用执行查询, `sql` 其中是要运行的SQL查询。

以下查询使用包含 [ExperienceEvents的](../creating-queries/experience-event-queries.md) ，并根据设备的屏幕高度创建网站的页面视图直方图。

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

有关如何编写和运行查询的更多信息，请阅读运 [行查询指南](../creating-queries/creating-queries.md)。