---
keywords: Experience Platform；主页；热门主题；数据摄取通知；通知；订阅事件；数据摄取状态事件；状态事件；订阅；状态通知；
solution: Experience Platform
title: 数据摄取通知
description: 为了帮助监控摄取过程，Adobe Experience Platform允许订阅由摄取过程的每个步骤发布的一组事件，向您通知摄取数据的状态和任何可能的失败。
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
source-git-commit: 76ef5638316a89aee1c6fb33370af943228b75e1
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 1%

---

# 数据摄取通知

将数据摄取到Adobe Experience Platform的过程由多个步骤组成。 确定需要引入的数据文件后 [!DNL Platform]，摄取过程随即开始，每个步骤都连续进行，直到成功摄取数据或数据失败为止。 可以使用启动摄取过程 [Adobe Experience Platform批量摄取API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) 或使用 [!DNL Experience Platform] 用户界面。

数据加载到 [!DNL Platform] 必须经过多个步骤才能到达其目标，即 [!DNL Data Lake] 或 [!DNL Real-Time Customer Profile] 数据存储。 每个步骤都涉及处理数据、验证数据，然后存储数据，然后再将其传递到下一个步骤。 根据所摄取的数据量，此过程可能会变成一个耗时的过程，并且始终有可能由于验证、语义或处理错误而失败。 如果出现故障，则需要修复数据问题，然后必须使用纠正的数据文件重新启动整个摄取过程。

为了帮助监测摄取过程， [!DNL Experience Platform] 使您可以订阅该过程的每个步骤发布的一组事件，向您通知摄取数据的状态和任何可能的故障。

## 注册webhook以获取数据摄取通知

要接收数据摄取通知，您必须使用 [Adobe Developer控制台](https://www.adobe.com/go/devs_console_ui) 将webhook注册到Experience Platform集成。

请阅读以下教程： [订阅 [!DNL Adobe I/O Event] 通知](../../observability/alerts/subscribe.md) 有关如何完成此操作的详细步骤。

>[!IMPORTANT]
>
>在订阅过程中，请确保选择 **[!UICONTROL 平台通知]** 作为事件提供程序，然后选择 **[!UICONTROL 数据摄取通知]** 事件订阅（出现提示时）。

## 接收数据摄取通知

成功注册webhook并摄取新数据后，即可开始接收事件通知。 可以使用webhook本身或通过选择 **[!UICONTROL 调试跟踪]** Adobe Developer选项卡。

以下JSON是在批量摄取事件失败的情况下发送到webhook的通知有效负载示例：

```json
{
  "event_id": "93a5b11a-b0e6-4b29-ad82-81b1499cb4f2",
  "event": {
    "xdm:ingestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:customerIngestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:imsOrg": "{ORG_ID}",
    "xdm:completed": 1598374341560,
    "xdm:datasetId": "5e55b556c2ae4418a8446037",
    "xdm:eventCode": "ing_load_failure",
    "xdm:sandboxName": "prod",
    "sentTime": "1598374341595",
    "processStartTime": 1598374342614,
    "transformedTime": 1598374342621,
    "header": {
      "_adobeio": {
        "imsOrgId": "{ORG_ID}",
        "providerMetadata": "aep_observability_catalog_events",
        "eventCode": "platform_event"
      }
    }
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `event_id` | 系统为通知生成的唯一ID。 |
| `event` | 包含触发通知的事件详细信息的对象。 |
| `event.xdm:datasetId` | 提取事件应用于的数据集的ID。 |
| `event.xdm:eventCode` | 状态代码，指示为数据集触发的事件类型。 请参阅 [附录](#event-codes) 的特定值及其定义。 |

要查看事件通知的完整模式，请参阅 [公共GitHub存储库](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json).

## 后续步骤

注册后 [!DNL Platform] 通知您的项目，您可以从 [!UICONTROL 项目概述]. 请参阅指南，网址为 [跟踪Adobe I/O事件](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) 以获取有关如何跟踪事件的详细说明。

## 附录

以下部分包含有关解释数据摄取通知有效负载的其他信息。

### 可用状态通知事件 {#event-codes}

下表列出了您可以订阅的可用数据摄取状态通知。

| 事件代码 | 平台服务 | 状态 | 事件描述 |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | 已成功将批次摄取到 [!DNL Data Lake]. |
| `ing_load_failure` | [!DNL Data Ingestion] | 失败 | 批次无法摄取到的数据集内 [!DNL Data Lake]. |
| `ps_load_success` | [!DNL Real-Time Customer Profile] | success | 批次已成功引入 [!DNL Profile] 数据存储。 |
| `ps_load_failure` | [!DNL Real-Time Customer Profile] | 失败 | 无法将批次摄取到 [!DNL Profile] 数据存储。 |
| `ig_load_success` | [!DNL Identity Service] | success | 数据已成功加载到身份图中。 |
| `ig_load_failure` | [!DNL Identity Service] | 失败 | 未能将数据加载到身份图中。 |

>[!NOTE]
>
>对于所有数据摄取通知，仅提供一个事件主题。 为了区分不同的状态，可以使用事件代码。
