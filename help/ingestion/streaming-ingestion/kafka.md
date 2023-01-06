---
keywords: Experience Platform；主页；热门主题；kafka;kafka连接器；Kafka;
solution: Experience Platform
title: Kafka Connector
description: Adobe Experience Platform的流连接器基于Apache Kafka Connect。 此库可用于直接在您的数据中心中将JSON事件从Kafka主题流式传输到实时Experience Platform。
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# [!DNL Kafka] Adobe Experience Platform连接器

Adobe Experience Platform的流连接器基于 [!DNL Apache Kafka Connect]. 此库可用于从流式传输JSON事件 [!DNL Kafka] 数据中心中的主题直接 [!DNL Experience Platform] 实时。

流连接器是接收器（单向）连接器，用于从 [!DNL Kafka] 上已注册端点的主题 [!DNL Experience Platform]. 要使用此连接器，您必须下载库，并将其添加到现有 [!DNL Kafka] 部署和配置 [!DNL Kafka] 主题到Adobe流HTTP URL。 其他代码为 **not** 必需。 连接器支持以下功能：

- 经过验证的数据集合
- 对消息进行批处理以减少网络调用并提高吞吐量

有关 [!DNL Kafka] 连接器，包括有关如何设置连接器的说明，请阅读 [入门指南](https://github.com/adobe/experience-platform-streaming-connect). 有关更详细的工作流，请阅读 [开发人员指南](https://www.adobe.com/go/kafka-connector-developer-guide).
