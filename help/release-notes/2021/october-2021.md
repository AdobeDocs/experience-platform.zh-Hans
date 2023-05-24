---
title: Adobe Experience Platform發行說明2021年10月
description: Adobe Experience Platform的2021年10月發行說明。
exl-id: 8f8bcb24-6478-4281-9362-9559158384af
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 8%

---

# Adobe Experience Platform 发行说明

**发行日期：2021 年 10 月 27 日**

## Experience Platform的更新

Experience Platform的更新。

### 用户界面 {#ui}

使用者介面已更新，其中包含下列變更：

| 功能 | 描述 |
| --- | --- |
| 深色主题 | 在Platform介面中，使用深色佈景主題切換開關在淺色和深色佈景主題之間切換。 交換器位於使用者名稱和電子郵件下方的使用者設定檔中。 |
| 切換左側導覽 | 使用應用程式標題頂端的改良導覽切換功能，可顯示或隱藏顯示Experience Platform功能的功能表。 系統會記住您最後的選擇，並僅顯示您有權存取的功能。 |
| 存取可見性 | 左側導覽列僅顯示您可以存取的功能。 在舊版Adobe Experience Platform中，即使您無法存取不可用的專案，也會顯示不可用的專案。 |

請參閱 [Platform UI指南](../../landing/ui-guide.md) 以深入瞭解。

## 現有功能的更新

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Prep]](#data-prep)
- [源](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 可讓資料工程師對應、轉換及驗證與Experience Data Model (XDM)之間的資料。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| `contains_key` 函数 | 此 `contains_key` 函式已匯入，可讓您檢查來源內是否有物件。 此函式取代 `is_set` 函式，現已棄用。 |
| 错误消息 | 傳回的錯誤訊息 `/mappingSets/preview` 「資料準備API」中的端點現在與執行階段產生的錯誤訊息一致。 |

請參閱 [[!DNL Data Prep] 概觀](../../data-prep/home.md) 以進一步瞭解此服務。

### 源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

| 功能 | 描述 |
| --- | --- |
| [!DNL Amazon S3] 來源增強功能 | 您現在可以使用 `s3SessionToken` 用於連線您的 [!DNL Amazon S3] 使用臨時安全性憑證的帳戶至Platform。 此Token可讓您對您的提供短期、暫時的存取權 [!DNL Amazon S3] 資源提供給不受信任環境中的使用者。 有关详细信息，请参阅[[!DNL Amazon S3] 文档](../../sources/connectors/cloud-storage/s3.md#prerequisites)。 |
| [!DNL Generic REST API] (Beta) | 您現在可以建立 [!DNL Generic REST API] 來源連線使用 [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) 將一般REST應用程式的資料帶入Platform。 請參閱 [[!DNL Generic REST API] 概觀](../../sources/connectors/protocols/generic-rest.md) 以取得詳細資訊。 |
| [!DNL Zoho CRM] (Beta) | 您現在可以建立 [!DNL Zoho CRM] 來源連線使用 [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) 或 [使用者介面](../../sources/tutorials/ui/create/crm/zoho.md) 將資料從您的 [!DNL Zoho CRM] 至平台的帳戶。 請參閱 [[!DNL Zoho CRM] 概觀](../../sources/connectors/crm/zoho.md) 以取得詳細資訊。 |

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md).
