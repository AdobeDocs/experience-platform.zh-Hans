---
keywords: Experience Platform；首頁；熱門主題；結構描述；結構描述；XDM；ExperienceEvent；欄位；結構描述；結構描述；結構描述設計；欄位群組；欄位群組；預訂；就餐；
title: 餐飲預訂結構描述欄位群組
description: 本檔案提供「餐飲預訂」結構描述欄位群組的概觀。
exl-id: 672b7a77-c433-4502-a1ad-a17c811b253e
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 5%

---

# [!UICONTROL 餐飲預訂] 結構描述欄位群組

[!UICONTROL 餐飲預訂] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md) 用於擷取關於餐飲預訂的資訊。

欄位群組是 [!UICONTROL 預訂詳細資料] 欄位群組，並在單一物件型別欄位下包含所有相同的欄位， `reservations`. 除了這些通用欄位外， [!UICONTROL 餐飲預訂] 也包含 `diningReservations` 陣列。 這個物件陣列可用來說明一或多個保留區與餐廳特定屬性。

>[!NOTE]
>
>本檔案涵蓋以下專案的詳細資訊： `diningReservations` 陣列。 如需底下其他欄位的詳細資訊， `reservations` 物件，請參閱 [[!UICONTROL 預訂詳細資料] 欄位群組參考](./reservation-details.md).

![餐飲預訂結構](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations` 是一個物件陣列，代表一個餐飲預訂清單。 例如，如果預訂事件涉及在一天中的不同時間在多個不同餐廳的預訂，則這些預訂可以列為下的個別物件 `diningReservations` （針對單一事件）。

下提供的每個物件的結構 `diningReservations` 提供如下。

![diningReservations結構](../../images/field-groups/dining-reservation/diningReservations.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `ID` | 字符串 | 預訂編號或識別碼。 |
| `cancellation` | 整数 | 此值會在預訂取消時擷取。 |
| `confirmationNumber` | 字符串 | 預訂確認號碼或識別碼。 |
| `created` | 整数 | 此值會在建立預訂時擷取。 |
| `cuisine` | 整数 | 餐廳菜餚的型別。 |
| `currencyCode` | 字符串 | 用於進行購買的ISO 4217貨幣代碼。 |
| `deliveryPartners` | 字符串 | 餐廳提供的送餐合作夥伴。 |
| `diningOptions` | 字符串 | 餐廳提供外賣和餐飲選擇。 |
| `groupReservation` | 布尔值 | 指出是否為群組進行預訂。 |
| `length` | 整数 | 預訂的總天數。 |
| `loyaltyID` | 字符串 | 預訂中列出的賓客的熟客方案ID。 |
| `modification` | 整数 | 此值會在預訂被修改時擷取。 |
| `modificationDate` | 日期時間 | 上次修改預訂的時間。 |
| `numberOfAdults` | 整数 | 和預訂相關聯的成人數量。 |
| `numberOfChildren` | 整数 | 和預訂相關聯的子項數目。 |
| `numberOfRooms` | 整数 | 和預訂相關聯的房間數。 |
| `partySize` | 整数 | 宴會中的人數。 |
| `priceCategory` | 字符串 | 進行預訂的價格類別。 |
| `purpose` | 字符串 | 預訂的目的，通常為商業或個人目的。 |
| `reservationTime` | 日期時間 | 餐飲預訂的時間。 |
| `restaurantID` | 字符串 | 餐廳或就餐位置的識別碼。 |
| `reservationStatus` | 字符串 | 預訂的狀態。 |
| `specialOccasion` | 布尔值 | 表示此預訂是否為特別場合所做。 |
| `status` | 整数 | 餐飲預訂的狀態。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.schema.json)
