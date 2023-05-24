---
keywords: Experience Platform；首頁；熱門主題；統一標籤；標籤；
title: 統一標籤總覽（測試版）
description: 本檔案提供Adobe Experience Platform中統一標籤的相關資訊
exl-id: a19e37c3-697a-4000-9cb8-d67478b47dc6
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 1%

---

# 統一標籤總覽（測試版）

>[!IMPORTANT]
>
>統一標籤為測試版。 如果您想要留下意見回饋，請選取「標籤管理」頁面頂端的按鈕以提出意見。

標籤是Adobe Experience Platform的一項功能，可讓管理員管理中繼資料分類法，以便分類業務物件，以便於探索和分類。 標籤是中繼資料，可視為可附加至區段、資料集、歷程或其他物件的關鍵字，以啟用搜尋來尋找該物件和相關物件。 標籤分為兩種型別：已分類和未分類。

為了提供更多上下文並定義標籤的目的，類別會將標籤組織成有用的集合。 管理員會定義哪些分類標籤可供使用者新增至物件。 不包含類別的新標籤也可以在套用標籤的工作流程中內聯建立。 這些標籤會顯示在標籤詳細目錄中未分類的部分中。 管理員和使用者均可套用標籤，無論其建立者為何。 指派給物件、搜尋或篩選時，所有型別的標籤都可供選取。

## 標籤術語

標籤涉及下列元件：

| 术语 | 定义 |
| --- | --- |
| 已封存 | 標籤的狀態，會保留目前與物件的關聯，但限制標籤無法套用至其他物件。  封存的標籤會隱藏在標籤選擇器中。 |
| 对象 | 可套用標籤的Experience Cloud專案。  範例：區段、歷程、資料集。 |
| 标记 | 標籤是中繼資料，可視為可附加至區段、資料集、歷程或其他物件的關鍵字，以啟用搜尋來尋找該物件和相關物件。 |
| 標籤類別 | 「標籤類別」會將標籤分組為有意義的集合，以提供更大的內容或說明標籤的用途。  管理員管理標籤類別和類別中的標籤。 |
| 未分類的標籤 | 在套用標籤的位置內嵌建立的新標籤。 這些標籤可由任何使用者建立和套用，但它們未繫結至類別。  管理員可以將這些標籤移動到類別，以便與其他類似標籤保持一致。 |

## 標籤詳細目錄

標籤類別和使用標籤庫存的標籤管理可在Experience Platform和Journey Optimizer導覽中取得。 庫存中標籤變更會反映在所有支援標籤的物件中。 所有使用者都能夠存取和瀏覽標籤詳細目錄，但標籤管理僅限於系統和產品管理員。

標籤詳細目錄有三層階層，可讓使用者管理標籤類別、類別內的標籤及個別標籤。 管理個別標籤時，使用者可以檢視並導覽至目前套用該標籤的任何物件。

### 標籤類別

類別會將標籤分組為有意義的集合，以提供更大的上下文或說明標籤的用途。 在任何具有類別的標籤上，標籤名稱前面都會是類別名稱，後面接著冒號。

使用標籤類別時，可能會執行下列動作：

* [建立標籤類別](./ui/tags-categories.md#create-tag-category)
* [編輯標籤類別](./ui/tags-categories.md#edit-tag-category-edit-tag-category)
* [刪除標籤類別](./ui/tags-categories.md#delete-tag-category-delete-tag-category)

### 管理類別中的標籤

>[!NOTE]
>
>若要管理Experience Cloud的標籤，您必須是貴組織擁有Experience Cloud訂閱的Adobe Experience Platform的系統管理員或產品管理員。

在類別中（或預設的「未分類」群組），您可以建立和管理標籤。 管理標籤時，可能會執行下列動作：

* [创建标记](./ui/managing-tags.md#create-a-tag-create-tag)
* [編輯標籤](./ui/managing-tags.md#edit-a-tag-edit-tag)
* [在類別之間移動標籤](./ui/managing-tags.md#move-a-tag-between-categories-move-tag)
* [封存標籤](./ui/managing-tags.md#archive-a-tag-archive-tag)
* [還原已封存的標籤](./ui/managing-tags.md#restore-an-archived-tag-restore-archived-tag)
* [删除标记](./ui/managing-tags.md#delete-a-tag-delete-tag)
* [檢視標籤的物件](./ui/managing-tags.md#viewing-tagged-objects-view-tagged)
