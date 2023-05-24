---
keywords: 設定檔；即時客戶設定檔；疑難排解；護欄；指引；限制；實體；主要實體；維度實體；RTCDP；CDP；B2B Edition；Real-time Customer Data Platform；即時客戶資料平台；real time cdp；b2b；cdp；
title: Real-time Customer Data Platform B2B版本的預設護欄
type: Documentation
description: Adobe Experience Platform 使用与传统关系数据模型不同的高度非规范化混合数据模型。本檔案提供預設的使用和速率限制，協助您使用Adobe Real-time Customer Data Platform B2B Edition為資料建立模型，以獲得最佳系統效能。
exl-id: 8eff8c3f-a250-4aec-92a1-719ce4281272
source-git-commit: 6327f5e6cb64a46c502613dd6074d84ed1fdd32b
workflow-type: tm+mt
source-wordcount: '1651'
ht-degree: 2%

---

# Real-time Customer Data Platform B2B版本的預設護欄

>[!NOTE]
>
>本檔案中概述的限制代表Real-time Customer Data Platform B2B Edition啟用的變更。 如需Real-Time CDP Adobe Experience Platform B2B版本的完整預設限制清單，請將這些限制與 [即時客戶設定檔資料檔案的護欄](../profile/guardrails.md).

Real-time Customer Data Platform B2B Edition可讓您根據行為深入分析和客戶屬性，以即時客戶設定檔和帳戶設定檔的形式，提供個人化的跨頻道體驗。 為了支援這種處理設定檔的新方法，Experience Platform使用與傳統關聯式資料模型不同的高度非標準化混合資料模型。

本檔案提供預設的使用和速率限制，幫助您為資料建立模型以獲得最佳系統效能。 檢閱下列護欄時，系統假設您已正確模型化資料。 如果您有任何關於如何建立資料模型的問題，請聯絡您的客戶服務代表。

>[!INFO]
>
>大多數客戶不會超過這些預設限制。 如果您想瞭解自訂限制，請聯絡客戶服務代表。

## 限制型別

本檔案有兩種預設限制：

* **軟限制：** 可以超出軟限制，但軟限制提供系統效能的建議指引。

* **硬限制：** 硬限制提供絕對最大值。

>[!INFO]
>
>本檔案中概述的限制正在不斷改進。 請定期回來檢視更新。 如果您有興趣瞭解自訂限制，請聯絡客戶服務代表。

## 資料模型限制

