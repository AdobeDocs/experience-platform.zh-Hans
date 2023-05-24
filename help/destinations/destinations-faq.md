---
keywords: 目的地；問題；常見問題；常見問題集；目的地常見問題集
title: 常见问题解答
description: 關於Adobe Experience Platform目的地最常見問題的解答
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 4%

---

# 常见问题解答 {#faq}

## 概述 {#overview}

本檔案提供有關Adobe Experience Platform目的地的常見問題解答。 關於其他相關問題和疑難排解 [!DNL Platform] 服務，包括在所有服務中遇到的服務 [!DNL Platform] API，請參閱 [Experience Platform疑難排解指南](../landing/troubleshooting.md).

## 一般目的地問題 {#general}

**為什麼在Experience PlatformUI和匯出的CSV檔案中會看到不同的設定檔計數？**

由於Experience Platform執行分段的方式，這是正常行為。

串流細分會更新一整天串流區段的設定檔計數，而批次細分則會每24小時更新一次批次區段的設定檔計數。

當區段匯出排程與區段排程不同時，設定檔會在UI和匯出的區段之間計算 [!DNL CSV] 檔案將會不同，尤其是當涉及到串流區段時。

請參閱 [Segment Service檔案](../segmentation/home.md) 以取得更多詳細資料。

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**我需要做什麼才能在中啟用對象 [!DNL Facebook Custom Audiences]？**

將受眾區段傳送至之前 [!DNL Facebook]，確認您符合下列需求：

