---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 数据集与表和模式
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# 数据集与表和模式

查看 [Adobe Experience Platform UI中可用数据集的列表](https://platform.adobe.com/datasets)，确保观察数据集名称。
>[!NOTE] 某些数据集名称有空格，否则可能不是SQL安全。

![](../images/queries/datasets-and-tables/dataset-names.png)


通过单击数据集表中的模式名称，在UI中查看数据集模式的层次结构。

![](../images/queries/datasets-and-tables/schema-information.png)

打开PSQL命令行，并从此处使用连接详细信息： [https://platform.adobe.com/query/configuration](https://platform.adobe.com/query/configuration)。

![](../images/clients/psql/connect-bi.png)

要将平台上的可用表与SQL视图，可以使用或 `\d` 执行 `SHOW TABLES;`。


`\d` 显示标准PostgreSQL视图

```
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

`SHOW TABLES;` 是一个自定义命令，它提供更详细的视图并显示表以及在平台UI中找到的数据集名称。

```
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

要视图表的根模式，请使用该命 `\d table_name` 令。

>[!NOTE] 显示的模式显示根字段，其中大多数是复杂的，在数据集模式UI中指的是对象类型。

`\d luma_midvalues`

```
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

要进一步进入模式，请使用下划线(`_`)在要描述的表中声明列。 例如：`\d table_name_column`

`\d luma_midvalues_web`

```
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```
