---
keywords: Experience Platform；首頁；熱門主題；資料擷取；資料位置；資料位置；資料管理；譜系；譜系；批次；批次；擷取的資料
solution: Experience Platform
title: 数据摄取概述
description: 本檔案會介紹將資料內嵌到Platform的三種主要方式，並提供各自概述檔案的連結，以取得更詳細的資訊。
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 15%

---

# 資料擷取概觀

Adobe Experience Platform 将来自多个来源的数据整合在一起，以帮助营销人员更好地了解其客户的行为。Adobe Experience Platform資料擷取代表多種方法，可供 [!DNL Platform] 從這些來源擷取資料，以及該資料如何儲存在資料湖中以供下游使用 [!DNL Platform] 服務。

本檔案會介紹三種主要的方式將資料擷取到 [!DNL Platform]，並附上其各自概述檔案的連結，以取得更詳細的資訊。

## 批量摄取

批次內嵌可讓您將資料內嵌至 [!DNL Experience Platform] 作為批次檔案。 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。摄取后，批量会提供元数据以描述已成功摄取的记录数量，以及任何失败记录和关联的错误消息。

必須使用此方法內嵌手動上傳的資料檔，例如一般CSV檔案（對應至XDM結構描述）和Parquet dataframe。

請參閱 [批次擷取概觀](./batch-ingestion/overview.md) 以取得詳細資訊。

## 流式摄取

串流內嵌可讓您從使用者端和伺服器端裝置傳送資料至 [!DNL Experience Platform] 即時。 [!DNL Platform] 支援使用資料匯入，將傳入的體驗資料串流處理，這些資料會儲存在Data Lake內啟用串流的資料集中。 資料匯入可設定為自動驗證其收集的資料，確保資料來自信任的來源。

請參閱 [串流擷取概觀](./streaming-ingestion/overview.md) 以取得詳細資訊。

## 源

[!DNL Experience Platform] 可讓您設定各種資料提供者的來源連線。 這些連線可讓您驗證外部資料來源、設定擷取執行時間，以及管理擷取輸送量。

來源連線可設定為從其他Adobe應用程式(例如Adobe Analytics和Adobe Audience Manager)、協力廠商雲端儲存空間(例如 [!DNL Azure Blob]， [!DNL Amazon] S3、FTP伺服器和SFTP伺服器)以及協力廠商CRM系統(例如 [!DNL Microsoft Dynamics] 和 [!DNL Salesforce])。

請參閱 [來源概觀](../sources/home.md) 以取得詳細資訊。

## 後續步驟和其他資源

本檔案簡要介紹 [!DNL Data Ingestion] 在 [!DNL Experience Platform]. 請繼續閱讀每個擷取方法的概觀檔案，以熟悉其不同的功能、使用案例和最佳實務。 您也可以觀看下方的擷取概觀影片，以補充您的學習。 如需如何操作的詳細資訊 [!DNL Experience Platform] 追蹤所擷取記錄的中繼資料，請參閱 [目錄服務概觀](../catalog/home.md).

>[!WARNING]
>
>以下影片中使用的「統一設定檔」一詞已過時。 條款 [!DNL "Profile"] 或 [!DNL "Real-Time Customer Profile"] 是中使用的正確術語 [!DNL Experience Platform] 說明檔案。 請參閱檔案以瞭解最新功能。

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
