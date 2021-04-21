---
keywords: Experience Platform；主页；热门主题；数据摄取通知；通知；订阅事件；数据摄取状态事件；状态事件；订阅；状态通知；
solution: Experience Platform
title: 数据摄取通知
topic-legacy: overview
description: 为了帮助监视摄取过程，Adobe Experience Platform允许订阅在该过程的每个步骤发布的一组事件，通知您所摄取数据的状态和任何可能的故障。
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 1%

---

# 数据获取通知

将数据引入Adobe Experience Platform的过程由多个步骤组成。 一旦确定需要收录到[!DNL Platform]中的数据文件，摄取过程即开始，每个步骤都会连续进行，直到数据被成功摄取或失败。 可以使用[Adobe Experience Platform Data Ingestion API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)或使用[!DNL Experience Platform]用户界面启动摄取过程。

加载到[!DNL Platform]中的数据必须经过多个步骤才能到达其目标、[!DNL Data Lake]或[!DNL Real-time Customer Profile]数据存储。 每个步骤都涉及处理数据、验证数据，然后在将数据传递到下一步之前存储数据。 根据所摄取的数据量，这可能会成为一个耗时的过程，并且始终有可能该过程因验证、语义或处理错误而失败。 在出现故障事件，需要修复数据问题，然后必须使用更正的数据文件重新启动整个摄取过程。

为了帮助监视摄取过程，[!DNL Experience Platform]使订阅一组由该过程的每个步骤发布的事件，通知您所摄取数据的状态和任何可能的故障。

## 注册网络挂钩以接收数据获取通知

要接收Adobe获取通知，您必须使用[Experience Platform开发者控制台](https://www.adobe.com/go/devs_console_ui)来注册网络挂接以进行集成。

有关如何实现此操作的详细步骤，请按照[订阅 [!DNL Adobe I/O Event] 通知](../../observability/notifications/subscribe.md)的教程进行操作。

>[!IMPORTANT]
>
>在订阅过程中，请确保选择&#x200B;**[!UICONTROL Platform notifications]**&#x200B;作为事件提供者，并在出现提示时选择&#x200B;**[!UICONTROL Data ingestion notification]**&#x200B;事件订阅。

## 接收数据获取通知

成功注册Webhook且已摄取新数据后，即可开始接收事件通知。 这些事件可以使用Webhook本身查看，或通过在Adobe开发人员控制台中选择项目事件注册概述中的&#x200B;**[!UICONTROL Debug Tracing]**&#x200B;选项卡来查看。

以下JSON是通知有效负荷的示例，在批处理摄取事件失败时，将发送到您的Webhook:

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
| `event.xdm:datasetId` | 应用摄取事件的数据集的ID。 |
| `event.xdm:eventCode` | 状态代码，指示为数据集触发的事件类型。 请参见[附录](#event-codes)以了解特定值及其定义。 |

要视图事件通知的完整模式，请参阅[公共GitHub存储库](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json)。

## 后续步骤

将[!DNL Platform]通知注册到项目后，即可视图从[!UICONTROL Project overview]收到的事件。 有关如何跟踪Adobe I/O的详细说明，请参阅[跟踪事件](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md)上的指南。

## 附录

以下部分包含有关解释数据摄取通知有效负载的其他信息。

### 可用状态通知事件{#event-codes}

下表列表了可供订阅的可用数据摄取状态通知。

| 事件代码 | 平台服务 | 状态 | 事件描述 |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | 已成功将批处理引入[!DNL Data Lake]中的数据集。 |
| `ing_load_failure` | [!DNL Data Ingestion] | 失败 | 未能将批处理引入[!DNL Data Lake]中的数据集。 |
| `ps_load_success` | [!DNL Real-time Customer Profile] | 成功 | 已成功将批处理引入[!DNL Profile]数据存储中。 |
| `ps_load_failure` | [!DNL Real-time Customer Profile] | 失败 | 未能将批处理引入[!DNL Profile]数据存储中。 |
| `ig_load_success` | [!DNL Identity Service] | 成功 | 已成功将数据加载到标识图中。 |
| `ig_load_failure` | [!DNL Identity Service] | 失败 | 无法将数据加载到标识图中。 |

>[!NOTE]
>
>只为所有事件获取通知提供了一个数据主题。 为了区分不同的状态，可以使用事件代码。