在模型化即時客戶設定檔資料時，下列護欄會提供建議的限制。 若要進一步瞭解主要實體和維度實體，請參閱以下小節： [實體型別](#entity-types) 在附錄中。

### 主要實體護欄

>[!NOTE]
>
>本節中概述的資料模型限制代表Real-time Customer Data Platform B2B Edition啟用的變更。 如需Real-Time CDP Adobe Experience Platform B2B版本的完整預設限制清單，請將這些限制與 [即時客戶設定檔資料檔案的護欄](../profile/guardrails.md).

| 護欄 | 限制 | 限制型別 | 描述 |
| --- | --- | --- | --- |
| Real-Time CDP B2B Edition標準XDM類別資料集 | 60 | 柔和 | 建議使用最多60個資料集，這些資料集會利用Real-Time CDP B2B版本提供的標準Experience Data Model (XDM)類別。 如需B2B使用案例的標準XDM類別的完整清單，請參閱 [Real-Time CDP B2B版本檔案中的結構描述](schemas/b2b.md). <br/><br/>*注意：由於Experience Platform非標準化混合資料模型的性質，大部分客戶不會超過此限制。 有關如何為您的資料建立模型的問題，或如果您想進一步瞭解自訂限制，請聯絡您的客戶服務代表。* |
| 舊版多實體關係 | 20 | 柔和 | 建議在主要實體和維度實體之間定義最多20個多實體關係。 在移除或停用現有關聯性之前，不應進行其他關聯性對應。 |
| 每個XDM類別的多對一關係 | 2 | 柔和 | 建議每個XDM類別最多定義2個多對一關係。 在移除或停用現有關係之前，不應建立其他關係。 如需如何在兩個結構描述之間建立關係的步驟，請參閱的教學課程： [定義B2B結構描述關係](../xdm/tutorials/relationship-b2b.md). |

### Dimension實體護欄

>[!NOTE]
>
>本節中概述的資料模型限制代表Real-time Customer Data Platform B2B Edition啟用的變更。 如需Real-Time CDP Adobe Experience Platform B2B版本的完整預設限制清單，請將這些限制與 [即時客戶設定檔資料檔案的護欄](../profile/guardrails.md).

| 護欄 | 限制 | 限制型別 | 描述 |
| --- | --- | --- | --- |
| 無巢狀舊版關係 | 0 | 柔和 | 您不應在兩個非關聯式之間建立關聯[!DNL XDM Individual Profile] 結構描述。 不建議將建立關係的功能用於不屬於的任何結構描述。 [!DNL Profile] 聯合結構描述。 |
| 只有B2B物件可以參與多對一關係 | 0 | 硬 | 系統僅支援B2B物件之間的多對一關係。 如需多對一關係的詳細資訊，請參閱以下教學課程： [定義B2B結構描述關係](../xdm/tutorials/relationship-b2b.md). |
| B2B物件之間巢狀關係的最大深度 | 3 | 硬 | B2B物件之間巢狀關係的最大深度為3。 這表示在高度巢狀的結構描述中，不應在巢狀層級超過3層的B2B物件之間建立關係。 |

## 資料大小限制

下列護欄會參照資料大小，針對可依預期擷取、儲存及查詢的資料提供建議的限制。 若要進一步瞭解主要實體和維度實體，請參閱以下小節： [實體型別](#entity-types) 在附錄中。

>[!INFO]
>
>資料大小是在內嵌時以JSON的未壓縮資料來測量。

### 主要實體護欄

>[!NOTE]
>
>本節中概述的資料大小限制代表Real-time Customer Data Platform B2B Edition啟用的變更。 如需Real-Time CDP Adobe Experience Platform B2B版本的完整預設限制清單，請將這些限制與 [即時客戶設定檔資料檔案的護欄](../profile/guardrails.md).

| 護欄 | 限制 | 限制型別 | 描述 |
| --- | --- | --- | --- |
| 每日每個XDM類別擷取的批次 | 45 | 柔和 | 每個XDM類別每天擷取的批次總數不應超過45。 擷取其他批次可能會妨礙最佳效能。 |

### Dimension實體護欄

>[!NOTE]
>
>本節中概述的資料大小限制代表Real-time Customer Data Platform B2B Edition啟用的變更。 如需Real-Time CDP Adobe Experience Platform B2B版本的完整預設限制清單，請將這些限制與 [即時客戶設定檔資料檔案的護欄](../profile/guardrails.md).

| 護欄 | 限制 | 限制型別 | 描述 |
| --- | --- | --- | --- |
| 所有維度實體的總大小 | 5 GB | 柔和 | 建議所有維度實體的總大小為5GB。 擷取大型尺寸圖元可能會影響系統效能。 例如，不建議嘗試載入10GB產品目錄作為維度實體。 |
| 每個維度實體結構描述的資料集 | 5 | 柔和 | 建議每個維度實體結構描述最多關聯5個資料集。 例如，如果您為「產品」建立結構描述，並新增五個貢獻資料集，則不應建立與產品結構描述繫結的第六個資料集。 |
| 每日擷取的Dimension實體批次 | 每個實體4個 | 柔和 | 建議每天擷取的維度實體批次數量上限為每個實體4個。 例如，您每天最多可以擷取4次產品目錄的更新。 擷取相同實體的其他維度實體批次可能會影響系統效能。 |

## 分段護欄

本節中概述的護欄是指組織可在Experience Platform內建立的區段數量和性質，以及對應及啟用區段至目的地。

>[!NOTE]
>
>本節中概述的區段限制代表Real-time Customer Data Platform B2B版本啟用的變更。 如需Real-Time CDP Adobe Experience Platform B2B版本的完整預設限制清單，請將這些限制與 [即時客戶設定檔資料檔案的護欄](../profile/guardrails.md).

| 護欄 | 限制 | 限制型別 | 描述 |
| --- | --- | --- | --- |
| 每個B2B沙箱的區段 | 400 | 柔和 | 只要每個個別B2B沙箱中有少於400個區段，組織總共可以有400多個區段。 嘗試建立其他區段可能會影響系統效能。 |

## 后续步骤

本檔案中概述的限制代表Real-time Customer Data Platform B2B Edition啟用的變更。 如需Real-Time CDP Adobe Experience Platform B2B版本的完整預設限制清單，請將這些限制與 [即時客戶設定檔資料檔案的護欄](../profile/guardrails.md).

## 附录

本節提供本檔案中限制的更多詳細資料。

### 實體型別

此 [!DNL Profile] 存放區資料模型包含兩種核心實體型別： [主要實體](#primary-entity) 和 [維度圖元](#dimension-entity).

#### 主要實體

主要實體或設定檔實體會將資料合併在一起，為個人形成「單一真實來源」。 此統一資料使用所謂的「聯合檢視」表示。 聯合檢視會將實施相同類別的所有結構描述的欄位彙總到單一聯合結構描述中。 的聯合結構描述 [!DNL Real-Time Customer Profile] 是一個非正規化的混合資料模型，可作為所有設定檔屬性和行為事件的容器。

與時間無關的屬性（也稱為「記錄資料」）是使用 [!DNL XDM Individual Profile]，而時間序列資料（也稱為「事件資料」）的模型化使用 [!DNL XDM ExperienceEvent]. 在Adobe Experience Platform中擷取記錄和時間序列資料時，就會觸發 [!DNL Real-Time Customer Profile] 以開始擷取已啟用的資料。 內嵌的互動和詳細資訊越多，個別設定檔就越健全。

![概述記錄資料與時間序列資料之間差異的資訊圖。](../profile/images/guardrails/profile-entity.png)

#### Dimension實體

雖然維護設定檔資料的設定檔資料存放區不是關聯式存放區，但設定檔允許與小型維度實體整合，以便以簡化且直覺的方式建立區段。 此整合稱為 [多實體分段](../segmentation/multi-entity-segmentation.md).

您的組織也可以定義XDM類別來說明個人以外的專案，例如商店、產品或屬性。 這些非[!DNL XDM Individual Profile] 結構描述稱為「維度實體」（也稱為「查詢實體」），不包含時間序列資料。 代表維度實體的結構描述會透過使用連結至設定檔實體 [結構描述關係](../xdm/tutorials/relationship-ui.md).

Dimension實體提供查閱資料，可輔助並簡化多實體區段定義，且必須足夠小，讓區段引擎可以將整個資料集載入記憶體，以進行最佳處理（快速點查閱）。

![顯示輪廓圖元是由尺寸圖元組成的資訊圖形。](../profile/images/guardrails/profile-and-dimension-entities.png)