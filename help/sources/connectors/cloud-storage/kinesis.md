---
keywords: Experience Platform;home;popular topics;Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: AmazonKinesis连接器
topic: overview
description: 以下文档提供了如何使用API或用户界面将AmazonKinesis连接到平台的信息。
translation-type: tm+mt
source-git-commit: e0a0b7fc28b8cc85c5140d3840e06e5c7078c307
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---


# （测试版）连 [!DNL Amazon Kinesis] 接器

>[!NOTE]
>
>连接 [!DNL Amazon Kinesis] 器为测试版。 有关使用 [测试版标记](../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform为AWS、和等云提供商提供本 [!DNL Google Cloud Platform]机连接 [!DNL Azure]。 您可以将数据从这些系统导入 [!DNL Platform]。

云存储源无需下载、格式化 [!DNL Platform] 或上传即可将您自己的数据导入其中。 摄取的数据可格式化为XDM JSON、XDM镶木地板或分隔。 流程的每个步骤都集成到源工作流中。 [!DNL Platform] 允许您实时 [!DNL Amazon Kinesis] 导入数据。

## IP地址允许列表

在使用源连接器之前，必须向允许列表添加IP地址列表。 如果无法向允许列表添加特定于区域的IP地址，则在使用源时可能会导致错误或性能不佳。 有关详细 [信息，请参阅](../../ip-address-allow-list.md) “IP地址允许列表”页。

## 连接 [!DNL Amazon Kinesis] 到 [!DNL Platform]

以下文档提供了如何使用API [!DNL Amazon Kinesis] 或 [!DNL Platform] 用户界面连接的信息：

### 使用API

- [使用Flow Service API创建AmazonKinesis连接器](../../tutorials/api/create/cloud-storage/kinesis.md)
- [使用Flow Service API浏览云存储系统](../../tutorials/api/explore/cloud-storage.md)
- [使用流服务API收集云存储数据](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中创建AmazonKinesis源连接器](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [在UI中为云存储连接器配置数据流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)