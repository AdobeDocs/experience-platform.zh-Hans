---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 订阅Privacy Service事件
topic: privacy events
description: 了解如何使用预配置的Webhook订阅Privacy Service事件。
translation-type: tm+mt
source-git-commit: 2b919a3b6cbbd59521874cfd2d11e20de3077740
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 1%

---


# 订阅[!DNL Privacy Service Events]

[!DNL Privacy Service Events] 是Adobe Experience Platform提供的消息， [!DNL Privacy Service]它利用发送到配置的webhook的Adobe I/O事件来促进高效的工作请求自动化。它们减少或消除了轮询[!DNL Privacy Service] API的需求，以检查作业是否完成或是否已到达工作流中的特定里程碑。

当前有四种类型的通知与隐私作业请求生命周期相关：

| 类型 | 描述 |
| --- | --- |
| 作业完成 | 所有[!DNL Experience Cloud]应用程序都已报告回来，作业的整体或全局状态已标记为完成。 |
| 作业错误 | 处理请求时，一个或多个应用程序报告了错误。 |
| 产品完成 | 与此作业关联的其中一个应用程序已完成其工作。 |
| 产品错误 | 其中一个应用程序在处理请求时报告了错误。 |

此文档提供了为[!DNL Privacy Service]通知设置事件注册的步骤，以及如何解释通知有效负荷。

## 入门指南

在开始本教程之前，请查阅以下Privacy Service文档：

* [Privacy Service概述](./home.md)
* [Privacy ServiceAPI开发人员指南](./api/getting-started.md)

## 向[!DNL Privacy Service Events]注册Webhook

要接收[!DNL Privacy Service Events]，您必须使用Adobe开发者控制台来注册用于[!DNL Privacy Service]集成的Webhook。

有关如何实现此操作的详细步骤，请参阅[订阅 [!DNL I/O Event] 通知](../observability/notifications/subscribe.md)的教程。 确保选择&#x200B;**[!UICONTROL Privacy Service事件]**&#x200B;作为事件提供者，以访问上面列出的事件。

## 接收[!DNL Privacy Service Event]通知

成功注册Webhook和隐私作业后，您可以开始接收事件通知。 这些事件可以使用Webhook本身进行查看，也可以通过在Adobe开发者控制台中选择项目的事件注册概述中的&#x200B;**[!UICONTROL 调试跟踪]**&#x200B;选项卡来查看。

![](images/privacy-events/debug-tracing.png)

以下JSON是[!DNL Privacy Service Event]通知有效负荷的示例，当与隐私作业关联的某个应用程序完成其工作时，该通知有效负荷将发送至您的Webhook:

```json
{
  "id":"b472e249-368b-4706-90f3-1d774713f827",
  "event_id":"b116f797-e50b-432e-9c65-189106a34820",
  "specversion":"0.2",
  "type":"com.adobe.platform.gdpr.productcomplete",
  "source":"https://ns.adobe.com/platform/gdpr",
  "time":"Wed Oct 23 18:52:32 GMT 2019",
  "data":{
    "imsOrg":"{IMS_ORG}",
    "value":{
      "jobId":"6f0f2b62-88a7-4515-ba05-432d9a7021c5",
      "message":"analytics.access.complete"
    }
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 通知的唯一、由系统生成的ID。 |
| `type` | 所发送通知的类型，提供`data`下提供的信息的上下文。 潜在值包括： <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | 发生事件的时间戳。 |
| `data.value` | 包含有关触发通知的其他信息： <ul><li>`jobId`:触发通知的隐私作业的ID。</li><li>`message`:有关作业特定状态的消息。对于`productcomplete`或`producterror`通知，此字段指示相关的Experience Cloud应用程序。</li></ul> |

## 后续步骤

此文档介绍如何将Privacy Service事件注册到已配置的Webhook，以及如何解释通知有效负载。 要了解如何使用用户界面跟踪隐私作业，请参阅[Privacy Service用户指南](./ui/user-guide.md)。