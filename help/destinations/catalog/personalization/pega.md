---
title: Pega客戶決策中心連線
description: 使用Adobe Experience Platform中的Pega客戶決策中心目的地，將設定檔屬性和區段會籍資料傳送至Pega客戶決策中心，以做出次佳決策。
exl-id: 0546da5d-d50d-43ec-bbc2-9468a7db4d90
source-git-commit: ae00b113308354e98f4448d2544e2a6e475c384e
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Pega客戶決策中心連線

## 概述 {#overview}

使用 [!DNL Pega Customer Decision Hub] Adobe Experience Platform中要將設定檔屬性和區段會籍資料傳送到的目的地 [!DNL Pega Customer Decision Hub] 進行次佳動作決策。

從Adobe Experience Platform載入時的設定檔區段會籍 [!DNL Pega Customer Decision Hub]，可作為最適化模型中的預測因子，且有助於提供正確的情境和行為資料，以達到次佳行動決策的目的。

>[!IMPORTANT]
>
>本檔案頁面由Pegasystems建立。 如有任何查詢或更新要求，請直接與Pega聯絡 [此處](mailto:support@pega.com).

## 用例

為了協助您更清楚瞭解應該如何及何時使用 [!DNL Customer Decision Hub] 目的地，以下是Adobe Experience Platform客戶可以使用此目的地來解決的範例使用案例。

### 電信

行銷人員想要運用資料科學模型式的深入分析，掌握由提供的下一個最佳動作 [!DNL Pega Customer Decision Hub] 以取得客戶參與。 [!DNL Pega Customer Decision Hub] 嚴重依賴客戶意圖，例如「Interest_In_5G」、「Interest_in_Unlimited_Dataplan」或「Interest_in_iPhone_accessories」。

### 金融服務

行銷人員想要為已訂閱或取消訂閱退休金計畫或退休計畫電子報的客戶最佳化優惠方案。 金融服務公司可從其CRM將多個客戶ID擷取至Adobe Experience Platform，從自己的離線資料建立區段，並將進入和退出區段的設定檔傳送至 [!DNL Pega Customer Decision Hub] 適用於傳出頻道中的次佳動作(NBA)決策。

## 先决条件 {#prerequisites}

使用此目的地將資料匯出Adobe Experience Platform之前，請務必完成下列必要條件： [!DNL Pega Customer Decision Hub]：

