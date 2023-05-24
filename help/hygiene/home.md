---
title: 資料檢疫概觀
description: Adobe Experience Platform資料檢疫可讓您透過更新或清除過時或不準確的記錄，來管理資料的生命週期。
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: 2913e9e687843e566db4ebf2031e610d1891d4c9
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 1%

---

# Adobe Experience Platform中的資料衛生

>[!IMPORTANT]
>
>資料檢疫目前僅適用於已購買的組織 **AdobeHealthcare Shield** 或 **Adobe隱私權與安全性盾牌**. 這些功能將於不久的未來正式發行。 如需其未來可用性的詳細資訊，請洽詢您的Adobe服務代表。 不過，您可以立即 [透過刪除資料集 [!UICONTROL 資料集] UI](../catalog/datasets/user-guide.md#delete).

Adobe Experience Platform提供一套強大的工具，可管理大型複雜資料作業，以便協調消費者體驗。 隨著時間推移，資料會內嵌到系統中，因此管理您的資料存放區變得越來越重要，以便資料能如預期使用、在不正確的資料需要更正時更新，並在組織原則認為必要時刪除。

<!-- Platform's data hygiene capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

這些活動可使用以下專案執行： [[!UICONTROL 資料衛生] UI工作區](#ui) 或 [資料衛生API](#api). 執行資料衛生工作時，系統會在流程的每個步驟提供透明度更新。 請參閱以下小節： [時間表與透明度](#timelines-and-transparency) 有關如何在系統中表示每種工作型別的詳細資訊。

## [!UICONTROL 資料衛生] UI工作區 {#ui}

此 [!UICONTROL 資料衛生] Platform UI中的工作區可讓您設定和排程資料檢疫作業，協助確保您的記錄得以如預期般維護。

如需在UI中管理資料檢疫任務的詳細步驟，請參閱 [資料衛生UI指南](./ui/overview.md).

## 資料衛生API {#api}

此 [!UICONTROL 資料衛生] UI建置在資料衛生API之上，如果您偏好自動化資料衛生活動，可以直接使用該API的端點。 請參閱 [資料衛生API指南](./api/overview.md) 以取得詳細資訊。

## 時間軸和透明度

記錄刪除和資料集到期要求都有各自的處理時間表，並在各自工作流程的關鍵時間點提供透明度更新。

<!-- ### Dataset expirations {#dataset-expiration-transparency} -->

下列情形會在下列情況下發生： [資料集到期要求](./ui/dataset-expiration.md) 已建立：

| 暂存 | 排程到期之後的時間 | 描述 |
| --- | --- | --- |
| 已提交請求 | 0 小时 | 資料管理員或隱私權分析人員會提交資料集請求，讓資料集在指定時間過期。 此請求會顯示在 [!UICONTROL 資料衛生UI] 在提交之後，且會維持擱置狀態，直到排定的到期時間（該時間過後）才會執行請求。 |
| 資料集已捨棄 | 1 小时 | 資料集會從 [資料集詳細目錄頁面](../catalog/datasets/user-guide.md) 在UI中。 Data Lake中的資料只會軟性刪除，直到程式結束為止，之後會硬性刪除。 |
| 設定檔計數已更新 | 30 小时 | 根據要刪除的資料集內容，如果某些設定檔的所有元件屬性都與該資料集相關聯，則可能會從系統中將其移除。 資料集刪除後30小時，整體設定檔計數的任何結果變更都會反映在 [儀表板Widget](../dashboards/guides/profiles.md#profile-count-trend) 和其他報表。 |
| 區段已更新 | 48 小时 | 更新所有受影響的設定檔後，所有相關的 [區段](../segmentation/home.md) 會更新以反映其新大小。 根據已移除的資料集和您進行區段的屬性，每個區段的大小可能會因刪除而增加或減少。 |
| 歷程和目的地已更新 | 50 小时 | [歷程](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html)， [行銷活動](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html)、和 [目的地](../destinations/home.md) 會根據相關區段中的變更進行更新。 |
| 硬刪除完成 | 14 天 | 所有與資料集相關的資料都會從資料湖中硬刪除。 此 [衛生工作的狀態](./ui/browse.md#view-details) 會更新已刪除的資料集以反映這一點。 |

{style="table-layout:auto"}

<!-- ### Record deletes {#record-delete-transparency}

>[!IMPORTANT]
>
>Record deletes are only available for organizations that have purchased Adobe Healthcare Shield.

The following takes place when a [record delete request](./ui/record-delete.md) is created:

| Stage | Time after request submission | Description |
| --- | --- | --- |
| Request is submitted | 0 hours | A data steward or privacy analyist submits a record delete request. The request is visible in the [!UICONTROL Data Hygiene UI] after it has been submitted. |
| Profile lookups updated | 3 hours | The change in profile counts caused by the deleted identity are reflected in [dashboard widgets](../dashboards/guides/profiles.md#profile-count-trend) and other reports. |
| Segments updated | 24 hours | Once profiles are removed, all related [segments](../segmentation/home.md) are updated to reflect their new size. |
| Journeys and destinations updated | 26 hours | [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campaigns](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), and [destinations](../destinations/home.md) are updated according to changes in related segments. |
| Records soft deleted in data lake | 7 days | The data is soft deleted from the data lake. |
| Data vacuuming completed | 14 days | The [status of the hygiene job](./ui/browse.md#view-details) updates to indicate that the job has completed, meaning that data vacuuming has been completed on the data lake and the relevant records have been hard deleted. |

{style="table-layout:auto"} -->

## 后续步骤

本檔案概述平台的資料檢疫功能。 若要開始在UI中提出資料檢疫請求，請參閱 [UI指南](./ui/overview.md). 若要瞭解如何以程式設計方式建立資料檢疫工作，請參閱 [資料衛生API指南](./api/overview.md)
