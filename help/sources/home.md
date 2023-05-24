---
keywords: Experience Platform；首頁；熱門主題；來源聯結器；來源聯結器；來源；資料來源；資料來源；資料來源連線
solution: Experience Platform
title: 來源聯結器概述
description: Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: feb05d5bddc4135c5fe14d3ec5d8fad62c5e2236
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 2%

---

# 來源聯結器概觀

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以从各种源中摄取数据，如 Adobe 应用程序、基于云的存储、数据库和许多其他源。

[!DNL Flow Service] 用於收集並集中來自Platform內各種不同來源的客戶資料。 此服務提供使用者介面和RESTful API，可讓您輕鬆設定與各種資料提供者的來源連線。 這些來源連線可讓您驗證協力廠商系統、設定擷取執行時間，以及管理資料擷取輸送量。

透過Experience Platform，您可以集中從不同來源收集的資料，並使用從中獲得的見解做更多事情。

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## 來源型別

Experience Platform中的來源會分組到下列類別中：

### Adobe應用程式 {#adobe-applications}

Experience Platform可讓您從其他Adobe應用程式(包括Adobe Analytics和Adobe Audience Manager)擷取資料。 如需詳細資訊，請參閱下列相關檔案：

- [Adobe Audience Manager來源概觀](connectors/adobe-applications/audience-manager.md)
   - [在使用者介面中建立Adobe Audience Manager來源連線](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics分類資料來源概觀](connectors/adobe-applications/classifications.md)
   - [在UI中建立Adobe Analytics分類資料來源連線](./tutorials/ui/create/adobe-applications/classifications.md)
- [Adobe Analytics報表套裝資料來源概觀](connectors/adobe-applications/analytics.md)
   - [在使用者介面中建立Adobe Analytics來源連線](./tutorials/ui/create/adobe-applications/analytics.md)
- [Adobe Campaign Managed Cloud Services來源概觀](connectors/adobe-applications/campaign.md)
   - [在使用者介面中建立Adobe Campaign Managed Cloud Services來源連線](./tutorials/ui/create/adobe-applications/campaign.md)
- [Adobe資料收集來源概觀](connectors/adobe-applications/data-collection.md)
   - [在使用者介面中建立客戶屬性來源連線](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] 來源概觀](connectors/adobe-applications/marketo/marketo.md)
   - [建立 [!DNL Marketo Engage] ui中的來源連線](./tutorials/ui/create/adobe-applications/marketo.md)
   - [建立 [!DNL Marketo Engage] 自訂活動資料的來源連線和資料流](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
- [Adobe Workfront來源概觀](connectors/adobe-applications/workfront.md)
   - [在使用者介面中建立Workfront來源連線](./tutorials/ui/create/adobe-applications/workfront.md)

### Advertising {#advertising}

Experience Platform提供從協力廠商廣告系統擷取資料的支援。 如需特定來源聯結器的詳細資訊，請參閱下列相關檔案：

- [Google Ads](connectors/advertising/ads.md)

### Analytics {#analytics}

Experience Platform支援從協力廠商analytics平台擷取資料。 如需詳細資訊，請參閱下列相關檔案：

- [[!DNL Mixpanel]](connectors/analytics/mixpanel.md)
- [[!DNL Pendo]](connectors/analytics/pendo-webhook.md)

### 雲端儲存空間 {#cloud-storage}

雲端儲存空間來源可將您自己的資料帶入Platform，而不需要下載、格式化或上傳。 內嵌的資料可以格式化為XDM JSON、XDM Parquet或分隔。 流程的每個步驟都會使用使用者介面整合至來源工作流程。 如需詳細資訊，請參閱下列相關檔案：

- [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob]](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3]](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md)
- [[!DNL FTP]](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md)
- [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md)
- [[!DNL SFTP]](connectors/cloud-storage/sftp.md)

### 同意和偏好設定 {#consent}

Experience Platform支援從協力廠商同意和偏好設定管理平台擷取資料。 如需詳細資訊，請參閱下列相關檔案：

