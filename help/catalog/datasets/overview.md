---
keywords: Experience Platform；首頁；熱門主題；資料位置；資料位置；資料管理；資料管理；譜系；譜系；資料型別；資料型別；資料型別；資料型別
solution: Experience Platform
title: 資料集概述
description: 本文档高度概括 Experience Platform 中的数据集。
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 8%

---

# 資料集總覽

所有成功內嵌至Adobe Experience Platform的資料都會儲存在 [!DNL Data Lake] 作為資料集。 数据集是用于数据集合的存储和管理结构，通常是表格，其中包含架构（列）和字段（行）。数据集还包含描述其存储的数据的各方面特性的元数据。

本檔案提供中資料集的高層級概觀 [!DNL Experience Platform].

## 建立資料集和追蹤中繼資料

[!DNL Catalog Service] 是內資料位置和譜系的記錄系統 [!DNL Experience Platform]，和可用來建立和管理資料集。 [!DNL Catalog] 追蹤每個資料集的中繼資料，其中包括對 [!DNL Experience Data Model] (XDM)結構描述資料集符合（下節將加以說明）並擷取到該資料集的記錄數。

請參閱 [目錄服務概觀](../home.md) 以取得詳細資訊。

## 對資料集資料強制執行限制

[!DNL Experience Data Model] (XDM)是標準化的架構，其中 [!DNL Platform] 組織客戶體驗資料。 擷取到的所有資料 [!DNL Platform] 必須符合預先定義的XDM結構描述，才能將其儲存在 [!DNL Data Lake] 作為資料集。

所有資料集都包含XDM結構描述的參考，限制可儲存資料的格式和結構。 嘗試上傳資料到不符合資料集XDM結構描述的資料集會導致擷取失敗。

如需XDM的詳細資訊，請參閱 [XDM系統總覽](../../xdm/home.md).

## 將資料擷取至資料集

Adobe Experience Platform資料擷取代表多種方法，可供 [!DNL Platform] 從各種來源擷取資料。 無論擷取方法為何，所有成功擷取的資料都會轉換為批次檔案。 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。然後，這些批次檔案會新增至專用資料集，並保留在 [!DNL Data Lake].

請參閱 [資料擷取概觀](../../ingestion/home.md) 以取得詳細資訊。

## 將使用標籤套用至資料集

Adobe Experience Platform資料控管可讓您管理客戶資料，以確保遵守適用於資料使用的法規、限制和原則。 資料控管架構可讓您套用使用標籤，以根據套用至該資料的使用原則來分類資料。

>[!IMPORTANT]
>
>僅資料控管使用案例支援在資料集層級套用標籤。 如果您嘗試建立資料的存取原則，您必須 [將標籤套用至結構描述](../../xdm/tutorials/labels.md) 資料集所根據的。 請參閱以下文章的概觀： [基於屬性的存取控制](../../access-control/abac/overview.md) 以取得詳細資訊。

資料使用情況標籤可套用至整個資料集或個別資料集欄位。 該資料集內的所有欄位都會繼承在資料集層級新增的標籤。

請參閱 [資料控管概觀](../../data-governance/home.md) 以取得服務的詳細資訊。 有關如何使用中的使用標籤的步驟 [!DNL Platform]，請參閱下列指南：

* [在UI中管理標籤](../../data-governance/labels/user-guide.md)
* [在API中管理資料集標籤](../../data-governance/labels/dataset-api.md)

## 下游的資料集 [!DNL Platform] 服務

資料集一旦用來儲存擷取的資料後，下游就會使用這些資料集 [!DNL Platform] 更新客戶設定檔、透過機器學習獲得深入分析等功能的服務。

以下是使用資料集進行各種操作的下游服務清單。 如需詳細資訊，請參閱各服務的檔案。

* [[!DNL Data Access API]](../../data-access/home.md)：可讓您存取和下載儲存在資料集中的檔案內容。
* [Adobe Experience Platform Identity Service](../../identity-service/home.md)：跨裝置和系統橋接身分，根據資料集符合的XDM結構描述所定義的身分欄位將其連結在一起。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：利用 [!DNL Identity Service] 以即時從資料集建立詳細的客戶設定檔。 [!DNL Real-Time Customer Profile] 從以下專案提取資料： [!DNL Data Lake] 並將客戶設定檔儲存在其專屬的資料存放區中。
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md)：可讓您建立區段，並從 [!DNL Real-Time Customer Profile] 資料。 然後，這些對象可以匯出至他們自己的資料集 [!DNL Data Lake].
* [Adobe Experience Platform資料科學工作區](../../data-science-workspace/home.md)：使用機器學習和人工智慧來發掘大型資料集中的深入分析。
* [Adobe Experience Platform查詢服務](../../query-service/home.md)：可讓您使用標準SQL在中查詢資料 [!DNL Experience Platform]，在中聯結任何資料集 [!DNL Data Lake] 以及將查詢結果擷取為新資料集以用於報表， [!DNL Data Science Workspace]，或 [!DNL Real-Time Customer Profile].
* [Adobe Experience Platform目標服務](../../destinations/home.md)：可讓您 [匯出資料集](/help/destinations/ui/export-datasets.md) 至您所需的雲端儲存空間或電子郵件行銷目的地，以用於報表或資料科學活動。

## 后续步骤

閱讀本檔案後，您將瞭解資料集的核心用法 [!DNL Experience Platform]以及各種 [!DNL Platform] 利用資料集的服務。 如需資料集在中的使用方式的詳細資訊 [!DNL Platform]，請檢閱本概述中連結的服務檔案。

如需如何與內的資料集互動的相關步驟， [!DNL Experience Platform] UI，請參閱 [資料集使用手冊](user-guide.md).
