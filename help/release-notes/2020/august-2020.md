---
title: Adobe Experience Platform發行說明2020年8月
description: Adobe Experience Platform的2020年8月發行說明。
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发行日期：2020 年 8 月 12 日**

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] 使用機器學習和人工智慧從您的資料中釋放見解。 整合至Adobe Experience Platform， [!DNL Data Science Workspace] 可協助您在各種Adobe解決方案中使用您的內容和資料資產進行預測。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| VM改善專案 [!DNL JupyterLab] | 改善長期執行的穩定性 [!DNL JupyterLab notebook] 虛擬機器器。 |

如需詳細資訊，請參閱 [!DNL JupyterLab]，請參閱 [[!DNL JupyterLab] 使用手冊](../../data-science-workspace/jupyterlab/overview.md).

## 目标 {#destinations}

在 [Real-time Customer Data Platform](../../rtcdp/overview.md)，目的地是預先建立的與目的地平台的整合，可透過順暢的方式為這些合作夥伴啟用資料。

**新目的地**

有新的目的地可供您啟用Adobe Experience Platform資料。 如需詳細資訊，請參閱下文：

| 目标 | 描述 |
|--- | ---|
| [!DNL Google Customer Match] | Google Customer Match可讓您使用線上和離線資料，透過Google所擁有和經營的屬性來聯絡客戶並重新與其互動，例如： [!DNL Search]， [!DNL Shopping]、 Gmail和YouTube。 <br><br> 造訪 [!DNL Google Customer Match] [頁面](../../destinations/catalog/advertising/google-customer-match.md) 目的地目錄，以取得有關目的地以及如何在Real-Time CDP中設定目的地的詳細資訊。 |

**新增功能**

| 功能 | 描述 |
|------- | -----------|
| 自訂檔案名稱編輯器 | 電子郵件行銷目標和雲端儲存體目標的資料啟用工作流程更新，可讓您編輯匯出檔案的名稱。 如需詳細資訊，請參閱 [ 設定步驟](../../destinations/ui/activate-batch-profile-destinations.md) 啟動工作流程中。 |
| 建議的屬性 | 更新電子郵件行銷目標和雲端儲存體目標的資料啟用工作流程，以顯示建議屬性，供您新增至匯出的檔案。 如需詳細資訊，請參閱 [選取屬性步驟](../../destinations/ui/activate-batch-profile-destinations.md) 啟動工作流程中。 |

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

以Experience Platform為基礎，Real-time Customer Data Platform ([!DNL Real-Time CDP])可協助公司整合已知和未知的資料，透過整個客戶歷程的智慧型決策來啟用客戶設定檔。 [!DNL Real-Time CDP] 結合多個企業資料來源，即時建立客戶設定檔。 然後，根據這些設定檔建立的區段可傳送至下游目的地，以跨所有管道和裝置提供一對一的個人化客戶體驗。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| IAB TCF 2.0支援 | [!DNL Real-Time CDP] 現在是2.0版的 [!DNL Transparency & Consent Framework] (TCF)，如 [!DNL Interactive Advertising Bureau] (IAB)。 您可以將資料作業和設定檔結構描述設定為接受CMP產生的客戶同意資料，並在對下游目的地啟用區段時強制執行客戶的同意偏好設定。 |

如需詳細資訊，請參閱 [!DNL Real-Time CDP]，請參閱 [[!DNL Real-Time CDP] 概觀](../../rtcdp/overview.md).

## 源 {#sources}

Adobe Experience Platform可從外部來源內嵌資料，同時允許您使用建構、加標籤及增強該資料 [!DNL Platform] 服務。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 流量執行監視 | 使用者可以監視所有流程執行，並檢視每個執行的詳細檢視，包括完成狀態、執行持續時間、已處理檔案的清單、錯誤和量度。 請參閱 [監控資料流](../../sources/tutorials/ui/monitor.md) 檔案以取得詳細資訊。 |
| 流程執行通知 | 使用者可以訂閱事件並註冊Webhook，以接收有關流量執行的狀態、量度和錯誤的即時通知。 |
| UI目錄改良 | 更新來源目錄畫面，以便更輕鬆地存取所選物件的主要動作。 |

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md).
