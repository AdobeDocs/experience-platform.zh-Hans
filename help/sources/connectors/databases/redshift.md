---
title: Amazon Redshift Source连接器概述
description: 了解如何使用API或用户界面将Amazon Redshift连接到Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 75e577dd-a0b0-4f82-a371-5ec9255544f8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# [!DNL Amazon Redshift]源

>[!IMPORTANT]
>
>- [!DNL Amazon Redshift]源在源目录中可供已购买Real-Time CDP Ultimate的用户使用。
>
>- 在Amazon Web Services (AWS)上运行Adobe Experience Platform时，您现在可以使用[!DNL Amazon Redshift]源。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../landing/multi-cloud.md)。


Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。 您可以从各种源(如Adobe应用程序、基于云的存储、数据库和许多其他源)中摄取数据。

Experience Platform支持从第三方数据库引入数据。 Experience Platform可以连接到各种类型的数据库，例如关系数据库、NoSQL数据库或数据仓库数据库。 对数据库提供程序的支持包括[!DNL Amazon Redshift]。

## 在Azure上为Experience Platform设置[!DNL Amazon Redshift]源 {#azure}

请按照以下步骤了解如何在Azure上为Experience Platform设置[!DNL Amazon Redshift]帐户。

### IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于区域的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 有关详细信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页。

## 在Amazon Web Services上为Experience Platform设置[!DNL Amazon Redshift]源 {#aws}

>[!AVAILABILITY]
>
>本节适用于在Amazon Web Services (AWS)上运行的Experience Platform的实施。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../landing/multi-cloud.md)。

### 列入允许列表在AWS上连接的IP地址

将源连接到AWS上的Experience Platform之前，必须将特定于区域的IP地址添加到允许列表。 有关详细信息，请阅读[将IP地址列入允许列表到AWS](../../ip-address-allow-list.md)上的Experience Platform的指南。

## 使用API将[!DNL Amazon Redshift]连接到Experience Platform

- [使用流服务API将Amazon Redshift连接到Experience Platform](../../tutorials/api/create/databases/redshift.md)
- [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
- [使用流服务API为数据库源创建数据流](../../tutorials/api/collect/database-nosql.md)

## 使用UI将[!DNL Amazon Redshift]连接到Experience Platform

- [在UI中创建Amazon Redshift源连接](../../tutorials/ui/create/databases/redshift.md)
- [在用户界面中为数据库源连接创建数据流](../../tutorials/ui/dataflow/databases.md)
