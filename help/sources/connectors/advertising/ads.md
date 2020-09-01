---
keywords: Experience Platform;home;popular topics;Google AdWords;google adwords
solution: Experience Platform
title: Google AdWords连接器
topic: overview
description: 以下文档提供了如何使用API或用户界面将Google AdWords连接到平台的信息。
translation-type: tm+mt
source-git-commit: 6934bfeee84f542558894bbd4ba5759891cd17f3
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# [!DNL Google AdWords] 连接器

>[!NOTE]
>
>连接 [!DNL Google AdWords] 器为测试版。 有关使用 [测试版标记](../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform允许从外部来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)收集数据。

[!DNL Experience Platform] 支持从第三方广告系统中摄取数据。 对广告提供商的支持包括 [!DNL Google AdWords]:

## IP地址允许列表

在使用源连接器之前，必须将以下IP地址添加到允许列表。 如果无法向允许列表添加特定于区域的IP地址，则在使用源时可能会导致错误或性能不佳。

### 美国东部地区

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### 西欧地区

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### 澳大利亚东部

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

以下文档提供了如何使用API [!DNL Google AdWords] 或 [!DNL Platform] 用户界面连接的信息：

## 连接 [!DNL Google AdWords] 到 [!DNL Platform] 使用API

- [使用Flow Service API创建Google AdWords连接器](../../tutorials/api/create/advertising/ads.md)
- [使用Flow Service API浏览广告系统](../../tutorials/api/explore/advertising.md)
- [使用Flow Service API收集广告数据](../../tutorials/api/collect/advertising.md)

## 连接 [!DNL Google AdWords] 到 [!DNL Platform] 使用UI

- [在UI中创建Google AdWords源连接器](../../tutorials/ui/create/advertising/ads.md)
- [在UI中为广告连接器配置数据流](../../tutorials/ui/dataflow/advertising.md)