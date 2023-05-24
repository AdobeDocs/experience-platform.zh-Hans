---
title: 瀏覽資料衛生工單
description: 瞭解如何在Adobe Experience Platform使用者介面中檢視和管理現有的資料衛生工單。
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 25%

---

# 瀏覽資料衛生工單 {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="工单 ID"
>abstract="在向系统发送数据卫生请求时，将创建工单以执行请求的任务。换句话说，工单代表一个特定的数据卫生流程，包括其当前状态和其他相关详细信息。每个工单在创建后会自动获得其唯一 ID。"
>text="See the data hygiene UI guide to learn more."

>[!IMPORTANT]
>
>Adobe Experience Platform中的資料檢疫功能目前僅適用於已購買的組織 **AdobeHealthcare Shield** 或 **Adobe隱私權與安全性盾牌**.

在向系统发送数据卫生请求时，将创建工单以执行请求的任务。工單代表特定的資料檢疫程式，例如排程的資料集到期日，其中包括其目前狀態和其他相關詳細資訊。

本指南說明如何在Adobe Experience Platform UI中檢視和管理現有工單。

## 列出及篩選現有工單

當您第一次存取 **[!UICONTROL 資料衛生]** 工作區在UI中，會顯示現有工單清單及其基本詳細資訊。

![影像顯示 [!UICONTROL 資料衛生] Platform UI中的工作區](../images/ui/browse/work-order-list.png)

清單一次只會顯示一個類別的工作訂單。 選取 **[!UICONTROL 消費者]** 若要檢視記錄刪除工作清單，以及 **[!UICONTROL 資料集]** 以檢視已排程資料集有效期的清單。

![影像顯示 [!UICONTROL 資料集] 標籤](../images/ui/browse/dataset-tab.png)

選取漏斗圖示(![漏斗圖示的影像](../images/ui/browse/funnel-icon.png))以檢視所顯示工單的篩選器清單。

![顯示的工作單篩選器影像](../images/ui/browse/filters.png)

根據您檢視的工作單型別，可使用不同的篩選選項。

### 記錄刪除的篩選器

以下篩選器適用於記錄刪除請求：

| 过滤器 | 描述 |
| --- | --- |
| [!UICONTROL 状态] | 根據工單的目前狀態進行篩選：<ul><li>**[!UICONTROL 已完成]**：工作已完成。</li><li>**[!UICONTROL 已失敗]**：工作發生錯誤，無法完成。</li><li>**[!UICONTROL 處理中]**：請求已開始，目前正在處理中。</li></ul> |
| [!UICONTROL 建立日期] | 根據工單建立時間進行篩選。 |
| [!UICONTROL 更新日期] | 根據上次更新工單的時間進行篩選。 建立即計為更新。 |

### 資料集有效期的篩選器

下列篩選器適用於資料集過期請求：

| 过滤器 | 描述 |
| --- | --- |
| [!UICONTROL 状态] | 根據工單的目前狀態進行篩選：<ul><li>**[!UICONTROL 已完成]**：工作已完成。</li><li>**[!UICONTROL 擱置中]**：工作已建立但尚未執行。 A [資料集到期要求](./dataset-expiration.md) 在排定的刪除日期之前假設此狀態。 刪除日期到達後，狀態會更新為 [!UICONTROL 執行中] 除非事先取消工作。</li><li>**[!UICONTROL 執行中]**：資料集到期要求已開始，目前正在處理中。</li><li>**[!UICONTROL 已取消]**：工作已取消，因為是手動使用者請求的一部分。</li></ul> |
| [!UICONTROL 建立日期] | 根據工單建立時間進行篩選。 |
| [!UICONTROL 过期日期] | 根據相關資料集的排程刪除日期篩選資料集到期請求。 |
| [!UICONTROL 更新日期] | 根據上次更新工單的時間進行篩選。 建立及過期均會計為更新。 |

{style="table-layout:auto"}

## 檢視工單的詳細資訊 {#view-details}

>[!CONTEXTUALHELP]
>id="platform_hygiene_statusbyservice"
>title="按服务显示的状态"
>abstract="数据卫生请求由多个 Experience Platform 服务独立处理。此部分概述了每个相应服务的请求的当前处理状态。要了解更多信息，请参阅《数据卫生 UI 指南》。"

>[!CONTEXTUALHELP]
>id="platform_hygiene_numberofidentities"
>title="标识数"
>abstract="其记录在此工单中被请求更新或删除的标识的数量。计数中包含的标识不一定存在于受影响的数据集中。要了解更多信息，请参阅《数据卫生 UI 指南》。"

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="记录删除响应"
>abstract="当记录删除过程收到来自系统的响应时，这些消息将显示在&#x200B;**[!UICONTROL 结果]**&#x200B;部分下。如果在处理工单时出现问题，任何相关的错误消息都会显示在此部分中，帮助您解决问题。要了解更多信息，请参阅《数据卫生 UI 指南》。"

選取所列工單的ID以檢視其詳細資訊。

![顯示所選取工單ID的影像](../images/ui/browse/select-work-order.png)

根據所選工單型別，會提供不同的資訊和控制項。 以下各節將說明這些內容。

### 記錄刪除詳細資料 {#record-delete}

記錄刪除請求的詳細資訊包括其目前狀態以及自提出請求以來經過的時間。 每個請求也包含 **[!UICONTROL 依服務的狀態]** 區段，提供刪除所涉及每個下游服務的個別狀態詳細資訊。 在右側邊欄上，您可以使用控制項來更新工單的名稱和說明。

![顯示記錄刪除工單之詳細資訊頁面的影像](../images/ui/browse/record-delete-details.png)

### 資料集到期日詳細資料 {#dataset-expiration}

資料集到期的詳細資訊頁面提供其基本屬性的資訊，包括排程的到期日（即刪除前的剩餘天數）。 在右側邊欄中，您可以使用控制項來編輯或取消有效期。

![顯示資料集到期工作單的詳細資訊頁面的影像](../images/ui/browse/ttl-details.png)

## 后续步骤

本指南說明如何在Platform UI中檢視及管理現有資料檢疫工單。 如需建立您自己的工單的相關資訊，請參閱下列檔案：

* [管理資料集有效期](./dataset-expiration.md)
<!-- * [Manage record deletes](./record-delete.md) -->
