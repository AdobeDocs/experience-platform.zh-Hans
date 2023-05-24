---
title: 管理資料集有效期
description: 瞭解如何在Adobe Experience Platform UI中排程資料集有效期。
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: a1628df7d0eefc795d1eaeefce842a65c7133322
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 22%

---

# 管理資料集有效期 {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="删除多余或到期的客户记录和数据集"
>abstract="<h2>描述</h2><p>要管理与监管合规无关的 Experience Platform 数据的生命周期，可删除使用者记录并安排数据集的到期日期。要创建或管理数据主体请求，请参阅“遵守数据主体隐私请求”用例块。</p>"

>[!IMPORTANT]
>
>Adobe Experience Platform中的資料檢疫功能目前僅適用於已購買的組織 **AdobeHealthcare Shield** 或 **Adobe隱私權與安全性盾牌**. 這些功能將於不久的未來正式發行。 如需其未來可用性的詳細資訊，請洽詢您的Adobe服務代表。 不過，您可以立即 [透過刪除資料集 [!UICONTROL 資料集] UI](../../catalog/datasets/user-guide.md#delete).

此 [[!UICONTROL 資料衛生] 工作區](./overview.md) Adobe Experience Platform UI中的可讓您排程資料集的到期時間。 當資料集到達其到期日時，Data Lake、Identity Service和Real-Time Customer Profile會開始個別程式，從各自的服務中移除資料集的內容。 從所有三項服務中刪除資料後，到期日即會標籤為完成。

>[!WARNING]
>
>如果資料集設為過期，您必須手動變更任何可能將資料擷取至該資料集的資料流程，讓您的下游工作流程不會受到負面影響。

本文介紹如何在Platform UI中排程和管理資料集有效期。

## 排程資料集到期日 {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="说明"
>abstract="<ul><li>在左侧导航中选择<a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/overview.html">数据卫生</a>，然后选择<b>创建请求</b>。</li><li>如果要删除记录：</li>   <li>选择<b>记录</b>。</li>   <li>选择要从中删除记录的特定数据集，或选择从所有数据集中删除记录的选项。</li>   <li>提供要删除其记录的使用者的身份。选择<b>添加身份</b>以一次提供一个身份，或改为选择<b>选择文件</b>以上传包含多个身份的 JSON 文件。</li>   <li>如果需要，请选择<b>模板</b>以查看该 JSON 文件的预期格式。</li><li>如果要<a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/dataset-expiration.html#schedule-dataset-expiration">安排数据集的到期日期</a>，请参阅说明文档。</li></ul>"

若要建立新請求，請選取「 」 **[!UICONTROL 建立請求]** 從工作區的首頁面。

![影像顯示 [!UICONTROL 建立請求] 正在選取按鈕](../images/ui/ttl/create-request-button.png)

此時會出現請求建立對話方塊。 在 **[!UICONTROL 請求的動作]** 區段，選取 **[!UICONTROL 刪除資料集]** 更新資料集到期排程的可用控制項。

![影像顯示 [!UICONTROL 建立請求] 正在選取按鈕](../images/ui/ttl/dataset-selected.png)

### 選取日期和資料集

此時會出現請求建立對話方塊。 在 **[!UICONTROL 請求的動作]** 區段，選取您要刪除資料集的日期。 您可以手動輸入日期(格式為 `mm/dd/yyyy`)或選取行事曆圖示(![行事曆圖示的影像](../images/ui/ttl/calendar-icon.png))以從對話方塊中選取日期。

![顯示資料集設定到期日的影像](../images/ui/ttl/select-date.png)

下一個，在 **[!UICONTROL 資料集詳細資料]**，選取資料庫圖示(![資料庫圖示的影像](../images/ui/ttl/database-icon.png))以開啟資料集選擇對話方塊。 從清單中選擇要套用到期日的資料集，然後選取 **[!UICONTROL 完成]**.

![顯示正在選取之資料集的影像](../images/ui/ttl/select-dataset.png)

>[!NOTE]
只會顯示屬於目前沙箱的資料集。

### 提交請求

此 [!UICONTROL 資料集詳細資料] 區段會填入，以包含所選資料集的主要身分和結構描述。 下 **[!UICONTROL 請求設定]**，輸入要求的名稱和說明（選擇性），然後按一下 **[!UICONTROL 提交]**.

![影像顯示 [!UICONTROL 提交] 正在選取按鈕](../images/ui/ttl/submit.png)

系統會要求您確認刪除資料集的日期。 選取 **[!UICONTROL 提交]** 以繼續。

提交請求後，即會建立工單並出現在「 」的主標籤上。 [!UICONTROL 資料衛生] 工作區。 從這裡，您可以在工單處理請求時監視工單的狀態。

>[!NOTE]
請參閱概述一節，網址為 [時間表與透明度](../home.md#dataset-expiration-transparency) 以取得資料集過期執行後如何處理的詳細資訊。

## 編輯或取消資料集有效期

若要編輯或取消資料集有效期，請選取「 」 **[!UICONTROL 資料集]** ，並從清單中選取資料集有效期。

在資料集到期的詳細資訊頁面上，右側欄會顯示用於編輯或取消排程刪除的控制項。

## 后续步骤

本檔案說明如何在Experience PlatformUI中排程資料集有效期。 有關如何在UI中執行其他資料檢疫工作的資訊，請參閱 [資料衛生UI總覽](./overview.md).

若要瞭解如何使用資料衛生API排程資料集有效期，請參閱 [資料集到期端點指南](../api/dataset-expiration.md).
