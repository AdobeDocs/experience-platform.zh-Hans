---
keywords: Experience Platform；首頁；熱門主題；資料擷取通知；通知；訂閱事件；資料擷取狀態事件；狀態事件；訂閱；狀態通知；
solution: Experience Platform
title: 資料擷取通知
description: 為協助監控擷取程式，Adobe Experience Platform可讓您訂閱由程式的每個步驟發佈的一組事件，通知您擷取資料的狀態和任何可能的失敗。
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
source-git-commit: 76ef5638316a89aee1c6fb33370af943228b75e1
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 1%

---

# 資料擷取通知

將資料內嵌至Adobe Experience Platform的程式由多個步驟組成。 識別需要內嵌到中的資料檔案後 [!DNL Platform]，擷取程式隨即開始，每個步驟會連續進行，直到資料成功擷取或失敗為止。 內嵌程式可透過以下方式啟動： [Adobe Experience Platform批次擷取API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) 或使用 [!DNL Experience Platform] 使用者介面。

資料載入到 [!DNL Platform] 必須執行多個步驟才能到達其目的地： [!DNL Data Lake] 或 [!DNL Real-Time Customer Profile] 資料存放區。 每個步驟都涉及處理資料、驗證資料，然後儲存資料，再將其傳遞至下一個步驟。 根據所擷取的資料量，這會成為一個耗時的程式，而且該程式總是有可能因驗證、語意或處理錯誤而失敗。 如果失敗，則需要修正資料問題，然後必須使用修正的資料檔案重新啟動整個擷取程式。

若要協助監控擷取程式， [!DNL Experience Platform] 可讓您訂閱流程每個步驟所發佈的一組事件，通知您所擷取資料的狀態和任何可能的失敗。

## 註冊webhook以取得資料擷取通知

若要接收資料擷取通知，您必須使用 [Adobe Developer主控台](https://www.adobe.com/go/devs_console_ui) 將webhook註冊到您的Experience Platform整合。

請依照上的教學課程進行 [訂閱 [!DNL Adobe I/O Event] 通知](../../observability/alerts/subscribe.md) 以取得如何完成此作業的詳細步驟。

>[!IMPORTANT]
>
>在訂閱程式期間，請確定您選取 **[!UICONTROL 平台通知]** 作為事件提供者，並選取 **[!UICONTROL 資料擷取通知]** 出現提示時，提供事件訂閱。

## 接收資料擷取通知

成功註冊webhook並擷取新資料後，您就可以開始接收事件通知。 您可以使用webhook本身或選取 **[!UICONTROL 偵錯追蹤]** 索引標籤(位於您專案的Adobe Developer Console中的事件註冊概覽中)。

以下JSON為通知裝載的範例，此裝載會在批次擷取事件失敗的情況下傳送至您的webhook：

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
| `event_id` | 系統產生的通知唯一ID。 |
| `event` | 包含觸發通知之事件詳細資料的物件。 |
| `event.xdm:datasetId` | 要套用內嵌事件的資料集ID。 |
| `event.xdm:eventCode` | 狀態代碼，指出針對資料集觸發的事件型別。 請參閱 [附錄](#event-codes) 以取得特定值及其定義。 |

若要檢視事件通知的完整結構描述，請參閱 [公用GitHub存放庫](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json).

## 后续步骤

註冊之後 [!DNL Platform] 通知您的專案，您可以檢視收到的以下事件： [!UICONTROL 專案概述]. 請參閱以下指南： [追蹤Adobe I/O事件](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) 以取得有關如何追蹤事件的詳細指示。

## 附录

下節包含有關解譯資料擷取通知裝載的額外資訊。

### 可用的狀態通知事件 {#event-codes}

下表列出您可以訂閱的可用資料擷取狀態通知。

| 事件代碼 | 平台服務 | 状态 | 事件描述 |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | 批次已成功內嵌至的資料集 [!DNL Data Lake]. |
| `ing_load_failure` | [!DNL Data Ingestion] | 失敗 | 批次無法內嵌到資料集中 [!DNL Data Lake]. |
| `ps_load_success` | [!DNL Real-Time Customer Profile] | success | 批次已成功內嵌至 [!DNL Profile] 資料存放區。 |
| `ps_load_failure` | [!DNL Real-Time Customer Profile] | 失敗 | 無法將批次擷取到 [!DNL Profile] 資料存放區。 |
| `ig_load_success` | [!DNL Identity Service] | success | 資料已成功載入身分圖表。 |
| `ig_load_failure` | [!DNL Identity Service] | 失敗 | 資料無法載入身分圖表。 |

>[!NOTE]
>
>所有資料擷取通知僅提供一個事件主題。 為了區分不同的狀態，可以使用事件程式碼。