* 設定 [Adobe Experience Platform設定檔和區段會籍整合元件](https://docs.pega.com/component/customer-decision-hub/adobe-experience-platform-profile-and-segment-membership-integration-component) 在您的 [!DNL Pega Customer Decision Hub] 執行個體。
* 設定OAuth 2.0 [使用使用者端憑證進行使用者端註冊](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) 授與型別 [!DNL Pega Customer Decision Hub] 執行個體。
* 設定 [即時執行資料流程](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) 適用於您的Adobe區段會籍資料流程 [!DNL Pega Customer Decision Hub] 執行個體。

## 支援的身分 {#supported-identities}

[!DNL Pega Customer Decision Hub] 支援自訂使用者ID的啟用，如下表所述。 如需詳細資訊，請參閱 [身分](/help/identity-service/namespaces.md).

| 目標身分 | 描述 |
|---|---|
| *客戶ID* | 可唯一識別中設定檔的一般使用者識別碼 [!DNL Pega Customer Decision Hub] 和Adobe Experience Platform |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | 匯出具有識別碼(*客戶ID*)、屬性（姓氏、名字、位置等） 和區段會籍資料。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地永遠是以API為基礎的連線。 一旦設定檔在Experience Platform中更新，聯結器就會根據區段評估，將更新傳送至下游的目標平台。 如需詳細資訊，請參閱 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 連線到目的地 {#connect}

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證至目的地 {#authenticate}

#### OAuth 2使用者端憑證驗證 {#oauth-2-client-credentials-authentication}

![UI熒幕的影像，您可透過此影像使用OAuth 2搭配使用者端憑證驗證連線至Pega CDH目的地](../../assets/catalog/personalization/pega/pega-api-authentication-oauth2-client-credentials.png)

填寫以下欄位並選取 **[!UICONTROL 連線到目的地]**：

* **[!UICONTROL 存取權杖URL]**：您電腦上的OAuth 2存取權杖URL [!DNL Pega Customer Decision Hub] 執行個體。
* **[!UICONTROL 使用者端ID]**：OAuth 2 [!DNL client ID] 您在中產生的 [!DNL Pega Customer Decision Hub] 執行個體。
* **[!UICONTROL 使用者端密碼]**：OAuth 2 [!DNL client secret] 您在中產生的 [!DNL Pega Customer Decision Hub] 執行個體。

### 填寫目的地詳細資料 {#destination-details}

在建立與的驗證連線之後 [!DNL Pega Customer Decision Hub]，提供目的地的下列資訊：

![顯示Pega CDH目的地詳細資訊已完成欄位的UI畫面影像](../../assets/catalog/personalization/pega/pega-connect-destination.png)

若要設定目的地的詳細資訊，請填寫必填欄位並選取 **[!UICONTROL 下一個]**.

* **[!UICONTROL 名稱]**：您日後用來辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL 主機名稱]**：設定檔匯出為JSON資料的Pega客戶決策中心主機名稱。

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

另請參閱 [將受眾資料啟用至串流設定檔匯出目的地](../../ui/activate-streaming-profile-destinations.md) 以取得啟用此目的地的受眾區段的指示。

### 目的地屬性 {#attributes}

在 [[!UICONTROL 選取屬性]](../../ui/activate-streaming-profile-destinations.md#select-attributes) 步驟，Adobe建議您從 [聯合結構描述](../../../profile/home.md#profile-fragments-and-union-schemas). 選取唯一識別碼以及您要匯出至目的地的任何其他XDM欄位。

### 對應範例：啟用設定檔更新於 [!DNL Pega Customer Decision Hub] {#mapping-example}

以下是將設定檔匯出至時的正確身分對應範例 [!DNL Pega Customer Decision Hub].

選取來源欄位：

* 選取識別碼（例如：CustomerID）作為在Adobe Experience Platform中唯一識別設定檔的來源身分，並且 [!DNL Pega Customer Decision Hub].
* 選取需要匯出和更新的XDM來源設定檔屬性變更 [!DNL Pega Customer Decision Hub].

選取目標欄位：

* 選取 `CustomerID` 作為目標身分的名稱空間。
* 選取需要對應至對應XDM來源設定檔屬性的目的地設定檔屬性名稱。

![身分對應](../../assets/catalog/personalization/pega/pega-source-destination-mapping.png)

## 匯出的資料/驗證資料匯出 {#exported-data}

成功更新設定檔的區段會籍會將區段識別碼、名稱和狀態插入Pega行銷區段會籍資料存放區。 成員資格資料與使用客戶設定檔設計工具的客戶相關聯 [!DNL Pega Customer Decision Hub]，如下所示。
![UI畫面影像，您可在其中使用Customer Profile Designer將Adobe區段會籍資料與客戶建立關聯](../../assets/catalog/personalization/pega/pega-profile-designer-associate.png)

區段會籍資料會用於Pega次佳動作設計人員參與政策，以供次佳動作決策使用，如下所示。
![UI畫面影像，您可以在其中新增區段會籍欄位，作為Pega下一個最佳動作設計工具的參與原則條件](../../assets/catalog/personalization/pega/pega-profile-designer-engagment.png)

客戶區段會籍資料欄位會新增為最適化模型中的預測值，如下所示。
![您可以使用Prediction Studio將區段會籍欄位新增為最適化模型中的預測值的UI畫面影像](../../assets/catalog/personalization/pega/pega-profile-designer-adaptivemodel.png)

## 其他资源 {#additional-resources}

另請參閱 [設定OAuth 2.0使用者端註冊](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) 在 [!DNL Pega Customer Decision Hub].

另請參閱 [建立資料流程的即時執行](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) 在 [!DNL Pega Customer Decision Hub].

另請參閱 [在客戶設定檔設計工具中管理客戶記錄](https://docs.pega.com/whats-new-pega-platform/manage-customer-records-customer-profile-designer-86).

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).
