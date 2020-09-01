---
keywords: Experience Platform;home;popular topics;query service;Query service;datasets;tables;schemas;
solution: Experience Platform
title: 数据集与表和模式
topic: queries
translation-type: tm+mt
source-git-commit: c5d3be4706ca6d6a30e203067db6ddc894b9bfb4
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 1%

---


# 数据集与表和模式

检查Adobe Experience PlatformUI中可用数据集 [的列表](https://platform.adobe.com/datasets)，确保观察数据集名称。
>[!NOTE]
>
>某些数据集名称有空格，否则可能不是SQL安全。

![](../images/queries/datasets-and-tables/dataset-names.png)


单击数据集表中的模式名，查看UI中数据集模式的层次结构。

![](../images/queries/datasets-and-tables/schema-information.png)

打开PSQL命令行，并从此处使用连接详细信息： [https://platform.adobe.com/query/configuration](https://platform.adobe.com/query/configuration)。

![](../images/clients/psql/connect-bi.png)

要使用SQL视图可 [!DNL Platform] 用的表，可以使用 `\d` 或 `SHOW TABLES;`。


`\d` 显示标准PostgreSQL视图

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

`SHOW TABLES;` 是一个自定义命令，它提供更详细的视图并显示表以及UI中的数据集名 [!DNL Platform] 称。

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

要视图表的根模式，请使用命 `\d table_name` 令。

>[!NOTE]
>
>显示的模式显示根字段，其中大多数是复杂的，在数据集模式UI中指的是对象类型。

`\d luma_midvalues`

```sql
                         Table "public.luma_midvalues"
      Column       |             Type            | Collation | Nullable | Default 
-------------------+-----------------------------+-----------+----------+---------
 timestamp         | timestamp                   |           |          | 
 _id               | text                        |           |          | 
 productlistitems  | anyarray                    |           |          | 
 commerce          | luma_midvalues_commerce     |           |          | 
 receivedtimestamp | timestamp                   |           |          | 
 enduserids        | luma_midvalues_enduserids   |           |          | 
 datasource        | datasource                  |           |          | 
 web               | luma_midvalues_web          |           |          | 
 placecontext      | luma_midvalues_placecontext |           |          | 
 identitymap       | anymap                      |           |          | 
 marketing         | marketing                   |           |          | 
 environment       | luma_midvalues_environment  |           |          | 
 _experience       | luma_midvalues__experience  |           |          | 
 device            | device                      |           |          | 
 search            | search                      |           |          | 
```

要进一步进入模式，请使`_`用下划线()在表中声明要描述的列。 例如：`\d table_name_column`

`\d luma_midvalues_web`

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```
