---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；身分；資料型別；資料型別；
solution: Experience Platform
title: 身分資料型別
description: 本檔案提供身分XDM資料型別的概觀。
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 3%

---

# [!UICONTROL 身分] 資料型別

[!UICONTROL 身分] 是標準XDM資料型別，用來明確區分與數位體驗互動的人。 身分由身分提供者建立，其本身會在以下專案中參照： `namespace` 屬性。 在每個 `namespace`，此身分是唯一的。

<img src="../images/data-types/identity.png" width="550" /><br />

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `namespace` | 对象 | 包含單一字串欄位(`code`)，表示與提供的相關聯的名稱空間 `id` 屬性。 |
| `authenticatedState` | 字符串 | 觀察到Experience事件時此身分的驗證狀態。 請參閱 [附錄](#authenticatedState) 以取得接受的值和定義。 |
| `id` | 字符串 | 消費者在相關名稱空間中的身分。 |
| `primary` | 布尔值 | 指出這是否為個人的主要身分。 每個個人只能有一個主要身分。 |
| `xid` | 字符串 | 當出現時，這個值代表跨名稱空間的識別碼，在所有名稱空間中都是唯一，也就是所有名稱空間中的範圍識別碼。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## 附录

以下小節包含更多關於 [!UICONTROL 身分] 資料型別。

## authenticatedState的接受值 {#authenticatedState}

下表概述下列專案的可接受值 `authenticatedState` 及其相關涵義：

| 值 | 描述 |
| --- | --- |
| `ambiguous` | 驗證狀態不明確。 |
| `authenticated` | 透過在事件觀察時有效的登入或類似動作來識別使用者。 |
| `loggedOut` | 在先前某個時間點，使用者已由登入動作識別，但在事件觀察時未登入。 |
