---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；資料模型；ui；工作區；關係；欄位；
solution: Experience Platform
title: 在UI中定義關係欄位
description: 瞭解如何在Experience Platform使用者介面中定義關係欄位。
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# 在UI中定義關係欄位

在Experience Data Model (XDM)中， [聯合結構描述](../../schema/composition.md#union) 是屬於已啟用的相同類別之所有結構描述的統一檢視 [即時客戶個人檔案](../../../profile/home.md). 設定檔會運用聯合結構描述，以從不同的體驗資料中建構客戶的完整表示法。

在某些情況下，您擷取的資料不一定是設定檔的一部分，但依然與設定檔相關。 這類資料的範例是客戶的「最喜愛的飯店」欄位。 由於個人最喜愛的飯店屬性不是個人本身的屬性，因此飯店最適合根據自訂類別以個別結構描述，而不是 [!DNL XDM Individual Profile].

由於聯合結構描述僅以共用相同類別的結構描述為基礎，僅啟用「飯店」結構描述以用於設定檔中將不會包含其欄位聯合結構描述 [!DNL XDM Individual Profile]. 而是必須定義「飯店」和屬於聯合的其他結構描述之間的關係。 這涉及定義 **關係欄位** 在參考參考結構描述的主要身分的來源結構描述中。

如需在Adobe Experience Platform UI中定義兩個結構描述之間關係的詳細步驟，請參閱 [關係UI教學課程](../../tutorials/relationship-ui.md).
