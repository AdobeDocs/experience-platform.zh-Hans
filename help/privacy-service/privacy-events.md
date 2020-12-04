---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 订阅Privacy Service事件
topic: privacy events
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 1%

---


# 订阅 [!DNL Privacy Service Events]

[!DNL Privacy Service Events] 是Adobe Experience Platform提供的消息， [!DNL Privacy Service]它利用发送到配置的webhook的Adobe I/O事件来促进高效的工作请求自动化。 它们减少或消除了对API进行轮询的 [!DNL Privacy Service] 需求，以便检查作业是否完成或是否到达了工作流中的特定里程碑。

当前有四种类型的通知与隐私作业请求生命周期相关：

| 类型 | 描述 |
| --- | --- |
| 作业完成 | 所有 [!DNL Experience Cloud] 应用程序都已报告，作业的整体或全局状态已标记为完成。 |
| 作业错误 | 处理请求时，一个或多个应用程序报告了错误。 |
| 产品完成 | 与此作业关联的其中一个应用程序已完成其工作。 |
| 产品错误 | 其中一个应用程序在处理请求时报告了错误。 |

此文档提供设置通知事件注册的步 [!DNL Privacy Service] 骤，以及如何解释通知有效负荷。

## 入门指南

在开始本教程之前，请查阅以下Privacy Service文档：

* [Privacy Service概述](./home.md)
* [Privacy ServiceAPI开发人员指南](./api/getting-started.md)

## 将网页挂接注册到 [!DNL Privacy Service Events]

要接收，您必 [!DNL Privacy Service Events]须使用Adobe开发者控制台来注册您的集成的网 [!DNL Privacy Service] 络挂接。

有关如何完成此 [操 [!DNL I/O Event] 作的详细步](../observability/notifications/subscribe.md) 骤，请按照教程订阅通知。 确保您选择 **[!UICONTROL Privacy Service事件]** ，作为事件提供者，以访问上面列出的事件。

## 接收通 [!DNL Privacy Service Event] 知

成功注册Webhook和隐私作业后，您可以开始接收事件通知。 这些事件可以使用Webhook本身进行查看，也可以通过在Adobe开 **[!UICONTROL 发人员控制台中]** ，选择项目事件注册概述中的“调试跟踪”选项卡进行查看。

![](images/privacy-events/debug-tracing.png)

以下JSON是通知有效负荷的 [!DNL Privacy Service Event] 示例，当与隐私作业关联的某个应用程序完成其工作时，通知有效负荷将发送至您的Webhook:

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
| `type` | 所发送通知的类型，提供下文信息 `data`。 潜在值包括： <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | 发生事件的时间戳。 |
| `data.value` | 包含有关触发通知的其他信息： <ul><li>`jobId`:触发通知的隐私作业的ID。</li><li>`message`:有关作业特定状态的消息。 对于 `productcomplete` 或通 `producterror` 知，此字段指示相关的Experience Cloud应用程序。</li></ul> |

## 后续步骤

此文档介绍如何将Privacy Service事件注册到已配置的Webhook，以及如何解释通知有效负载。 要了解如何使用用户界面跟踪隐私作业，请参阅 [Privacy Service用户指南](./ui/user-guide.md)。