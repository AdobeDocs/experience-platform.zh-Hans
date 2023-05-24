---
keywords: Experience Platform；首頁；熱門主題；資料控管；資料使用標籤api；原則服務api；資料使用標籤總覽
solution: Experience Platform
title: 資料使用標籤概觀
description: 瞭解如何使用資料使用標籤來協助強制執行Adobe Experience Platform中的資料控管合規性。
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: a1628df7d0eefc795d1eaeefce842a65c7133322
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 15%

---

# 数据使用标签概述 {#overview}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_description"
>title="控制访问敏感和受保护的数据"
>abstract="<h2>描述</h2><p>通过控制访问特定的数据属性和/或区段，可为操作 Experience Platform 用例的各种角色和团队设计灵活的工作流。</p>"

Adobe Experience Platform可讓您將資料使用標籤套用至資料集和欄位，並根據相關專案對每個欄位進行分類 [資料治理原則](../policies/overview.md) 和 [存取控制原則](../../access-control/abac/ui/policies.md).

本檔案提供資料使用標籤總覽，位於 [!DNL Experience Platform].

## 瞭解資料使用標籤

資料使用標籤可讓您根據套用至該資料的治理原則來分類資料集和欄位。 標籤可隨時套用，讓您靈活選擇控管資料的方式。 最佳實務建議在資料內嵌至後立即加上標籤 [!DNL Experience Platform]，或在資料可用於以下專案時立即啟用： [!DNL Platform].

套用至資料集層級的資料使用標籤會傳播至資料集內的所有欄位。 標籤也可以直接套用至資料集中的個別欄位（欄標題），而不需傳播。

[!DNL Platform] 提供數種現成的「核心」資料使用標籤，涵蓋適用於資料控管的各種常見限制。 如需這些標籤及其代表的治理原則的詳細資訊，請參閱以下指南： [核心資料使用標籤](reference.md).

除了Adobe提供的標籤之外，您也可以為組織定義自己的自訂標籤。 請參閱以下小節： [管理標籤](#manage-labels) 以取得詳細資訊。

## 對象區段的標籤繼承

建立的所有對象區段 [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) 繼承對應資料集的使用情況標籤。 這可讓Experience Platform在將區段啟用至目的地時，提供自動原則執行。

除了繼承資料集層級標籤之外，根據預設，區段還會從關聯的資料集中繼承所有欄位層級標籤。 因此，您可以更輕鬆地識別應從區段排除的屬性，並防止其從排除的欄位繼承標籤。

如需如何在Platform中自動強制執行的詳細資訊，請參閱以下主題的概觀： [自動原則執行](../enforcement/auto-enforcement.md).

### Adobe Audience Manager資料匯出控制項的繼承

[!DNL Experience Platform] 能夠與Adobe Audience Manager共用區段。 套用至Audience Manager區段的任何資料匯出控制都會轉譯為相等的標籤和行銷動作，可由 [!DNL Experience Platform] 資料控管。

如需瞭解特定資料匯出控制項如何對應至中的資料使用標籤，請參閱 [!DNL Platform]，請參閱 [Audience Manager檔案](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## 管理中的資料使用標籤 [!DNL Experience Platform] {#manage-labels}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_instructions"
>title="说明"
>abstract="<ul><li>为 XDM 字段和区段加标签以划分要限制访问其的字段和/或区段。</li><li>为角色加标签，通过将标签添加到角色，可定义此角色的成员应在其上具有限制的标签。</li><li>创建策略，策略在加了标签的对象（如 XDM 字段和区段）上的标签与角色上的标签之间建立关系。如果标签匹配，则可以定义允许或限制访问。</li></ul>"

您可以使用以下專案管理資料使用標籤 [!DNL Experience Platform] API或使用者介面。 如需各個專案的詳細資訊，請參閱以下各小節。

### 使用UI

此 **[!UICONTROL 原則]** 工作區在 [!DNL Experience Platform] UI可讓您檢視和管理組織的核心和自訂標籤。 您可以使用 **[!UICONTROL 結構描述]** 工作區至 [將標籤套用至您的Experience Data Model (XDM)結構描述](../../xdm/tutorials/labels.md)，或您可以使用 **[!DNL Datasets]** 工作區至 [將標籤套用至資料集](./user-guide.md) 而非。

>[!NOTE]
>
>僅資料控管使用案例支援在資料集層級套用標籤。 如果您嘗試建立資料的存取原則，必須將標籤套用至資料集所根據的結構描述。 請參閱以下文章的概觀： [基於屬性的存取控制](../../access-control/abac/overview.md) 以取得詳細資訊。

### 使用API

此 `/labels` 中的端點 [原則服務API](https://www.adobe.io/experience-platform-apis/references/policy-service/) 可讓您以程式設計方式管理資料使用標籤，包括建立自訂標籤。 請參閱 [標籤端點指南](../api/labels.md) 以取得詳細資訊。

此 [資料集服務API](https://www.adobe.io/experience-platform-apis/references/dataset-service/) 用於管理資料集和欄位的標籤。 請參閱指南： [管理資料集標籤](./dataset-api.md) 以取得詳細資訊。

>[!NOTE]
>
>僅資料控管使用案例支援在資料集層級套用標籤。 如果您嘗試建立資料的存取原則，您必須 [將標籤套用至結構描述](../../xdm/tutorials/labels.md) 資料集所根據的。 請參閱以下文章的概觀： [基於屬性的存取控制](../../access-control/abac/overview.md) 以取得詳細資訊。

## 后续步骤

本檔案介紹了資料使用標籤及其在資料控管框架中的角色。 請參閱本指南中的檔案連結，以進一步瞭解如何在中管理標籤 [!DNL Experience Platform].
