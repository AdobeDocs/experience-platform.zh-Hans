---
keywords: Experience Platform；身分；身分服務；疑難排解；護欄；指引；限制；
title: Identity Service的護欄
description: 本檔案提供Identity Service資料的使用和速率限制相關資訊，以協助您最佳化身分圖表的使用方式。
exl-id: bd86d8bf-53fd-4d76-ad01-da473a1999ab
source-git-commit: f619bbf2c8d313eabc6444b4bd8c09615a00cc42
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 2%

---

# 護欄 [!DNL Identity Service] 資料

本檔案提供以下專案的使用與速率限制相關資訊： [!DNL Identity Service] 資料可協助您最佳化身分圖表的使用方式。 檢閱下列護欄時，系統假設您已正確模型化資料。 如果您有任何關於如何建立資料模型的問題，請聯絡您的客戶服務代表。

## 快速入门

下列Experience Platform服務與模型化身分資料有關：

* [身分](home.md)：橋接擷取至Platform時的不同資料來源身分。
* [[!DNL Real-Time Customer Profile]](../profile/home.md)：使用來自多個來源的資料建立統一的消費者設定檔。

## 資料模型限制

下表提供靜態限制的護欄指南，以及身分名稱空間要考量的驗證規則。

### 靜態限制

下表概述套用至身分資料的靜態限制。

| 護欄 | 限制 | 注释 |
| --- | --- | --- |
| 圖表中的身分數量 | 150 | 此限制會套用至沙箱層級。 一旦達到限制，身分圖表將不會更新。 **注意**：身分圖表中的身分數量上限 **適用於個別合併的設定檔** 為50。 根據具有超過50個身分的身分圖表合併的設定檔會從即時客戶設定檔中排除。 如需詳細資訊，請閱讀以下指南： [設定檔資料的護欄](../profile/guardrails.md). |
| XDM記錄中的身分數量 | 20 | 需要的XDM記錄數量下限為2。 |
| 自訂名稱空間的數量 | None | 您可以建立的自訂名稱空間數量沒有限制。 |
| 圖表數量 | None | 您可以建立的身分圖表數量沒有限制。 |
| 名稱空間顯示名稱或身分符號的字元數 | None | 名稱空間顯示名稱或身分符號的字元數沒有限制。 |

### 身分值驗證

下表概述您必須遵循的現有規則，以確保身分值成功驗證。

| 命名空间 | 驗證規則 | 違反規則時的系統行為 |
| --- | --- | --- |
| ECID | <ul><li>ECID的身分值必須剛好38個字元。</li><li>ECID的身分值只能包含數字。</li></ul> | <ul><li>如果ECID的身分值不完全是38個字元，則會略過記錄。</li><li>如果ECID的身分值包含非數字字元，則會略過記錄。</li></ul> |
| 非ECID | 身分值不可超過1024個字元。 | 如果身分值超過1024個字元，則會略過記錄。 |

### 身分名稱空間擷取

自2023年3月31日起，Identity Service將封鎖新客戶的Adobe Analytics ID (AAID)擷取。 此身分通常是透過 [Adobe Analytics來源](../sources/connectors/adobe-applications/analytics.md) 和 [Adobe Audience Manager來源](../sources//connectors/adobe-applications/audience-manager.md) 和是多餘的，因為ECID代表相同的網頁瀏覽器。 如果您想要變更此預設設定，請聯絡您的Adobe客戶團隊。

## 后续步骤

請參閱下列檔案，瞭解更多關於 [!DNL Identity Service]：

* [[!DNL Identity Service] 概述](home.md)
* [身分圖表檢視器](ui/identity-graph-viewer.md)