- [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md)

### 客戶關係管理(CRM) {#customer-relationship-management}

CRM系統提供的資料可協助建立客戶關係，進而建立忠誠度並提升客戶保留率。 Experience Platform提供從擷取CRM資料的支援 [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce]. 如需詳細資訊，請參閱下列相關檔案：

- [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce]](connectors/crm/salesforce.md)
- [[!DNL SugarCRM]](connectors/crm/sugarcrm.md)
- [[!DNL Veeva CRM]](connectors/crm/veeva.md)
- [[!DNL Zoho CRM]](connectors/crm/zoho.md)

### 客戶成功 {#customer-success}

Experience Platform提供從協力廠商客戶成功應用程式擷取資料的支援。 如需詳細資訊，請參閱下列相關檔案：

- [[!DNL Oracle Service Cloud]](connectors/customer-success/oracle-service-cloud.md)
- [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow]](connectors/customer-success/servicenow.md)
- [[!DNL Zendesk]](connectors/customer-success/zendesk.md)

### 数据库 {#database}

Experience Platform支援從協力廠商資料庫擷取資料。 如需特定來源聯結器的詳細資訊，請參閱下列相關檔案：

- [[!DNL Amazon Redshift]](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage]](connectors/databases/ats.md)
- [[!DNL Couchbase]](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery]](connectors/databases/bigquery.md)
- [[!DNL GreenPlum]](connectors/databases/greenplum.md)
- [[!DNL HP Vertica]](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2]](connectors/databases/ibm-db2.md)
- [[!DNL MariaDB]](connectors/databases/mariadb.md)
- [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md)
- [[!DNL MySQL]](connectors/databases/mysql.md)
- [[!DNL Oracle]](connectors/databases/oracle.md)
- [[!DNL Phoenix]](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL]](connectors/databases/postgres.md)
- [[!DNL Snowflake]](connectors/databases/snowflake.md)
- [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md)

### 电子商务 {#ecommerce}

Experience Platform支援從協力廠商電子商務系統擷取資料。 如需特定來源聯結器的詳細資訊，請參閱下列相關檔案：

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)
- [[!DNL Shopify Streaming]](connectors/ecommerce/shopify-streaming.md)

### 本機系統 {#local-system}

Experience Platform提供從本機系統擷取資料的支援。 如需特定來源聯結器的詳細資訊，請參閱下列相關檔案：

- [本機檔案上傳](connectors/local-system/local-file-upload.md)

### 行銷自動化 {#marketing-automation}

Experience Platform提供從協力廠商行銷自動化系統擷取資料的支援。 如需特定來源聯結器的詳細資訊，請參閱下列相關檔案：

- [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md)
- [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md)
- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md)
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md)
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md)
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md)
<!-- 
- [[!DNL Oracle Responsys]](connectors/marketing-automation/oracle-responsys.md)
-->

### 付款 {#payments}

Experience Platform支援從協力廠商付款系統擷取資料。 如需特定來源聯結器的詳細資訊，請參閱下列相關檔案：

- [[!DNL PayPal]](connectors/payments/paypal.md)
- [[!DNL Square]](connectors/payments/square.md)

### 串流 {#streaming}

Experience Platform支援從串流來源擷取資料。 如需特定來源聯結器的詳細資訊，請參閱下列相關檔案：

- [[!DNL HTTP API]](connectors/streaming/http.md)

### 通訊協定 {#protocols}

Experience Platform支援從協力廠商通訊協定系統擷取資料。 如需特定來源聯結器的詳細資訊，請參閱下列相關檔案：

- [[!DNL Generic OData]](connectors/protocols/odata.md)
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md)

## 資料擷取中來源的存取控制

