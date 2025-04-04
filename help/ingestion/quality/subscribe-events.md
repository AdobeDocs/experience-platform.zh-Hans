---
keywords: Experience Platform；主页；热门主题；数据摄取通知；通知；订阅事件；数据摄取状态事件；状态事件；订阅；状态通知；
solution: Experience Platform
title: 数据摄取通知
description: 为了协助监控摄取过程，Adobe Experience Platform允许订阅由流程的每个步骤发布的一组事件，向您通知摄取数据的状态和任何可能的失败。
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 1%

---

# 数据摄取通知

将数据摄取到Adobe Experience Platform的过程包括多个步骤。 确定需要摄取到[!DNL Experience Platform]中的数据文件后，摄取过程将开始，每个步骤将连续进行，直到数据成功摄取或失败。 可以使用[Adobe Experience Platform批量摄取API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)或使用[!DNL Experience Platform]用户界面启动摄取过程。

加载到[!DNL Experience Platform]的数据必须经过多个步骤才能到达其目标、[!DNL Data Lake]或[!DNL Real-Time Customer Profile]数据存储。 每个步骤都涉及处理数据、验证数据，然后存储数据，然后再将其传递到下一个步骤。 根据摄取的数据量，此过程可能会成为一个耗时的过程，并且始终存在因验证、语义或处理错误而失败的可能性。 如果失败，则需要修复数据问题，然后必须使用更正的数据文件重新启动整个摄取过程。

为了协助监视摄取过程，[!DNL Experience Platform]允许订阅由过程的每个步骤发布的一组事件，通知您摄取数据的状态和任何可能的失败。

## 注册webhook以获取数据摄取通知

若要接收数据摄取通知，您必须使用[Adobe Developer Console](https://www.adobe.com/go/devs_console_ui)注册webhook以将其添加到您的Experience Platform集成。

请阅读有关[订阅 [!DNL Adobe I/O Event] 通知](../../observability/alerts/subscribe.md)的教程，以了解有关如何完成此操作的详细步骤。

>[!IMPORTANT]
>
>在订阅过程中，请确保选择&#x200B;**[!UICONTROL 平台通知]**&#x200B;作为事件提供程序，并在出现提示时选择&#x200B;**[!UICONTROL 数据摄取通知]**&#x200B;事件订阅。

## 接收数据摄取通知

成功注册webhook并摄取新数据后，即可开始接收事件通知。 可以使用webhook本身或通过在Adobe Developer Console中选择项目事件注册概述中的&#x200B;**[!UICONTROL 调试跟踪]**&#x200B;选项卡来查看这些事件。

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
| `event.xdm:eventCode` | 状态代码，指示为数据集触发的事件类型。 有关特定值及其定义，请参阅[附录](#event-codes)。 |

要查看事件通知的完整架构，请参阅[公共GitHub存储库](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json)。

## 后续步骤

向项目注册[!DNL Experience Platform]通知后，您可以从[!UICONTROL 项目概述]查看接收的事件。 有关如何跟踪事件的详细说明，请参阅[跟踪Adobe I/O Events](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md)指南。

## 附录

以下部分包含有关解释数据摄取通知有效负载的其他信息。

### 可用状态通知事件 {#event-codes}

下表列出了您可以订阅的可用数据摄取状态通知。

| 事件代码 | Experience Platform服务 | 状态 | 事件描述 |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | 已成功将批次摄取到[!DNL Data Lake]内的数据集。 |
| `ing_load_failure` | [!DNL Data Ingestion] | 失败 | 无法将批次摄取到[!DNL Data Lake]内的数据集。 |
| `ps_load_success` | [!DNL Real-Time Customer Profile] | success | 已成功将批次摄取到[!DNL Profile]数据存储。 |
| `ps_load_failure` | [!DNL Real-Time Customer Profile] | 失败 | 无法将批次摄取到[!DNL Profile]数据存储。 |
| `ig_load_success` | [!DNL Identity Service] | success | 数据已成功加载到身份图中。 |
| `ig_load_failure` | [!DNL Identity Service] | 失败 | 未能将数据加载到身份图中。 |

>[!NOTE]
>
>对于所有数据摄取通知，只提供一个事件主题。 为了区分不同的状态，可以使用事件代码。
