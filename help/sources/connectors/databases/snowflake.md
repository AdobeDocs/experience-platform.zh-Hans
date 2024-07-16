---
title: SnowflakeSource连接器概述
description: 了解如何使用API或用户界面将Snowflake连接到Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 8b0f6eca87deedd8090830e3375d5099bfb0dfc0
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# [!DNL Snowflake]源

>[!IMPORTANT]
>
>* [!DNL Snowflake]源在源目录中可供已购买Real-time Customer Data Platform Ultimate的用户使用。
>* 默认情况下，[!DNL Snowflake]源将`null`解释为空字符串。 请联系您的Adobe代表，以确保在Adobe Experience Platform中将您的`null`值正确写入`null`。
>* 要使Experience Platform摄取数据，必须将所有基于表的批处理源的时区配置为UTC时区。 [!DNL Snowflake]源支持的唯一时间戳是带有UTC时间的TIMESTAMP_NTZ。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

Experience Platform支持从第三方数据库引入数据。 Platform可以连接到不同类型的数据库，如关系数据库、NoSQL数据库或数据仓库数据库。 对数据库提供程序的支持包括[!DNL Snowflake]。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于区域的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 有关详细信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页。

以下文档提供了有关如何使用API或用户界面将[!DNL Snowflake]连接到Platform的信息：

## 使用API将[!DNL Snowflake]连接到平台

* [使用流服务API创建基于Snowflake的连接](../../tutorials/api/create/databases/snowflake.md)
* [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
* [使用流服务API为数据库源创建数据流](../../tutorials/api/collect/database-nosql.md)

## 使用UI将[!DNL Snowflake]连接到平台

* [在UI中创建Snowflake源连接](../../tutorials/ui/create/databases/snowflake.md)
* [在用户界面中为数据库源连接创建数据流](../../tutorials/ui/dataflow/databases.md)
