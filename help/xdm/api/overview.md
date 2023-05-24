---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；體驗資料模型；體驗資料模型；資料模型；資料模型；結構描述登入；結構描述登入；
solution: Experience Platform
title: Schema Registry API指南
description: Schema Registry API可讓開發人員以程式設計方式管理Adobe Experience Platform中的所有結構描述和相關的Experience Data Model (XDM)資源。 参阅本指南，了解如何使用 API 执行关键操作。
exl-id: 9e693d29-303e-462a-a1e2-93c0d517b8e3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 2%

---

# [!DNL Schema Registry] API指南

此 [!DNL Schema Registry] 用於存取Adobe Experience Platform中的Schema Library，提供可存取所有可用程式庫資源的使用者介面和RESTful API。

Schema Registry API提供數個端點，可讓您以程式設計方式管理Platform中可供您使用的所有結構描述和相關的Experience Data Model (XDM)資源。 這包括Adobe所定義的那些專案， [!DNL Experience Platform] 您使用之應用程式的合作夥伴與廠商。

這些端點概述如下。 如需詳細資訊，請參閱個別端點指南，並參閱 [快速入門手冊](./getting-started.md) 如需必要標題的重要資訊，請參閱範例API呼叫等。

>[!IMPORTANT]
>
>XDM使用JSON結構描述格式來說明和驗證所擷取客戶體驗資料的結構。 在使用Schema Registry API之前，強烈建議您檢閱 [官方JSON結構描述檔案](https://json-schema.org/) 以進一步瞭解這項基礎技術。

若要檢視所有可用的端點和CRUD作業，請造訪 [結構描述登入API參考](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## 架构

XDM結構描述會呈現並驗證擷取到Platform的資料結構和格式。 結構描述由一個類別和零個或多個結構描述欄位群組組成。 您可以使用建立、檢視、編輯和刪除方案 `/schemas` 端點。 若要瞭解如何使用此端點，請參閱 [結構描述端點指南](./schemas.md).

如需如何在Schema Registry API中手動建立完整結構描述的逐步指南，包括建立和新增欄位群組和資料型別，請參閱 [API結構描述建立教學課程](../tutorials/create-schema-api.md).

如果您要擷取CSV資料，請參閱以下小節： [CSV至結構描述轉換](#csv-to-schema).

## 行为

行為會定義結構描述之資料的性質。 每個XDM類別都必須參考特定行為，而使用該類別的所有結構描述都會繼承該行為。 請參閱 [行為端點指南](./behaviors.md) 以瞭解如何檢視API中的可用行為。

## 类

類別定義以該類別為基礎的所有結構描述都必須包含的通用屬性的基底結構，並決定哪些欄位群組適合用於這些結構描述。 每個類別都必須與現有行為相關聯。 請參閱 [類別端點指南](./classes.md) 以取得在API中使用類別的詳細資訊。

## 字段组

欄位群組是可重複使用的元件，可定義代表特定概念的一或多個欄位，例如個人、郵寄地址或網頁瀏覽器環境。 視欄位群組代表的資料行為（記錄或時間序列）而定，這些欄位群組旨在包含在實作相容類別的結構描述中。 請參閱 [欄位群組端點指南](./field-groups.md) 以瞭解如何在API中使用欄位群組。

## 数据类型

資料型別在類別或欄位群組中的參考型別欄位使用方式，與基本常值欄位相同，主要差異在於資料型別可以定義多個子欄位。 雖然資料型別與欄位群組類似，因為它們允許一致地使用多欄位結構，但資料型別更靈活，因為它們可以包含在結構描述結構中的任何位置，而欄位群組只能新增到根層級。 請參閱 [資料型別端點指南](./data-types.md) 以取得在API中使用資料型別的詳細資訊。

## 描述項

描述項是指派給結構描述內特定欄位的一組中繼資料，提供各種內容詳細資訊，包括這些欄位（以及結構描述本身）如何與其他結構描述相關。 每個結構描述可以套用一或多個描述項實體，並且有幾種不同的描述項型別可用於不同的目的。 請參閱 [描述項端點指南](./descriptors.md) 如需在API中使用描述項的詳細資訊，以及不同描述項型別及其使用案例的概觀。

## 聯合

雖然Platform可讓您針對特定使用案例撰寫結構描述，但也可讓您撰寫屬於特定類別的結構描述的「聯合」。 聯合結構描述會將共用相同類別的所有結構描述的欄位彙總到單一表示中。 透過啟用結構描述以用於 [即時客戶個人檔案](../../profile/home.md)，該結構描述會納入其特定類別的聯集內。 因此，聯合結構描述不能直接編輯，並且只能受到在設定檔中包含或排除使用結構描述的影響。

若要瞭解如何在Schema Registry API中檢視聯合，請參閱 [聯合端點指南](./unions.md).

## CSV至結構描述轉換 {#csv-to-schema}

您可以使用CSV檔案作為範本自動產生XDM結構描述，允許您建立範本以大量匯入結構描述欄位，並縮短手動API或UI工作。

請參閱 [CSV至結構描述轉換端點指南](./export.md) 以取得詳細資訊。

>[!NOTE]
>
>您也可以使用UI來 [使用AI產生的建議將CSV對應到結構描述](../../ingestion/tutorials/map-csv/recommendations.md) （目前為測試版）。

## 导出 {#export}

Schema Registry API可讓您在沙箱和組織之間傳輸和共用XDM資源。 對於任何結構描述、欄位群組或資料型別，您可以產生包含資源結構和任何相依資源的匯出裝載。 然後，此裝載可用於將資源匯入目標沙箱和組織。

請參閱 [匯出端點指南](./export.md) 有關如何為現有XDM資源建立匯出裝載的詳細資訊。

## 导入

如果您使用 [匯出](#export) 或 [CSV至結構描述轉換](./import.md) 端點若要建立匯出裝載，您可以將該裝載傳送至目標組織和沙箱，以匯入指定的資源。

請參閱 [匯入端點指南](./export.md) 有關如何從匯出裝載產生XDM資源的詳細資訊。

## 範例資料

您可以為結構描述資料庫中任何指定的結構描述產生範例資料。 接著，傳回的回應物件即可作為資料擷取的來源。

請參閱 [範例資料端點指南](./sample-data.md) 以取得有關使用此端點的詳細資訊。

## 稽核記錄

「結構描述登入」會維護不同更新之間對資源（類別、欄位群組、資料型別或結構描述）發生的所有變更記錄。 您可以提供特定資源的記錄，擷取其記錄 `$id` 或 `meta:altId` 在此端點的GET要求路徑中。

請參閱 [稽核記錄端點指南](./audit-log.md) 以取得有關使用此端點的詳細資訊。

## 后续步骤

若要開始使用Schema Registry API進行呼叫，請參閱 [快速入門手冊](./getting-started.md) 然後選取其中一個端點指南，以瞭解如何使用特定端點。
