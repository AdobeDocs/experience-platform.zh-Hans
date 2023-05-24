---
keywords: Experience Platform；首頁；熱門主題；客戶屬性聯結器
solution: Experience Platform
title: 客戶屬性來源聯結器概述
description: 瞭解如何使用API或使用者介面將客戶屬性連結至Adobe Experience Platform
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 10%

---

# 客戶屬性聯結器

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=en) Experience Cloud可讓您上傳從客戶關係管理(CRM)資料庫擷取的企業資料。 您可以将数据上传到 Experience Cloud 中的客户属性数据源，然后在 Adobe Analytics 和 Adobe Target 中使用这些数据。

Experience Platform提供擷取支援 [!DNL Customer Attributes] 將設定檔資料匯入Adobe Experience Platform。

## 資料集和結構描述

此 [!DNL Customer Attributes] source會自動建立資料集，以供資料著陸使用。 此自動建立的資料集已修正，無法手動選取。 來源也會根據輸入資料來源自動建立資料集的結構描述。 此程式也涉及在結構描述和來源資料之間自動建立必要的對應。

## 标识

資料集的主要身分包含在來源資料的CSV檔案的第一欄。 此 [!DNL Customer Attributes] 來源假設身分一律對應至 [`CORE` 名稱空間](../../../identity-service/namespaces.md)，系統產生的名稱空間，由以下程式庫支援： [[!DNL Identity Service]](../../../identity-service/home.md).

使用時，您無法選取身分的現有名稱空間 [!DNL Customer Attributes] 來源，因為 [!DNL Customer Attributes] 假設結構描述的主要身分一律在身分對應中。 [!DNL Customer Attributes] 然後以自動方式建立來源ID與身分對應UUID的對應。

對象 [!DNL Customer Attributes] 連結至其他人的資料 [!DNL Profile] 資料集、其資料和身分必須能夠與Experience CloudID相符。

您可以建立 `CORE` 名稱空間，方法是使用設定訪客的Experience CloudID [Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en)， [行動SDK](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/identity)，或 [Experience CloudID服務API](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=en).

此 [!DNL Customer Attributes] 檔案不會進一步填入任何其他身分關係。 例如，如果 [!DNL Customer Attributes] 來源資料集包含 **電子郵件** 和 **熟客ID** 欄位，則這些欄位必須在結構描述中標籤為身分欄位，才能處理到 [!DNL Identity Service].

請參閱教學課程，位置如下： [建立 [!DNL Customer Attributes] ui中的來源連線](../../tutorials/ui/create/adobe-applications/customer-attributes.md) 以取得詳細資訊。
