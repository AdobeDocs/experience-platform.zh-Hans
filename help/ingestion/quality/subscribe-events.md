---
keywords: Experience Platform;home;popular topics;data ingestion notifications;notifications;subscribe events;data ingestion status events;status events;subscribe;status notifications;
solution: Experience Platform
title: 订阅数据获取事件
topic: overview
description: 为了帮助监视摄取过程，Adobe Experience Platform允许订阅在该过程的每个步骤发布的一组事件，通知您所摄取数据的状态和任何可能的故障。
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 1%

---


# 数据获取通知

将数据引入Adobe Experience Platform的过程由多个步骤组成。 确定需要摄取的数据文件后，摄取过 [!DNL Platform]程将开始，每个步骤将连续进行，直到数据被成功摄取或失败。 可以使用Adobe Experience Platform数据摄取 [API或使用用户界面](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) ，启动 [!DNL Experience Platform] 摄取过程。

加载到的 [!DNL Platform] 数据必须经过多个步骤才能到达其目标、 [!DNL Data Lake] 或数据存储 [!DNL Real-time Customer Profile] 区。 每个步骤都包括处理数据、验证数据，然后在将数据传递到下一步之前存储数据。 根据所摄取的数据量，这可能会成为一个耗时的过程，并且始终有由于验证、语义或处理错误而导致该过程失败的可能。 在故障事件，需要修复数据问题，然后必须使用更正的数据文件重新启动整个摄取过程。

为了帮助监视摄取过程， [!DNL Experience Platform] 可以订阅在该过程的每个步骤发布的一组事件，通知您所摄取数据的状态和任何可能的故障。

## 注册网络挂接以接收数据获取通知

要接收Adobe获取通知，您必须使用 [开发者控制台](https://www.adobe.com/go/devs_console_ui) ，为Experience Platform集成注册网络挂接。

有关如何完成此 [操 [!DNL Adobe I/O Event] 作的详细步](../../observability/notifications/subscribe.md) 骤，请按照教程订阅通知。

>[!IMPORTANT]
>
>在订阅过程中，请确保选择 **[!UICONTROL 平台通知]** 作为事件提供者，并在出现提 **[!UICONTROL 示时选择数]** 据摄取通知事件订阅。

## 接收数据获取通知

成功注册Webhook且已摄取新数据后，您可以开始接收事件通知。 这些事件可以使用Webhook本身进行查看，也可以通过在Adobe开 **[!UICONTROL 发人员控制台中]** ，选择项目事件注册概述中的“调试跟踪”选项卡进行查看。

以下JSON是通知有效负荷的示例，在批量摄取事件失败时，通知有效负荷将发送到您的Webhook:

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
| `event_id` | 通知的唯一、由系统生成的ID。 |
| `event` | 一个对象，其中包含触发通知的事件的详细信息。 |
| `event.xdm:datasetId` | 摄取事件所应用的数据集的ID。 |
| `event.xdm:eventCode` | 状态代码，指示为数据集触发的事件类型。 有关特定 [值](#event-codes) 及其定义，请参阅附录。 |

要视图事件通知的完整模式，请参 [阅公共GitHub存储库](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json)。

## 后续步骤

在将通知注 [!DNL Platform] 册到项目后，您可以视图从项目概述中收 [!UICONTROL 到的事件]。 有关如何跟踪 [Adobe的详细说明](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) ，请参阅事件I/O事件跟踪指南。

## 附录

以下部分包含有关解释数据获取通知有效负荷的其他信息。

### 可用状态通知事件 {#event-codes}

下表列表了可供订阅的可用数据获取状态通知。

| 事件代码 | 平台服务 | 状态 | 事件描述 |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | 成功将批摄取到数据集中 [!DNL Data Lake]。 |
| `ing_load_failure` | [!DNL Data Ingestion] | 失败 | 无法将批摄取到数据集中 [!DNL Data Lake]。 |
| `ps_load_success` | [!DNL Real-time Customer Profile] | success | 已成功将批引入数据 [!DNL Profile] 存储中。 |
| `ps_load_failure` | [!DNL Real-time Customer Profile] | 失败 | 未能将批处理引入数据 [!DNL Profile] 存储。 |
| `ig_load_success` | [!DNL Identity Service] | success | 数据已成功加载到标识图中。 |
| `ig_load_failure` | [!DNL Identity Service] | 失败 | 数据无法加载到标识图中。 |

>[!NOTE]
>
>只为所有数据获取通知提供一个事件主题。 为了区分不同的状态，可以使用事件代码。