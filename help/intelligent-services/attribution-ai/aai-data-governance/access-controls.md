---
keywords: Experience Platform；首頁；熱門主題；存取控制；adobe admin console
solution: Experience Platform
feature: Attribution AI
title: Attribution AI的存取控制
description: 本檔案提供Attribution AI的屬性型存取控制相關資訊。
exl-id: 3ed672bf-1fa6-4893-99e0-afc2b2179543
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---

# 访问控制

Attribution AIAdobe Experience Platform的存取控制是透過 [Adobe Admin Console](https://adminconsole.adobe.com/). 此功能運用Admin Console中的產品設定檔，將使用者與許可權和沙箱連結。

如需存取控制的詳細資訊，請參閱 [存取控制總覽](../../../access-control/home.md).

## 基于属性的访问控制

>[!IMPORTANT]
>
>以屬性為基礎的存取控制目前僅在有限版本中可用。

[以屬性為基礎的存取控制](../../../access-control/abac/overview.md) 是Adobe Experience Platform的一項功能，可讓管理員根據屬性控制特定物件和/或權能的存取權。 屬性可以是新增至物件的中繼資料，例如新增至結構描述欄位或區段的標籤。 管理員定義包含管理使用者存取許可權的屬性的存取原則。

此功能可讓您使用定義組織或資料使用範圍的標籤來標籤Experience Data Model (XDM)結構描述欄位。 同時，管理員可以使用使用者和角色管理介面來定義圍繞XDM結構描述欄位的存取原則，並更好地管理授予使用者或使用者群組（內部、外部或第三方使用者）的存取權。 此外，屬性型存取控制可讓管理員管理特定區段的存取權。

透過屬性型存取控制，管理員可控制使用者對所有Platform工作流程與資源的敏感個人資料(SPD)和個人識別資訊(PII)的存取權。 管理員可以定義僅能存取特定欄位及對應至這些欄位之資料的使用者角色。

由於屬性型存取控制，某些欄位和功能可能會受到存取限制，並且無法用於某些Attribution AI服務模型。 範例包括「身分」、「評分定義」和「原地複製」。

在Attribution AI工作區頂端 **深入分析頁面**&#x200B;時，側邊欄中顯示的詳細資料具有受限制的存取權。

![反白顯示受限制結構描述欄位的Attribution AI工作區。](../images/user-guide/access-restricted.png)

如果您在「 」上選取包含受限制結構的資料集 **[!UICONTROL 建立模型工作流程]** 頁面，資料集名稱旁會出現警告符號，並出現訊息： [!UICONTROL 已排除受限制的資訊].

![反白顯示受限制資料集欄位的Attribution AI工作區。](../images/user-guide/restricted-info-excluded.png)

當您在「 」上預覽包含受限結構描述的資料集時 **[!UICONTROL 建立模型工作流程]** 頁面，會出現警告以告知您 [!UICONTROL 由於存取限制，某些資訊不會顯示在資料集預覽中。]

![反白顯示受限制預覽結構描述欄位結果的Attribution AI工作區。](../images/user-guide/restricted-dataset-preview.png)

建立包含限制資訊的模型後，請繼續前往 **[!UICONTROL 定義目標]** 步驟，頂端會顯示警告： [!UICONTROL 由於存取限制，某些資訊不會顯示在設定中。]

![反白顯示模型結果之限制欄位的Attribution AI工作區。](../images/user-guide/information-not-displayed-save-and-exit.png)

## 后续步骤

閱讀本指南後，您已經瞭解中存取控制的主要原則 [!DNL Experience Platform]. 您現在可以繼續前往 [存取控制使用手冊](../overview.md) 以取得有關如何使用 [!DNL Admin Console] 若要建立產品設定檔並指派許可權 [!DNL Platform].
