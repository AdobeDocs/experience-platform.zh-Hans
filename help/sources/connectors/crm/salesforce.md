---
keywords: Experience Platform；首頁；熱門主題；crm結構描述；crm；CRM；salesforce；Salesforce
solution: Experience Platform
title: Salesforce來源聯結器概述
description: 瞭解如何使用API或使用者介面將Salesforce連線至Adobe Experience Platform。
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---

# [!DNL Salesforce] 聯結器

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform提供從協力廠商CRM系統擷取資料的支援。 CRM提供者的支援包括 [!DNL Salesforce].

## IP位址允許清單

在使用來源聯結器之前，必須將IP位址清單新增至允許清單。 使用來源時，若未將您地區專屬的IP位址新增至允許清單，可能會導致錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## 欄位對應來源 [!DNL Salesforce] 至XDM

若要建立來源連線，請執行下列步驟： [!DNL Salesforce] 和Platform， [!DNL Salesforce] 來源資料欄位必須先對應到適當的目標XDM欄位，才能內嵌至Platform。

如需以下欄位對應規則的詳細資訊，請參閱下列內容： [!DNL Salesforce] 資料集和平台：

- [連絡人](../adobe-applications/mapping/salesforce.md#contact)
- [銷售機會](../adobe-applications/mapping/salesforce.md#lead)
- [帐户](../adobe-applications/mapping/salesforce.md#account)
- [機會](../adobe-applications/mapping/salesforce.md#opportunity)
- [機會聯絡人角色](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [营销活动](../adobe-applications/mapping/salesforce.md#campaign)
- [行銷活動成員](../adobe-applications/mapping/salesforce.md#campaign-member)
- [帳戶聯絡人關係](../adobe-applications/mapping/salesforce.md#account-contact-relation)

## 設定 [!DNL Salesforce] 名稱空間和結構描述自動產生公用程式

若要使用 [!DNL Salesforce] 來源作為的一部分 [!DNL B2B-CDP]，您必須先設定 [!DNL Postman] 自動產生「 」的公用程式 [!DNL Salesforce] 名稱空間和結構描述。 下列檔案提供有關設定 [!DNL Postman] 公用程式：

- 您可以從這裡下載名稱空間和結構描述自動產生公用程式集合和環境 [GitHub存放庫](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- 如需有關使用Platform API的資訊，包括有關如何收集所需標頭值和讀取範例API呼叫的詳細資訊，請參閱以下指南： [Platform API快速入門](../../../landing/api-guide.md).
- 如需如何為Platform API產生認證的詳細資訊，請參閱以下教學課程： [驗證和存取Experience PlatformAPI](../../../landing/api-authentication.md).
- 如需如何設定的詳細資訊 [!DNL Postman] 若為Platform API，請參閱以下教學課程： [設定開發人員控制檯和 [!DNL Postman]](../../../landing/postman.md).

使用Platform開發人員控制檯和 [!DNL Postman] 設定，您現在可以開始將適當的環境值套用至 [!DNL Postman] 環境。

下表包含範例值，以及有關填入 [!DNL Postman] 環境：

| Variable | 描述 | 示例 |
| --- | --- | --- |
| `CLIENT_SECRET` | 用於產生 `{ACCESS_TOKEN}`. 請參閱教學課程，位置如下： [驗證和存取Experience PlatformAPI](../../../landing/api-authentication.md) 以取得如何擷取 `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web權杖(JWT)是用於產生您的{ACCESS_TOKEN}的驗證認證。 請參閱教學課程，位置如下： [驗證和存取Experience PlatformAPI](../../../landing/api-authentication.md) 瞭解如何產生 `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | 用於驗證Experience Platform API呼叫的唯一識別碼。 請參閱教學課程，位置如下： [驗證和存取Experience PlatformAPI](../../../landing/api-authentication.md) 以取得如何擷取 `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | 完成對Experience Platform API的呼叫所需的授權權杖。 請參閱教學課程，位置如下： [驗證和存取Experience PlatformAPI](../../../landing/api-authentication.md) 以取得如何擷取 `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | 關於 [!DNL Marketo]，此值為固定值，且一律設為： `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | 此 `global` container保有所有標準Adobe和Experience Platform合作夥伴提供的類別、結構描述欄位群組、資料型別和結構描述。 關於 [!DNL Marketo]，此值為固定值，一律設為 `global`. | `global` |
| `PRIVATE_KEY` | 用於驗證您的身分的認證 [!DNL Postman] 執行個體以Experience PlatformAPI。 請參閱有關設定開發人員控制檯的教學課程，並 [設定開發人員控制檯和 [!DNL Postman]](../../../landing/postman.md) 以取得如何擷取您的{PRIVATE_KEY}的說明。 | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | 用來整合至Adobe I/O的認證。 | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management系統(IMS)提供驗證Adobe服務的架構。 關於 [!DNL Marketo]，此值為固定值，一律設為： `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | 企業實體，可以擁有或授權產品及服務，並允許存取其成員。 請參閱教學課程，位置如下： [設定開發人員控制檯和 [!DNL Postman]](../../../landing/postman.md) 以取得如何擷取 `{ORG_ID}` 資訊。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | 您正在使用的虛擬沙箱分割的名稱。 | `prod` |
| `TENANT_ID` | ID，用來確保您建立的資源已正確命名並包含在您的組織內。 | `b2bcdpproductiontest` |
| `PLATFORM_URL` | 您對其進行API呼叫的URL端點。 此值是固定的，一律設為： `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | 您的唯一ID [!DNL Marketo] 帳戶。 請參閱教學課程，位置如下： [驗證您的 [!DNL Marketo] 例項](../adobe-applications/marketo/marketo-auth.md) 以取得如何擷取 `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | 您的組織ID [!DNL Salesforce] 帳戶。 請參閱下列內容 [[!DNL Salesforce] 指南](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) 以取得您專屬的 [!DNL Salesforce] 組織ID。 | `00D4W000000FgYJUA0` |
| `has_abm` | 表示您是否訂閱的布林值 [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | 表示您是否訂閱的布林值 [!DNL Marketo Sales Insight]. | `false` |

{style="table-layout:auto"}

### 執行指令碼

搭配您的 [!DNL Postman] 收集和環境設定，您現在可以透過以下指令碼執行： [!DNL Postman] 介面。

在 [!DNL Postman] 介面，選取自動產生器公用程式的根資料夾，然後選取 **[!DNL Run]** 從頂端標題。

![root-folder](../../images/tutorials/create/salesforce/root-folder.png)

此 [!DNL Runner] 介面出現。 從這裡，確定已選取所有核取方塊，然後選取 **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![執行產生器](../../images/tutorials/create/salesforce/run-generator.png)

成功的請求會根據測試版規格建立B2B名稱空間和結構描述。

## Connect [!DNL Salesforce] 使用API移至Platform

以下檔案提供有關如何連線的資訊 [!DNL Salesforce] 使用API或使用者介面的to Platform：

- [使用Flow Service API建立Salesforce基本連線](../../tutorials/api/create/crm/salesforce.md)
- [使用Flow Service API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流量服務API為CRM來源建立資料流](../../tutorials/api/collect/crm.md)

## Connect [!DNL Salesforce] 使用UI移至Platform

- [在使用者介面中建立Salesforce來源連線](../../tutorials/ui/create/crm/salesforce.md)
- [在UI中為CRM連線建立資料流](../../tutorials/ui/dataflow/crm.md)
