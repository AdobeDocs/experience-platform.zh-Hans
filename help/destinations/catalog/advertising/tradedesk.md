---
keywords: 廣告；交易台；廣告交易台
title: 交易台連線
description: Trade Desk是廣告購買者的自助服務平台，可跨顯示器、影片和行動詳細目錄來源執行重新定位和以對象為目標的數位行銷活動。
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 2%

---

# [!DNL The Trade Desk] 連線

## 概述 {#overview}

[!DNL The Trade Desk] 目的地可協助您將設定檔資料傳送至 [!DNL The Trade Desk].

[!DNL The Trade Desk] 是一個自助式平台，供廣告購買者跨顯示器、影片和行動詳細目錄來源執行重新定位和以對象為目標的數位行銷活動。

若要將設定檔資料傳送至 [!DNL Trade Desk]，您必須先連線至目的地。

## 用例 {#use-cases}

身為行銷人員，我想能夠使用以下專案建立的區段： [!DNL Trade Desk IDs] 或裝置ID來建立重新定位或對象定位的數位行銷活動。

## 支援的身分 {#supported-identities}

[!DNL The Trade Desk] 支援下表所述的身分啟用。 進一步瞭解 [身分](/help/identity-service/namespaces.md).

| 目標身分 | 描述 |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| 交易台ID | Trade Desk平台中的廣告商ID |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 区段导出]** | 您正在將區段（受眾）的所有成員匯出至目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦設定檔根據區段評估在Experience Platform中更新，聯結器就會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

>[!IMPORTANT]
>
>如果您想要使用建立您的第一個目的地 [!DNL The Trade Desk] 且尚未啟用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 若是過去的Experience CloudID服務(使用Adobe Audience Manager或其他應用程式)，請聯絡Adobe諮詢或客戶服務以啟用ID同步。 如果您先前已設定 [!DNL The Trade Desk] Audience Manager中的整合，您所設定的ID同步會結轉到Platform。

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md).

### 連線引數 {#parameters}

當 [設定](../../ui/connect-destination.md) 您必須提供下列資訊：

* **[!UICONTROL 名稱]**：您日後用來辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL 帳戶ID]**：您的 [!DNL Trade Desk] [!UICONTROL 帳戶ID].
* **[!UICONTROL 伺服器位置]**：詢問您的 [!DNL Trade Desk] 代表您應使用的地區伺服器。 這些是您可選擇使用的地區伺服器：
   * **[!UICONTROL 欧洲]**
   * **[!UICONTROL 新加坡]**
   * **[!UICONTROL 东京]**
   * **[!UICONTROL 北美東部]**
   * **[!UICONTROL 北美西部]**
   * **[!UICONTROL 拉丁美洲]**

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

另請參閱 [啟用串流區段匯出目的地的受眾資料](../../ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地的受眾區段的指示。

在 [區段排程](../../ui/activate-segment-streaming-destinations.md#scheduling) 步驟，您必須手動將區段對應至目的地平台中其對應的ID或易記名稱。

對應區段時，建議您使用Platform區段名稱或較短的形式，以方便使用。 不過，目的地中的區段ID或名稱不需要與您的Platform帳戶中的相符專案。 您在對應欄位中插入的任何值都會反映在目的地中。

如果您使用多個裝置對應(Cookie ID、 [!DNL IDFA]， [!DNL GAID])，請確定所有這三個對應都使用相同的對應值。 [!DNL The Trade Desk] 會將其彙總至單一區段，並包含裝置層級的劃分。

![區段對應ID](../../assets/common/segment-mapping-id.png)

## 匯出的資料 {#exported-data}

驗證資料是否已成功匯出至 [!DNL The Trade Desk] 目的地，檢查您的 [!DNL Trade Desk] 帳戶。 如果成功啟用，系統會將對象填入您的帳戶。
