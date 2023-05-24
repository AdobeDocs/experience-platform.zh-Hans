---
title: Adobe Experience Platform發行說明2021年11月
description: Adobe Experience Platform的2021年11月發行說明。
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 12%

---

# Adobe Experience Platform 发行说明

**发行日期：2021 年 11 月 17 日**

## 新增功能

Adobe Experience Platform中的新功能：

- [Real-Time Customer Data Platform B2B 版](#B2B)
- [（測試版）透過臨機啟動API將受眾區段啟動至批次目的地](#ad-hoc-activation)

## 現有功能的更新

Adobe Experience Platform 现有功能的更新包括：

- [归因人工智能](#attribution-ai)
- [Customer AI](#customer-ai)

### Real-Time Customer Data Platform B2B 版 {#B2B}

**发行日期：2021 年 11 月 12 日**

Real-Time CDP B2B Edition以Real-time Customer Data Platform (Real-Time CDP)為基礎，專為以B2B服務模式運作的行銷人員所打造。 它會整合來自多個來源的資料，並將其合併為單一檢視的人員與帳戶設定檔。 此統一的資料可讓行銷人員精準鎖定特定對象，並透過所有可用管道吸引這些對象。

有各種Adobe Experience Platform功能的改善，可區分Real-Time CDP B2B版本與其B2C版本。 其中包括改善B2B使用案例的Experience Data Model (XDM)、升級身分解析和設定檔分段，以及自訂建置的聯結器和Marketo Engage目的地。 Marketo聯結器可讓B2B品牌將其領先業界的B2B參與資料與行為資訊連結，以培育潛在客戶並增強以帳戶為基礎的行銷作業。

-[全新B2B和B2P版本](#editions)
-[全新Marketo資料來源和目的地聯結器](#marketo)
-[標準B2B XDM](#XDM)

### 全新B2B和B2P版本 {#editions}

您可購買新版B2B和B2P，這些版本將B2B資料和功能整合至Real-Time CDP和Platform Activation產品。

若要進一步瞭解Real-Time CDP B2B版本，請參閱 [概觀](../../rtcdp/overview.md).

### 全新Marketo資料來源和目的地聯結器 {#marketo}

新的Marketo資料來源和目的地聯結器可將Marketo資料串流至Platform和Platform受眾，回到Marketo。 適用於所有Platform使用者。

| 功能 | 描述 |
|----------|-------------|
| Marketo Engage來源聯結器 | 此 [Marketo Engage來源聯結器](../../sources/connectors/adobe-applications/marketo/marketo.md) 可讓行銷人員順暢地將一或多個Marketo執行個體的資料擷取到其Adobe Experience Platform執行個體中，並提供適用於潛在客戶管理和B2B行銷人員的完整解決方案。 |
| Marketo Engage目的地 | 此 [Marketo目的地](../../destinations/catalog/adobe/marketo-engage.md) 可讓行銷人員將在Adobe Experience Platform中建立的區段推送至Marketo，並在其中顯示為靜態清單。 |

### 標準B2B XDM {#XDM}

標準B2B XDM類別、欄位群組和資料型別適用於所有Platform使用者。

| 功能 | 描述 |
|-----------|--------------|
| 標準B2B XDM類別 | Real-time Customer Data Platform B2B Edition提供數個標準XDM，可擷取基本B2B資料實體的詳細資訊，例如帳戶、商機、促銷活動等。 |

請參閱 [Real-time Customer Data Platform B2B版本中的結構描述](../../rtcdp/schemas/b2b.md) 檔案以瞭解更多有關擷取B2B資料實體的資訊。

### （測試版）透過臨機啟動API將受眾區段啟動至批次目的地 {#ad-hoc-activation}

隨選啟用API可讓行銷人員針對需要立即啟用的情況，以快速且有效率的方式以程式設計方式啟用目的地的受眾區段。 僅支援隨選對象啟用 [批次檔案型目的地](../../destinations/destination-types.md#file-based) 且目前為測試版。 如需詳細資訊，請參閱 [臨機啟動API檔案](../../destinations/api/ad-hoc-activation-api.md).

### 归因人工智能 {#attribution-ai}

Attribution AI 用于将点数归因于导致转化事件的接触点。营销人员可利用此功能，促进量化客户旅程中每个营销接触点的营销影响。

| 功能 | 描述 |
|-----------|---------------|
| 支援多個資料集 | Attribution AI現在可以輕鬆地直接在UI中擷取多個資料集，而無需對應和拼接每個資料集。 這項新的省時功能提供更強大且更精確的分數，包含來自多個資料集的更豐富資料。 |
| 媒體頻道與行銷活動欄位對應 | Attribution AI現在支援媒體頻道與行銷活動欄位的對應。 資料集之間的媒體管道對應可改善從Attribution AI衍生的見解，並有助於提供更清晰、易於解讀的結果。 |

如需Attribution AI的詳細資訊，請參閱 [Attribution AI檔案](../../intelligent-services/attribution-ai/overview.md).

### Customer AI {#customer-ai}

Real-time Customer Data Platform中提供的Customer AI可產生自訂傾向評分，例如大規模個別設定檔的流失和轉換情形。 这无需通过将业务需求转变为机器学习问题、选择算法、培训或部署即可完成。

**更新的功能**

| 功能 | 描述 |
|-----------|-------------|
| 支援多個資料集 | Customer AI現在可以輕鬆地直接在UI中擷取多個資料集，而無需對應和拼接每個資料集。 這項新的省時功能提供更強大且更精確的分數，包含來自多個資料集的更豐富資料。 |
| 自訂設定檔屬性 | 除了標準事件欄位外，Customer AI現在還支援在資料中定義自訂設定檔資料集欄位（含時間戳記）。 使用此選項可讓您新增您認為有影響力的其他設定檔屬性，這些屬性可能會改善模型的品質，並提供更準確的結果。 |

如需Customer AI的詳細資訊，請參閱 [Customer AI檔案](../../intelligent-services/customer-ai/overview.md).
