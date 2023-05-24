---
keywords: Experience Platform；首頁；熱門主題；資料控管；資料使用原則使用手冊
solution: Experience Platform
title: 在UI中管理資料使用原則
description: Adobe Experience Platform資料控管提供使用者介面，可讓您建立和管理資料使用原則。 本檔案概述您可以在Experience Platform使用者介面的「原則」工作區中執行的動作。
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
source-git-commit: a1628df7d0eefc795d1eaeefce842a65c7133322
workflow-type: tm+mt
source-wordcount: '1618'
ht-degree: 19%

---

# 在UI中管理資料使用原則 {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_description"
>title="在您的配置文件数据中集成并强制客户同意"
>abstract="<h2>描述</h2><p>通过 Platform，可将从客户收集的同意数据集成到其各自的配置文件中。然后可设置同意策略以确定能否在对于特定目标激活的区段中包括这些数据。</p>"

本檔案說明如何使用 **[!UICONTROL 原則]** Adobe Experience Platform UI中的工作區，用來建立和管理資料使用原則。

>[!NOTE]
>
>有關如何在UI中管理存取控制原則的資訊，請參閱 [屬性型存取控制UI指南](../../access-control/abac/ui/policies.md) 而非。

>[!IMPORTANT]
>
>所有資料使用原則(包括Adobe提供的核心原則)預設為停用。 為了將個別原則考慮為強制執行，您必須手動啟用該原則。 請參閱以下小節： [啟用原則](#enable) 以瞭解如何在UI中執行此動作的步驟。

## 先决条件

本指南需要您深入瞭解下列各項 [!DNL Experience Platform] 概念：

* [資料控管](../home.md)
* [数据使用策略](./overview.md)

## 檢視現有原則 {#view-policies}

在 [!DNL Experience Platform] UI，選取 **[!UICONTROL 原則]** 以開啟 **[!UICONTROL 原則]** 工作區。 在 **[!UICONTROL 瀏覽]** 索引標籤中，您可以看到可用原則的清單，包括其關聯的標籤、行銷動作和狀態。

![](../images/policies/browse-policies.png)

如果您有權存取同意政策，請選取 **[!UICONTROL 同意原則]** 切換即可在 [!UICONTROL 瀏覽] 標籤。

![](../images/policies/consent-policy-toggle.png)

選取列出的原則以檢視其說明和型別。 如果選取自訂原則，則會顯示其他控制項以編輯、刪除或 [啟用/停用原則](#enable).

![](../images/policies/policy-details.png)

## 建立自訂原則 {#create-policy}

若要建立新的自訂資料使用原則，請選取 **[!UICONTROL 建立原則]** 右上角 **[!UICONTROL 瀏覽]** 索引標籤中的 **[!UICONTROL 原則]** 工作區。

![](../images/policies/create-policy-button.png)

根據您是否為同意政策Beta版的一部分，會發生下列其中一種情況：

* 如果您不屬於Beta版，系統會立即將您帶至工作流程進行 [建立資料治理原則](#create-governance-policy).
* 如果您是測試版的一部分，對話方塊會提供額外選項，可 [建立同意原則](#consent-policy).
   ![](../images/policies/choose-policy-type.png)

### 建立資料治理原則 {#create-governance-policy}

此 **[!UICONTROL 建立原則]** 工作流程隨即顯示。 首先，提供新原則的名稱和說明。

![](../images/policies/create-policy-description.png)

接下來，選取原則將依據的資料使用標籤。 選取多個標籤時，您可以選擇資料應包含所有標籤，還是僅包含其中一個標籤，以套用原則。 選取 **[!UICONTROL 下一個]** 完成後。

![](../images/policies/add-labels.png)

此 **[!UICONTROL 選取行銷動作]** 步驟隨即顯示。 從提供的清單中選擇適當的行銷動作，然後選取「 」 **[!UICONTROL 下一個]** 以繼續。

>[!NOTE]
>
>選取多個行銷動作時，原則會將它們解譯為「或」規則。 換言之，此原則適用於 **任何** 所選行銷動作中的最後一個專案。

![](../images/policies/add-marketing-actions.png)

此 **[!UICONTROL 檢閱]** 步驟隨即顯示，可讓您在建立新原則之前先檢閱其詳細資訊。 在您滿意後，請選取 **[!UICONTROL 完成]** 以建立原則。

![](../images/policies/policy-review.png)

此 **[!UICONTROL 瀏覽]** 標籤會重新顯示，現在會列出「草稿」狀態的新建立原則。 若要啟用此原則，請參閱下一節。

![](../images/policies/created-policy.png)

### 建立同意原則 {#consent-policy}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_instructions"
>title="说明"
>abstract="<ul><li>确保您通过 OneTrust 源连接器或用于同意的标准 XDM 架构将首选项数据引入到您的联合架构中。</li><li>在左侧导航中选择<a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=zh-Hans">策略</a>，然后选择<a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html#create-governance-policy">创建策略</a>。</li><li>在<b>如果</b>部分下面，描述将触发策略检查的条件或操作。</li><li>在<b>则</b>部分下面，输入必须存在才能在触发该策略的操作中包括配置文件的同意属性。</li><li>选择<b>保存</b>以创建该策略。要启用该策略，请选择右边栏中的<b>状态</b>切换开关。</li><li>Experience Platform 在您对于目标激活区段时自动执行您启用的同意策略，并提供有关每项策略如何影响您的受众规模的详细信息。</li><li>有关此功能的更多帮助，请参阅 Experience League 上关于<a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html#consent-policy">创建同意策略</a>的指南。</li></ul>"

>[!IMPORTANT]
>
>同意原則僅適用於已購買的組織 **AdobeHealthcare Shield** 或 **Adobe隱私權與安全性盾牌**.

如果您選擇建立同意原則，則會顯示一個新畫面，讓您設定新原則。

![](../images/policies/consent-policy-dialog.png)

為了使用同意原則，您的設定檔資料中必須有同意屬性。 請參閱指南： [Experience Platform中的同意處理](../../landing/governance-privacy-security/consent/adobe/overview.md) 瞭解如何在聯合結構描述中包含所需屬性的詳細步驟。

同意原則包含兩個邏輯元件：

* **[!UICONTROL 若]**：將觸發原則檢查的條件。 這可能根據所執行的特定行銷動作、特定資料使用標籤的出現或兩者的組合而定。
* **[!UICONTROL 則]**：設定檔必須存在的同意屬性，才能納入觸發原則的動作中。

#### 設定條件 {#consent-conditions}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentif"
>title="“如果”条件"
>abstract="首先定义会触发策略检查的条件。条件可以包括正在采取的某些营销行动、存在的某些数据治理标签，或两者的组合。"

在 **[!UICONTROL 若]** 區段，選取應該觸發此原則的行銷動作和/或資料使用標籤。 選取 **[!UICONTROL 檢視全部]** 和 **[!UICONTROL 選取標籤]** 以分別檢視可用行銷動作和標籤的完整清單。

新增至少一個條件後，您可以選取 **[!UICONTROL 新增條件]** 若要繼續視需要新增其他條件，請從下拉式選單中選擇適當的條件型別。

![](../images/policies/add-condition.png)

如果您選取多個條件，您可以使用出現在它們之間的圖示，來切換「與」和「或」之間的條件關係。

![](../images/policies/and-or-selection.png)

#### 選取同意屬性 {#consent-attributes}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentthen"
>title="“则”条件"
>abstract="定义“如果”条件后，使用“则”部分从联合架构中选择至少一个同意属性。这是必须存在的属性，以便配置文件包含在此策略所控制的操作中。"

在 **[!UICONTROL 則]** 區段，從聯合結構描述中選取至少一個同意屬性。 这是必须存在的属性，以便配置文件包含在此策略所控制的操作中。您可以從清單中選擇其中一個提供的選項，或選取 **[!UICONTROL 檢視全部]** 以直接從聯合結構描述選擇屬性。

選取同意屬性時，請選擇您要此原則檢查的屬性值。

![](../images/policies/select-schema-field.png)

選取至少一個同意屬性後， **[!UICONTROL 原則屬性]** 面板更新以顯示此原則允許的預估設定檔數目，包括設定檔存放區總數的百分比。 當您調整原則設定時，此估算會自動更新。

![](../images/policies/audience-preview.png)

若要進一步新增同意屬性至原則，請選取 **[!UICONTROL 新增結果]**.

![](../images/policies/add-result.png)

您可以視需要繼續新增和調整條件和同意屬性至原則。 當您對設定感到滿意時，請先提供原則的名稱和選擇性說明，然後再選取 **[!UICONTROL 儲存]**.

![](../images/policies/name-and-save.png)

同意原則現在已建立，其狀態已設為 [!UICONTROL 已停用] 依預設。 若要立即啟用原則，請選取 **[!UICONTROL 狀態]** 在右側邊欄中切換。

![](../images/policies/enable-consent-policy.png)

#### 驗證原則執行

建立並啟用同意原則後，您可以預覽原則在啟用目的地的區段時如何影響您同意的對象。 請參閱以下小節： [同意原則評估](../enforcement/auto-enforcement.md#consent-policy-evaluation) 以取得詳細資訊。

## 啟用或停用原則 {#enable}

所有資料使用原則(包括Adobe提供的核心原則)預設為停用。 對於要考慮強制執行的個別原則，您必須透過API或UI手動啟用該原則。

您可以從以下位置啟用或停用原則： **[!UICONTROL 瀏覽]** 索引標籤中的 **[!UICONTROL 原則]** 工作區。 從清單中選取自訂原則，以在右側顯示其詳細資訊。 下 **[!UICONTROL 狀態]**，選取切換按鈕以啟用或停用原則。

![](../images/policies/enable-policy.png)

## 檢視行銷動作 {#view-marketing-actions}

在 **[!UICONTROL 原則]** 工作區中，選取 **[!UICONTROL 行銷動作]** 標籤以檢視Adobe與您自己的組織所定義的可用行銷動作清單。

![](../images/policies/marketing-actions.png)

## 建立行銷動作 {#create-marketing-action}

若要建立新的自訂行銷動作，請選取 **[!UICONTROL 建立行銷動作]** 右上角 **[!UICONTROL 行銷動作]** 索引標籤中的 **[!UICONTROL 原則]** 工作區。

![](../images/policies/create-marketing-action.png)

此 **[!UICONTROL 建立行銷動作]** 對話方塊隨即顯示。 輸入行銷動作的名稱和說明，然後選取 **[!UICONTROL 建立]**.

![](../images/policies/create-marketing-action-details.png)

新建立的動作會出現在 **[!UICONTROL 行銷動作]** 標籤。 您現在可以在以下情況下使用行銷動作： [建立新的資料使用原則](#create-policy).

![](../images/policies/created-marketing-action.png)

## 編輯或刪除行銷動作 {#edit-delete-marketing-action}

>[!NOTE]
>
>只能編輯您的組織定義的自訂行銷動作。 無法變更或刪除Adobe定義的行銷動作。

在 **[!UICONTROL 原則]** 工作區中，選取 **[!UICONTROL 行銷動作]** 標籤以檢視Adobe與您自己的組織所定義的可用行銷動作清單。 從清單中選取自訂行銷動作，然後使用右側區段中提供的欄位來編輯行銷動作的詳細資訊。

![](../images/policies/edit-marketing-action.png)

如果任何現有使用原則未使用行銷動作，您可以選取「 」，將其刪除 **[!UICONTROL 刪除行銷動作]**.

>[!NOTE]
>
>嘗試刪除現有原則正在使用的行銷動作會導致出現錯誤訊息，指出刪除嘗試失敗。

![](../images/policies/delete-marketing-action.png)

## 后续步骤

本檔案概述如何在中管理資料使用原則 [!DNL Experience Platform] UI。 有關如何使用管理原則的步驟 [!DNL Policy Service API]，請參閱 [開發人員指南](../api/getting-started.md). 如需如何強制執行資料使用原則的詳細資訊，請參閱 [原則執行概觀](../enforcement/overview.md).

以下影片示範如何使用中的使用原則 [!DNL Experience Platform] UI：

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
