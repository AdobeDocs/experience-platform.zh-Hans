---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: PayPal连接器
topic: overview
translation-type: tm+mt
source-git-commit: 52a01c5f90a9643691a25e2d0a5f03a7f0334a7d
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# （测试版）连 [!DNL PayPal] 接器

>[!NOTE]
>连接 [!DNL PayPal] 器为测试版。 有关使用 [测试版标记](../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform允许从外部源摄取数据，同时使您能够使用服务构建、标记和增强传入数 [!DNL Platform] 据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)收集数据。

[!DNL Experience Platform] 支持从第三方支付应用程序中获取数据。 支持支付提供商包括 [!DNL PayPal]:

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

以下文档提供了如何使用API [!DNL PayPal] 或 [!DNL Platform] 用户界面连接的信息：

## 连接 [!DNL PayPal] 到 [!DNL Platform] 使用API

- [使用Flow Service API创建PayPal连接器](../../tutorials/api/create/payments/paypal.md)
- [使用Flow Service API浏览支付应用程序](../../tutorials/api/explore/payments.md)
- [使用Flow Service API从支付应用程序收集数据](../../tutorials/api/collect/payments.md)

## 连接 [!DNL PayPal] 到 [!DNL Platform] 使用UI

- [在UI中创建PayPal源连接器](../../tutorials/ui/create/payments/paypal.md)
- [在UI中为付款连接器配置数据流](../../tutorials/ui/dataflow/payments.md)