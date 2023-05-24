---
solution: Experience Platform
title: 區段定義類別
description: 本檔案提供Experience Data Model (XDM)中區段定義類別的概觀。
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# [!UICONTROL 區段定義] 類別

&quot;[!UICONTROL 區段定義]「是一個標準的體驗資料模型(XDM)類別，可擷取區段定義的詳細資訊。 類別包含必要欄位（例如區段的ID和名稱）以及其他選用屬性。 如果您要將外部系統的區段定義帶入Adobe Experience Platform，應使用此類別。

>[!NOTE]
>
>此類別只應用於擷取有關區段定義本身的資訊。 若要在設定檔資料中擷取區段會籍資訊，您應使用 [區段會籍詳細資料欄位群組](../field-groups/profile/segmentation.md) 在您的 [!UICONTROL XDM個別設定檔] 結構描述。

![](../images/classes/segment-definition.png)

| 属性 | 描述 |
| --- | --- |
| `_repo` | 包含下列專案的物件 [!UICONTROL 日期時間] 欄位： <ul><li>`createDate`：在資料存放區中建立資源的日期和時間，例如首次擷取資料的時間。</li><li>`modifyDate`：上次修改資源的日期和時間。</li></ul> |
| `_id` | 記錄的唯一、系統產生的字串識別碼。 此欄位用於追蹤個別記錄的唯一性、防止資料重複，以及在下游服務中查詢該記錄。<br><br>由於此欄位是系統產生的，因此在資料擷取期間不會向其提供明確值。 不過，您仍然可以視需要選擇提供自己的唯一ID值。<br><br>請務必區分此欄位 **不會** 代表與個人相關的身分，而不是資料記錄本身。 與個人相關的身分資料應委派至 [身分欄位](../schema/composition.md#identity) 而非。 |
| `createdByBatchID` | 導致建立記錄之擷取批次的ID。 |
| `description` | 區段定義的說明。 |
| `identityMap` | 包含區段套用至之個人的一組名稱空間身分的對映欄位。 請參閱「 」中有關身分對應的章節 [結構描述組合基本概念](../schema/composition.md#identityMap) 以取得其使用案例的詳細資訊。 |
| `modifiedByBatchID` | 導致記錄更新的上次擷取批次的ID。 |
| `repositoryCreatedBy` | 建立記錄的使用者ID。 |
| `repositoryLastModifiedBy` | 上次修改記錄的使用者ID。 |
| `segmentName` | **（必要）** 區段定義的名稱。 |
| `segmentStatus` | 來自外部系統的區段狀態。 接受下列值： <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | 區段定義的最新版本號碼。 |

{style="table-layout:auto"}
