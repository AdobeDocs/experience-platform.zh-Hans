---
keywords: Experience Platform；首頁；熱門主題；結構描述；結構描述；XDM；ExperienceEvent；欄位；結構描述；結構描述；結構描述設計；欄位群組；欄位群組；預訂；預訂詳細資料；
title: 預訂詳細資料結構描述欄位群組
description: 本檔案提供「預訂詳細資料」結構描述欄位群組的概觀。
exl-id: 06f9ee37-9879-4db2-af68-9336366f7521
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 4%

---

# [!UICONTROL 預訂詳細資料] 結構描述欄位群組

[!UICONTROL 預訂詳細資料] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md) 用於擷取預訂的相關資訊，包括長度、修改、可退款狀態和房間數。

欄位群組提供單一物件型別欄位， `reservations`. 此物件中包含的屬性說明如下。

![預訂詳細資料結構](../../images/field-groups/reservation-details.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `nonRefundableAmount` | [货币](../../data-types/currency.md) | 預訂價格的金額（已標籤為不可退款）。 |
| `transaction` | [交易](../../data-types/transaction.md) | 說明預訂的貨幣交易。 |
| `id` | 字符串 | 預訂的唯一識別碼。 |
| `cancellation` | 整数 | 此值會在預訂取消時擷取。 |
| `confirmationNumber` | 字符串 | 預訂的確認號碼或識別碼。 |
| `created` | 整数 | 此值會在建立預訂時擷取。 |
| `currencyCode` | 字符串 | 用於進行購買的ISO 4217貨幣代碼。 |
| `endDate` | 日期時間 | 預訂的交車、還車或結帳結束日期。 |
| `length` | 整数 | 預訂的總天數。 |
| `modification` | 整数 | 此值會在預訂被修改時擷取。 |
| `modificationDate` | 日期時間 | 上次修改預訂的時間。 |
| `numberOfAdults` | 整数 | 和預訂相關聯的成人數量。 |
| `numberOfChildren` | 整数 | 和預訂相關聯的子項數目。 |
| `purpose` | 字符串 | 預訂的目的，通常為商業或個人目的。 |
| `startDate` | 日期時間 | 預訂的開始接送、出埠或簽到日期。 |
| `triptype` | 字符串 | 表示此預訂是單程旅行、往返還是多城市旅行。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.schema.json)

## 特定產業的預訂欄位群組

有其他幾個標準欄位群組可擴充 [!UICONTROL 預訂詳細資料] 適用於產業特定使用案例的結構描述。 如需更多詳細資訊，請參閱下列檔案：

* [[!UICONTROL 餐飲預訂]](./dining-reservation.md)
* [[!UICONTROL 航班預訂]](./flight-reservation.md)
* [[!UICONTROL 住宿預訂]](./lodging-reservation.md)
