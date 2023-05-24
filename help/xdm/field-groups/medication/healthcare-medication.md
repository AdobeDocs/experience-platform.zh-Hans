---
title: 醫療保健結構描述欄位群組
description: 本檔案提供Healthcare Media方案欄位群組的概觀。
exl-id: 3423d067-fe8c-44e5-a6f9-ce0458d26ebc
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 5%

---

# [!UICONTROL 醫療保健] 結構描述欄位群組

[!UICONTROL 醫療保健] 是的標準結構描述欄位群組 [[!UICONTROL 藥物] 類別](../../classes/medication.md). 它提供單一物件型別欄位 `medication` 擷取品牌名稱、批號及數量等細節。

![](../../images/field-groups/healthcare-medication.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `ingredients` | 物件陣列 | 列出藥物中的成分。 每個物件包含下列屬性： <ul><li>`isActive`：（布林值）指出此成份是否仍用於此藥物中。</li><li>`name`：（字串）成份的名稱。</li><li>`quantity`：（字串）藥物中存在的配料數量。</li></ul> |
| `brandName` | 字符串 | 藥物的品牌名稱。 |
| `codes` | 字串陣列 | 可識別此藥物的程式碼清單。 |
| `dosageUnitNumber` | 双精度 | 適用於藥物的劑量單位編號。 |
| `dosageUnitOfMeasurement` | 字符串 | 劑量數的測量單位。 |
| `expiryDate` | 日期時間 | 藥物有效期。 |
| `genericName` | 字符串 | 藥物的通用名稱。 |
| `lotNumber` | 字符串 | 藥物批次的唯一識別碼。 |
| `manufacturerName` | 字符串 | 製藥商名稱。 |
| `quantity` | 双精度 | 包裝中的藥物量。 |
| `status` | 字符串 | 表示藥物/藥物是否有效的一般狀態。 |
| `volume` | 双精度 | 藥物的量。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json).
