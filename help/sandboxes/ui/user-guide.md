---
keywords: Experience Platform；首頁；熱門主題；沙箱使用手冊；沙箱指南
solution: Experience Platform
title: 沙箱UI指南
description: 本檔案提供如何在Adobe Experience Platform使用者介面中執行與沙箱相關的各種操作的步驟。
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 8%

---

# 沙箱UI指南

本檔案提供如何在Adobe Experience Platform使用者介面中執行與沙箱相關的各種操作的步驟。

## 檢視沙箱

在Platform UI中選取 **[!UICONTROL 沙箱]** 在左側導覽中，然後選取 **[!UICONTROL 瀏覽]** 以開啟 [!UICONTROL 沙箱] 儀表板。 儀表板會列出貴組織的所有可用沙箱，包括其個別型別（生產或開發）。

![檢視 — 沙箱](../images/ui/view-sandboxes.png)

## 在沙箱之間切換

沙箱指標位於Platform UI的頂端標題中，會顯示您目前所在沙箱的標題、其區域和型別。

![sandbox-indicate](../images/ui/sandbox-indicator.png)

若要在沙箱之間切換，請選取沙箱指標，然後從下拉式清單中選取所需的沙箱。

![切換器介面](../images/ui/switcher-interface.png)

選取沙箱後，畫面會重新整理並更新至您選取的沙箱。

![沙箱交換](../images/ui/sandbox-switched.png)

## 建立新沙箱 {#create}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxname"
>title="沙盒名称"
>abstract="沙盒名称是在后端用于为此沙盒创建唯一 ID 的文本。"

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtitle"
>title="沙盒标题"
>abstract="沙盒标题是在整个 Experience Platform UI 的菜单和下拉列表中代表沙盒的显示名称。"

>[!NOTE]
>
>建立新沙箱時，您必須先將該新沙箱新增到您的產品設定檔中 [Adobe Admin Console](https://adminconsole.adobe.com/) 開始使用新沙箱之前。 請參閱以下說明檔案： [管理產品設定檔的許可權](../../access-control/ui/permissions.md) 有關如何將沙箱布建至產品設定檔的資訊。

使用下列影片快速概略瞭解如何在Experience Platform中使用沙箱。

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

若要建立新沙箱，請選取 **[!UICONTROL 建立沙箱]** 在畫面的右上角。

![create-sandbox](../images/ui/create-sandbox.png)

此 **[!UICONTROL 建立沙箱]** 對話方塊隨即顯示。 如果您正在建立開發沙箱，請選取 **[!UICONTROL 開發]** 在下拉式面板中。 若要建立新的生產沙箱，請選取 **[!UICONTROL 生產]**.

![sandbox-type](../images/ui/sandbox-type.png)

選取型別後，為您的沙箱提供名稱和標題。 標題應該可人為讀取，且描述性應足以輕鬆識別。 沙箱名稱是用於API呼叫的全小寫識別碼，因此應是唯一的且簡潔的。 沙箱名稱必須以字母開頭，最多可有256個字元，而且僅包含英數字元和連字型大小(-)。

完成後，選取 **[!UICONTROL 建立]**.

![sandbox-info](../images/ui/sandbox-info.png)

當您完成建立沙箱後，請重新整理頁面，新沙箱隨即會出現在 **[!UICONTROL 沙箱]** 具有「」狀態的儀表板[!UICONTROL 建立]「。 系統布建新沙箱大約需要30秒，之後其狀態會變更為&quot;[!UICONTROL 作用中]「。

![new-sandbox](../images/ui/new-sandbox.png)

## 重設沙箱

>[!WARNING]
>
>以下是可阻止您重設預設生產沙箱或使用者建立的生產沙箱的例外清單： <ul><li>如果Adobe Analytics也將沙箱中代管的身分圖表用於，則無法重設預設的生產沙箱 [跨裝置分析(CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html) 功能。</li><li>如果Adobe Audience Manager也將沙箱中代管的身分圖表用於，則無法重設預設的生產沙箱 [以人物為基礎的目的地(PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html).</li><li>如果預設的生產沙箱包含CDA和PBD功能的資料，則無法重設。</li><li>在出現警告訊息後，可以重設使用者建立的、用於與Adobe Audience Manager或Audience Core Service雙向區段共用的生產沙箱。</li></ul>

重設生產或開發沙箱會刪除與該沙箱關聯的所有資源（結構描述、資料集等），同時保留沙箱的名稱和關聯的許可權。 此「乾淨」沙箱可繼續供擁有存取權的使用者以相同名稱使用。

從沙箱清單中選取您要重設的沙箱。 在出現的右側導覽面板中，選取 **[!UICONTROL 沙箱重設]**.

![重設](../images/ui/reset.png)

會出現一個對話方塊，提示您確認您的選擇。 選取 **[!UICONTROL 繼續]** 以繼續進行。

![reset-warning](../images/ui/reset-warning.png)

在最終確認視窗中，在對話方塊中輸入沙箱名稱，然後選取 **[!UICONTROL 重設]**.

![reset-confirm](../images/ui/reset-confirm.png)

## 刪除沙箱

>[!WARNING]
>
>您無法刪除預設的生產沙箱。 但是，任何使用者建立的、用於雙向區段共用的生產沙箱， [!DNL Audience Manager] 或 [!DNL Audience Core Service] 可在警告訊息後刪除。

刪除生產或開發沙箱會永久移除與該沙箱關聯的所有資源，包括許可權。

從沙箱清單中選取您要刪除的沙箱。 在出現的右側導覽面板中，選取 **[!UICONTROL 刪除]**.

![delete](../images/ui/delete.png)

會出現一個對話方塊，提示您確認您的選擇。 選取 **[!UICONTROL 繼續]** 以繼續進行。

![delete-warning](../images/ui/delete-warning.png)

在最終確認視窗中，在對話方塊中輸入沙箱名稱，然後選取  **[!UICONTROL 繼續]**.

![delete-confirm](../images/ui/delete-confirm.png)

## 后续步骤

本檔案會示範如何在Experience PlatformUI中管理沙箱。 如需有關如何使用沙箱API管理沙箱的資訊，請參閱 [沙箱開發人員指南](../api/getting-started.md).
