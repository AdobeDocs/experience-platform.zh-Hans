---
keywords: Experience Platform；首頁；熱門主題；Marketo Engage；marketo engage；marketo
solution: Experience Platform
title: Marketo Engage聯結器
description: 本檔案提供Marketo Engage來源聯結器的概觀，包括關於其驗證、對應和資料延遲的資訊。
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: d8cd69524d984fdb828447287f3f4a4fe5913d61
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# [!DNL Marketo Engage] 聯結器

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (以下稱&quot;[!DNL Marketo]「)是銷售機會管理的完整解決方案，也適合B2B行銷人員使用，而透過該解決方案，他們可參與複雜購買歷程的每個階段，從中轉變客戶體驗。

使用 [!DNL Marketo] 來源聯結器，您可以將B2B資料從 [!DNL Marketo] 至平台，並使用平台連線的應用程式保持這些資料在最新狀態。

>[!IMPORTANT]
>
>您必須擁有下列專案的存取權： [Adobe Real-time Customer Data Platform B2B版本](../../../../rtcdp/b2b-overview.md) 若要使用所有Marketo資料集進行細分，請依下列步驟： [即時客戶個人檔案](../../../../profile/home.md). 如果沒有Real-Time CDP B2B版本，您仍可使用Marketo來源，將人員和活動資料集的資料匯入即時客戶個人檔案，以進行分段。

本檔案提供 [!DNL Marketo] 來源聯結器，包括如何驗證聯結器、如何對映的資訊 [!DNL Marketo] Experience Data Model (XDM)的欄位以及聯結器的資料延遲。

## 驗證您的 [!DNL Marketo] 聯結器

為了連線 [!DNL Marketo] 對於Platform，您必須先擷取 `munchkinId`， `clientId`、和 `clientSecret`.

請參閱以下說明的步驟 [驗證您的Marketo來源聯結器](./marketo-auth.md) 檔案以擷取您的認證。

## 設定Adobe組織對應

建立對應集之前 [!DNL Marketo]，您必須先設定Adobe組織對應。 如需如何完成此作業的詳細步驟，請參閱以下指南中的 [設定Adobe組織對應 [!DNL Marketo]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## 設定B2B名稱空間和結構描述自動產生公用程式

接下來，使用B2B名稱空間和結構描述自動產生公用程式，來設定您的Platform開發人員主控台和Postman環境。 這可讓您自動填入B2B名稱空間和結構描述。 如需詳細指示，請參閱以下指南： [設定您的B2B名稱空間和結構描述自動產生公用程式](./marketo-namespaces.md)

## 體驗資料模型(XDM)

XDM是公開記錄的規格，提供通用結構和定義，可讓您從協力廠商來源擷取資料，用於下游平台服務。

遵守XDM標準可將資料統一整合至平台生態系統，讓您更輕鬆地傳送資料及收集資訊。

若要進一步瞭解XDM及其在Platform中的角色，請參閱 [XDM系統總覽](../../../../xdm/home.md).

## 欄位對應來源 [!DNL Marketo] 至XDM

若要建立來源連線，請執行下列步驟： [!DNL Marketo] 和Platform整合，則Marketo來源資料欄位必須在內嵌至Platform之前對應至其適當的目標XDM欄位。

如需以下欄位對應規則的詳細資訊，請參閱下列內容： [!DNL Marketo] 資料集和平台：

* [活动](../mapping/marketo.md#activities)
* [项目](../mapping/marketo.md#programs)
* [計畫成員資格](../mapping/marketo.md#program-memberships)
* [公司](../mapping/marketo.md#companies)
* [靜態清單](../mapping/marketo.md#static-lists)
* [靜態清單成員資格](../mapping/marketo.md#static-list-memberships)
* [具名帳戶](../mapping/marketo.md#named-accounts)
* [機會](../mapping/marketo.md#opportunities)
* [機會聯絡人角色](../mapping/marketo.md#opportunity-contact-roles)
* [人員](../mapping/marketo.md#persons)

## 預期延遲 [!DNL Marketo] 平台上的資料

下表概述預期引致的延遲 [!DNL Marketo] 根據內嵌的性質和所要的目的地，將資料匯入Platform：

| 目标 | 預期延遲 |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 1分鐘 |
| 資料湖 | &lt; 60 分钟 |

## 後續步驟和其他資源

以下檔案提供有關建立 [!DNL Marketo] 來源連線：

* 如需如何連線的詳細資訊， [!DNL Marketo] 資料轉換至Platform，請閱讀上的教學課程： [建立 [!DNL Marketo] ui中的來源連線](../../../tutorials/ui/create/adobe-applications/marketo.md).
   * 如需如何設定方案和擷取自訂活動資料的詳細資訊，請閱讀以下教學課程： [為建立來源連線和資料流 [!DNL Marketo] 自訂活動資料](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
* 有關搭配使用的B2B名稱空間和結構描述的基礎設定的資訊 [!DNL Marketo]，請參閱「 」檔案 [B2B名稱空間和結構描述](./marketo-namespaces.md).
* 如需尋找您的電腦的相關資訊， [!DNL Marketo] munchkin ID並產生您的認證，請閱讀 [[!DNL Marketo] 驗證指南](./marketo-auth.md).
* 適用於下列專案的特定對應規則的相關資訊： [!DNL Marketo] 資料集，請閱讀以下檔案： [[!DNL Marketo] 欄位對應](../mapping/marketo.md).
* 如需一般資訊，請參閱 [!DNL Real-Time Customer Data Platform B2B Edition] 及其功能，請閱讀以下檔案： [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
