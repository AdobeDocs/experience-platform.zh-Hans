---
title: B2B名稱空間和結構描述
description: 本檔案提供建立B2B來源聯結器時所需的自訂名稱空間概觀。
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1717'
ht-degree: 4%

---

# B2B名稱空間和結構描述

>[!NOTE]
>
>您可以在Adobe Experience Platform UI中使用範本，快速建立B2B和B2C資料的資產。 如需詳細資訊，請閱讀以下指南： [在Platform UI中使用範本](../../../tutorials/ui/templates.md).

本檔案提供與B2B來源搭配使用的名稱空間和結構描述的基礎設定資訊。 本檔案也提供設定Postman自動化公用程式（產生B2B名稱空間和結構描述所需）的詳細資訊。

>[!IMPORTANT]
>
>您必須擁有下列專案的存取權： [Adobe Real-time Customer Data Platform B2B版本](../../../../rtcdp/b2b-overview.md) 以便B2B結構描述參與 [即時客戶個人檔案](../../../../profile/home.md).

## 設定B2B名稱空間和結構描述自動產生公用程式

使用B2B名稱空間和結構描述自動產生公用程式的第一個步驟是設定您的Platform開發人員主控台，並 [!DNL Postman] 環境。

- 您可以從這裡下載名稱空間和結構描述自動產生公用程式集合和環境 [GitHub存放庫](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- 如需有關使用Platform API的資訊，包括有關如何收集所需標頭值和讀取範例API呼叫的詳細資訊，請參閱以下指南： [Platform API快速入門](../../../../landing/api-guide.md).
- 如需如何為Platform API產生認證的詳細資訊，請參閱以下教學課程： [驗證和存取Experience PlatformAPI](../../../../landing/api-authentication.md).
- 如需如何設定的詳細資訊 [!DNL Postman] 若為Platform API，請參閱以下教學課程： [設定開發人員控制檯和 [!DNL Postman]](../../../../landing/postman.md).

使用Platform開發人員控制檯和 [!DNL Postman] 設定，您現在可以開始將適當的環境值套用至 [!DNL Postman] 環境。

下表包含範例值，以及有關填入 [!DNL Postman] 環境：

| Variable | 描述 | 示例 |
| --- | --- | --- |
| `CLIENT_SECRET` | 用於產生 `{ACCESS_TOKEN}`. 請參閱教學課程，位置如下： [驗證和存取Experience PlatformAPI](../../../../landing/api-authentication.md) 以取得如何擷取 `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web權杖(JWT)是用於產生您的{ACCESS_TOKEN}的驗證認證。 請參閱教學課程，位置如下： [驗證和存取Experience PlatformAPI](../../../../landing/api-authentication.md) 瞭解如何產生 `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | 用於驗證Experience Platform API呼叫的唯一識別碼。 請參閱教學課程，位置如下： [驗證和存取Experience PlatformAPI](../../../../landing/api-authentication.md) 以取得如何擷取 `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | 完成對Experience Platform API的呼叫所需的授權權杖。 請參閱教學課程，位置如下： [驗證和存取Experience PlatformAPI](../../../../landing/api-authentication.md) 以取得如何擷取 `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | 關於 [!DNL Marketo]，此值為固定值，且一律設為： `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | 此 `global` container保有所有標準Adobe和Experience Platform合作夥伴提供的類別、結構描述欄位群組、資料型別和結構描述。 關於 [!DNL Marketo]，此值為固定值，一律設為 `global`. | `global` |
| `PRIVATE_KEY` | 用於驗證您的身分的認證 [!DNL Postman] 執行個體以Experience PlatformAPI。 請參閱有關設定開發人員控制檯的教學課程，並 [設定開發人員控制檯和 [!DNL Postman]](../../../../landing/postman.md) 以取得如何擷取您的{PRIVATE_KEY}的說明。 | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | 用來整合至Adobe I/O的認證。 | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management系統(IMS)提供驗證Adobe服務的架構。 關於 [!DNL Marketo]，此值為固定值，一律設為： `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | 企業實體，可以擁有或授權產品及服務，並允許存取其成員。 請參閱教學課程，位置如下： [設定開發人員控制檯和 [!DNL Postman]](../../../../landing/postman.md) 以取得如何擷取 `{ORG_ID}` 資訊。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | 您正在使用的虛擬沙箱分割的名稱。 | `prod` |
| `TENANT_ID` | ID，用來確保您建立的資源已正確命名並包含在您的組織內。 | `b2bcdpproductiontest` |
| `PLATFORM_URL` | 您對其進行API呼叫的URL端點。 此值是固定的，一律設為： `http://platform.adobe.io/`. | `http://platform.adobe.io/` |

{style="table-layout:auto"}

### 執行指令碼

搭配您的 [!DNL Postman] 收集和環境設定，您現在可以透過以下指令碼執行： [!DNL Postman] 介面。

在 [!DNL Postman] 介面，選取自動產生器公用程式的根資料夾，然後選取 **[!DNL Run]** 從頂端標題。

![root-folder](../images/marketo/root-folder.png)

此 [!DNL Runner] 介面出現。 從這裡，確定已選取所有核取方塊，然後選取 **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![執行產生器](../images/marketo/run-generator.png)

成功的請求會建立B2B所需的名稱空間和結構描述。

## B2B名稱空間

身分名稱空間是的元件 [[!DNL Identity Service]](../../../../identity-service/home.md) 用於區分身分的上下文或型別。 完整身分包含ID值和名稱空間。 請參閱 [名稱空間概觀](../../../../identity-service/namespaces.md) 以取得詳細資訊。

B2B名稱空間會用於實體的主要身分識別。

下表包含B2B名稱空間的基礎設定資訊。

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 显示名称 | 身份符号 | 身份类型 |
| --- | --- | --- |
| B2B人員 | `b2b_person` | `CROSS_DEVICE` |
| B2B帳戶 | `b2b_account` | `B2B_ACCOUNT` |
| B2B機會 | `b2b_opportunity` | `B2B_OPPORTUNITY` |
| B2B機會個人關係 | `b2b_opportunity_person_relation` | `B2B_OPPORTUNITY_PERSON` |
| B2B行銷活動 | `b2b_campaign` | `B2B_CAMPAIGN` |
| B2B行銷活動會員 | `b2b_campaign_member` | `B2B_CAMPAIGN_MEMBER` |
| B2B行銷清單 | `b2b_marketing_list` | `B2B_MARKETING_LIST` |
| B2B行銷清單成員 | `b2b_marketing_list_member` | `B2B_MARKETING_LIST_MEMBER` |
| B2B帳戶個人關係 | `b2b_account_person_relation` | `B2B_ACCOUNT_PERSON` |

{style="table-layout:auto"}

## B2B結構描述

Experience Platform 会使用架构，以便以可重用的一致方式描述数据结构。通过在整个系统中以一致的方式定义数据，更容易保留含义并因此从数据中获取价值。

在將資料內嵌至Platform之前，必須組成結構描述來說明資料結構，並對可包含在每個欄位中的資料型別提供限制。 結構描述包含一個基底類別和零個或多個結構描述欄位群組。

如需結構描述組合模型的詳細資訊，包括設計原則和最佳實務，請參閱 [結構描述組合基本概念](../../../../xdm/schema/composition.md).

下表包含B2B結構描述的基本設定資訊。

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| 架构名称 | 基底類別 | 字段组 | [!DNL Profile] 在結構描述中 | 主要标识 | 主要身分名稱空間 | 次要身分 | 次要身分名稱空間 | 关系 | 注释 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| B2B帳戶 | [XDM商業帳戶](../../../../xdm/classes/b2b/business-account.md) | XDM商業帳戶細節 | 已启用 | `accountKey.sourceKey` 在基底類別中 | B2B帳戶 | `extSourceSystemAudit.externalKey.sourceKey` 在基底類別中 | B2B帳戶 | <ul><li>`accountParentKey.sourceKey` 在XDM商業帳戶詳細資料欄位群組中</li><li>目的地屬性： `/accountKey/sourceKey`</li><li>型別：一對一</li><li>參考結構描述： B2B帳戶</li><li>名稱空間： B2B帳戶</li></ul> |
| B2B人員 | [XDM 个人资料](../../../../xdm/classes/individual-profile.md) | <ul><li>XDM商業人士詳細資料</li><li>XDM商業人士要素</li><li>身分對應</li><li>同意和偏好設定詳細資料</li></ul> | 已启用 | `b2b.personKey.sourceKey` 在XDM業務人員詳細資料欄位群組中 | B2B人員 | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` 「XDM業務人員詳細資訊」欄位群組的</li><li>`workEmail.address` 「XDM業務人員詳細資訊」欄位群組的</ol></li> | <ol><li>B2B人員</li><li>电子邮件</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` 「XDM業務人員要素」欄位群組</li><li>型別：多對一</li><li>參考結構描述： B2B帳戶</li><li>名稱空間： B2B帳戶</li><li>目的地屬性： accountKey.sourceKey</li><li>來自目前結構描述的關係名稱：帳戶</li><li>引用結構描述中的關係名稱：人員</li></ul> |
| B2B機會 | [XDM商業機會](../../../../xdm/classes/b2b/business-opportunity.md) | XDM商業機會詳細資料 | 已启用 | `opportunityKey.sourceKey` 在基底類別中 | B2B機會 | `extSourceSystemAudit.externalKey.sourceKey` 在基底類別中 | B2B機會 | <ul><li>`accountKey.sourceKey` 在基底類別中</li><li>型別：多對一</li><li>參考結構描述： B2B帳戶</li><li>名稱空間： B2B帳戶</li><li>目的地屬性： `accountKey.sourceKey`</li><li>來自目前結構描述的關係名稱：帳戶</li><li>參考結構描述中的關係名稱：商機</li></ul> |
| B2B機會個人關係 | [XDM商業機會個人關係](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) | None | 已启用 | `opportunityPersonKey.sourceKey` 在基底類別中 | B2B機會個人關係 | `extSourceSystemAudit.externalKey.sourceKey` 在基底類別中 | B2B機會個人關係 | **第一次關聯**<ul><li>`personKey.sourceKey` 在基底類別中</li><li>型別：多對一</li><li>參考結構描述： B2B Person</li><li>名稱空間： B2B Person</li><li>目的地屬性： b2b.personKey.sourceKey</li><li>來自目前結構描述的關係名稱： Person</li><li>參考結構描述中的關係名稱：商機</li></ul>**第二個關係**<ul><li>`opportunityKey.sourceKey` 在基底類別中</li><li>型別：多對一</li><li>參考結構描述：B2B機會 </li><li>名稱空間： B2B機會 </li><li>目的地屬性： `opportunityKey.sourceKey`</li><li>來自目前結構描述的關係名稱：機會</li><li>引用結構描述中的關係名稱：人員</li></ul> |
| B2B行銷活動 | [XDM商業活動](../../../../xdm/classes/b2b/business-campaign.md) | XDM商業活動細節 | 已启用 | `campaignKey.sourceKey` 在基底類別中 | B2B行銷活動 | `extSourceSystemAudit.externalKey.sourceKey` 在基底類別中 | B2B行銷活動 |
| B2B行銷活動會員 | [XDM商業活動會員](../../../../xdm/classes/b2b/business-campaign-members.md) | XDM商業活動會員詳細資料 | 已启用 | `ccampaignMemberKey.sourceKey` 在基底類別中 | B2B行銷活動會員 | `extSourceSystemAudit.externalKey.sourceKey` 在基底類別中 | B2B行銷活動會員 | **第一次關聯**<ul><li>`personKey.sourceKey` 在基底類別中</li><li>型別：多對一</li><li>參考結構描述： B2B Person</li><li>名稱空間： B2B Person</li><li>目的地屬性： `b2b.personKey.sourceKey`</li><li>來自目前結構描述的關係名稱： Person</li><li>引用結構描述中的關係名稱：行銷活動</li></ul>**第二個關係**<ul><li>`campaignKey.sourceKey` 在基底類別中</li><li>型別：多對一</li><li>參考結構描述： B2B行銷活動</li><li>名稱空間： B2B行銷活動</li><li>目的地屬性： `campaignKey.sourceKey`</li><li>來自目前結構描述的關係名稱：行銷活動</li><li>引用結構描述中的關係名稱：人員</li></ul> |
| B2B行銷清單 | [XDM業務行銷清單](../../../../xdm/classes/b2b/business-marketing-list.md) | None | 已启用 | `marketingListKey.sourceKey` 在基底類別中 | B2B行銷清單 | None | None | None | 靜態清單未同步自 [!DNL Salesforce] 因此沒有次要身分。 |
| B2B行銷清單成員 | [XDM業務行銷清單成員](../../../../xdm/classes/b2b/business-marketing-list-members.md) | None | 已启用 | `marketingListMemberKey.sourceKey` 在基底類別中 | B2B行銷清單成員 | None | None | **第一次關聯**<ul><li>`PersonKey.sourceKey` 在基底類別中</li><li>型別：多對一</li><li>參考結構描述： B2B Person</li><li>名稱空間： B2B Person</li><li>目的地屬性： `b2b.personKey.sourceKey`</li><li>來自目前結構描述的關係名稱： Person</li><li>參考結構描述中的關係名稱：行銷清單</li></ul>**第二個關係**<ul><li>`marketingListKey.sourceKey` 在基底類別中</li><li>型別：多對一</li><li>參考結構描述：B2B行銷清單</li><li>名稱空間： B2B行銷清單</li><li>目的地屬性： `marketingListKey.sourceKey`</li><li>來自目前結構描述的關係名稱：行銷清單</li><li>引用結構描述中的關係名稱：人員</li></ul> | 靜態清單成員未同步自 [!DNL Salesforce] 因此沒有次要身分。 |
| B2B活動 | [XDM ExperienceEvent](../../../../xdm/classes/experienceevent.md) | <ul><li>造訪網頁</li><li>新銷售機會</li><li>轉換潛在客戶</li><li>新增至清單</li><li>從清單移除</li><li>新增至商機</li><li>從機會移除</li><li>表單已填寫</li><li>連結點按次數</li><li>電子郵件已傳遞</li><li>電子郵件已開啟</li><li>電子郵件已點按</li><li>電子郵件已退回</li><li>電子郵件已軟退回</li><li>電子郵件已取消訂閱</li><li>分數已變更</li><li>機會已更新</li><li>行銷活動進度中的狀態已變更</li><li>個人識別碼</li><li>Marketo網頁URL</li><li>有趣的時刻</li><li>呼叫Webhook</li><li>變更行銷活動步調</li><li>收入階段已變更</li><li>合併銷售機會</li><li>已发送电子邮件</li><li>變更行銷活動資料流</li><li>新增至行銷活動</li></ul> | 已启用 | `personKey.sourceKey` 個人識別碼欄位群組 | B2B人員 | None | None | **第一次關聯**<ul><li>`listOperations.listKey.sourceKey` 欄位</li><li>型別：一對一</li><li>參考結構描述：B2B行銷清單</li><li>名稱空間： B2B行銷清單</li></ul>**第二個關係**<ul><li>`opportunityEvent.opportunityKey.sourceKey` 欄位</li><li>型別：一對一</li><li>參考結構描述：B2B機會</li><li>名稱空間： B2B機會</li></ul>**第三個關係**<ul><li>`leadOperation.campaignProgression.campaignKey.sourceKey` 欄位</li><li>型別：一對一</li><li>參考結構描述： B2B行銷活動</li><li>名稱空間： B2B行銷活動</li></ul> | `ExperienceEvent` 與實體不同。 體驗事件的身分識別是執行活動的人員。 |
| B2B帳戶個人關係 | [XDM商業帳戶個人關係](../../../../xdm/classes/b2b/business-account-person-relation.md) | 标识映射 | 已启用 | `accountPersonKey.sourceKey` 在基底類別中 | B2B帳戶個人關係 | None | None | **第一次關聯**<ul><li>`personKey.sourceKey` 在基底類別中</li><li>型別：多對一</li><li>參考結構描述： B2B Person</li><li>名稱空間： B2B Person</li><li>目的地屬性： `b2b.personKey.SourceKey`</li><li>來自目前結構描述的關係名稱： People</li><li>引用結構描述中的關係名稱：帳戶</li></ul>**第二個關係**<ul><li>`accountKey.sourceKey` 在基底類別中</li><li>型別：多對一</li><li>參考結構描述： B2B帳戶</li><li>名稱空間： B2B帳戶</li><li>目的地屬性： `accountKey.sourceKey`</li><li>來自目前結構描述的關係名稱：帳戶</li><li>引用結構描述中的關係名稱：人員</li></ul> |

{style="table-layout:auto"}

## 后续步骤

若要瞭解如何連結 [!DNL Marketo] 資料轉換至Platform，請參閱以下主題上的教學課程： [在UI中建立Marketo來源聯結器](../../../tutorials/ui/create/adobe-applications/marketo.md).
