---
keywords: Experience Platform；主页；热门主题；AmazonKinesis；亚马孙基因；Kinesis；基因
solution: Experience Platform
title: AmazonKinesis源连接器概述
topic: overview
description: 了解如何使用API或用户界面将Amazon·Kinesis连接到Adobe Experience Platform。
translation-type: tm+mt
source-git-commit: a489ab248793a063295578943ad600d8eacab6a2
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---


# （测试版）[!DNL Amazon Kinesis]连接器

>[!NOTE]
>
>[!DNL Amazon Kinesis]接头为测试版。 有关使用测试版标签的连接器的详细信息，请参见[源概述](../../home.md#terms-and-conditions)。

Adobe Experience Platform为AWS、[!DNL Google Cloud Platform]和[!DNL Azure]等云提供商提供本机连接。 您可以将数据从这些系统导入[!DNL Platform]。

云存储源可以将您自己的数据导入[!DNL Platform]，而无需下载、格式化或上传。 摄取的数据可格式化为XDM JSON、XDM Perface或分隔。 流程的每个步骤都集成到源工作流中。 [!DNL Platform] 允许您实时 [!DNL Amazon Kinesis] 导入数据。

## IP地址允许列表

在使用源连接器之前，必须向允许列表添加IP地址列表。 如果无法向允许列表添加特定于区域的IP地址，则在使用源时可能会导致错误或性能不佳。 有关详细信息，请参阅[ IP地址允许列表](../../ip-address-allow-list.md)页。

## 将[!DNL Amazon Kinesis]连接到[!DNL Platform]

以下文档提供了如何使用API或用户界面将[!DNL Amazon Kinesis]连接到[!DNL Platform]的信息：

### 使用API

- [使用Flow Service API创建AmazonKinesis源连接](../../tutorials/api/create/cloud-storage/kinesis.md)
- [使用Flow Service API收集流数据](../../tutorials/api/collect/streaming.md)

### 使用UI

- [在UI中创建AmazonKinesis源连接](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [在UI中为云存储连接配置数据流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)