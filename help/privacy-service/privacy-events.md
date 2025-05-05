---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 订阅Privacy Service活动
description: 了解如何使用预配置的webhook订阅Privacy Service事件。
exl-id: 9bd34313-3042-46e7-b670-7a330654b178
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 2%

---

# 订阅[!DNL Privacy Service Events]

[!DNL Privacy Service Events]是由Adobe Experience Platform [!DNL Privacy Service]提供的消息，这些消息利用发送到配置的webhook的Adobe I/O事件促进高效的作业请求自动化。 它们减少或消除了轮询[!DNL Privacy Service] API以检查作业是否完成或工作流中是否已达到特定里程碑的需要。

目前与隐私作业请求生命周期相关的通知有四种类型：

| 类型 | 描述 |
| --- | --- |
| 作业完成 | 所有[!DNL Experience Cloud]应用程序都已报告，作业的整体或全局状态已标记为完成。 |
| 作业错误 | 一个或多个应用程序在处理请求时报告错误。 |
| 产品完成 | 与此作业关联的应用程序之一已完成其工作。 |
| 产品错误 | 其中一个应用程序在处理请求时报告错误。 |

本文档提供了为[!DNL Privacy Service]通知设置事件注册的步骤，以及如何解释通知负载。

## 快速入门

在开始本教程之前，请查看以下Privacy Service文档：

* [Privacy Service 概述](./home.md)
* [Privacy ServiceAPI指南](./api/overview.md)

## 向[!DNL Privacy Service Events]注册webhook

要接收[!DNL Privacy Service Events]，您必须使用Adobe Developer Console注册[!DNL Privacy Service]集成的webhook。

请阅读有关[订阅[!DNL I/O Event]通知](../observability/alerts/subscribe.md)的教程，以了解有关如何完成此操作的详细步骤。 请确保选择&#x200B;**[!UICONTROL Privacy Service事件]**&#x200B;作为事件提供程序，以便访问上面列出的事件。

## 接收[!DNL Privacy Service Event]通知

成功注册webhook并运行隐私作业后，即可开始接收事件通知。 可以使用webhook本身或通过在Adobe Developer Console中选择项目事件注册概述中的&#x200B;**[!UICONTROL 调试跟踪]**&#x200B;选项卡来查看这些事件。

![](images/privacy-events/debug-tracing.png)

以下JSON是[!DNL Privacy Service Event]通知有效负载的示例，当与隐私作业关联的应用程序之一完成其工作时，该有效负载将发送到您的webhook：

```json
{
  "id":"b472e249-368b-4706-90f3-1d774713f827",
  "event_id":"b116f797-e50b-432e-9c65-189106a34820",
  "specversion":"0.2",
  "type":"com.adobe.platform.gdpr.productcomplete",
  "source":"https://ns.adobe.com/platform/gdpr",
  "time":"Wed Oct 23 18:52:32 GMT 2019",
  "data":{
    "imsOrg":"{ORG_ID}",
    "value":{
      "jobId":"6f0f2b62-88a7-4515-ba05-432d9a7021c5",
      "message":"analytics.access.complete"
    }
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 系统为通知生成的唯一ID。 |
| `type` | 正在发送的通知类型，为`data`下提供的信息提供上下文。 潜在值包括： <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | 事件发生时间的时间戳。 |
| `data.value` | 包含有关触发通知的因素的其他信息： <ul><li>`jobId`：触发通知的隐私作业的ID。</li><li>`message`：有关作业特定状态的消息。 对于`productcomplete`或`producterror`通知，此字段表示有问题的Experience Cloud应用程序。</li></ul> |

## 后续步骤

本文档介绍了如何将Privacy Service事件注册到配置的webhook，以及如何解释通知负载。 要了解如何使用用户界面跟踪隐私作业，请参阅[Privacy Service用户指南](./ui/user-guide.md)。