資料內嵌來源的許可權可在Adobe Admin Console中管理。 您可以透過以下方式存取許可權 **[!UICONTROL 許可權]** 標籤中指定產品的設定檔。 從 **[!UICONTROL 編輯許可權]** 面板中，您可以透過以下方式存取與來源相關的許可權： **[!UICONTROL 資料擷取]** 功能表專案。 此 **[!UICONTROL 檢視來源]** 許可權會授予「 」中可用來源的唯讀存取權 **[!UICONTROL 目錄]** 索引標籤和已驗證的來源 **[!UICONTROL 瀏覽]** 標籤，而 **[!UICONTROL 管理來源]** 許可權會授予讀取、建立、編輯和停用來源的完整存取權。

下表概述UI根據這些許可權的不同組合時的行為方式：

| 許可權層級 | 描述 |
| ---- | ----|
| **[!UICONTROL 檢視來源]** 開啟 | 授予「目錄」標籤中每個來源型別以及「瀏覽」、「帳戶」和「資料流」標籤的來源的唯讀存取權。 |
| **[!UICONTROL 管理來源]** 開啟 | 除了包含的函式以外 **[!UICONTROL 檢視來源]**，授予存取權 **[!UICONTROL 連線來源]** 中的選項 **[!UICONTROL 目錄]** 和 **[!UICONTROL 選取資料]** 中的選項 **[!UICONTROL 瀏覽]**. **[!UICONTROL 管理來源]** 也可讓您啟用或停用 **[!UICONTROL DataFlows]** 並編輯其排程。 |
| **[!UICONTROL 檢視來源]** 關閉和 **[!UICONTROL 管理來源]** 關閉 | 撤銷對來源的所有存取權。 |

如需透過Adobe許可權授與的可用許可權的詳細資訊，請參閱 [存取控制總覽](../access-control/home.md).

### 基于属性的访问控制

Adobe Experience Platform中基於屬性的存取控制可讓管理員根據屬性控制對特定物件和/或權能的存取。

透過以屬性為基礎的存取控制，您可以將對應設定套用至您擁有許可權的欄位。 此外，如果您無權存取資料集中的所有欄位，則無法將資料內嵌至資料集。

#### 支援來源中的屬性型存取控制

>[!TIP]
>
>屬性型存取控制的運作方式如下： **角色** 建立用來分類與您的Platform執行個體互動的使用者型別。 **標籤** 套用至 **角色** 以指定該指定角色的存取權。 **標籤** 也會套用至結構描述欄位和區段等資源。 為了讓使用者能存取某些結構描述欄位和區段，必須將其新增至 *具有指派給查詢資源的相同標籤的角色*. 如需詳細資訊，請閱讀 [屬性型存取控制端對端指南](../access-control/abac/end-to-end-guide.md).

- 將標籤套用至結構描述欄位，以定義對組織中特定結構描述欄位的存取權。 建立對特定結構描述欄位的存取權後，使用者將只能為他們有權存取的欄位建立對應。
- 沒有適當角色的使用者將無法使用包含無法存取之結構描述欄位的對應建立或更新資料流程。 此外，未經授權的使用者無法更新、刪除、啟用或停用具有無法存取之結構描述欄位的現有資料流。
- 此外，資料流在其對應、目標資料集和目標連線中，必須有完全相同的結構描述ID和版本。

如需以屬性為基礎的存取控制的詳細資訊，請閱讀 [屬性型存取控制概觀](../access-control/abac/overview.md).

## 條款與條件 {#terms-and-conditions}

使用任何標示為Beta版(「Beta」)的來源，即表示您確認已提供Beta版 ***「原樣」，不含任何保固***.

Adobe沒有義務維護、更正、更新、變更、修改或以其他方式支援Beta版。 建議您謹慎使用，不要依賴此類Beta版及/或隨附資料的正確功能或效能。 Beta版被視為Adobe的機密資訊。

任何「意見回饋」（有關Beta版資訊，包括但不限於您在使用Beta版時遇到的問題或缺陷、建議、改進和建議）一律指定給Adobe，包括此等意見回饋的所有權利、標題和興趣，以及Adobe。

提交公開意見或建立支援票證以分享您的建議或報告錯誤，並尋求功能增強。
