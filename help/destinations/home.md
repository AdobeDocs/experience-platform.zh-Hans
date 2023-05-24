---
keywords: 目的地；adobe experience platform；平台；目的地概觀；啟用資料；啟用；
title: 目标概述
description: 目的地是預先建立的與目的地平台的整合，可無縫地從Adobe Experience Platform啟用資料。 您可以使用Adobe Experience Platform中的目的地，針對跨頻道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例，啟用已知和未知的資料。
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: 546758c419670746cf55de35cbb33131d4457cb9
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---

# [!DNL Destinations] 概述 {#overview}

![目的地概觀橫幅](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** 是預先建立的與目標平台的整合，可無縫啟用Adobe Experience Platform的資料。 您可以使用目的地，針對跨頻道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例，啟用已知和未知的資料。

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## 目的地和來源 {#destinations-and-sources}

Platform的核心功能之一，就是擷取您的第一方資料，並根據您的業務需求加以啟用。 使用 [來源](../sources/home.md) 將資料內嵌至Platform和目的地，以從Platform匯出資料。

## 目的地步驟 {#steps}

* 從 [自助服務目錄](./catalog/overview.md) Platform中可用的所有目的地。
* 使用目的地將設定檔或區段傳送至行銷自動化平台、數位廣告平台等。
* 排程資料定期匯出至您偏好的目的地。

## 控制項 {#controls}

中的控制項 [目的地工作區](./ui/destinations-workspace.md) 允許您：

* 瀏覽可啟用資料的目的地平台目錄；
* 建立、編輯、啟用和停用資料流到目錄中的目的地；
* 在儲存位置中建立帳戶，或將Platform連結至目的地平台中的帳戶；
* 選取應該對目的地啟用的區段；
* 選擇哪一個 [體驗資料模型(XDM)欄位](../xdm/home.md) 以於啟用區段至電子郵件行銷目的地時匯出。

## 目的地型別和類別 {#types-and-categories}

透過Experience Platform，您可以對各種型別的目的地啟用資料，以滿足您的啟用使用案例。 目標範圍從API式整合，到與檔案接收系統、設定檔查詢目的地等的整合。 如需所有可用目的地的詳細資訊，請參閱 [目的地型別和類別概觀](./destination-types.md).

## 目的地和存取控制 {#access-controls}

Platform中的目標功能可搭配Adobe Experience Platform存取控制許可權使用。 您可以檢視、管理和啟用目的地，實際取決於您的使用者許可權等級。 如需個別許可權的相關資訊，請參閱 [Adobe Experience Platform中的存取控制](../access-control/home.md) 並向下捲動至頁面底部。

下表概述對目的地執行特定動作所需的許可權和許可權組合：

| 許可權層級 | 描述 |
| ---- | ----|
| **[!UICONTROL 管理目的地]** | 若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). |
| **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** | 若要啟用目的地的區段並啟用 [對應步驟](ui/activate-batch-profile-destinations.md#mapping) 的工作流程中，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). |
| **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 啟用區段而不進行對應]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** | 若要對目的地啟用區段並隱藏 [對應步驟](ui/activate-batch-profile-destinations.md#mapping) 的工作流程中，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 啟用區段而不進行對應]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). |

{style="table-layout:auto"}

如需存取控制的詳細資訊，請參閱 [存取控制使用手冊](../access-control/ui/overview.md).

### 目的地的屬性型存取控制 {#attribute-based-access}

Adobe Experience Platform中基於屬性的存取控制可讓管理員根據屬性控制對特定物件和/或權能的存取。

透過以屬性為基礎的存取控制，您可以將對應設定套用至您擁有許可權的欄位。 此外，如果您無法存取資料集中的所有欄位，就無法將資料匯出至目的地。

如需目的地如何使用屬性型存取控制的詳細資訊，請參閱 [屬性型存取控制概觀](../access-control/abac/overview.md#destinations).

## 目的地監視 {#destinations-monitoring}

在建立與目的地的連線並完成啟動工作流程後，您可以監控匯出至接收系統的資料。 閱讀 [在UI中監控資料流到目的地的指南](/help/dataflows/ui/monitor-destinations.md) 以取得詳細資訊。

您也可以驗證資料是否成功到達您的目的地。 目錄中的大多數目的地檔案頁面都有 *驗證資料匯出區段*，可指示您如何從目的地平台簽入資料是否已成功從Experience Platform匯入。

## 將資料啟用至目的地的資料治理限制 {#data-governance}

透過下列方式，對Platform目的地強制執行資料控管：

* *行銷動作* 在「建立目的地」工作流程中選取的專案；
* *資料使用原則* 限制將包含特定使用標籤的資料啟用至具有特定行銷動作的目的地。

如需有關的詳細資訊，請參閱Platform檔案中的資料控管 [行銷動作](../data-governance/policies/overview.md) 和 [解決資料原則違規](../data-governance/enforcement/auto-enforcement.md).

如需在建立目標工作流程中選取行銷動作的詳細資訊，請參閱Platform中不同目標型別的下列頁面：

* [廣告目的地 — Google廣告管理員 ](./catalog/advertising/google-ad-manager.md)
* [Advertising目的地 — Google Ads](./catalog/advertising/google-ads-destination.md)
* [廣告目的地 — Google Display &amp; Video 360 ](./catalog/advertising/google-dv360.md)
* [雲端儲存空間目的地](./catalog/cloud-storage/overview.md)
* [電子郵件行銷目的地](./catalog/email-marketing/overview.md)
* [社交目的地](./catalog/social/overview.md)

如需區段啟用工作流程中資料原則違規的詳細資訊，請參閱 **[!UICONTROL 檢閱]** 請逐步執行下列指南：

* [啟用串流區段匯出目的地的受眾資料](./ui/activate-segment-streaming-destinations.md#review)
* [將受眾資料啟用至串流設定檔匯出目的地](./ui/activate-streaming-profile-destinations.md#review)
* [啟用對象資料以批次設定檔匯出目的地](./ui/activate-batch-profile-destinations.md#review)
