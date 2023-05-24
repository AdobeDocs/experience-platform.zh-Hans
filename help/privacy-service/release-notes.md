---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Privacy Service發行說明
description: Adobe Experience Platform Privacy Service最新版本注意事項。
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 5%

---

# [!DNL Privacy Service] 发行说明

本檔案包含Adobe Experience Platform新功能的相關資訊 [!DNL Privacy Service]以及增強功能和重大錯誤修正。

>[!NOTE]
>
>其他版本的最新發行說明 [!DNL Experience Platform] 可以找到服務 [此處](../release-notes/latest/latest.md).

## 2020 年 9 月 9 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| 支援LGPD （巴西） | 隱私權工作現在可以在巴西的 [!DNL Lei Geral de Proteção de Dados] (LGPD)法規。 這些工作會根據法規代碼進行追蹤 `lgpd_bra`. |

## 2020 年 4 月 8 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| PDPA支援 | [!DNL Privacy] 現在起，您可在泰國根據個人資料保護法(PDPA)建立及追蹤請求。 在API中提出隱私權請求時， `regulation` 陣列接受值「pdpa_tha」。 |
| UI中的名稱空間型別 | 您現在可以在的請求產生器中指定不同的名稱空間型別。 [!DNL Privacy Service] UI。 請參閱 [使用手冊](ui/user-guide.md) 以取得詳細資訊。 |
| 棄用舊端點 | 舊的API端點(`data/privacy/gdpr`)已過時。 |

## 2020年1月14日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| [!DNL Privacy Service] 品牌重塑 | 先前稱為「GDPR服務」的服務品牌已變更為 [!DNL Privacy Service] 隨著服務的成長，除了GDPR之外，還支援其他法規。 |
| 新API端點 | 的基礎路徑 [!DNL Privacy Service] API更新自 `/data/privacy/gdpr` 至 `/data/core/privacy/jobs` |
| 需要新增 `regulation` 屬性 | 在中建立新工作時 [!DNL Privacy Service] API， a `regulation` 請求承載中必須提供屬性，以指出要追蹤其下之工作的法規。 接受的值為 `gdpr` 和 `ccpa`. 檢視檔案： [隱私權工作](api/privacy-jobs.md) 在 [!DNL Privacy Service] API指南，以瞭解詳細資訊。 |
| 支援Adobe Primetime驗證 | [!DNL Privacy Service] 現在接受來自Adobe Primetime Authentication的存取/刪除請求，使用 `primetimeAuthentication` 作為其產品價值。 請參閱 [Primetime驗證檔案](https://tve.helpdocsonline.com/how-to-make-a-privacy-request) 以取得詳細資訊。 |

### 增强功能

* [!DNL Privacy Service] UI增強功能：
   * GDPR和CCPA法規的個別工作追蹤頁面。
   * 新增 *法規型別* 下拉式清單，用於在GDPR和CCPA的追蹤資料之間切換。

## 2019年725日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| 請求量度控制面板 | 中的新量度控制面板 [!DNL Privacy Service] UI可讓您檢視已提交、有錯誤和已完成的GDPR請求。 |
| 請求產生器 | 為了服務具有提交GDPR請求的技術和非技術使用者的組織， UI中新增了「建立請求」功能。 JSON檔案提交功能仍可在 [!DNL Privacy Service] 適用於偏好繼續使用的組織的UI。 |
| GDPR工作事件通知 | 有關GDPR工作狀態的事件通知是許多工作流程的關鍵元素。 雖然先前是使用個別電子郵件通知來提供通知，但GDPR事件通知是運用Adobe I/O事件的訊息，這些通知會傳送至已設定的webhook，以促進工作請求自動化。 [!DNL Privacy Service] UI使用者可以訂閱Adobe I/OGDPR事件，以便在產品或GDPR工作完成後接收更新。 |

## 2019 年 4 月 18 日

### 增强功能

* 中狀態表格的預設範圍 [!DNL Privacy Service] UI已修改為7天跨度。
* 改善內部例外狀況處理。
* 針對低資料變更率的常見內部呼叫引入快取，以提升效能。

### 错误修复

* 新增以下專案的已篩選查詢遺漏的記錄資訊： `GET /` 中的端點 [!DNL Privacy Service] API。

## 2019 年 4 月 11 日

### 增强功能

* 更新UI以支援測試版客戶的新功能
* 支援UI 2.0功能（測試版）的全新量度API

## 2019 年 4 月 9 日

### 增强功能

* 將所有查詢(GET) API呼叫更新為預設的30天回顧範圍
* 限制使用API的回顧範圍上限為45天

## 2019年2月14日

### 增强功能

* 強制執行 `include` 每個POST提交中的欄位。
* 強制執行 `include` 上傳JSON時的欄位。

### 错误修复

* 修正客戶無法載入 [!DNL Privacy Service] UI。
