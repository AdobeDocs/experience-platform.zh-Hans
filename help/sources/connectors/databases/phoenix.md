---
title: Phoenix Source概述
description: 了解如何使用API或用户界面将您的Phoenix帐户连接到Adobe Experience Platform。
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: 45e6ef18-a0b7-4bb2-b099-b2a878e96637
source-git-commit: 474b81aa8caf58013f8ea7cff9ad59d92466aac8
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# [!DNL Phoenix]

>[!WARNING]
>
>[!DNL Phoenix]源将于2025年5月底弃用。

Adobe Experience Platform源支持从第三方数据库（如[[!DNL Phoenix]](https://phoenix.apache.org/index.html)）摄取数据。 在通过[!DNL Flow Service] API或Experience Platform用户界面连接[!DNL Phoenix]帐户之前，本文档提供先决条件信息。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于区域的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 有关详细信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页。

以下文档提供了有关如何使用API或用户界面将[!DNL Phoenix]连接到Experience Platform的信息：

## 连接[!DNL Phoenix]以使用APIExperience Platform

* [使用流服务API创建Phoenix基本连接](../../tutorials/api/create/databases/phoenix.md)
* [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
* [使用流服务API为数据库源创建数据流](../../tutorials/api/collect/database-nosql.md)

## 使用UI连接[!DNL Phoenix]以Experience Platform

* [使用Experience Platform用户界面连接你的 [!DNL Phoenix] 帐户](../../tutorials/ui/create/databases/phoenix.md)
* [在用户界面中为数据库源连接创建数据流](../../tutorials/ui/dataflow/databases.md)
