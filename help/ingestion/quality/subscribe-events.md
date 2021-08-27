---
keywords: Experience Platform；主页；热门主题；数据摄取通知；通知；订阅事件；数据摄取状态事件；状态事件；订阅；状态通知；
solution: Experience Platform
title: 数据摄取通知
topic-legacy: overview
description: 为了帮助监控摄取过程，Adobe Experience Platform允许订阅一组在该过程的每个步骤发布的事件，并通知您摄取数据的状态以及任何可能的失败。
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 1%

---

# 数据摄取通知

将数据摄取到Adobe Experience Platform的过程由多个步骤组成。 在确定需要摄取到[!DNL Platform]的数据文件后，摄取过程将开始，并且每个步骤都会连续进行，直到数据被成功摄取或失败为止。 可以使用[Adobe Experience Platform数据摄取API](https://www.adobe.io/experience-platform-apis/references/data-ingestion/)或使用[!DNL Experience Platform]用户界面来启动摄取过程。

加载到[!DNL Platform]的数据必须经过多个步骤才能到达其目标、[!DNL Data Lake]或[!DNL Real-time Customer Profile]数据存储。 每个步骤都包括处理数据、验证数据，然后存储数据，然后再将其传递到下一步。 根据所摄取的数据量，这可能会成为一个耗时的过程，并且该过程始终可能因验证、语义或处理错误而失败。 在失败时，需要修复数据问题，然后必须使用更正的数据文件重新启动整个摄取过程。

为了帮助监控摄取过程，[!DNL Experience Platform]允许订阅一组在该过程的每个步骤发布的事件，并通知您摄取数据的状态以及任何可能的故障。

## 为数据摄取通知注册Web挂接

要接收数据摄取通知，您必须使用[Adobe开发人员控制台](https://www.adobe.com/go/devs_console_ui)将Web挂接注册到您的Experience Platform集成。

有关如何完成此操作的详细步骤，请按照[订阅 [!DNL Adobe I/O Event] 通知](../../observability/alerts/subscribe.md)的教程操作。

>[!IMPORTANT]
>
>在订阅过程中，确保选择&#x200B;**[!UICONTROL Platform notifications]**&#x200B;作为事件提供程序，并在出现提示时选择&#x200B;**[!UICONTROL 数据摄取通知]**&#x200B;事件订阅。

## 接收数据摄取通知

成功注册Webhook并摄取新数据后，即可开始接收事件通知。 可以使用Webhook本身，或通过在Adobe开发人员控制台中选择项目事件注册概述中的&#x200B;**[!UICONTROL 调试跟踪]**&#x200B;选项卡来查看这些事件。

以下JSON是通知有效负载的示例，在批量摄取事件失败时，将该有效负载发送到您的Webhook:

```json
{
  "event_id": "93a5b11a-b0e6-4b29-ad82-81b1499cb4f2",
  "event": {
    "xdm:ingestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:customerIngestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:imsOrg": "{IMS_ORG}",
    "xdm:completed": 1598374341560,
    "xdm:datasetId": "5e55b556c2ae4418a8446037",
    "xdm:eventCode": "ing_load_failure",
    "xdm:sandboxName": "prod",
    "sentTime": "1598374341595",
    "processStartTime": 1598374342614,
    "transformedTime": 1598374342621,
    "header": {
      "_adobeio": {
        "imsOrgId": "{IMS_ORG}",
        "providerMetadata": "aep_observability_catalog_events",
        "eventCode": "platform_event"
      }
    }
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `event_id` | 系统生成的唯一通知ID。 |
| `event` | 一个对象，其中包含触发通知的事件的详细信息。 |
| `event.xdm:datasetId` | 摄取事件所应用到的数据集的ID。 |
| `event.xdm:eventCode` | 状态代码，用于指示为数据集触发的事件类型。 有关特定值及其定义，请参阅[附录](#event-codes)。 |

要查看事件通知的完整架构，请参阅[公共GitHub存储库](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json)。

## 后续步骤

在向项目注册[!DNL Platform]通知后，即可查看[!UICONTROL 项目概述]中收到的事件。 有关如何跟踪事件的详细说明，请参阅[跟踪Adobe I/O事件](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md)上的指南。

## 附录

以下部分包含有关解释数据摄取通知负载的其他信息。

### 可用的状态通知事件 {#event-codes}

下表列出了可订阅的可用数据摄取状态通知。

| 事件代码 | 平台服务 | 状态 | 事件描述 |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | 已成功将批量摄取到[!DNL Data Lake]内的数据集中。 |
| `ing_load_failure` | [!DNL Data Ingestion] | 失败 | 无法将批量摄取到[!DNL Data Lake]内的数据集中。 |
| `ps_load_success` | [!DNL Real-time Customer Profile] | 成功 | 已成功将批次摄取到[!DNL Profile]数据存储中。 |
| `ps_load_failure` | [!DNL Real-time Customer Profile] | 失败 | 无法将批次摄取到[!DNL Profile]数据存储中。 |
| `ig_load_success` | [!DNL Identity Service] | 成功 | 数据已成功加载到身份图中。 |
| `ig_load_failure` | [!DNL Identity Service] | 失败 | 数据无法加载到身份图中。 |

>[!NOTE]
>
>只为所有数据摄取通知提供了一个事件主题。 为了区分不同的状态，可以使用事件代码。
