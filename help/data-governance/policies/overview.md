---
keywords: Experience Platform；首頁；熱門主題；dule；DULE
solution: Experience Platform
title: 資料使用原則概觀
description: 資料使用原則是描述允許或限制您在Adobe Experience Platform中對資料執行的行銷動作型別的規則。
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 2%

---

# 資料使用原則概觀 {#policies-overview}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_restrictusage"
>title="限制数据使用"
>abstract="数据使用策略类型将评估应用于数据治理标签的具体营销行为，以便限制用于营销活动的数据使用。"

為了使資料使用標籤有效地支援資料合規性，必須實施資料使用原則。 資料使用原則是描述允許或限制您對內資料執行何種行銷動作的規則 [!DNL Experience Platform].

有兩種可用的原則：

* **[!UICONTROL 資料治理原則]**：根據執行的行銷動作和有問題資料攜帶的資料使用標籤，限制資料啟用。
* **[!UICONTROL 同意原則]**：篩選可以啟用的設定檔 [目的地](../../destinations/home.md) 根據客戶的同意或偏好

>[!NOTE]
>
>資料使用原則切勿與混淆 [存取控制原則](../../access-control/abac/end-to-end-guide.md#policy)，此變數會判斷貴組織中的特定Platform使用者是否可存取特定資料欄位，並透過 [!UICONTROL 許可權] 標籤。

本檔案提供資料使用原則的高層級概觀，並提供在UI或API中使用原則的進一步檔案連結。

## 行銷動作 {#marketing-actions}

在資料控管框架中的行銷動作（也稱為行銷使用案例）是 [!DNL Experience Platform] 資料消費者可能會採取某些措施，而您的組織想要針對這些措施限制資料使用。 因此，以下內容會定義資料使用原則：

1. 特定行銷動作
2. 限制該動作執行的條件

行銷動作的範例可能是想要將資料集匯出至協力廠商服務。 如果制定原則規定無法匯出特定型別的資料(例如個人識別資訊(PII))，而您嘗試匯出包含「I」標籤（身分資料）的資料集，您將會收到 [!DNL Policy Service] 告知您已違反資料使用原則。

>[!NOTE]
>
>行銷動作本身不會限制資料使用。 它們必須包含在啟用的資料使用原則中，才能評估這些動作是否違反原則。

當貴組織的服務中使用資料時，應指出相關的行銷動作，以便識別任何原則違規。 然後，您可以使用 [原則服務API](https://www.adobe.io/experience-platform-apis/references/policy-service/) 檢查整合中的原則違規。

>[!NOTE]
>
>您可以在目的地上設定行銷使用案例，以自動化原則執行。 請參閱 [目的地檔案](../../destinations/home.md) 以取得特定目的地之組態選項的詳細資訊。

請參閱本檔案的附錄以取得 [可用的Adobe定義行銷動作](#core-actions). 您也可以使用定義自己的自訂行銷動作 [!DNL Policy Service] API或 [!DNL Experience Platform] 使用者介面。 下一節將提供有關使用行銷動作和原則的更多資訊。

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## 管理資料使用原則 {#manage}

套用資料使用標籤後，資料管理員可以使用 [!DNL Policy Service] API或 [!DNL Experience Platform] 用於管理和評估對包含資料使用標籤之資料採取的行銷動作相關原則的UI。 您可以建立和更新原則、判斷原則的狀態，並與行銷動作合作，評估特定動作是否違反資料使用原則。

>[!IMPORTANT]
>
>所有資料使用原則(包括Adobe提供的核心原則)預設為停用。 為了將個別原則考慮為強制執行，您必須透過API或UI手動啟用該原則。

如需在API中使用行銷動作和資料使用原則的逐步指示，請參閱以下教學課程： [建立和評估資料使用原則](create.md). 如需詳細資訊，請參閱 [!DNL Policy Service] API，請參閱 [原則服務開發人員指南](../api/getting-started.md).

有關如何使用中的行銷動作和原則的資訊 [!DNL Platform] UI，請參閱 [資料使用原則使用手冊](./user-guide.md).

## 后续步骤

本檔案介紹了資料控管框架中的資料使用原則。 您現在可以繼續閱讀本指南中連結的流程檔案，以進一步瞭解如何在API和UI中使用原則。

## 附录

下節提供有關資料使用原則的其他資訊。

### Adobe定義的行銷動作 {#core-actions}

下表說明可透過Adobe立即使用的核心行銷動作。

>[!NOTE]
>
>應將核心行銷動作視為起點，協助您識別要建立和檢查違規的使用原則。 定義和其解譯方式取決於貴組織的需求和原則。

| 行銷動作 | 描述 |
| --- | --- |
| Analytics | 此動作會將資料用於分析目的，例如衡量、分析和報告客戶對您組織的網站或應用程式的使用情況。 |
| 與可直接識別的資料結合 | 此動作會將任何個人識別資訊(PII)與匿名資料結合。 來自廣告網路、廣告伺服器和協力廠商資料提供者的資料合約通常包含明確的合約禁令，禁止將此類資料與可直接識別的資料一起使用。 |
| 跨網站目標定位 | 此動作會將資料用於跨網站廣告目標定位。 來自多個網站的資料組合（包括站上資料和站外資料的組合，或來自多個站外來源的資料組合）稱為跨網站資料。 通常會收集和處理跨網站資料，以推斷使用者的興趣。 |
| 数据科学 | 此動作會將資料用於資料科學工作流程。 有些合約包含明確禁令，禁止將資料用於資料科學。 有時候，這些措辭會禁止將資料用於人工智慧(AI)、機器學習(ML)或模型。 |
| 電子郵件目標定位 | 此動作會將資料用於電子郵件目標定位行銷活動。 |
| 匯出至第三方 | 此動作會將資料匯出至與客戶沒有直接關係的處理器和實體。 許多資料提供者在合約中都有條款，禁止從最初收集資料的地方匯出資料。 例如，社交網路合約通常會限制您從合約中接收的資料傳輸。 |
| 站上廣告 | 此動作會將資料用於站內廣告，包括在您組織的網站或應用程式上選擇和投放廣告，或衡量此類廣告的投放和有效性。 |
| 站上個人化 | 此動作會將資料用於站上內容個人化。 網站上的個人化是用於推斷使用者興趣的任何資料，並用於根據這些推斷選擇提供哪些內容或廣告。 |
| 區段比對 | 此動作會將資料用於Adobe Experience Platform區段比對，允許兩個或更多Platform使用者交換區段資料。 透過啟用參考此動作的原則，您可以限制用於區段比對的資料。 例如，如果啟用核心原則「限制資料共用」，則任何資料具有 [C11標籤](../labels/reference.md#c11) 無法用於區段比對。 |
| 單一身分個人化 | 此動作會要求將單一身分用於個人化目的，而非拼接來自多個來源的身分。 |
