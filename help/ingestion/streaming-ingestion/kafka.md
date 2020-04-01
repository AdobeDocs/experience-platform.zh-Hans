---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 卡夫卡连接器
topic: overview
translation-type: tm+mt
source-git-commit: f80b2e1d787d1f8d9fe8ac306422aa7744a69cd3

---


# Adobe Experience Platform的Kafka连接器

Adobe Experience Platform的流连接器基于Apache Kafka Connect。 此库可用于将JSON事件从数据中心的Kafka主题实时流化到Experience Platform。

流连接器是汇流（单向）连接器，可将数据从Kafka主题传送到Experience Platform上的注册端点。 要使用此连接器，您必须下载库，将其添加到现有的Kafka部署中，并将Kafka主题配置到Adobe流HTTP URL。 不需要其 **他代码** 。 该连接器支持以下功能：

- 经过身份验证的数据集合
- 对消息进行批处理以减少网络调用并提高吞吐量

有关Kafka连接器的更多信息（包括如何设置连接器的说明），请阅读入 [门指南](https://github.com/adobe/experience-platform-streaming-connect)。 有关更详细的工作流程，请阅读开发 [人员指南](https://github.com/adobe/experience-platform-streaming-connect/blob/master/DEVELOPER_GUIDE.md)。