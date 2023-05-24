---
keywords: Experience Platform；目的地api；隨選啟用；隨選啟用區段
solution: Experience Platform
title: 透過臨時啟用API將受眾區段啟用至批次目的地
description: 本文說明透過臨機啟動API啟動對象區段的端對端工作流程，包括啟動前發生的細分工作。
type: Tutorial
exl-id: 1a09f5ff-0b04-413d-a9f6-57911a92b4e4
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 1%

---

# 透過Ad Hoc Activation API依需求對批次目的地啟用對象區段

>[!IMPORTANT]
>
>完成Beta版階段後， [!DNL ad-hoc activation API] 現已正式向所有Experience Platform客戶提供(GA)。 在GA版本中，API已升級至版本2。 步驟4 ([取得最新的區段匯出作業ID](#segment-export-id))不再是必要專案，因為API不再要求匯出ID。
>
>另請參閱 [執行隨選啟動工作](#activation-job) 如需詳細資訊，請參閱本教學課程底下的內容。

## 概述 {#overview}

隨選啟用API可讓行銷人員針對需要立即啟用的情況，以快速且有效率的方式以程式設計方式啟用目的地的受眾區段。

使用Ad Hoc Activation API將完整檔案匯出至您想要的檔案接收系統。 僅支援隨選對象啟用 [批次檔案型目的地](../destination-types.md#file-based).

下圖說明透過臨時啟用API啟用區段的端對端工作流程，包括每24小時在Platform中發生的區段工作。

![臨機啟動](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)



## 用例 {#use-cases}

### Flash銷售或促銷

一家線上零售商正在準備進行限量搶購，並希望在短時間內通知客戶。 透過Experience Platform隨選啟用API，行銷團隊可依需求匯出區段，並快速傳送促銷電子郵件給客戶群。

### 最新事件或突發新聞

一家飯店預計接下來幾天會有惡劣天氣，而團隊想要迅速通知到來的客人，以便他們做出相應的計畫。 行銷團隊可以使用Experience Platform臨機啟動API來隨選匯出區段，並通知來賓。

### 整合測試

IT管理員可使用Experience Platform隨選啟用API來隨選匯出區段，以便測試其與Adobe Experience Platform的自訂整合，並確保一切都正常運作。

## 护栏 {#guardrails}

使用臨機啟動API時，請牢記以下護欄。

* 目前，每個隨選啟動工作最多可啟動80個區段。 嘗試為每個工作啟動超過80個區段會導致工作失敗。 未來版本可能會對此行為有所變更。
* 臨機操作啟動工作無法與排程同時執行 [區段匯出工作](../../segmentation/api/export-jobs.md). 在執行臨機啟動工作之前，請確定已排程的區段匯出工作已完成。 另請參閱 [目的地資料流監視](../../dataflows/ui/monitor-destinations.md) 以取得如何監視啟動流程狀態的資訊。 例如，若您的啟動資料流顯示 **[!UICONTROL 處理中]** 狀態，請等待它完成後再執行臨機操作啟動工作。
* 每個區段請勿執行超過一個並行臨機啟動工作。

## 區段考量事項 {#segmentation-considerations}

Adobe Experience Platform每24小時執行一次排程的區段工作。 隨選啟用API會根據最新的細分結果執行。

## 步驟1：必要條件 {#prerequisites}

呼叫Adobe Experience Platform API之前，請確定您符合下列先決條件：

* 您擁有可存取Adobe Experience Platform的組織帳戶。
* 您的Experience Platform帳戶具有 `developer` 和 `user` Adobe Experience Platform API產品設定檔啟用的角色。 聯絡您的 [Admin Console](../../access-control/home.md) 管理員為您的帳戶啟用這些角色。
* 您有Adobe ID。 如果您沒有Adobe ID，請前往 [Adobe Developer主控台](https://developer.adobe.com/console) 並建立新帳戶。

## 步驟2：收集認證 {#credentials}

若要對Platform API發出呼叫，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會提供所有Experience PlatformAPI呼叫中每個必要標題的值，如下所示：

* 授權：持有人 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Experience Platform中的資源可隔離至特定的虛擬沙箱。 在對Platform API的請求中，您可以指定將在其中執行操作的沙箱的名稱和ID。 這些是選用引數。

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需Experience Platform中沙箱的詳細資訊，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的媒體型別標頭：

* Content-Type: `application/json`

## 步驟3：在Platform UI中建立啟用流程 {#activation-flow}

您必須先在平台UI中針對所選目的地設定啟用流程，才能透過隨選啟用API啟用區段。

這包括進入啟動工作流程、選取區段、設定排程並啟動。 您可以使用UI或API來建立啟用流程：

* [使用Platform UI建立批次設定檔匯出目的地的啟用流程](../ui/activate-batch-profile-destinations.md)
* [使用流程服務API來連線到批次設定檔匯出目的地並啟用資料](../api/connect-activate-batch-destinations.md)

## 步驟4：取得最新的區段匯出作業ID （v2中不需要） {#segment-export-id}

>[!IMPORTANT]
>
>在v2的臨機啟動API中，您不需要取得最新的區段匯出作業ID。 您可以略過此步驟，繼續下一個步驟。

當您為批次目的地設定啟動流程後，排程的分段作業會每24小時自動執行一次。

您必須先取得最新區段匯出作業的ID，才能執行隨選啟動作業。 您必須在隨選啟動工作請求中傳遞此ID。

請依照說明操作 [此處](../../segmentation/api/export-jobs.md#retrieve-list) 以擷取所有區段匯出作業的清單。

在回應中，尋找包含下列結構描述屬性的第一個記錄。

```
"schema":{
   "name":"_xdm.context.profile"
}
```

區段匯出作業ID位於 `id` 屬性，如下所示。

![區段匯出作業ID](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## 步驟5：執行隨選啟動工作 {#activation-job}

Adobe Experience Platform每24小時執行一次排程的區段工作。 隨選啟用API會根據最新的細分結果執行。

>[!IMPORTANT]
>
>請注意下列一次性限制：在執行隨選啟動工作之前，請確定根據您設定的排程，從區段首次啟動之日起已過去至少20分鐘 [步驟3 — 在Platform UI中建立啟動流程](#activation-flow).

在執行臨機啟動工作之前，請確定已排程區段的區段匯出工作已完成。 另請參閱 [目的地資料流監視](../../dataflows/ui/monitor-destinations.md) 以取得如何監視啟動流程狀態的資訊。 例如，若您的啟動資料流顯示 **[!UICONTROL 處理中]** 狀態，請等待它完成後再執行臨機操作啟動工作以匯出完整檔案。

區段匯出作業完成後，您可以觸發啟動。

>[!NOTE]
>
>目前，每個隨選啟動工作最多可啟動80個區段。 嘗試為每個工作啟動超過80個區段會導致工作失敗。 未來版本可能會對此行為有所變更。

### 请求 {#request}

>[!IMPORTANT]
>
>必須包含 `Accept: application/vnd.adobe.adhoc.activation+json; version=2` 標頭來使用Ad Hoc Activation API v2。

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun' \
--header 'x-gw-ims-org-id: 5555467B5D8013E50A494220@AdobeOrg' \
--header 'Authorization: Bearer {{token}}' \
--header 'x-sandbox-id: 6ef74723-3ee7-46a4-b747-233ee7a6a41a' \
--header 'x-sandbox-name: {sandbox-id}' \
--header 'Accept: application/vnd.adobe.adhoc.activation+json; version=2' \
--header 'Content-Type: application/json' \
--data-raw '{
   "activationInfo":{
      "destinationId1":[
         "segmentId1",
         "segmentId2"
      ],
      "destinationId2":[
         "segmentId2",
         "segmentId3"
      ]
   }
}'
```

| 属性 | 描述 |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | 您要對其啟用區段的目的地執行個體的ID。 您可以導覽至，從Platform UI取得這些ID **[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]** 標籤，然後按一下所需的目的地列，在右側邊欄中顯示目的地ID。 如需詳細資訊，請閱讀 [目的地工作區檔案](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | 您要啟用至所選目的地的區段ID。 |

{style="table-layout:auto"}

### 具有匯出ID的請求（將棄用） {#request-deprecated}

>[!IMPORTANT]
>
>**已棄用的請求型別**. 此範例型別說明API版本1的要求型別。 在臨機啟動API的v2中，您不需要包含最新的區段匯出作業ID。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -d '
{
   "activationInfo":{
      "destinationId1":[
         "segmentId1",
         "segmentId2"
      ],
      "destinationId2":[
         "segmentId2",
         "segmentId3"
      ]
   },
   "exportIds":[
      "exportId1"
   ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | 您要對其啟用區段的目的地執行個體的ID。 您可以導覽至，從Platform UI取得這些ID **[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]** 標籤，然後按一下所需的目的地列，在右側邊欄中顯示目的地ID。 如需詳細資訊，請閱讀 [目的地工作區檔案](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | 您要啟用至所選目的地的區段ID。 |
| <ul><li>`exportId1`</li></ul> | 回應中傳回的ID [區段匯出](../../segmentation/api/export-jobs.md#retrieve-list) 工作。 另請參閱 [步驟4：取得最新的區段匯出作業ID](#segment-export-id) 以取得有關如何尋找此ID的說明。 |

{style="table-layout:auto"}

### 响应 {#response}

成功的回應會傳回HTTP狀態200。

```shell
{
   "order":[
      {
         "segment":"db8961e9-d52f-45bc-b3fb-76d0382a6851",
         "order":"ef2dcbd6-36fc-49a3-afed-d7b8e8f724eb",
         "statusURL":"https://platform.adobe.io/data/foundation/flowservice/runs/88d6da63-dc97-460e-b781-fc795a7386d9"
      }
   ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `segment` | 已啟動區段的ID。 |
| `order` | 區段啟用的目的地識別碼。 |
| `statusURL` | 啟動流程的狀態URL。 您可以使用以下專案追蹤流程進度： [流程服務API](../../sources/tutorials/api/monitor.md). |

{style="table-layout:auto"}

## API錯誤處理 {#api-error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../landing/troubleshooting.md#request-header-errors) （在平台疑難排解指南中）。

### API錯誤代碼和特定於Ad Hoc Activation API的訊息 {#specific-error-messages}

使用臨機啟動API時，您可能會遇到特定於此API端點的錯誤訊息。 請檢閱表格以瞭解如何在它們出現時解決它們。

| 错误消息 | 解决方法 |
|---------|----------|
| 已為區段執行 `segment ID` 訂購 `dataflow ID` 具有執行id `flow run ID` | 此錯誤訊息指出區段的隨選啟用流程目前正在進行中。 再次觸發啟動工作之前，請等待工作完成。 |
| 區段 `<segment name>` 不是此資料流的一部分或超出排程範圍！ | 此錯誤訊息指出您選取要啟動的區段未對應至資料流，或是為區段設定的啟動排程已過期或尚未開始。 檢查區段是否確實對應至資料流，並確認區段啟用排程與目前日期重疊。 |

## 相關資訊 {#related-information}

* [使用流程服務API連線到批次目的地並啟用資料](/help/destinations/api/connect-activate-batch-destinations.md)
* [（測試版）使用Experience PlatformUI隨選將檔案匯出至批次目的地](/help/destinations/ui/export-file-now.md)