---
keywords: Experience Platform；主页；热门话题；kafka;kafka连接器；
solution: Experience Platform
title: 卡夫卡连接器
topic: 概述
description: Adobe Experience Platform的流连接器基于Apache Kafka Connect。 此库可用于将JSON事件从数据中心的Kafka主题直接流化到Experience Platform。
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# [!DNL Kafka] Adobe Experience Platform

Adobe Experience Platform的流连接器基于[!DNL Apache Kafka Connect]。 此库可用于将JSON事件从数据中心的[!DNL Kafka]主题直接实时流化到[!DNL Experience Platform]。

流连接器是接收器（单向）连接器，将数据从[!DNL Kafka]主题传送到[!DNL Experience Platform]上的已注册端点。 要使用此连接器，您必须下载库，将其添加到现有的[!DNL Kafka]部署，然后将[!DNL Kafka]主题配置到Adobe流HTTP URL。 其他代码为&#x200B;**不**。 连接器支持以下功能：

- 已验证的数据集合
- 对消息进行批处理以减少网络调用并提高吞吐量

有关[!DNL Kafka]连接器的详细信息（包括如何设置连接器的说明），请阅读[快速入门指南](https://github.com/adobe/experience-platform-streaming-connect)。 有关更详细的工作流程，请阅读[开发人员指南](https://www.adobe.com/go/kafka-connector-developer-guide)。