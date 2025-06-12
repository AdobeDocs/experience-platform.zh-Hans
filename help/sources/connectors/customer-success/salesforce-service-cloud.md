---
title: Salesforce Service Cloud Source连接器概述
description: 了解如何使用API或用户界面将Salesforce Service Cloud连接到Adobe Experience Platform。
exl-id: 9bebbc00-55b3-4aec-9357-4127c05844e2
source-git-commit: d8d9303e358c66c4cd891d6bf59a801c09a95f8e
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# [!DNL Salesforce Service Cloud]

>[!WARNING]
>
>[!DNL Salesforce Service Cloud]源的基本身份验证将于2026年1月被弃用。 您必须移至OAuth 2客户端凭据身份验证，才能继续使用该源并将数据从[!DNL Salesforce Service Cloud]帐户摄取到Experience Platform。

Adobe Experience Platform允许从外部源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。 您可以从各种源(如Adobe应用程序、基于云的存储、数据库和许多其他源)中摄取数据。

[!DNL Experience Platform]支持从第三方客户成功系统中引入数据。 对客户成功提供商的支持包括[!DNL Salesforce Service Cloud]。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表。 未能将特定于地区的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 列入允许列表有关详细信息，请参阅[IP地址](../../ip-address-allow-list.md)页。

以下文档提供了有关如何使用API或用户界面将[!DNL Salesforce Service Cloud]连接到[!DNL Experience Platform]的信息：

## 使用API将[!DNL Salesforce Service Cloud]连接到[!DNL Experience Platform]

- [使用流服务API创建Salesforce服务云基本连接](../../tutorials/api/create/customer-success/salesforce-service-cloud.md)
- [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
- [使用流服务API为客户成功来源创建数据流](../../tutorials/api/collect/customer-success.md)

## 使用UI将[!DNL Salesforce Service Cloud]连接到[!DNL Experience Platform]

- [在UI中创建Salesforce Service Cloud源连接](../../tutorials/ui/create/customer-success/salesforce-service-cloud.md)
- [在UI中为客户成功源连接创建数据流](../../tutorials/ui/dataflow/customer-success.md)
