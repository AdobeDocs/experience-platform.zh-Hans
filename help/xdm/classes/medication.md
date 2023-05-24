---
title: 藥物類別
description: 本檔案提供Experience Data Model (XDM)中Media類別的概觀。
exl-id: e5786241-dd6e-450f-98c8-2de46affb3e2
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 3%

---

# [!UICONTROL 藥物] 類別

在Experience Data Model (XDM)中， [!UICONTROL 藥物] class會擷取定義用於醫療的物質（尤其是藥物或藥物）的最小屬性集。

![類別結構](../images/classes/medication.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `_id` | [!UICONTROL 字符串] | 記錄的唯一、系統產生的字串識別碼。 此欄位用於追蹤個別記錄的唯一性、防止資料重複，以及在下游服務中查詢該記錄。<br><br>由於此欄位是系統產生的，因此在資料擷取期間不會向其提供明確值。 不過，您仍然可以視需要選擇提供自己的唯一ID值。 |
| `medicationId` | [!UICONTROL 字符串] | 適用於藥物的唯一識別碼。 |
| `medicationName` | [!UICONTROL 字符串] | 藥物名稱。 |

{style="table-layout:auto"}

可以使用來擴充類別 [[!UICONTROL 醫療保健] 欄位群組](../field-groups/medication/healthcare-medication.md) 以進一步說明藥物或藥物的詳細資訊。
