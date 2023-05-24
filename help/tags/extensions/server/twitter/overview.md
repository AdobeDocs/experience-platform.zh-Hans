---
keywords: 事件轉送擴充功能；twitter；twitter事件轉送擴充功能
title: twitter事件轉送擴充功能
description: 此Adobe Experience Platform事件轉送擴充功能可讓您將事件擷取至Twitter，以滿足您的業務需求。
source-git-commit: d51dae024da0cce770be91601c52b8c2958c3f64
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 3%

---

# [!DNL Twitter] 事件轉送擴充功能

[[!DNL Twitter]](https://www.twitter.com) 是一種線上社群媒體和社交網路服務，使用者可在該服務上發佈和互動280個字元的訊息，稱為推文。 使用者可以使用瀏覽器、行動前端軟體，或以程式設計方式透過其與Twitter互動 [API](https://developer.twitter.com/en/docs/twitter-api)

此 [!DNL Twitter] 網頁轉換API [事件轉送](../../../ui/event-forwarding/overview.md) 擴充功能可讓您運用Adobe Experience Platform Edge Network中擷取的資料，並將其傳送至 [!DNL Twitter]. 本檔案說明擴充功能的使用案例、安裝方式，以及如何將其功能整合至事件轉送中 [規則](../../../ui/managing-resources/rules.md).

[!DNL Twitter] 需要 [OAuth 1.0](https://developer.twitter.com/en/docs/authentication/oauth-1-0a) 以進行驗證 [!DNL Twitter] [!DNL Web Conversions] API。

## 用例

如果您想要使用來自Edge Network的資料，請使用此擴充功能 [!DNL Twitter] 以善用其客戶分析和目標定位功能。

例如，以組織中的行銷團隊為例。 團隊會從其網站擷取使用者互動事件資料，作為來自其網站的事件資料，並將其載入到 [!DNL Twitter] 使用此事件轉送擴充功能。

行銷與分析團隊就可以善用 [!DNL Twitter's] 執行其他分析並鎖定這些使用者，以鎖定目標廣告行銷活動的功能。

如需特定使用案例的詳細資訊，請參閱 [!DNL Twitter]，請參閱 [[!DNL Twitter] 使用案例](https://developer.twitter.com/en/use-cases/build-for-businesses) 說明檔案。

## [!DNL Twitter] 必要條件和護欄 {#prerequisites}

您必須具備有效的 [!DNL Twitter] 帳戶，以便使用此擴充功能。 前往 [[!DNL Twitter] 註冊頁面](https://help.twitter.com/en/using-twitter/create-twitter-account) 註冊並建立帳戶。

您必須將帳戶設定為 [!DNL Twitter] 開發人員帳戶。 若要瞭解如何註冊為開發人員，請參閱 [[!DNL Twitter] 開發人員帳戶](https://developer.twitter.com/en/support/twitter-api/developer-account).

### API護欄 {#guardrails}

此 [!DNL Twitter] Web Conversions API的速率限製為每15分鐘間隔60,000個請求，其中每個請求允許500個事件。

### 收集必要的設定詳細資料 {#configuration-details}

為了將Experience Platform連線到 [!DNL Twitter]，需要下列輸入：

| 金鑰型別 | 描述 |
| --- | --- |
| 使用者金鑰 | 應用程式&#x200B;的API金鑰可存取 [!DNL Twitter] API。 請參閱 [!DNL Twitter] 檔案： [api金鑰和秘密](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) 以取得指引。 |  |
| 使用者密碼 | API密碼可讓您的應用程式存取 [!DNL Twitter] API。 請參閱 [!DNL Twitter] 檔案： [api金鑰和秘密](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) 以取得指引。 |
| 權杖密碼 | 您應用程式的不會到期的Token密碼，用於驗證 [!DNL Twitter] 透過OAuth的API。 請參閱 [!DNL Twitter] 檔案： [取得使用存取權杖](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) 以取得指引。 |
| 存取Token | 應用程式不會到期的存取Token，用於驗證 [!DNL Twitter] 透過OAuth的API。 請參閱 [!DNL Twitter] 檔案： [取得使用存取權杖](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) 以取得指引。 |
| 畫素ID | 此 [!DNL Twitter] Pixel是在您的網站上實作的網站標籤，用來追蹤網站動作或轉換。 請參閱 [!DNL Twitter] 檔案： [網站的轉換追蹤](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html) 以取得指引。 |

## 安裝並設定 [!DNL Twitter] 擴充功能 {#install}

若要安裝擴充功能， [建立事件轉送屬性](../../../ui/event-forwarding/overview.md#properties) 或選擇現有屬性進行編輯。

選取 **[!UICONTROL 擴充功能]** 左側導覽列中。 在 **[!UICONTROL 目錄]** 索引標籤，選取 **[!UICONTROL 安裝]** 在的卡片上 [!DNL Twitter] 副檔名。

![目錄顯示 [!DNL Twitter] 擴充功能醒目提示安裝。](../../../images/extensions/server/twitter/install.png)

>[!IMPORTANT]
>
>根據您的實作需求，您可能需要在設定擴充功能前建立結構、資料元素和資料集。 開始之前，請先檢閱所有設定步驟，以決定您需要為使用案例設定的實體。

在下一個畫面中，輸入下列內容 [設定值](#configuration-details) 您先前收集的 [!DNL Twitter]：

* **[!UICONTROL 畫素ID]**
* **[!UICONTROL 使用者金鑰]**
* **[!UICONTROL 使用者密碼]**
* **[!UICONTROL Token]**
* **[!UICONTROL 權杖密碼]**

完成後，選取 **[!UICONTROL 儲存]**.

![[!DNL Twitter] 的設定畫面 [!DNL Twitter] 副檔名。](../../../images/extensions/server/twitter/configure.png)

## 設定事件轉送規則 {#config-rule}

設定好所有資料元素後，您就可以開始建立事件轉送規則，判斷將事件傳送至的時間和方式 [!DNL Twitter].

建立新的 [規則](../../../ui/managing-resources/rules.md) 在事件轉送屬性中。 下 **[!UICONTROL 動作]**，新增動作並將擴充功能設為 **[!UICONTROL twitter]**. 傳送Adobe Experience Edge Network事件至 [!DNL Twitter]，設定 **[!UICONTROL 動作型別]** 至 **[!UICONTROL 傳送網頁轉換].**

選取後，會出現其他控制項以進一步設定事件。 您需要對應 [!DNL Twitter] 事件屬性至您先前建立的資料元素。 如需詳細資訊，請參閱 [[!DNL Twitter] 網頁轉換API](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions).

![此 [!DNL Twitter] 建立轉換事件規則。](../../../images/extensions/server/twitter/action-configuration.png)

**[!UICONTROL 使用者識別]**

| 字段名称 | 描述 | 示例 | 必需 |
| --- | --- | --- | --- |
| [!UICONTROL [!DNL Twitter] 點按ID] | [!DNL Twitter] 從點進URL剖析的點選ID。 | 26l6412g5p4iyj65a2oic2ayg2 | 如果未新增其他識別碼，則為必要。 |
| [!UICONTROL 电子邮件] | 使用SHA256雜湊處理的電子郵件地址。 文字必須為小寫，且必須在雜湊前移除任何結尾或前導空格。 | eventforwarding@example.com | 如果未新增其他識別碼，則為必要。 |
| [!UICONTROL Phone] | 手機可作為識別碼，以符合轉換事件。 電話號碼必須是E164格式[+][國家/地區代碼][區碼][local phone number] 雜湊前。 | +911234567875 | 如果未新增其他識別碼，則為必要。 |

**[!UICONTROL 轉換資料]**

| 字段名称 | 描述 | 示例 | 必需 |
| --- | --- | --- | --- |
| [!UICONTROL 轉換時間] | ISO 8601或yyyy-MM-dd&#39;T&#39;HH中的字串形式的日期 — 時間:mm:SSSZ格式。 | 2022-02-18T01:14:00.603盎司 | 是 |
| [!UICONTROL 事件ID] | 特定事件的基底36 ID。 此ID應符合「 」中預先設定的事件，該事件包 [!DNL Twitter] 廣告帳戶。 這稱為「事件管理員」中對應事件的ID。 | o87ne或tw-o8z6j-o87ne (tw-pixel_id-event-id) | 是 |
| [!UICONTROL 專案數] | 在事件中購買的專案數。 這必須是大於0的正數。 | 4 | 否 |
| [!UICONTROL 货币] | 事件中購買專案的貨幣。 以ISO-4217表示，若未提供，預設值將為USD。 | 美元 | 否 |
| [!UICONTROL 值] | 在事件中購買之專案的價格值。 | 100.00 | 否 |
| [!UICONTROL 轉換ID] | 轉換事件的識別碼，可用於相同事件標籤中的網頁畫素和轉換API轉換之間的去重複化。 | 23294827 | 否 |
| [!UICONTROL 描述] | 說明以及有關轉換的任何其他資訊。 | 測試轉換 | 否 |

## 驗證中的資料 [!DNL Twitter]

建立並執行事件轉送規則後，請驗證是否已將事件傳送至 [!DNL Twitter] API會如預期般顯示在中 [!DNL Twitter] UI。

如果事件集合和 [!DNL Experience Platform] 整合成功，您將會在 [!DNL Twitter] [!UICONTROL 事件管理員].

![此 [!DNL Twitter] 事件管理員](../../../images/extensions/server/twitter/event-manager.png)

## 后续步骤

本指南說明如何將轉換事件傳送至 [!DNL Twitter] 使用事件轉送。 如需這些基礎技術的詳細資訊，請參閱正式檔案：

* [[!DNL Twitter] API](https://developer.twitter.com/en/docs/twitter-api)
* [[!DNL Twitter] 網頁轉換API](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)
* [[!DNL Twitter] 使用者存取權杖](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)
* [畫素ID和轉換追蹤](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)
