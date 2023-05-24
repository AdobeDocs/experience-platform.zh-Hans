---
keywords: Experience Platform；首頁；熱門主題；綱要；綱要；XDM；ExperienceEvent；欄位；綱要；綱要；綱要設計；欄位群組；欄位群組；
solution: Experience Platform
title: 商務詳細資料結構描述欄位群組
description: 本檔案提供Commerce Details結構欄位群組的概觀。
exl-id: 36aba186-fadb-4abb-a94f-7e151ff3f744
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 1%

---

# [!UICONTROL 商務詳細資料] 結構描述欄位群組

>[!NOTE]
>
>數個結構描述欄位群組的名稱已變更。 檢視檔案： [欄位群組名稱更新](../name-updates.md) 以取得詳細資訊。

[!UICONTROL 商務詳細資料] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md)，用於描述商業資料，例如產品資訊（SKU、名稱、數量）和標準購物車操作（訂單、結帳、放棄）。

![](../../images/field-groups/commerce-details.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `commerce` | [Commerce](../../data-types/commerce.md) | 說明產品退貨、保固註冊及購物車/訂單流程的物件。 |
| `productListItems` | 陣列 [產品清單專案](../../data-types/product-list-item.md) | 代表客戶所選產品的專案清單，具有特定選項和在特定時間點的定價（這可能與產品記錄不同）。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json)
