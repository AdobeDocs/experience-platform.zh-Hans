---
keywords: RTCDP；CDP；B2B版本；Real-time Customer Data Platform；即時客戶資料平台；real time cdp；b2b；cdp；客戶人工智慧
title: Real-Time CDP B2B版本概觀
description: Real-Time Customer Data Platform B2B 版本帐户概述
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 1%

---

# Real-time Customer Data Platform B2B版本概觀

Real-Time CDP B2B Edition以Adobe Real-time Customer Data Platform (Real-Time CDP)為基礎，專為以B2B服務模式運作的行銷人員所打造。 它會整合來自多個來源的資料，並將其合併為單一檢視的人員與帳戶設定檔。 此統一的資料可讓行銷人員精準鎖定特定對象，並透過所有可用管道吸引這些對象。

有各種Adobe Experience Platform功能的改善，可區分Real-Time CDP B2B版本與其B2C版本。 其中包括改善B2B使用案例的Experience Data Model (XDM)、升級身分解析和設定檔分段，以及針對以下專案自訂建立的聯結器和目的地： [!DNL Marketo Engage]. 此 [!DNL Marketo] connector可讓B2B品牌將其領先業界的B2B參與資料與行為資訊連結，以培育潛在客戶並增強以帳戶為基礎的行銷作業。

使用Real-Time CDP B2B版本，您可以：

* 將從多個來源收集的資料合併到單一檢視中，以建立整體性的人員和帳戶設定檔。
* 從統一帳戶設定檔的集中存放區擴充、劃分及匯出所有跨來源資料。
* 使用資料控管工具來管理您的資料，這些工具可在集中程式的每個步驟中使用，以確保您的資料符合法律法規和業務政策。

有關Real-Time CDP B2B版本改進功能的更完整詳細資訊，分為以下幾節。

## XDM

Real-Time CDP B2B Edition提供數種新的XDM結構描述類別、欄位群組和關係型別，以擷取和建構您的資料並專門用於B2B用途。 請參閱以下文章的概觀： [Real-Time CDP B2B版本中的XDM](./schemas/b2b.md) 以取得每個增強功能的劃分資訊。

透過使用預先設定的B2B結構描述，您可以將資料匯入標準化的可操作結構中。 許多新結構描述類別幾乎直接對應到主流CRM中遇到的類別，例如 [!DNL Salesforce]， [!DNL Microsoft Dynamics]， [!DNL Marketo]和其他B2B資料來源。 有了Real-Time CDP B2B Edition，您可以直接的方式將資料從B2B來源帶入Platform，而且結果易於稽核。

這些XDM增強功能可讓您透過以B2B為中心的來源和目的地更好地擷取和啟用資料，進而改善資料統一和呈現，以因應更多樣化和彈性的使用案例。

## 身分解析

定義結構描述並擷取符合這些結構描述的資料後，Real-Time CDP B2B Edition會透過功能強大的即時身分識別系統識別代表真實世界人員和企業的來源記錄。

身分解析系統提供下列功能：

* 合併B2B和B2C人員記錄
* 多重層次科目階層
* 多對多人員對帳戶連線
* 即時解析人員和帳戶身分

身分解析系統已擴充，以支援更多元化的人員分類。 此系統可讓相關人員被識別為商業機會的潛在客戶以及客戶。

由來源CRM同步並透過系統內的多個路徑連線的帳戶記錄由Platform合併在一起。 此系統將與業務機會相關的人員和記錄為客戶的人員，但如果可識別，則還能保留他們之間的區別作為屬性。

相符的識別碼可用來連結在一起，並合併來自多個系統的帳戶記錄。 在整個過程中都會保留帳戶階層。 差異區段可用來仔細檢視個人是否與帳戶相關聯，並提供了視需要將其與帳戶區分開的功能。

## 設定檔和區段

一旦Real-Time CDP B2B Edition擷取了與人員、公司、屬性和行為相關的資料並解析了身分後，該資料就會用於建構設定檔。 然後，這些設定檔可以區分為可瀏覽的對象，這些對象然後可以啟動到各種目的地。

正確實作後，系統會使用唯一的主要識別碼（而非可變更的屬性，例如電子郵件地址）來追蹤人員。 這表示當有人變更工作時，系統仍會追蹤這些工作。 個人仍是相同的實體，但他們會連結至新帳戶。 此原生功能提供擴充至新帳戶的絕佳向量，因為系統以包括他們所有屬性和行為的個人身分追蹤這些人。

## B2B來源

Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 此 [!DNL Marketo] 來源可讓您將B2B資料串流到Platform，並使用平台連線的應用程式保持這些資料在最新狀態。 它支援任意數量的例項 [!DNL Marketo] （對擁有多個例項的大型公司有好處），並提取至單一組織，資料會合併至其中。

>[!NOTE]
>
>此 [!DNL Marketo] 來源為 **not** 使用Real-Time CDP B2B版本時需要。

請參閱 [Real-Time CDP B2B版本中的來源](./sources/b2b.md) 有關Marketo和將B2B資料帶入Platform的詳細資訊，請參閱相關檔案。

## B2B目的地

Google Customer Match、Facebook、LinkedIn、Marketo Engage、Amazon S3、Google Display &amp; Video 360、Google Ads和Google Ad Manager等Experience Platform目的地都由Real-Time CDP B2B Edition提供和完全支援。 Marketo Engage目的地也會將區段會籍資料從Platform串流出來，並以Marketo中的清單形式提供。

請參閱以下文章的概觀： [Marketo Engage目的地](../destinations/catalog/adobe/marketo-engage.md) 以取得詳細資訊。

對於擁有多個CRM的公司，Real-Time CDP B2B Edition提供將目的地聯結器設定為分隔Marketo或CRM執行個體的選項。 如有需要，您可以為每個執行個體設定目的地聯結器，並單獨將對象傳送到每個CRM執行個體。

## 后续步骤

現在您已更瞭解Real-Time CDP B2B Edition為行銷人員提供的好處，以及它與Real-Time CDP之間的差異，您可以瞭解如何將這些功能套用至您自己的組織。

若要瞭解Real-Time CDP B2B Edition如何讓您的企業對企業服務模式受益，請參閱以下檔案以幫助您開始使用：

* [Real-Time CDP B2B版本的範例使用案例](./b2b-use-case.md)
* [Real-time Customer Data Platform B2B版本的端對端教學課程](./b2b-tutorial.md)
* [如何內嵌資料](./sources/b2b.md)
* [如何存取設定檔](./profile/profile-overview.md)
* [Real-time Customer Data Platform B2B版本中的結構描述](./schemas/b2b.md)
* [如何建立區段](./segmentation/b2b.md)
* [如何啟用目的地的區段](./destinations/b2b.md)
* [如何定義及強制執行資料控管原則](./privacy/data-governance-overview.md)
