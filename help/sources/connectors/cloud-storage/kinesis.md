---
keywords: Experience Platform；主页；热门主题；Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Amazon Kinesis Source Connector概述
topic-legacy: overview
description: 了解如何使用API或用户界面将Amazon Kinesis连接到Adobe Experience Platform。
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
translation-type: tm+mt
source-git-commit: d6f1521470b8dc630060584189690545c724de6b
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] 连接器

Adobe Experience Platform为AWS、[!DNL Google Cloud Platform]和[!DNL Azure]等云提供商提供本机连接。 您可以将这些系统中的数据导入[!DNL Platform]。

云存储源可以将您自己的数据导入[!DNL Platform]，而无需下载、格式化或上传。 收录的数据可以格式化为XDM JSON、XDM Perface或分隔。 流程的每个步骤都集成到源工作流中。 [!DNL Platform] 让您能够实时导入 [!DNL Amazon Kinesis] 数据。

## IP地址允许列表

在使用源连接器之前，必须向允许列表添加IP地址列表。 如果无法将您的区域特定IP地址添加到允许列表，在使用源时可能会导致错误或性能不佳。 有关详细信息，请参阅[ IP地址允许列表](../../ip-address-allow-list.md)页。

## 将[!DNL Amazon Kinesis]连接到[!DNL Platform]

以下文档提供了如何使用API或用户界面将[!DNL Amazon Kinesis]连接到[!DNL Platform]的信息：

### 使用API

- [使用Flow Service API创建Amazon Kinesis源连接](../../tutorials/api/create/cloud-storage/kinesis.md)
- [使用Flow Service API收集流数据](../../tutorials/api/collect/streaming.md)

### 使用UI

- [在UI中创建Amazon Kinesis源连接](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [在UI中为云存储连接配置数据流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
