---
title: Adobe Experience Platform發行說明2020年4月
description: Adobe Experience Platform的2020年4月發行說明。
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: 发行说明;
exl-id: 0f68c71e-3c9d-453b-a953-1cd1b6ca2e35
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 10%

---

# Adobe Experience Platform 发行说明

**发布日期：2020 年 4 月 8 日**

Adobe Experience Platform中的新功能：
* [[!DNL Intelligent Services]](#intelligent)

更新現有功能：
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [数据治理](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] 讓行銷分析人員和從業人員運用客戶體驗使用案例中人工智慧和機器學習的強大功能。 這可讓行銷分析人員使用業務層級設定，針對公司需求設定專屬預測，而不需要資料科學專業知識。 此外，行銷從業人員可以在Adobe Experience Cloud、Adobe Experience Platform和第三方應用程式中啟用預測。

**主要功能**

| 功能 | 描述 |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] 讓行銷人員能夠產生個人層面的客戶預測，並提供相關解釋。 在影響因素的協助下， [!DNL Customer AI] 可告訴您客戶可能會做什麼以及為什麼。 此外，行銷人員也可以受益於 [!DNL Customer AI] 預測和深入分析，透過提供最合適的優惠方案和訊息來個人化客戶體驗。 |
| [!DNL Attribution AI] | [!DNL Attribution AI] 是一種多管道的演演算法歸因服務，可計算客戶互動對指定結果的影響和累加影響。 利用 [!DNL Attribution AI]，营销人员可以通过了解客户历程各个阶段每个客户互动的影响来衡量和优化营销和广告支出。 |

**已知问题**

* 目前沒有已知問題。

如需詳細資訊，請參閱 [!DNL Intelligent Services] 以及它所提供的功能，請參閱 [Intelligent Services概觀](../../intelligent-services/home.md).

## [!DNL Experience Data Model] (XDM)系統 {#xdm}

標準化和互用性是背後的重要概念 [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM)以Adobe為導向，致力於標準化客戶體驗資料並定義客戶體驗管理的結構。

XDM是公開記錄的規格，旨在改善數位體驗的力量。 它為任何應用程式提供通用結構和定義，以便與Adobe Experience Platform上的服務通訊。 藉由遵守XDM標準，所有客戶體驗資料都可以整合到通用表示中，以更快、更整合的方式提供深入分析。 您可以從客戶動作獲得有價值的深入分析、透過區段定義客戶對象，以及使用客戶屬性進行個人化。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 自動替代顯示資訊 | 此 [!DNL Schema Registry] 自動套用中設定的自訂標題和說明值 `alternateDisplayInfo` 描述項。 |
| 純量欄位限制 | 此 [!DNL Schema Registry] 不允許在單一結構描述中超過6000個純量欄位。 |
| 效能檢修 | 此 [!DNL Schema Registry] 已全面整修，以符合下列需求： [!DNL Experience Platform] 更好。 |

**错误修复**

* 將XDM更新為XED已轉換，以支援標準XDM中巢狀URI欄位的較乾淨的XED格式。

**已知问题**

* 已知

## 数据治理 {#governance}

Adobe Experience Platform資料控管是用於管理客戶資料並確保遵守適用於資料使用的法規、限制和政策的一系列策略與技術。 它在以下方面發揮著關鍵作用 [!DNL Experience Platform] 包括目錄、資料譜系、資料使用標籤、資料存取原則，以及行銷動作資料的存取控制。

開始使用資料控管需要深入瞭解適用於客戶資料的規定、合約義務和公司政策。 從那裡，可以透過套用適當的資料使用標籤來分類資料，並且可以透過定義資料使用原則來控制其使用。

資料控管架構透過簡化及簡化分類資料和建立資料使用原則的流程。 [!DNL Experience Platform] 使用者介面和 [!DNL Policy Service] API。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 在UI中管理資料使用原則 | 您現在可以在以下位置管理資料使用原則： **原則** 工作區在 [!DNL Experience Platform] UI。 請參閱 [原則使用手冊](../../data-governance/policies/user-guide.md) 以取得詳細資訊。 |

**已知问题**

* None.

如需詳細資訊，請參閱 [資料控管概觀](../../data-governance/home.md).


## 目标 {#destinations}

在 [Real-time Customer Data Platform](../../rtcdp/overview.md)，目的地是預先建立的與目的地平台的整合，可透過順暢的方式為這些合作夥伴啟用資料。

**新目的地**

Real-Time CDP現在支援超過五十個資料啟用的功能 [!DNL Experience Cloud Launch] 擴充功能、啟用Analytics、個人化和其他使用案例。 如需詳細資訊，請參閱下文：

| 文档 | 描述 |
|--- | ---|
| [目的地型別和類別](../../destinations/destination-types.md) | 本文說明Real-Time CDP介面中的連線與擴充功能之間的差異，並建議何時應使用這些目的地。 |
| [Experience Platform Launch擴充功能](../../destinations/catalog/launch-extensions/overview.md) | 此頁面說明內容 [!DNL Launch] 擴充功能是，列出使用這些擴充功能的使用案例，以及每個擴充功能的檔案連結 [!DNL Launch] Real-Time CDP中的擴充功能。 |

如需詳細資訊，請參閱 [目的地概觀](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

新的法律和组织规定正在用户提供相应的权利，允许他们请求访问或删除您的数据存储中的用户个人数据。Adobe Experience Platform [!DNL Privacy Service] 提供RESTful API和使用者介面，協助您管理客戶的這些資料請求。 替換為 [!DNL Privacy Service]，您可以提交存取和刪除Adobe Experience Cloud應用程式中私人或個人客戶資料的請求，協助實現法律和組織隱私法規的自動合規性。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| PDPA支援 | 隱私權請求現在可以在泰國根據個人資料保護法(PDPA)進行建立和追蹤。 在API中提出隱私權請求時， `regulation` 陣列接受值「pdpa_tha」。 |
| UI中的名稱空間型別 | 您現在可以在的請求產生器中指定不同的名稱空間型別。 [!DNL Privacy Service] UI。 請參閱 [使用手冊](../../privacy-service/ui/user-guide.md) 以取得詳細資訊。 |
| 棄用舊端點 | 舊的API端點(`data/privacy/gdpr`)已過時。 |

已知问题

* None

如需有關的詳細資訊 [!DNL Privacy Service]，請先閱讀 [Privacy Service概觀](../../privacy-service/home.md).

## 源 {#sources}

Adobe Experience Platform可從外部來源內嵌資料，同時允許您使用建構、加標籤及增強該資料 [!DNL Platform] 服務。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 資料庫的API和UI支援 | 新的來源聯結器 [!DNL Apache Spark] （在HDInsights上）， [!DNL Azure Synapse Analytics]， [!DNL Azure Table Storage]， [!DNL Hive] （在HDInsights上），以及 [!DNL Phoenix]. |
| 支付型應用程式的API和UI支援 | 新的來源聯結器 [!DNL PayPal]. |
| 通訊協定型應用程式的API和UI支援 | 新的來源聯結器 [!DNL Generic OData]. |

**已知问题**

* None

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md).
