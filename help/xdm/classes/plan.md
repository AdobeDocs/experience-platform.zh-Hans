---
title: 計畫類別
description: 本檔案提供Experience Data Model (XDM)中Plan類別的概觀。
exl-id: ccff962d-3104-482c-8d65-d2bd2602a9be
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 3%

---

# [!UICONTROL 計畫] 類別

在Experience Data Model (XDM)中， [!UICONTROL 計畫] class會擷取定義計畫的最小屬性集，例如健康計畫或保險計畫。

![類別結構](../images/classes/plan.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `_id` | [!UICONTROL 字符串] | 記錄的唯一、系統產生的字串識別碼。 此欄位用於追蹤個別記錄的唯一性、防止資料重複，以及在下游服務中查詢該記錄。<br><br>由於此欄位是系統產生的，因此在資料擷取期間不會向其提供明確值。 不過，您仍然可以視需要選擇提供自己的唯一ID值。 |
| `planId` | [!UICONTROL 字符串] | 計畫的唯一識別碼。 |
| `planName` | [!UICONTROL 字符串] | 計畫的名稱。 |

{style="table-layout:auto"}

可以使用來擴充類別 [[!UICONTROL 醫療保健計畫詳細資料] 欄位群組](../field-groups/plan/healthcare-plan-details.md) 說明健康保險計畫的詳細資訊。
