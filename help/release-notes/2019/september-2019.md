---
title: Adobe Experience Platform發行說明2019年9月
description: Adobe Experience Platform 2019年9月發行說明。
doc-type: release notes
last-update: September 13, 2019
author: ens28527
exl-id: 7f503046-a3b4-4fdb-833c-4205b6e9fa04
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 5%

---

# Adobe Experience Platform 发行说明

**发布日期：2019 年 9 月 10 日**

Adobe Experience Platform 现有功能的更新包括：

* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Query Service]](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform提供豐富的功能，可擷取任何型別和延遲的資料。 Adobe Experience Platform [!DNL Data Ingestion] 提供多種擷取資料的替代方案，包括批次API、串流API、原生Adobe聯結器、資料整合合作夥伴或Adobe Experience Platform UI。

**新增功能**

| 功能 | 描述 |
| ----------- | ---------- |
| 串流擷取的新網域 | 此 `dcs.data.adobe.net` 網域已移至新的通用資料收集網域 `dcs.adobedc.net`. 使用者必須根據修訂後的Adobe Experience Platform串流擷取檔案更新其實作。 所有與Adobe Experience Platform串流擷取相關的檔案已更新，以使用新網域。 |

如需詳細資訊，請瀏覽 [資料擷取檔案](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] 是一項完全受管理的服務，位於 [!DNL Experience Platform] 可讓資料科學家透過建立並操作機器學習模型，從Adobe解決方案和協力廠商系統的資料和內容順暢地產生深入分析。 [!DNL Data Science Workspace] 緊密整合 [!DNL Platform] 和支援端對端資料科學生命週期，包括探索和準備XDM資料，然後開發和實施模型以自動擴充 [!DNL Real-Time Customer Profile] 搭配機器學習深入分析。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 透過UI排程服務 | 與整合 [!DNL Platform] 協調服務，可使用UI透過使用者定義的排程來自動化模型訓練和評分。 |
| [!DNL Service Gallery] | 瀏覽、監控及存取機器學習服務，並排程自動化訓練和評分工作，這一切都在重新設計的範圍內 [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] UI改良。 |

**已知问题**

* 中目前沒有可存取的方式 [!DNL Service Gallery] 刪除現有服務。 同時，請參閱 [Sensei Machine Learning API參考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) 透過API呼叫刪除現有服務。
* 此 [!DNL Service Gallery] 不支援分頁以篩選服務的訓練和評分回合。
* 設定排程的訓練或評分回合時，透過 [!DNL Service Gallery]，將頻率設定為每小時可防止套用排程。

如需詳細資訊，請瀏覽 [資料科學工作區概觀](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] 提供在Adobe Experience Platform中使用標準SQL查詢資料的功能，以支援各種分析和資料管理使用案例。 這是一種無伺服器工具，可讓您從 [!DNL Data Lake] 並將查詢結果擷取為新資料集，以用於報表， [!DNL Data Science Workspace]，或用於內嵌至 [!DNL Real-Time Customer Profile].

您可以使用 [!DNL Query Service] 以建立資料分析生態系統，進而瞭解客戶在不同互動管道中的行為。 這些管道可能包括銷售點系統、網路、行動裝置或CRM系統。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 改善以下專案： [!DNL Query Editor] | 新增儲存功能，可讓您儲存查詢並稍後處理。 新增「瀏覽」標籤至 [!DNL Query Service] Adobe Experience Platform的使用者介面，顯示貴組織使用者儲存的查詢。 實作「查詢詳細資訊」面板，顯示有關正在檢視的查詢的有用中繼資料。 |
| 新的歸因函式 | 中的Adobe定義函式 [!DNL Query Service] 以使用到期引數查詢管道歸因。 |
| SQL語法的增強功能 | 支援iLike語法。 |
| 使用定義的XDM結構描述產生資料集 | 在Create Table as Select (CTAS)查詢中新增子句，可讓您指定目標綱要。 |

如需詳細資訊，請參閱 [查詢服務檔案](../../query-service/home.md).
