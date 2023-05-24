---
keywords: target個人化；目的地； experience platform target目的地； adobe target目的地；
title: Adobe Target連線
description: Adobe Target應用程式可在跨網站、行動應用程式等的所有傳入客戶互動中提供即時的AI支援個人化和實驗功能。
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: f97b667f8d4dc311683b018bb1c1792aae871648
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 7%

---

# Adobe Target連線 {#adobe-target-connection}

## 目的地變更記錄檔 {#changelog}

>[!IMPORTANT]
>
>使用增強型Adobe Target V2目的地聯結器的測試版時，您可能會在目的地目錄中看到兩個Adobe Target卡。
>Adobe Target V2目的地聯結器目前為測試版，僅適用於特定數量的客戶。 除了AdobeV1卡提供的功能外，Target V2聯結器還新增了 [對應步驟](/help/destinations/ui/activate-profile-request-destinations.md#map-attributes) 至啟用工作流程，可讓您將設定檔屬性對應至Adobe Target，啟用以屬性為基礎的相同頁面和下一頁個人化。

![並排檢視中的兩個Adobe Target目的地卡片影像。](/help/destinations/assets/catalog/personalization/adobe-target-connection/adobe-target-side-by-side-view.png)

## 概述 {#overview}

Adobe Target應用程式可在跨網站、行動應用程式等的所有傳入客戶互動中提供即時的AI支援個人化和實驗功能。

Adobe Target是Adobe Experience Platform目標目錄中的個人化連線。

## 先决条件 {#prerequisites}

### 資料串流ID {#datastream-id}

將Adobe Target連線設定至時 [使用資料串流ID](#parameters)，您必須擁有 [Adobe Experience Platform Web SDK](../../../edge/home.md) 已實作。

在不使用資料串流ID的情況下設定Adobe Target連線不需要您實作Web SDK。

>[!IMPORTANT]
>
>建立之前 [!DNL Adobe Target] connection，閱讀操作指南 [設定相同頁面和下一頁個人化的個人化目的地](../../ui/configure-personalization-destinations.md). 本指南會針對跨多個Experience Platform元件的相同頁面和下一頁個人化使用案例，引導您進行必要的設定步驟。 相同頁面和下一頁個人化功能會要求您在設定Adobe Target連線時使用資料串流ID。

### Adobe Target的必要條件 {#prerequisites-in-adobe-target}

在Adobe Target中，確定您的使用者具有：

* 存取 [預設工作區](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#default-workspace)；
* 此 **核准者** [角色](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#roles-and-permissions).

深入瞭解授與許可權 [Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=en#section_8C425E43E5DD4111BBFC734A2B7ABC80) 和for [Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html?lang=en#roles-permissions).

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!DNL Profile request]** | 您正在要求在Adobe Target目的地對映的所有區段都使用單一設定檔。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦設定檔根據區段評估在Experience Platform中更新，聯結器就會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 用例 {#use-cases}

**個人化首頁橫幅**

一家家用租賃和銷售公司想要根據Adobe Experience Platform中的客戶區段資格，以橫幅來個人化他們的首頁。 公司可以選取應該讓哪些對象獲得個人化體驗，並將這些對象傳送到Adobe Target，作為其Target選件的鎖定目標條件。

## 連線到目的地 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="关于数据流 ID"
>abstract="此选项确定区段将包含在哪个数据收集数据流中。下拉菜单仅显示已启用目标配置的数据流。要使用边缘分段，您必须选择数据流 ID。选择“无”将禁用所有使用边缘分段的用例。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html#parameters" text="了解有关选择数据流的更多信息"

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md).

Adobe Experience Platform會自動連線至貴公司的Adobe Target執行個體。 不需要驗證。

### 連線引數 {#parameters}

當 [設定](../../ui/connect-destination.md) 您必須提供下列資訊：

* **名稱**：填寫此目的地的偏好名稱。
* **說明**：輸入目的地的說明。 例如，您可以提及要將此目的地用於哪個行銷活動。 此欄位為選用。
* **資料串流ID**：這會決定要將區段納入哪個資料收集資料串流。 下拉式功能表只會顯示已啟用Target和Adobe Experience Platform服務的資料串流。 另請參閱 [設定資料串流](../../../edge/datastreams/configure.md#aep) 以取得如何設定Adobe Experience Platform和Adobe Target資料流的詳細資訊。
   * **[!UICONTROL 無]**：如果您需要設定Adobe Target個人化，但無法實作 [Experience PlatformWeb SDK](../../../edge/home.md). 使用此選項時，從Experience Platform匯出至Target的區段僅支援下一次工作階段個人化，且會停用邊緣區段。 如需詳細資訊，請參閱下表。

| 未選取任何資料串流 | 已選取資料流 |
|---|---|
| <ul><li>[邊緣細分](../../../segmentation/ui/edge-segmentation.md) 不受支援。</li><li>[相同頁面和下一頁個人化](../../ui/configure-personalization-destinations.md) 不受支援。</li><li>您只能將區段共用至Adobe Target連線， *預設生產沙箱*.</li><li>若要在不使用資料流ID的情況下設定下一個工作階段個人化，請使用 [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=en).</li></ul> | <ul><li>邊緣細分如預期般運作。</li><li>[相同頁面和下一頁個人化](../../ui/configure-personalization-destinations.md) 支援。</li><li>其他沙箱支援區段共用。</li></ul> |

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

讀取 [對設定檔請求目的地啟用設定檔和區段](../../ui/activate-profile-request-destinations.md) 以取得啟用此目的地的受眾區段的指示。

## 匯出的資料 {#exported-data}

Adobe Target會從Adobe Experience Platform Edge Network讀取設定檔資料，因此不會匯出任何資料。

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請閱讀 [資料控管概觀](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans).
