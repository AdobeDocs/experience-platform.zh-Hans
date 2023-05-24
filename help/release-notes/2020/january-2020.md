---
title: Adobe Experience Platform發行說明2020年1月
description: Adobe Experience Platform的2020年1月發行說明。
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 9%

---

# Adobe Experience Platform 发行说明

**发行日期：2020 年 1 月 15 日**

Adobe Experience Platform 现有功能的更新包括：

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## [!DNL Experience Data Model] (XDM)系統 {#xdm}

標準化和互用性是背後的重要概念 [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM)以Adobe為導向，致力於標準化客戶體驗資料並定義客戶體驗管理的結構。

XDM是公開記錄的規格，旨在改善數位體驗的力量。 它為任何應用程式提供通用結構和定義，以便與Adobe Experience Platform上的服務通訊。 藉由遵守XDM標準，所有客戶體驗資料都可以整合到通用表示中，以更快、更整合的方式提供深入分析。 您可以從客戶動作獲得有價值的深入分析、透過區段定義客戶對象，以及使用客戶屬性進行個人化。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 相同階層欄位的欄位型別限制 | 將XDM欄位定義為特定型別後，無論使用相同名稱和階層的任何其他欄位或結構描述欄位群組，都必須使用相同的欄位型別。 例如，如果XDM的欄位群組 [!DNL Profile] 類別包含 `profile.age` 「整數」型別的欄位，XDM的類似欄位群組 [!DNL ExperienceEvent] 不能有 `profile.age` 「字串」型別的欄位。 為了使用不同的欄位型別，欄位必須與先前定義的欄位具有不同的階層(例如， `profile.person.age`)。 此功能旨在防止將結構描述集合在聯合中時發生衝突。 雖然限制不會回溯影響現有結構描述，但強烈建議您檢閱結構描述是否有欄位型別衝突，並視需要加以編輯。 |
| 區分大小寫的欄位驗證 | 相同層級上的自訂欄位必須有不同的名稱，無論大小寫為何。 例如，如果您新增名為「電子郵件」的自訂欄位，則無法在名為「電子郵件」的相同層級新增另一個自訂欄位。 |

**已知问题**

* None

若要進一步瞭解如何使用XDM [!DNL Schema Registry] API和 [!DNL Schema Editor] 使用者介面，請閱讀 [XDM系統檔案](../../xdm/home.md).

## [!DNL Privacy Service] {#privacy}

新的法律和组织规定正在用户提供相应的权利，允许他们请求访问或删除您的数据存储中的用户个人数据。Adobe Experience Platform [!DNL Privacy Service] 提供RESTful API和使用者介面，協助您管理客戶的這些資料請求。 替換為 [!DNL Privacy Service]，您可以提交存取和刪除Adobe Experience Cloud應用程式中私人或個人客戶資料的請求，協助實現法律和組織隱私法規的自動合規性。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| [!DNL Privacy Service] 品牌重塑 | 先前稱為「GDPR服務」的服務品牌已變更為 [!DNL Privacy Service] 隨著服務的成長，除了GDPR之外，還支援其他法規。 |
| 新API端點 | 的基礎路徑 [!DNL Privacy Service] API更新自 `/data/privacy/gdpr` 至 `/data/core/privacy/jobs`. |
| 需要新增 `regulation` 屬性 | 在中建立新工作時 [!DNL Privacy Service] API， a `regulation` 請求承載中必須提供屬性，以指出要追蹤其下之工作的法規。 接受的值為 `gdpr` 和 `ccpa`. |
| 支持 [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] 現在接受來自Adobe的存取/刪除請求 [!DNL Primetime Authentication]，使用 `primetimeAuthentication` 作為其產品價值。 |
| Privacy Service UI增強功能 | GDPR和CCPA法規的個別工作追蹤頁面。 全新**法規型別**下拉式清單，可切換GDPR和CCPA的追蹤資料。 |

**已知问题**

* None

如需有關的詳細資訊 [!DNL Privacy Service]，請先閱讀 [Privacy Service概觀](../../privacy-service/home.md).

## 源 {#sources}

Adobe Experience Platform可從外部來源內嵌資料，同時允許您使用建構、加標籤及增強該資料 [!DNL Platform] 服務。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 支援客戶屬性資料 | 用於建立串流聯結器以擷取客戶屬性資料的UI和API支援。 |
| 雲端儲存的其他檔案格式支援 | 從雲端儲存區擷取的檔案現在支援XDM相容的Parquet和JSON檔案格式。 |
| 存取控制許可權支援 | Adobe Experience Platform中的存取控制架構提供授予資料擷取中來源存取權所需的許可權。 根據使用者的許可權層級，使用者可以檢視來源、管理來源或被完全拒絕存取。 |

**存取控制許可權**

| 类别 | 权限 | 描述 |
|--- | --- | ---|
| 数据引入 | 管理來源 | 讀取、建立、編輯和停用來源的存取權。 |
| 数据引入 | 檢視來源 | 對中的可用來源具有唯讀存取權 **[!UICONTROL 目錄]** 索引標籤和已驗證的來源 **[!UICONTROL 瀏覽]** 標籤。 |

**已知问题**

* None

如需來源的詳細資訊，請參閱 [來源概觀](../../sources/home.md)

## 目标 {#destinations}

在 [Real-Time CDP](../../rtcdp/overview.md)，目的地是預先建立的與目的地平台的整合，可透過順暢的方式為這些合作夥伴啟用資料。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 存取控制許可權支援 | Real-Time CDP中的目的地功能可搭配Adobe Experience Platform存取控制許可權使用。 您可以檢視、管理和啟用目的地，實際取決於您的使用者許可權等級。 |

**存取控制許可權**

| 类别 | 权限 | 描述 |
|--- | --- | ---|
| 目标 | 管理目的地 | 讀取、建立、編輯和停用目的地的存取權。 |
| 目标 | 檢視目的地 | 以唯讀方式存取中的可用目的地 **[!UICONTROL 目錄]** 索引標籤和已驗證的目標 **瀏覽** 標籤。 |
| 目标 | 啟用目的地 | 能夠將資料啟用至目的地。 此許可權需要將「管理目的地」或「檢視目的地」新增至產品設定檔。 |

**已知问题**

* None

請參閱 [目的地概觀](../../destinations/home.md) 以取得詳細資訊。
