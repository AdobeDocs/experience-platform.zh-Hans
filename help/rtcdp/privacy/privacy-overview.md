---
keywords: 資料治理rtcdp；rtcdp資料治理；即時客戶資料設定檔資料治理；隱私權rtcdp；rtcdp隱私權
title: Real-time Customer Data Platform中的隱私權
description: Adobe Real-time Customer Data Platform可讓您精簡資料作業符合隱私權法規的程式。
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# Real-time Customer Data Platform中的隱私權

[!DNL Adobe Real-Time Customer Data Platform] ([!DNL Real-Time CDP])可協助行銷人員將來自多個企業系統的資料彙集在一起，讓他們更能識別、瞭解客戶，並與客戶互動。 Adobe將消費者資料隱私權視為基本設計原則，並提供各種控制項，以協助行銷人員管理其客戶的資料隱私權。

大部份 [!DNL Real-Time CDP] 功能由Adobe Experience Platform提供。 本檔案提供以下支援的各種隱私權增強技術的相關資訊： [!DNL Real-Time CDP]，包含連結至 [!DNL Experience Platform] 說明檔案以取得詳細資訊。

## 接受客戶存取和刪除請求

法律隱私權法規，例如 [!DNL General Data Protection Regulation] (GDPR)和 [!DNL California Consumer Privacy Act] (CCPA)給予客戶要求存取或刪除您向他們收集之個人資料的權利。 從 [!DNL Real-Time CDP] 利用 [!DNL Experience Platform] 資料收集與儲存功能、客戶存取和刪除其個人資料的請求應在以下進行管理： [!DNL Platform]. 請參閱以下文章的概觀： [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) 以取得詳細資訊。

>[!IMPORTANT]
>
> 透過Adobe Experience Platform Privacy Service for Adobe Marketo Engage提交的隱私權請求僅適用於Real-Time CDP B2B客戶。

## 選擇退出功能

[!DNL Real-Time CDP] 可讓客戶選擇退出在細分使用案例中包含其個人資料。 客戶選擇退出的偏好設定會透過以下方式擷取和儲存： [!DNL Real-Time Customer Profile]，並可在區段述詞中使用布林值邏輯(「AND NOT」)來排除已選擇退出區段的使用者。

檢視檔案： [接受選擇退出請求](../../segmentation/consents.md) 如需詳細資訊，請參閱Adobe Experience Platform Segmentation Service檔案。

## IAB TCF 2.0支援

[!DNL Real-Time CDP] 內建於Adobe Experience Platform，是已註冊的 [廠商清單](https://iabeurope.eu/vendor-list-tcf-v2-0/) 的 [!DNL Transparency & Consent Framework (TCF)]，如 [!DNL Interactive Advertising Bureau (IAB)]. 為符合TCF 2.0的要求，Platform可讓您收集詳細的客戶同意資料，並將其整合至您儲存的客戶設定檔中。 之後，可根據特定設定檔的使用案例，將此同意資料納入轉存的對象區段中，決定是否包含這些設定檔。

請參閱以下文章的概觀： [Experience Platform中的IAB TCF 2.0支援](../../landing/governance-privacy-security/consent/iab/overview.md) 以取得詳細資訊。

## 后续步骤

本檔案簡要介紹的隱私權功能 [!DNL Real-Time CDP]. 請參閱本指南中的檔案連結，瞭解每項功能的詳細資訊。
