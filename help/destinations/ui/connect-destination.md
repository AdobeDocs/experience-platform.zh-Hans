---
keywords: 連線目的地；目的地連線；如何連線目的地
title: 建立新的目的地連線
type: Tutorial
description: 瞭解如何在Adobe Experience Platform中連線至目的地、啟用警示，以及為已連線的目的地設定行銷動作。
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: 606038116391e75ba4ffc36bab11757f963a8346
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 0%

---

# 建立新的目的地連線

>[!IMPORTANT]
> 
>* 若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 若要連線至支援資料集匯出的目的地，您需要 **[!UICONTROL 管理和啟用資料集目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。


## 概述 {#overview}

您必須先設定與目的地平台的連線，才能將對象資料傳送至目的地。 本文說明如何設定新的目的地連線，然後您可以使用Adobe Experience Platform使用者介面啟用區段或匯出資料集。

## 在目錄中尋找所需的目的地 {#setup}

1. 前往 **[!UICONTROL 連線]** > **[!UICONTROL 目的地]**，然後選取 **[!UICONTROL 目錄]** 標籤。

   ![顯示目的地目錄頁面的Experience PlatformUI熒幕擷圖。](../assets/ui/connect-destinations/catalog.png)

2. 目錄中的目的地卡片可能會有不同的動作控制項，具體取決於您是否有與目的地的現有連線，以及目的地是否支援啟用區段、匯出資料集或兩者。 您可能會看到目的地卡的下列任何控制項：

   * **[!UICONTROL 設定]**. 在啟用區段或匯出資料集之前，必須先將連線設定到此目的地。
   * **[!UICONTROL 激活]**. 已設定連線至此目的地。 此目的地支援區段啟用和資料集匯出。
   * **[!UICONTROL 啟用區段]**. 已設定連線至此目的地。 此目的地僅支援區段啟用。

   如需這些控制項之間差異的詳細資訊，您也可以參閱 [目錄](../ui/destinations-workspace.md#catalog) 區段。

   選取 **[!UICONTROL 設定]**， **[!UICONTROL 啟動]**，或 **[!UICONTROL 啟用區段]**，視您可用的控制項而定。

   ![Experience PlatformUI的熒幕擷圖，其中顯示反白顯示「設定」控制項的目的地目錄頁面。](../assets/ui/connect-destinations/set-up.png)

   ![Experience PlatformUI的熒幕擷圖，其中顯示反白顯示「啟用區段」控制項的目的地目錄頁面。](../assets/ui/connect-destinations/activate-segments.png)

3. 如果您已選取 **[!UICONTROL 設定]**，請跳至下一個步驟，即 [驗證](#authenticate) 到目的地。

   如果您已選取 **[!UICONTROL 啟動]**， **[!UICONTROL 啟用區段]**，或 **[!UICONTROL 匯出資料集]**，您現在可以看到現有目的地連線的清單。

   選取 **[!UICONTROL 設定新目的地]** 以建立與目的地的新連線。

   ![Experience PlatformUI的熒幕擷圖，其中顯示可用目的地的清單，並反白顯示「設定新目的地」控制項。](../assets/ui/connect-destinations/configure-new-destination.png)

## 驗證至目的地 {#authenticate}

連線至目的地的第一個步驟是驗證至目的地平台。

根據您連線的目的地，您可能會被帶往目的地合作夥伴的頁面進行驗證，或者系統可能會要求您直接在Platform工作流程中輸入驗證認證。 以下是驗證所需的輸入範例。 [!DNL Amazon S3] 目的地。 每個目的地檔案頁面都會提供必要輸入的詳細指示(例如，請參閱 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) 和for [[!DNL Facebook]](/help/destinations/catalog/social/facebook.md#authenticate))。

**[!DNL Amazon S3]必要和選用驗證引數**

![此影像顯示驗證Amazon S3目的地時的必要和選用輸入引數。](../assets/ui/connect-destinations/authenticate-amazon-s3-example.png)

## 設定連線引數 {#set-up-connection-parameters}

如果您已設定目的地驗證，您可以繼續使用現有帳戶，也可以設定新帳戶。

視您連線的目的地而定，可能會要求您輸入不同型別的連線引數。 例如，當連線到 [!DNL Amazon S3] 目的地，請您提供以下相關詳細資訊 [!DNL Amazon S3] 儲存貯體名稱和將儲存檔案的資料夾路徑。 以下是兩個需要的輸入範例 [!DNL Amazon S3] 目的地和 [!DNL Trade Desk] 目的地。 每個目的地檔案頁面都會提供必要輸入的詳細指示。

>[!IMPORTANT]
>
>下列影像僅供說明之用。 目的地連線的詳細資料因目的地而異。 如需目的地連線詳細資訊的詳細資訊，請閱讀 **連線到目的地** 區段在每個 [目的地目錄](../catalog/overview.md) 頁面(例如， [[!DNL Google Customer Match]](../catalog/advertising/google-customer-match.md#connect)， [[!DNL Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md#connect)，或 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details))。

**[!DNL Amazon S3]必要和選用輸入引數**

![此影像顯示連線至Amazon S3目的地時的必要和選用輸入引數。](../assets/ui/connect-destinations/connect-destination-amazons3-example.png)

**[!DNL The Trade Desk]必要和選用輸入引數**

![此影像顯示連線至交易台目的地時的必要和選用輸入引數。](../assets/ui/connect-destinations/connect-destination-trade-desk-example.png)

### （測試版）設定匯出檔案的檔案格式選項 {#file-formatting-and-compression-options}

對於以檔案為基礎的目的地，您可以設定與匯出檔案的格式化和壓縮方式相關的各種設定。 如需所有可用格式設定和壓縮選項的詳細資訊，請閱讀 [針對以檔案為基礎的目的地教學課程，設定檔案格式選項](/help/destinations/ui/batch-destinations-file-formatting-options.md).

![此影像顯示CSV檔案的檔案型別選取範圍及各種選項。](/help/destinations/assets/ui/connect-destinations/file-formatting-options.png)

### 設定區段啟動或資料集匯出的目的地連線 {#segment-activation-or-dataset-exports}

有些檔案型目的地支援區段啟用和資料集匯出。 對於這些目的地，您可以選擇是否要建立連線，以啟用區段或匯出資料集。

![此影像顯示資料型別選擇控制項，可讓使用者在區段啟用和資料集匯出之間選擇。](/help/destinations/assets/ui/connect-destinations/data-type-selection.png)

### 啟用目的地警示 {#enable-alerts}

1. （選用）選取您要訂閱的目的地資料流警示。 建立資料流以接收有關資料流執行的狀態、成功或失敗的警報訊息時，您可以訂閱警報。 可用的警報會因您連線的目的地型別（檔案型或串流）而異。 讀取 [訂閱內容感知目的地警示](alerts.md) 以取得目的地資料流警示的詳細資訊。

   ![「設定新目的地」對話方塊中反白了內容中目的地警示訂閱選項。](../assets/ui/connect-destinations/subscribe-to-alerts.png)

2. 选择&#x200B;**[!UICONTROL 下一步]**。

   ![「設定新目的地」對話方塊中反白顯示「下一步」控制項，可讓使用者繼續進行工作流程中的下一個步驟。](../assets/ui/connect-destinations/next.png)

## 選取行銷動作 {#select-marketing-actions}

1. 選取適用於您要匯出至目的地之資料的行銷動作。 行銷動作會指出資料匯出至目的地的目的。 您可以從Adobe定義的行銷動作中進行選取，也可以建立自己的行銷動作。 如需行銷動作的詳細資訊，請參閱 [資料使用原則概觀](../../data-governance/policies/overview.md) 頁面。

   ![「設定新目的地」對話方塊中會反白顯示可用的行銷動作。 用來完成「連線至目的地」工作流程的可用控制項也會反白顯示。](../assets/ui/connect-destinations/governance.png)

2. 選取 **[!UICONTROL 儲存並退出]** 以儲存目的地組態，或選取 **[!UICONTROL 下一個]** 以繼續前往對象資料 [啟用流程](activation-overview.md).

## 后续步骤 {#next-steps}

閱讀本檔案後，您已瞭解如何使用Experience PlatformUI建立與目的地的連線。 提醒您，可用和必要的連線引數會因目的地而異。 您也應該參閱 [目的地目錄](/help/destinations/catalog/overview.md) 以取得每個目的地型別的必要輸入和可用選項的特定資訊。

接下來，您可以繼續前往 [啟用區段](/help/destinations/ui/activation-overview.md) 或 [匯出資料集](/help/destinations/ui/export-datasets.md) 前往您的目的地。