---
keywords: 啟用設定檔目的地；啟用目的地；啟用資料；啟用電子郵件行銷目的地；啟用雲端儲存空間目的地
title: 將受眾資料啟用至串流設定檔匯出目的地
type: Tutorial
description: 瞭解如何透過將區段傳送至串流設定檔型目的地，以啟用您在Adobe Experience Platform中的受眾資料。
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: 5bb2981b8187fcd3de46f80ca6c892421b3590f6
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 5%

---

# 將受眾資料啟用至串流設定檔匯出目的地

>[!IMPORTANT]
> 
> * 若要啟用資料並啟用 [對應步驟](#mapping) 的工作流程中，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions).
> * 若要在不透過 [對應步驟](#mapping) 的工作流程中，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用區段而不進行對應]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions).
> 
> 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

## 概述 {#overview}

本文說明在Adobe Experience Platform串流設定檔型目的地(例如Amazon Kinesis)中啟用受眾資料所需的工作流程。

## 先决条件 {#prerequisites}

若要啟用目的地的資料，您必須已成功 [已連線至目的地](./connect-destination.md). 如果您尚未這麼做，請前往 [目的地目錄](../catalog/overview.md)，瀏覽支援的目的地並設定您要使用的目的地。

## 選取您的目的地 {#select-destination}

1. 前往 **[!UICONTROL 連線>目的地]**，然後選取 **[!UICONTROL 目錄]** 標籤。

   ![顯示目的地目錄索引標籤的影像。](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. 選取 **[!UICONTROL 啟用區段]** 對應至您要啟用區段之目的地的卡片上，如下圖所示。

   ![醒目提示目標目錄標籤中啟用區段控制項的影像。](../assets/ui/activate-streaming-profile-destinations/activate-segments-button.png)

1. 選取您要用來啟用區段的目的地連線，然後選取 **[!UICONTROL 下一個]**.

   ![此影像顯示兩個您可連線之目的地的選取範圍。](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. 移至下一區段至 [選取您的區段](#select-segments).

## 選取您的區段 {#select-segments}

使用區段名稱左邊的核取方塊來選取您要啟用至目的地的區段，然後選取 **[!UICONTROL 下一個]**.

![反白啟動工作流程選取區段步驟中核取方塊選取範圍的影像。](../assets/ui/activate-streaming-profile-destinations/select-segments.png)

## 選取設定檔屬性 {#select-attributes}

在 **[!UICONTROL 對應]** 步驟，選取您要傳送至目標目的地的設定檔屬性。

>[!NOTE]
>
> Adobe Experience Platform會使用結構描述中四個建議且常用的屬性來預先填入您的選取範圍： `person.name.firstName`， `person.name.lastName`， `personalEmail.address`， `segmentMembership.status`.

檔案匯出內容會依下列方式而有所不同，具體取決於是否 `segmentMembership.status` 已選取：
* 如果 `segmentMembership.status` 欄位已選取，匯出的檔案包括 **[!UICONTROL 作用中]** 初始完整快照中的成員和 **[!UICONTROL 作用中]** 和 **[!UICONTROL 已過期]** 後續增量匯出中的成員。
* 如果 `segmentMembership.status` 未選取欄位，匯出的檔案僅包含 **[!UICONTROL 作用中]** 初始完整快照和後續增量匯出中的成員。

![顯示對應步驟中預先填入的建議屬性的影像。](../assets/ui/activate-streaming-profile-destinations/attributes-default.png)

1. 在 **[!UICONTROL 選取屬性]** 頁面，選取 **[!UICONTROL 新增欄位]**.

   ![在對應步驟中反白顯示「新增欄位」控制項的影像。](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. 選取右側的箭頭 **[!UICONTROL 結構描述欄位]** 登入點。

   ![在對應步驟中反白如何選取來源欄位的影像。](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. 在 **[!UICONTROL 選取欄位]** 頁面上，選取您要傳送至目的地的XDM屬性，然後選擇 **[!UICONTROL 選取]**.

   ![顯示可選取作為來源欄位的一系列XDM欄位的影像。](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)


1. 若要新增更多對應，請重複步驟1至3，然後選取 **[!UICONTROL 下一個]**.

## 请查看 {#review}

於 **[!UICONTROL 檢閱]** 頁面中，您可以看到選取範圍的摘要。 選取 **[!UICONTROL 取消]** 若要分解流量， **[!UICONTROL 返回]** 修改您的設定，或 **[!UICONTROL 完成]** 以確認您的選擇並開始傳送資料至目的地。

![稽核步驟中的選取專案摘要。](/help/destinations/assets/ui/activate-streaming-profile-destinations/review.png)

### 同意原則評估 {#consent-policy-evaluation}

如果您的组织购买了 **Adobe Healthcare Shield** 或 **Adobe Privacy &amp; Security Shield**，请选择&#x200B;**[!UICONTROL 查看适用的同意策略]**&#x200B;以查看应用了哪些同意策略以及作为其结果包含在激活中的配置文件数量。閱讀關於 [同意原則評估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 以取得詳細資訊。

### 資料使用原則檢查 {#data-usage-policy-checks}

在 **[!UICONTROL 檢閱]** 步驟，Experience Platform也會檢查是否有任何資料使用原則違規。 以下是違反原則的範例。 您必須先解決違規，才能完成區段啟用工作流程。 如需有關如何解決原則違規的資訊，請閱讀關於 [資料使用原則違規](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) （位於資料控管檔案區段）。

![資料原則違規](../assets/common/data-policy-violation.png)

### 过滤区段 {#filter-segments}

此外，在此步驟中，您可以使用頁面上的可用篩選器，只顯示其排程或對應已隨著此工作流程而更新的區段。

![熒幕錄製，顯示稽核步驟中可用的區段篩選器。](/help/destinations/assets/ui/activate-streaming-profile-destinations/filter-segments-review-step.gif)

如果您對您的選擇感到滿意，並且未偵測到任何原則違規，請選取 **[!UICONTROL 完成]** 以確認您的選擇並開始傳送資料至目的地。

## 驗證區段啟用 {#verify}

您的匯出 [!DNL Experience Platform] 資料以JSON格式登陸您的目標目的地。 例如，下列事件包含符合特定區段資格並退出其他區段之對象的電子郵件地址設定檔屬性。 此潛在客戶的身分識別為ECID和電子郵件。

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```
