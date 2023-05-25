---
keywords: Experience Platform；主页；热门主题；kafka；kafka连接器；Kafka；
solution: Experience Platform
title: Kafka连接器
description: Adobe Experience Platform的流连接器基于Apache Kafka Connect。 此库可用于直接从数据中心中的Kafka主题流式传输JSON事件以实时Experience Platform。
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# [!DNL Kafka] Adobe Experience Platform连接器

Adobe Experience Platform的流连接器基于 [!DNL Apache Kafka Connect]. 此库可用于从中流式传输JSON事件 [!DNL Kafka] 数据中心中的主题直接指向 [!DNL Experience Platform] 实时。

流连接器是接收器（单向）连接器，从传送数据 [!DNL Kafka] 的主题到已注册的端点 [!DNL Experience Platform]. 要使用此连接器，您必须下载库，并将其添加到现有库 [!DNL Kafka] 部署，并配置 [!DNL Kafka] Adobe流HTTP URL的主题。 其他代码为 **非** 必需。 连接器支持以下功能：

- 经过身份验证的数据收集
- 对消息进行批处理以减少网络调用并提高吞吐量

欲知关于 [!DNL Kafka] 连接器，包括有关如何设置连接器的说明，请阅读 [快速入门指南](https://github.com/adobe/experience-platform-streaming-connect). 有关更详细的工作流程，请阅读 [开发人员指南](https://www.adobe.com/go/kafka-connector-developer-guide).
