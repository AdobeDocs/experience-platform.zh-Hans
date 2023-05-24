---
title: Google Ads增強型轉換擴充功能
description: 瞭解Adobe Experience Platform中用於事件轉送的Google Ads Enhanced Conversions擴充功能。
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 1%

---

# [!DNL Google Ads] 增強型轉換延伸功能

使用 [!DNL Google Ads] API，您可以善用 [增強型轉換](https://support.google.com/google-ads/answer/9888656) 透過以轉換調整的形式傳送第一方客戶資料。 Google會使用這項額外資料，改善由廣告互動驅動的線上轉換報表。

此 [[!DNL Google Ads] 增強型轉換事件轉送擴充功能](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (先前稱為 [!DNL Enhanced Conversions] 擴充功能)提供使用者易記的範本，以輕鬆實作的 [!DNL Google Ads] API。

>[!IMPORTANT]
>
>增強型轉換僅適用於存在客戶資料的轉換型別，例如訂閱、註冊和購買。 下列一或多個客戶資料片段必須可供使用，因為它們在下列情況下是必要的： [設定轉換動作](#conversion-action-event-forwarding) 若為事件轉送規則：
>
>* 電子郵件地址（偏好設定）
>* 名稱和住家地址（街道地址、城市、州/地區和郵遞區號）
>* 電話號碼（除了上述另外兩則資訊之一外，另外必須提供）


## 实施概述

增強型轉換可運用 [!DNL Google Ads] 將第一方資料新增至使用者端裝置（通常是網站）上發生的轉換的API。 這表示實作增強型轉換有兩個步驟：

1. 從使用者端傳送轉換。
1. 使用事件轉送來傳送其他第一方資料，以增強從使用者端傳送的轉換資料。

>[!TIP]
>
>若要將使用者端轉換事件與事件轉送所傳送的第一方資料建立關聯， `transaction_ID` 兩個呼叫中的內容必須相同。 如需每個服務必須提供此值的位置的詳細資訊，請參閱有關設定轉換動作的區段 [標籤](#conversion-action-tags) 和 [事件轉送](#conversion-action-event-forwarding)（分別）。

由於傳送轉換事件涉及使用者端和伺服器端實施，因此本檔案涵蓋設定使用者端的先決條件步驟 [[!DNL Google Global Site Tag] (gtag)擴充功能](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) 除了 [!DNL Enhanced Conversions] 事件轉送的擴充功能。

以下影片會介紹 [!DNL Enhanced Conversions] 擴充功能並從高層級逐步說明實作步驟：

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## 使用標籤傳送轉換

若要從網站上傳送轉換事件， [!DNL Google Global Site Tag] (gtag)必須部署。 您可以透過設定和安裝 [!DNL Google Global Site Tag] (gtag)擴充功能。

### 設定並安裝 [!DNL Google Global Site Tag] 擴充功能

導覽至 [!UICONTROL 資料彙集] UI或Experience PlatformUI並選取 **[!UICONTROL 標籤]** 左側導覽列中。 選取您要安裝擴充功能的標籤屬性，然後選取 **[!UICONTROL 擴充功能]** 左側導覽列中。 在 **[!UICONTROL 目錄]** 索引標籤中，找到 [!UICONTROL Google全域網站標籤(gtag)] 擴充功能並選取 **[!UICONTROL 安裝]**.

![此 [!UICONTROL Google全域網站標籤(gtag)] 擴充功能選取於 [!UICONTROL 擴充功能] 在中檢視 [!UICONTROL 資料彙集] UI。](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

安裝對話方塊隨即顯示。 從此處選取 **[!UICONTROL 新增帳戶]** 並在出現提示時提供下列值：

| 帳戶屬性 | 描述 |
| --- | --- |
| 帳戶名稱 | 帳戶的唯一名稱。 此名稱僅用於標籤UI。 |
| 帐户 ID | 您的 [!DNL Google Ads] 帳戶ID。 若要尋找此值，請登入 [!DNL Google Ads] 並導覽至： **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**. 帳戶ID字串可在開頭為的程式碼片段視窗中找到 `AW-` 或 `d`. |
| 产品 | 選取 **[!UICONTROL Google Ads (AdWords)]**. |

{style="table-layout:auto"}

完成後，選取 **[!UICONTROL 新增帳戶]**，然後選取 **[!UICONTROL 儲存]**.

### 新增傳送轉換動作 {#conversion-action-tags}

安裝擴充功能後，您就可以開始將轉換動作納入標籤規則。 建立或編輯監聽要增強之轉換的規則時，請選取 **[!UICONTROL 新增]** 在 [!UICONTROL 動作]. 在下一個對話方塊中，選取 **[!UICONTROL Google全域網站標籤(gtag)]** 從 [!UICONTROL 副檔名] 下拉式清單，然後選取 **[!UICONTROL 傳送事件]** 在 [!UICONTROL 動作型別].

![此 [!UICONTROL 傳送事件] 在規則編輯工作流程的動作設定檢視中選取的動作型別。](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

會出現其他控制項，讓您設定 [!DNL gtag] 事件。 至少必須填寫下列欄位：

1. **[!UICONTROL 事件名稱（動作）]**：輸入 `conversion` 做為值。
1. 新增索引鍵為的新欄位 `transaction_id` 而值是 [資料元素](../../../ui/managing-resources/data-elements.md) 包含 [交易ID](https://support.google.com/google-ads/answer/6386790) 值。
1. **[!UICONTROL 轉換標籤]**：輸入適當的轉換標籤，來自 [!DNL Google Ads] 帳戶。 若要尋找此值，請登入Google Ads並導覽至 **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. 轉換標籤位於 [!DNL Instructions].
   >[!IMPORTANT]
   >
   >當您在「 」的標籤設定區域時， [!DNL Google Ads] 帳戶，確定已啟用增強型轉換。 若要這麼做，請檢閱並接受服務條款，然後選取 **[!DNL Turn on enhanced conversions]** 和 **[!DNL API]** 作為實作方法。

設定動作後，選取 **[!UICONTROL 保留變更]** 以將動作新增至規則設定。 如果您對規則滿意，請選取 **[!UICONTROL 儲存至程式庫]**.

最後，發佈新的 [建置](../../../ui/publishing/builds.md) 以啟用程式庫的變更。

## 使用事件轉送功能傳送第一方資料

一旦您能夠從使用者端傳送轉換事件，您就可以使用 [!DNL Enhanced Conversions] 事件轉送擴充功能。

### 建立Google OAuth 2密碼和資料元素 {#create-secret-data-element}

在設定擴充功能之前，您必須在事件轉送中建立存取Token，以驗證至 [!DNL Google Ads] API。

請參閱指南： [建立事件轉送密碼](../../../ui/event-forwarding/secrets.md) 以取得詳細步驟。 確定您選取 **[!UICONTROL Google OAuth 2]** 作為秘密型別。 繼續依照提示進行，並在系統要求您選取Google帳戶設定檔時，請選取可存取您正在設定的轉換動作的帳戶。

建立密碼後， [建立新資料元素](../../../ui/managing-resources/data-elements.md#create-a-data-element) 並選取 **[!UICONTROL 密碼]** （資料元素型別）。 為每個環境選取適當的Google OAuth 2密碼，然後選取 **[!UICONTROL 儲存至程式庫]**.

### 設定並安裝 [!DNL Enhanced Conversions] 擴充功能 {#install-enhanced-conversions}

尋找 [!UICONTROL Google Ads增強型轉換] 事件轉送目錄中的擴充功能並選取「 」 **[!UICONTROL 安裝]**.

![此 [!UICONTROL Google Ads增強型轉換] 擴充功能選取於 [!UICONTROL 擴充功能] 在中檢視 [!UICONTROL 資料彙集] UI。](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

若要設定擴充功能，您必須填入兩個必填欄位：

1. **[!UICONTROL 客戶ID]**：可唯一識別您的 [!DNL Google Ads] 帳戶。 若要尋找此值，請登入 [!DNL Google Ads] 並導覽至 **[!DNL Help]** > **[!DNL Customer ID]**.
1. **[!UICONTROL 存取Token資料元素]**：選取資料元素圖示(![資料元素圖示](../../../images/extensions/server/google-ads-enhanced-conversions/data-element-icon.png))，然後選擇您所使用的Google OAuth 2機密資料元素 [在上一步中設定](#create-secret-data-element) 功能表中的。

完成後，選取 **[!UICONTROL 儲存]** 以安裝擴充功能。

### 新增 [!UICONTROL 傳送轉換] 規則的動作 {#conversion-action-event-forwarding}

安裝擴充功能後，您可以開始包含 [!UICONTROL 傳送轉換] 動作。 建立或編輯監聽要增強之轉換的規則時，請選取 **[!UICONTROL 新增]** 在 [!UICONTROL 動作]. 在下一個對話方塊中，選取 **[!UICONTROL Google Ads增強型轉換]** 從 [!UICONTROL 副檔名] 下拉式清單，然後選取 **[!UICONTROL 傳送轉換]** 在 [!UICONTROL 動作型別].

![此 [!UICONTROL 傳送轉換] 在規則編輯工作流程的動作設定檢視中選取的動作型別。](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

新的控制項會顯示在右側面板中，供您設定轉換。 至少必須完成下列欄位：

**轉換資訊**

| 輸入 | 描述 |
| --- | --- |
| 客户 ID | 您的 [!DNL Google Ads] 客戶ID。 預設為您在下列情況下輸入的客戶識別碼： [安裝擴充功能](#install-enhanced-conversions). |
| 轉換ID或轉換標籤 | 追蹤值取得自 [!DNL Google Ads] 設定轉換追蹤時。 值開頭為 `AW-`.<br><br>如需如何尋找這些值的詳細資訊，請參閱 [[!DNL Google Ads] 檔案](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| Transaction ID | 選取具有相同交易ID值的資料元素，該值 [從使用者端傳送](#conversion-action-tags) 使用 [!DNL Google Global Site Tag] 副檔名。 |

**使用者識別**

* 至少必須包含三個使用者識別碼中的一個：
   * 电子邮件
   * 電話號碼
   * 完整地址

>[!TIP]
>
>必須先雜湊使用者識別資料，才能將其傳送至Google。 如果事件轉送收到資料時，資料並未進行雜湊處理，請選取 **[!UICONTROL 標準化與雜湊]** 開啟指定欄位，指示擴充功能將值雜湊。
>
>![此 [!UICONTROL 標準化與雜湊] 已為以下專案啟用切換： [!UICONTROL 電子郵件] 輸入於 [!UICONTROL 傳送轉換] 動作設定表單。](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

完成後，選取 **[!UICONTROL 保留變更]** 以將動作新增至規則設定。 如果您對規則滿意，請選取 **[!UICONTROL 儲存至程式庫]**.

最後，發佈新的事件轉送 [建置](../../../ui/publishing/builds.md) 以啟用程式庫的變更。

## 后续步骤

本指南說明如何將轉換事件傳送至 [!DNL Google Ads] 使用 [!DNL Enhanced Conversions] 事件轉送擴充功能。 如需Experience Platform中事件轉送功能的詳細資訊，請參閱 [事件轉送概觀](../../../ui/event-forwarding/overview.md).
