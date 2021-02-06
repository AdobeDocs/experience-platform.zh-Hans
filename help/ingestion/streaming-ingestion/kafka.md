---
keywords: Experience Platform；主页；热门话题； kafka; kafka连接器；
solution: Experience Platform
title: 卡夫卡连接器
topic: overview
description: Adobe Experience Platform的流连接器基于Apache Kafka Connect。 此库可用于将JSON事件从数据中心的Kafka主题直接流化到实时Experience Platform。
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# [!DNL Kafka] adobe experience platform连接器

Adobe Experience Platform的流连接器基于[!DNL Apache Kafka Connect]。 此库可用于将JSON事件从数据中心的[!DNL Kafka]主题直接实时流化到[!DNL Experience Platform]。

流连接器是接收器（单向）连接器，将数据从[!DNL Kafka]主题传送到[!DNL Experience Platform]上的已注册端点。 要使用此连接器，您必须下载库，将其添加到现有[!DNL Kafka]部署，并将[!DNL Kafka]主题配置到Adobe流HTTP URL。 其他代码为&#x200B;**不**。 连接器支持以下功能：

- 已验证的数据集合
- 对消息进行批处理以减少网络调用并提高吞吐量

有关[!DNL Kafka]连接器的详细信息（包括如何设置连接器的说明），请阅读[快速入门指南](https://github.com/adobe/experience-platform-streaming-connect)。 有关更详细的工作流程，请阅读[开发人员指南](https://www.adobe.com/go/kafka-connector-developer-guide)。