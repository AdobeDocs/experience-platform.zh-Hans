---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 卡夫卡连接器
topic: overview
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# [!DNL Kafka] Adobe Experience Platform连接器

Adobe Experience Platform流连接器基于 [!DNL Apache Kafka Connect]。 此库可用于将JSON事件从数 [!DNL Kafka] 据中心主题直接流 [!DNL Experience Platform] 到实时流。

流连接器是接收器（单向）连接器，将数据从主题传 [!DNL Kafka] 送到上的注册端点 [!DNL Experience Platform]。 要使用此连接器，您必须下载库，将其添 [!DNL Kafka] 加到现有部 [!DNL Kafka] 署，并将主题配置到Adobe流HTTP URL。 不需要其 **他代** 码。 连接器支持以下功能：

- 已验证的数据集合
- 对消息进行批处理以减少网络调用并提高吞吐量

有关连接器的 [!DNL Kafka] 详细信息（包括如何设置连接器的说明），请阅读 [入门指南](https://github.com/adobe/experience-platform-streaming-connect)。 有关更详细的工作流程，请阅读开发 [人员指南](https://github.com/adobe/experience-platform-streaming-connect/blob/master/DEVELOPER_GUIDE.md)。