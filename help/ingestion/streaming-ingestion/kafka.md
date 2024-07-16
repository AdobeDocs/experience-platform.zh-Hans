---
keywords: Experience Platform；主页；热门主题；kafka；kafka连接器；Kafka；
solution: Experience Platform
title: Kafka连接器
description: Adobe Experience Platform的流连接器基于Apache Kafka Connect。 此库可用于直接从数据中心中的Kafka主题流式传输JSON事件以实时Experience Platform。
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# 适用于Adobe Experience Platform的[!DNL Kafka]连接器

Adobe Experience Platform的流连接器基于[!DNL Apache Kafka Connect]。 此库可用于实时将JSON事件从数据中心中的[!DNL Kafka]主题直接流式传输到[!DNL Experience Platform]。

流连接器是接收器（单向）连接器，将数据从[!DNL Kafka]主题传递到[!DNL Experience Platform]上的注册端点。 若要使用此连接器，必须下载库，将其添加到现有[!DNL Kafka]部署，并将[!DNL Kafka]主题配置到Adobe流HTTP URL。 其他代码是&#x200B;**不需要**。 连接器支持以下功能：

- 经过身份验证的数据收集
- 对消息进行批处理以减少网络调用并提高吞吐量

有关[!DNL Kafka]连接器的详细信息，包括有关如何设置连接器的说明，请阅读[入门指南](https://github.com/adobe/experience-platform-streaming-connect)。 有关更详细的工作流程，请阅读[开发人员指南](https://www.adobe.com/go/kafka-connector-developer-guide)。
