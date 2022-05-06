---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 订阅Privacy Service事件
topic-legacy: privacy events
description: 了解如何使用预配置的WebHook订阅Privacy Service事件。
exl-id: 9bd34313-3042-46e7-b670-7a330654b178
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 1%

---

# 订阅 [!DNL Privacy Service Events]

[!DNL Privacy Service Events] 是Adobe Experience Platform提供的报文 [!DNL Privacy Service]，可利用发送到已配置WebHook的Adobe I/O事件来促进高效的作业请求自动化。 它们可减少或消除轮询 [!DNL Privacy Service] API，以检查作业是否完成或是否已到达工作流中的特定里程碑。

当前，有四种类型的通知与隐私作业请求生命周期相关：

| 类型 | 描述 |
| --- | --- |
| 作业完成 | 全部 [!DNL Experience Cloud] 应用程序已报告，作业的整体或全局状态已标记为完成。 |
| 作业错误 | 一个或多个应用程序在处理请求时报告了错误。 |
| 产品完成 | 与此作业关联的某个应用程序已完成其工作。 |
| 产品错误 | 其中一个应用程序在处理请求时报告了错误。 |

本文档提供了为 [!DNL Privacy Service] 通知以及如何解释通知负载。

## 快速入门

在开始本教程之前，请查看以下Privacy Service文档：

* [Privacy Service概述](./home.md)
* [Privacy ServiceAPI指南](./api/overview.md)

## 注册网页挂接到 [!DNL Privacy Service Events]

为了接收 [!DNL Privacy Service Events]，则必须使用Adobe Developer Console向您的 [!DNL Privacy Service] 集成。

请阅读本教程 [订阅[!DNL I/O Event]通知](../observability/alerts/subscribe.md) 以详细了解如何完成此操作。 确保您选择 **[!UICONTROL Privacy Service事件]** 作为事件提供商，以访问上面列出的事件。

## 接收 [!DNL Privacy Service Event] 通知

成功注册Webhook并运行隐私作业后，便可开始接收事件通知。 这些事件可以使用Webhook本身或通过选择 **[!UICONTROL 调试跟踪]** 选项卡(位于Adobe Developer控制台中的项目事件注册概述中)。

![](images/privacy-events/debug-tracing.png)

以下JSON是 [!DNL Privacy Service Event] 当与隐私作业关联的某个应用程序完成其工作时将发送到webhook的通知有效负载：

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
| `id` | 系统生成的唯一通知ID。 |
| `type` | 要发送的通知类型，提供了下文所提供信息 `data`. 潜在值包括： <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | 事件发生时间的时间戳。 |
| `data.value` | 包含有关触发通知的内容的其他信息： <ul><li>`jobId`:触发通知的隐私作业的ID。</li><li>`message`:有关作业的特定状态的消息。 对于 `productcomplete` 或 `producterror` 通知，此字段表示相关的Experience Cloud应用程序。</li></ul> |

## 后续步骤

本文档介绍了如何将Privacy Service事件注册到配置的WebHook，以及如何解释通知负载。 要了解如何使用用户界面跟踪隐私作业，请参阅 [Privacy Service用户指南](./ui/user-guide.md).
