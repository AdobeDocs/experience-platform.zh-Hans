---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；ExperienceEvent；欄位；結構；結構描述；結構描述設計；欄位群組；欄位群組；預訂；航班；
title: 航班預訂結構描述欄位群組
description: 本檔案提供航班預訂結構描述欄位群組的概觀。
exl-id: df4bb525-c2d3-4e1d-921f-903142a570ac
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 4%

---

# [!UICONTROL 航班預訂] 結構描述欄位群組

[!UICONTROL 航班預訂] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md) 用於擷取有關航班預訂的資訊。

欄位群組是 [!UICONTROL 預訂詳細資料] 欄位群組，並在單一物件型別欄位下包含所有相同的欄位， `reservations`. 除了這些通用欄位外， [!UICONTROL 航班預訂] 也包含 `flightReservations` 陣列。 這個物件陣列用來描述一個或多個訂位，其屬性是航空旅行所獨有的。

>[!NOTE]
>
>本檔案涵蓋以下專案的詳細資訊： `flightReservations` 陣列。 如需底下其他欄位的詳細資訊， `reservations` 物件，請參閱 [[!UICONTROL 預訂詳細資料] 欄位群組參考](./reservation-details.md).

![航班預訂結構](../../images/field-groups/flight-reservation/structure.png)

## `flightReservations`

`flightReservations` 是一個物件陣列，代表航班預訂清單。 舉例來說，如果預訂事件涉及在某個航程上為多個連線航班進行預訂，則這些預訂可列為下的個別物件 `flightReservations` （針對單一事件）。

下提供的每個物件的結構 `flightReservations` 提供如下。

![flightReservations結構](../../images/field-groups/flight-reservation/flightReservations.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `flightCheckIn` | 对象 | 擷取航班簽到的詳細資訊。 物件包含下列屬性：<ul><li>`arrivalAirportCode`：（字串）抵達城市的機場代碼。</li><li>`boardingGroup`：（字串）航空公司特定的登機通知指標。</li><li>`checkInMethod`：（字串）用於簽入的方法，例如計數器、線上、資訊站或自助服務。</li><li>`checkedBags`：（整數）航班託運的行李數。</li><li>`checkedPassengers`：（整數）同一預訂號碼如果有多名乘客，則為航班辦理登機手續的乘客人數。</li><li>`confirmationNumber`：（字串）預訂確認號碼或識別碼。</li><li>`departureAirportCode`：（字串）出發城市的機場代碼。</li><li>`flightNumber`：（字串）預訂航班的航班號碼。</li></ul> |
| `flightStatusSearch` | 对象 | 擷取搜尋航班狀態時傳回的詳細資料。 物件包含下列屬性：<ul><li>`arrivalAirportCode`：（字串）抵達城市的機場代碼。</li><li>`boardingGroup`：（字串）航空公司特定的登機通知指標。</li><li>`departureAirportCode`：（字串）出發城市的機場代碼。</li><li>`departureDate`：（日期時間）預訂航班的出發日期。</li><li>`flightNumber`：（字串）預訂航班的航班號碼。</li><li>`searchCount`：（整數）搜尋預訂航班狀態的次數。</li></ul> |
| `agentID` | 字符串 | 負責預訂的代理商或預訂者（如適用）。 |
| `aircraftID` | 字符串 | 飛機的識別碼。 |
| `aircraftType` | 字符串 | 飛機型別。 |
| `arrivalAirportCode` | 字符串 | 抵達城市的機場代碼。 |
| `arrivalDate` | 日期時間 | 預訂航班的抵達日期。 |
| `cancellation` | 整数 | 此值會在預訂取消時擷取。 |
| `confirmationNumber` | 字符串 | 預訂確認號碼或識別碼。 |
| `created` | 字符串 | 此值會在建立預訂時擷取。 |
| `currencyCode` | 字符串 | 用於進行購買的ISO 4217貨幣代碼。 |
| `departureAirportCode` | 字符串 | 出發城市的機場代碼。 |
| `departureDate` | 日期時間 | 預訂航班的出發日期。 |
| `fareClass` | 字符串 | 所預訂航班的票價等級。 |
| `flightNumber` | 字符串 | 預訂航班的航班號碼。 |
| `length` | 整数 | 預訂的總天數。 |
| `loyaltyID` | 字符串 | 預訂中列出之乘客的熟客或獎勵方案ID。 |
| `modification` | 整数 | 此值會在預訂被修改時擷取。 |
| `modificationDate` | 日期時間 | 上次修改預訂的時間。 |
| `numberOfAdults` | 整数 | 和預訂相關聯的成人數量。 |
| `numberOfChildren` | 整数 | 和預訂相關聯的子項數目。 |
| `passengerID` | 字符串 | 和預訂相關聯的乘客資訊。 |
| `purpose` | 字符串 | 預訂的目的，通常為商業或個人目的。 |
| `salesChannel` | 字符串 | 預訂的銷售管道。 |
| `securityScreening` | 字符串 | 乘客須接受的安全檢查型別。 |
| `status` | 字符串 | 航班預訂的狀態。 |
| `ticketNumber` | 字符串 | 預訂編號或識別碼。 |
| `tripType` | 字符串 | 表示此預訂是單程旅行、往返還是多城市旅行。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.schema.json)
