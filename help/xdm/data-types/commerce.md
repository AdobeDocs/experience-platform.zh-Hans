---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；商務；資料型別；資料型別；
solution: Experience Platform
title: Commerce資料型別
description: 本檔案提供Commerce Experience Data Model (XDM)資料型別的概述。
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# [!UICONTROL 商務] 資料型別

[!UICONTROL 商務] 是標準的體驗資料模型(XDM)資料型別，可描述與購買和銷售活動相關的記錄。

<img src="../images/data-types/commerce.PNG" width="400" /><br />

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `order` | [[!UICONTROL 訂購]](./order.md) | 說明一或多個產品的已下訂單。 |
| `cartAbandons` | [[!UICONTROL 測量]](./measure.md) | 用於說明何時已將產品清單識別為使用者無法再存取或購買。 |
| `checkouts` | [[!UICONTROL 測量]](./measure.md) | 產品清單結帳程式中的動作。 如果結帳程式中有多個步驟，就可能有一個以上的結帳事件。 如果有多個步驟，事件時間資訊和參照的頁面或體驗可用來識別依序表示的步驟和個別事件。 |
| `inStorePurchase` | [[!UICONTROL 測量]](./measure.md) | 說明與店內購買相關聯以供分析使用的值。 |
| `productListAdds` | [[!UICONTROL 測量]](./measure.md) | 將產品新增至產品清單，例如將產品新增至購物車。 |
| `productListOpens` | [[!UICONTROL 測量]](./measure.md) | 新產品清單的初始化，例如正在建立的購物車。 |
| `productListRemovals` | [[!UICONTROL 測量]](./measure.md) | 從產品清單中移除或移除產品專案，例如從購物車移除的產品。 |
| `productListReopens` | [[!UICONTROL 測量]](./measure.md) | 先前已捨棄且已由使用者重新啟動的產品清單。 |
| `productListViews` | [[!UICONTROL 測量]](./measure.md) | 說明何時發生產品清單檢視。 |
| `productViews` | [[!UICONTROL 測量]](./measure.md) | 說明何時已發生個別產品的檢視。 |
| `purchases` | [[!UICONTROL 測量]](./measure.md) | 用於追蹤何時接受訂單。 購買事件是商務轉換中唯一需要的動作。 購買事件必須有參考的產品清單。 |
| `saveForLaters` | [[!UICONTROL 測量]](./measure.md) | 儲存產品清單以供日後使用，例如願望清單。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
