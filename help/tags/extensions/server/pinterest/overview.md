---
keywords: 事件轉送擴充功能；pinterest；pinterest事件轉送擴充功能
title: pinterest事件轉送擴充功能
description: 此Adobe Experience Platform事件轉送擴充功能可讓您將事件擷取至Pinterest，以滿足您的業務需求。
last-substantial-update: 2023-04-27T00:00:00Z
source-git-commit: 87c76ef4b95bc05a64d9d124d69c2a51b7b77c08
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 4%

---

# [!DNL Pinterest] 事件轉送擴充功能

[!DNL Pinterest] 是視覺探索引擎，用於尋找配方、家庭裝飾、風格靈感等概念。 有數十億個圖釘 [!DNL Pinterest]，也可在上與其他人共用 [!DNL Pinterest]. 您可以整理使用者互動事件並運用 [!DNL Pinterest Analytics] 以瞭解使用者行為並執行鎖定目標的廣告。

此 [[!DNL Pinterest] 轉換](https://developers.pinterest.com/docs/conversions/conversion-management/) API [事件轉送](../../../ui/event-forwarding/overview.md) 擴充功能可讓您運用Adobe Experience Platform Edge Network中擷取的資料，並將其傳送至 [!DNL Pinterest]. 本檔案說明擴充功能的使用案例、安裝方式，以及如何將其功能整合至事件轉送中 [規則](../../../ui/managing-resources/rules.md).

轉換存取權杖為使用的驗證方法 [!DNL Pinterest] 與互動時 [!DNL Pinterest] API。

## 用例

如果您想要使用來自Edge Network的資料，請使用此擴充功能 [!DNL Pinterest] 以善用其Customer Analytics功能。

例如，以組織中的行銷團隊為例。 團隊會從他們的網站擷取使用者互動事件資料，並將其載入到 [!DNL Pinterest] 使用此事件轉送擴充功能。

行銷與分析團隊就可以善用 [!DNL Pinterest] Analytics功能，可瞭解關鍵使用者互動和行為，讓您更瞭解使用者，並針對鎖定目標的廣告促銷活動鎖定使用者。

如需特定使用案例的詳細資訊，請參閱 [!DNL Pinterest]，請參閱 [[!DNL Pinterest] 使用案例](https://business.pinterest.com/en/success-stories) 說明檔案。

## [!DNL Pinterest] 必備條件 {#prerequisites}

您必須具備有效的 [!DNL Pinterest] [商業帳戶](https://help.pinterest.com/en/business/article/get-a-business-account) 才能使用此擴充功能。 前往 [[!DNL Pinterest] 註冊頁面](https://www.pinterest.com/business/create/) 註冊並建立帳戶。

您還需要 [!DNL Pinterest] 開發人員帳戶，需要與您建立關聯 [!DNL Pinterest] 商業帳戶。 若要將您的開發人員帳戶與企業帳戶建立關聯，請參閱 [[!DNL Pinterest ] 開發人員帳戶](https://developers.pinterest.com/account-setup/).

### 收集必要的設定詳細資料 {#configuration-details}

為了將Experience Platform連線到 [!DNL Pinterest]，需要下列輸入：

| 認證 | 描述 | 示例 |
| --- | --- | --- |
| 廣告帳戶ID | 您的 [!DNL Pinterest] 廣告帳戶ID。 請參閱 [[!DNL Pinterest] 檔案](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager) 以取得指引。 | 123456789012 |
| 轉換存取權杖 | 您的 [!DNL Pinterest] 轉換存取Token。 請參閱 [[!DNL Pinterest] 轉換API](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token) 指引檔案。 <br> **您只需執行此動作一次，因為此Token並未過期。** | {YOUR_PINTEREST_BEARER_TOKEN} |

## 安裝並設定 [!DNL Pinterest] 擴充功能 {#install}

若要安裝擴充功能， [建立事件轉送屬性](../../../ui/event-forwarding/overview.md#properties) 或選擇現有屬性進行編輯。

在左側導覽中，選取 **[!UICONTROL 擴充功能]**. 選取 **[!UICONTROL 安裝]** 在的卡片上 [!DNL Pinterest] 中的擴充功能 **[!UICONTROL 目錄]** 標籤。

![目錄顯示 [!DNL Pinterest] 擴充功能，搭配 [!UICONTROL 安裝] 反白顯示。](../../../images/extensions/server/pinterest/install.png)

### 配置 [!DNL Pinterest] 扩展

>[!IMPORTANT]
>
>根據您的實作需求，您可能需要在設定擴充功能前建立結構、資料元素和資料集。 開始之前，請先檢閱所有設定步驟，以決定您需要為使用案例設定的實體。

在左側導覽中，選取 **[!UICONTROL 擴充功能]**. 選取 **[!UICONTROL 設定]** 在的卡片上 [!DNL Pinterest] 中的擴充功能 [!UICONTROL 已安裝]**標籤。

![[!DNL Pinterest] 擴充功能顯示於 [!UICONTROL 安裝] 定位方式 [!UICONTROL 設定] 反白顯示。](../../../images/extensions/server/pinterest/configure.png)

在下一個畫面中，輸入 [!UICONTROL 廣告帳戶ID] 和 [!UICONTROL 轉換存取權杖] 您之前收集於 [設定詳細資料](#configuration-details) 區段。 完成後，選取 **[!UICONTROL 儲存]**.

![此 [!DNL Pinterest] [!UICONTROL 設定] 熒幕醒目提示 [!UICONTROL 廣告帳戶ID] 和 [!UICONTROL 轉換存取權杖] 輸入欄位。](../../../images/extensions/server/pinterest/input.png)

## 設定事件轉送規則 {#config-rule}

設定好所有資料元素後，您就可以開始建立事件轉送規則，判斷將事件傳送至的時間和方式 [!DNL Pinterest].

建立新的 [規則](../../../ui/managing-resources/rules.md) 在事件轉送屬性中。 下 **[!UICONTROL 動作]**，新增動作並將擴充功能設為 **[!UICONTROL pinterest]**. 傳送Adobe Experience Edge Network事件至 [!DNL Pinterest]，設定 **[!UICONTROL 動作型別]** 至 **[!UICONTROL 傳送事件].**

![此 [!DNL Pinterest] [!UICONTROL 傳送事件] 規則建立。](../../../images/extensions/server/pinterest/rule.png)

選取後，會出現其他控制項以進一步設定事件。 您需要對應 [!DNL Pinterest] 事件屬性至您先前建立的資料元素。

### [!UICONTROL 事件資料]

建立新規則需要下列事件資料：

| 字段名称 | 描述 | 示例 |
| --- | --- | --- | 
| [!UICONTROL 活动名称] | 使用者事件的型別。 不過，這可以是任何事件型別，以便運用 [!DNL Pinterest Analytics] 建議使用 [[!DNL Pinterest] 事件代碼](https://help.pinterest.com/en/business/article/add-event-codes) | *結帳 <br> * add_to_cart <br> * page_visit <br> *註冊 <br> * [使用者定義的事件] |
| [!UICONTROL 動作來源] | 表示轉換事件發生位置的來源。 | * app_android <br> * app_ios <br> *網頁 <br> *離線 |
| [!UICONTROL 事件時間] | 這是指事件時間。 使用的預設時間格式為UNIX，格式為 `<seconds>.<miliseconds>` 視您的當地時區而定。 如需詳細資訊，請參閱 [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create). | 1433188255.500表示在epoch之後的1433188255秒和500毫秒，或2015年6月1日星期一的7秒:50:格林威治標準時間下午55點。 |
| [!UICONTROL 事件ID] | 此唯一ID字串可識別此事件，並可用於透過轉換API和Pinterest追蹤所擷取事件之間的重複資料刪除。 若沒有此專案，事件的資料可能會重複計算，並回報量度膨脹。 | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL 事件屬性] | 包含事件的自訂屬性的JSON物件。 從提供原始JSON或使用一組簡化的鍵值輸入進行選取。 | { &quot;event_source_url&quot;： &quot;http://site.com&quot; } |

![此 [!DNL Pinterest] [!UICONTROL 事件資料] 在「規則」動作中反白顯示。](../../../images/extensions/server/pinterest/event-data.png)

可設定下列事件屬性：

| 字段名称 | 描述 |
| --- | --- |
| 事件來源URL | 網頁轉換事件的URL。 |
| 應用程式存放區ID | 應用程式商店應用程式ID。 |
| 应用程序名称 | 應用程式的名稱。 |
| Application Version | 應用程式的版本。 |
| 裝置品牌 | 使用者正在使用的裝置品牌。 |
| 裝置載體 | 使用者裝置的行動電信業者。 |
| 裝置型號 | 使用者裝置的型號。 |
| Device Type | 使用者使用的裝置型別。 |
| 作業系統版本 | 裝置的作業系統版本。 |
| 使用者語言 | 表示使用者語言的雙字元ISO-639-1語言代碼。 |

### [!UICONTROL 使用者資料]

下列使用者資料可由輸入，這些不是必填欄位：

| 字段名称 | 描述 | 示例 |
| --- | --- | --- | 
| [!UICONTROL 电子邮件] | 使用者電子郵件地址或使用者地址電子郵件的SHA256雜湊。 | ebd543592...f2b7e1 |
| [!UICONTROL 行動廣告ID] | 使用者的「Google Advertising ID」(GAID)或「Apple的廣告商識別碼」(IDFA)的Sha256雜湊 | ebd543592...f2b7e1 |
| [!UICONTROL 使用者端IP位址] | 使用者的IP位址，可以是IPv4或IPv6格式。 用於比對。 | 192.168.0.1 |
| [!UICONTROL 使用者端使用者代理] | 使用者網頁瀏覽器的使用者代理字串。 | Mozilla/5.0 （平台；rv：geckoversion） Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL 客戶資訊資料] | 包含其他客戶資訊的JSON物件。 從提供原始JSON或使用一組簡化的鍵值輸入進行選取。 | { &quot;ph&quot;： &quot;122333445&quot; } |

![此 [!DNL Pinterest] [!UICONTROL 使用者資料] 在「規則」動作中反白顯示。](../../../images/extensions/server/pinterest/user-data.png)

可設定的客戶資訊屬性包括：

| 字段名称 | 描述 |
| --- | --- |
| Phone | 使用者聯絡電話。 只接受數字，並應使用國碼、區碼和數字輸入。 |
| 性别 | 性別可以輸入為「f」代表女性、「m」代表男性、或「n」代表非二進位。 |
| 出生日期 | 以年、月、日形式輸入的出生日期。 |
| 姓氏 | 使用者的姓氏。 |
| 名字 | 使用者的名字。 |
| 城市 | 使用者的居住城市。 這主要用於計費目的。 |
| State | 使用者狀態，以小寫提供為兩個字母的程式碼。 |
| 邮政编码 | 使用者的郵遞區號，主要用於計費用途。 |
| 国家/地区 | 表示使用者國家/地區的兩個字元ISO-3166國家/地區代碼。 |
| 外部ID | 來自廣告商的唯一ID，可識別其空間中的使用者。 例如，使用者ID、忠誠度ID等。 |
| 點按ID | 儲存在網域上_epik Cookie或URL中&amp;epik=查詢引數的唯一識別碼。 |

>[!IMPORTANT]
>
>將資料傳送至之前 [!DNL Pinterest] API端點，擴充功能會將下列欄位的值雜湊並正規化：電子郵件、電話號碼、名字、姓氏、性別、出生日期、城市、州、郵遞區號、國家/地區和外部ID。 如果已經存在SHA256字串，擴充功能將不會雜湊這些欄位的值。

### [!UICONTROL 自訂資料]

您可以為規則輸入下列自訂資料：

| 字段名称 | 描述 |
| --- | --- |
| 货币 | ISO-4217貨幣代碼。 如果未提供， [!DNL Pinterest] 將預設為在帳戶建立期間設定的廣告商貨幣。 |
| 值 | 事件的總值。 已接受為請求中的字串。 這將會剖析為雙位數。 |
| 搜尋字串 | 與使用者轉換事件相關的搜尋字串。 |
| 訂單ID | 訂單ID。 傳送中 `order_id` 會有所幫助 [!DNL Pinterest] 必要時刪除重複事件。 |
| 產品數量 | 事件的產品總數。 例如，在結帳事件中購買的專案總數。 |
| 內容ID | 產品ID清單（陣列）。 |
| 内容 | 包含產品相關資訊（例如價格和數量）的物件清單（陣列）。 |

![此 [!DNL Pinterest] [!UICONTROL 自訂資料] 在「規則」動作中反白顯示。](../../../images/extensions/server/pinterest/custom-data.png)

## 驗證中的資料 [!DNL Pinterest]

建立並執行事件轉送規則後，請驗證是否已將事件傳送至 [!DNL Pinterest] API會如預期般顯示在中 [!DNL Pinterest] UI。

如果事件集合和 [!DNL Experience Platform] 整合成功，您將會在 [!DNL Pinterest] UI。

![此 [!DNL Pinterest] 事件管理員](../../../images/extensions/server/pinterest/event-history.png)

您可以進一步鑽研並檢視 [!DNL Pinterest] 事件資料分佈。

![此 [!DNL Pinterest] 資料分佈](../../../images/extensions/server/pinterest/event-history-distribution.png)

## 后续步骤

本指南說明如何安裝和設定 [!DNL Pinterest] UI中的事件轉送擴充功能。 如需詳細資訊，請參閱正式檔案：

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] 轉換API概觀](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
