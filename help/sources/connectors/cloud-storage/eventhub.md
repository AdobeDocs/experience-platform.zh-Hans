---
keywords: Experience Platform；首頁；熱門主題；Azure事件中樞；Azure事件中樞；事件中樞；事件中樞
solution: Experience Platform
title: Azure事件中樞來源聯結器總覽
description: 瞭解如何使用API或使用者介面將Azure事件中樞連線至Adobe Experience Platform。
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# [!DNL Azure Event Hubs] 聯結器

Adobe Experience Platform為AWS等雲端服務供應商提供原生連線， [!DNL Google Cloud Platform]、和 [!DNL Azure]. 您可以將資料從這些系統帶入Platform。

雲端儲存空間來源可將您自己的資料帶入Platform，而不需要下載、格式化或上傳。 內嵌的資料可以格式化為XDM JSON、XDM Parquet或分隔。 流程的每個步驟都會整合至來源工作流程。 Platform可讓您從匯入資料 [!DNL Event Hubs] 即時。

## 縮放方式 [!DNL Event Hubs]

的縮放因數 [!DNL Event Hubs] 如果您需要擷取大量資料、增加平行度或提高擷取平台的速度，則必須增加執行個體。

### 匯入較大量的資料

目前，您可從以下專案取得的最大資料量： [!DNL Event Hubs] account to Platform是每秒2000筆記錄。 若要擴充並擷取較大量的資料，請聯絡您的Adobe代表。

### 增加上的平行度 [!DNL Event Hubs] 和Platform

平行程度是指在多個處理單元上同時執行相同工作，以提高速度和效能。 您可以增加上的平行度 [!DNL Event Hubs] 增加分割區或取得更多處理單元 [!DNL Event Hubs] 帳戶。 檢視此 [[!DNL Event Hubs] 縮放檔案](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability) 以取得詳細資訊。

若要提高平台端的擷取速度，平台必須增加來源聯結器中讀取的任務數量。 [!DNL Event Hubs] 資料分割。 一旦您增加 [!DNL Event Hubs] 另外，請聯絡您的Adobe代表，以根據您的新磁碟分割調整平台任務。 目前，此程式尚未自動化。

## 使用虛擬網路連線到 [!DNL Event Hubs] 至平台

您可以設定要連線的虛擬網路 [!DNL Event Hubs] 至Platform，同時啟用防火牆測量。 若要設定虛擬網路，請前往此 [[!DNL Event Hubs] 網路規則集檔案](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set#code-try-0) 並遵循下列步驟：

* 選取 **試試看** 從REST API面板；
* 驗證您的 [!DNL Azure] 在相同瀏覽器中使用您憑證的帳戶；
* 選取 [!DNL Event Hubs] 名稱空間、資源群組和訂閱，然後選取「 」 **執行**；
* 在出現的JSON內文中，將下列Platform子網路新增至 `virtualNetworkRules` 裡面 `properties`：


>[!IMPORTANT]
>
>您必須先備份收到的JSON內文，才能進行更新 `virtualNetworkRules` 使用Platform子網路，因為它包含您現有的IP篩選規則。 否則，將在呼叫後刪除規則。


```json
{
    "subnet": {
        "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
    },
    "ignoreMissingVnetServiceEndpoint": true
}
```

有關Platform子網路的不同區域，請參閱以下清單：

### VA7：北美

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### NLD2：歐洲

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
            "id": "/subscriptions/40bde086-46ad-44c3-afba-c306f54b64ec/resourceGroups/ethos_12_prod_nld2_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_nld2_network_10_20_40_0_23/subnets/ethos_12_prod_nld2_network_10_20_40_0_23"
        }, 
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### AUS5：澳洲

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/1618ef18-9edc-48bf-88dd-61cc979629b5/resourceGroups/ethos_12_prod_aus5_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_aus5_network_10_21_116_0_22/subnets/ethos_12_prod_aus5_network_10_21_116_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

請參閱下列內容 [[!DNL Event Hubs] 檔案](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set) 以取得網路規則集的詳細資訊。

## Connect [!DNL Event Hubs] 至平台

以下檔案提供有關如何連線的資訊 [!DNL Event Hubs] 使用API或使用者介面的to Platform：

### 使用API

* [使用流程服務API建立事件中樞來源連線](../../tutorials/api/create/cloud-storage/eventhub.md)
* [使用流量服務API收集串流資料](../../tutorials/api/collect/streaming.md)

### 使用UI

* [在UI中建立事件中樞來源連線](../../tutorials/ui/create/cloud-storage/eventhub.md)
* [在UI中設定雲端儲存體連線的資料流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
