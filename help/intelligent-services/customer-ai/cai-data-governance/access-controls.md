---
keywords: Experience Platform；使用手冊；customer ai；熱門主題；存取控制；建立模型；
solution: Experience Platform
feature: Customer AI
title: Customer AI的存取控制
description: 本檔案提供Customer AI的屬性型存取控制相關資訊。
exl-id: 02e3b6a4-304a-4ac4-b07c-010531101feb
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# 基于属性的访问控制

>[!IMPORTANT]
>
>以屬性為基礎的存取控制目前僅在有限版本中可用。

[以屬性為基礎的存取控制](../../../access-control/abac/overview.md) 是Adobe Experience Platform的一項功能，可讓管理員根據屬性控制特定物件和/或權能的存取權。 屬性可以是新增至物件的中繼資料，例如新增至結構描述欄位或區段的標籤。 管理員定義包含管理使用者存取許可權的屬性的存取原則。

此功能可讓您使用定義組織或資料使用範圍的標籤來標籤Experience Data Model (XDM)結構描述欄位。 同時，管理員可以使用使用者和角色管理介面來定義圍繞XDM結構描述欄位的存取原則，並更好地管理授予使用者或使用者群組（內部、外部或第三方使用者）的存取權。 此外，屬性型存取控制可讓管理員管理特定區段的存取權。

透過屬性型存取控制，貴組織的管理員可控制使用者對所有Platform工作流程和資源的敏感個人資料(SPD)和個人識別資訊(PII)的存取權。 管理員可以定義僅能存取特定欄位的使用者角色，以及對應至這些欄位的資料。

由於屬性型存取控制，某些欄位和功能會有存取限制，不適用於某些Customer AI服務模型。 範例包括「身分」、「評分定義」和「原地複製」。

![Customer AI工作區中反白了服務模型結果的受限制欄位。](../images/user-guide/unavailable-functionalities.png)

在Customer AI工作區頂端 **深入分析頁面**，請注意，側欄、分數定義、身分和設定檔屬性中的詳細資訊都顯示「存取受限」。

![反白顯示結構描述受限制欄位的Customer AI工作區。](../images/user-guide/access-restricted.png)

當您在「 」上預覽包含受限結構描述的資料集時 **[!UICONTROL 建立模型工作流程]** 頁面，會出現警告以告知您 [!UICONTROL 由於存取限制，某些資訊不會顯示在資料集預覽中。]

![Customer AI工作區，其預覽資料集的限制欄位中反白顯示限制的結構描述結果。](../images/user-guide/restricted-dataset-preview-save-and-exit-cai.png)

建立包含限制資訊的模型後，請繼續前往 **[!UICONTROL 定義目標]** 步驟，頂端會顯示警告： [!UICONTROL 由於存取限制，某些資訊不會顯示在設定中。]

![Customer AI工作區中反白了服務模型結果的受限制欄位。](../images/user-guide/information-not-displayed-save-and-exit.png)

使用存取控制時， **檢視Customer AI** 和 **管理Customer AI** 許可權可授予對Customer AI不同功能的存取權。 此 **管理Customer AI** 許可權可讓您 **建立**，**更新**， **刪除**， **啟用**，或 **disable** 模型，當 **檢視Customer AI** 可讓您閱讀或檢視。 此 **建立**， **更新** 和 **刪除** 動作由稽核記錄檔記錄。

請參閱檔案以瞭解 [指派存取控制的許可權](../../../access-control/home.md) 或如何 [使用稽核記錄來監視存取和活動](../../../landing/governance-privacy-security/audit-logs/overview.md).

## 后续步骤

閱讀本指南後，您已經瞭解中存取控制的主要原則 [!DNL Experience Platform]. 您現在可以繼續前往 [存取控制使用手冊](../overview.md) 以取得有關如何使用 [!DNL Admin Console] 若要建立產品設定檔並指派許可權 [!DNL Platform].