* 您的 [!DNL Facebook] 使用者帳戶必須具備 **[!DNL Manage campaigns]** 已為您計畫使用的廣告帳戶啟用許可權。
* 此 **Adobe Experience Cloud** 必須將商業帳戶新增為中的廣告合作夥伴 [!DNL Facebook Ad Account]. 使用 `business ID=206617933627973`。另請參閱 [新增合作夥伴至您的業務經理](https://www.facebook.com/business/help/1717412048538897) 詳細資訊，請參閱Facebook檔案。
   >[!IMPORTANT]
   >
   > 設定Adobe Experience Cloud的許可權時，您必須啟用 **管理行銷活動** 許可權。 [!DNL Adobe Experience Platform] 集成要求具备此权限。
* 閱讀並簽署 [!DNL Facebook Custom Audiences] 服務條款。 为此，请转到 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`，其中 `accountID` 是您的 [!DNL Facebook Ad Account ID]。

**我需要將任何應用程式或畫素新增到我的 [!DNL Facebook] 廣告商帳戶？**

不会。由於這不是以畫素為基礎的整合，因此不需要將任何畫素新增至您的廣告商帳戶。

**facebook需要多久的時間來處理來自Adobe Experience Platform的資訊？**

自2021年3月起， [!DNL Facebook Custom Audiences] 最多需要一小時來處理從收到的資訊 [!DNL Platform].

**我可以使用 [!DNL Facebook Custom Audiences] 對於其他中的對象鎖定目標 [!DNL Facebook] 應用程式，例如 [!DNL Instagram]？**

您可以使用 [!DNL Facebook Custom Audiences] facebook所支援應用程式系列中的受眾鎖定目標目的地 [!DNL Facebook Custom Audiences]，包括 [!DNL Facebook]， [!DNL Instagram]， [!DNL Audience Network]、和 [!DNL Messenger]. 在中的版位層級會指出廣告商選擇要在其中執行行銷活動的應用程式 [!DNL Facebook Ads Manager].

**兩者之間有何差異 [!DNL Facebook Custom Audiences] 連線和 [!DNL Facebook Pixel] 擴充功能？**

此 [!DNL Facebook Custom Audiences] 連線使用 [!DNL Platform] 將受眾傳送至時的身分 [!DNL Facebook]，而 [[!DNL Facebook Pixel] 連線](../destinations/catalog/advertising/facebook-pixel.md) 使用 [!DNL Facebook] 已整合至網站中的畫素。

这两种集成是互补的，您可以同时使用这两种集成来确保更好的受众覆盖。例如，您可以使用 [!DNL Facebook Pixel] 尚未建立帳戶的潛在網站訪客擴充功能，而 [!DNL Facebook Custom Audiences] 可協助您根據以下專案鎖定現有客戶： [!DNL Platform] 身分。

**Adobe Experience Platform是否與整合 [!DNL Facebook Custom Audiences] 當使用者不再符合資格時，是否支援將他們從受眾中取消資格？**

是，整合支援將使用者從 [!DNL Facebook Custom Audiences] 當他們不再符合資格時。

**在傳送對象資料到之前，我該如何先將對象資料雜湊化 [!DNL Facebook]？**

[!DNL Facebook] 要求不會明確傳送任何個人識別資訊(PII)。 因此，啟用的對象 [!DNL Facebook] 可以關閉 *雜湊* 識別碼，例如電子郵件地址或電話號碼。

如需ID比對需求的詳細說明，請參閱 [ID比對需求](catalog/social/facebook.md#id-matching-requirements).

**我可以在哪一種身分啟用 [!DNL Facebook Custom Audiences]？**

[!DNL Facebook Custom Audiences] 支援啟用下列身分：雜湊電子郵件、雜湊電話號碼、 [!DNL GAID]， [!DNL IDFA]，以及自訂外部ID。

**我可以為個別的Facebook帳戶在Platform UI中建立多個Facebook目的地嗎？**

可以。Experience Platform中的Facebook目的地與Facebook中的廣告帳戶之比是1:1。 您可以為公司中的每個Facebook廣告帳戶建立個別的Facebook目的地。 請遵循 [目的地連線教學課程](/help/destinations/ui/connect-destination.md) 並為Platform UI中的每個新Facebook目的地連線至個別的Facebook帳戶。 您可以連線的Facebook廣告帳戶數量沒有限制。

## Google 客户匹配 {#google-customer-match}

**將區段匯出至Google Customer Match時，為什麼在Google介面的區段名稱結尾會附加額外的數字？**

Google要求區段名稱必須是唯一的。 您所看到的數字是 [UNIX時間戳記](https://www.unixtimestamp.com/) 如果您將相同區段對應至多個Google目的地，則會附加區段名稱，以保持區段名稱的唯一性。

## linkedIn相符的受眾 {#linkedin}

**我需要將任何應用程式或畫素新增到我的 [!DNL LinkedIn] 廣告商帳戶？**

不会。由於這不是以畫素為基礎的整合，因此不需要將任何畫素新增至您的廣告商帳戶。

**我需要做什麼才能在中啟用對象 [!DNL LinkedIn Matched Audiences]？**

開始使用 [!UICONTROL linkedIn相符的受眾] 目的地，確認您的 [!DNL LinkedIn Campaign Manager] 帳戶具有 [!DNL Creative Manager] 許可權層級或以上。

若要瞭解如何編輯您的 [!DNL LinkedIn Campaign Manager] 使用者許可權，請參閱 [新增、編輯和移除Advertising帳戶的使用者許可權](https://www.linkedin.com/help/lms/answer/5753) (位於LinkedIn檔案中)。

**在傳送對象資料到之前，我該如何先將對象資料雜湊化 [!DNL LinkedIn]？**

[!DNL LinkedIn] 要求不會明確傳送任何個人識別資訊(PII)。 因此，啟用的對象 [!DNL LinkedIn] 可以關閉 *雜湊* 識別碼，例如電子郵件地址或電話號碼。

如需ID比對需求的詳細說明，請參閱 [ID比對需求](catalog/social/linkedin.md#id-matching-requirements).

**我可以在哪一種身分啟用 [!DNL LinkedIn]？**

[!DNL LinkedIn Matched Audiences] 支援啟用下列身分：雜湊電子郵件、 [!DNL GAID]、和 [!DNL IDFA].
