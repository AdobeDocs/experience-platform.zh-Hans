---
keywords: Experience Platform；首頁；熱門主題；目標對應；目標對應
solution: Experience Platform
title: 將Adobe Target事件資料對應至XDM
description: 瞭解如何將Adobe Target事件欄位對應到體驗資料模型(XDM)結構描述，以便在Adobe Experience Platform中使用。
exl-id: dab08ab6-6c1c-460a-bb52-8dcdb5709a34
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# 目標對應欄位對應

Adobe Experience Platform可讓您透過Target來源聯結器內嵌Adobe Target資料。 使用聯結器時，必須將Target欄位中的所有資料對應至 [體驗資料模型(XDM)](../../../../xdm/home.md) 與XDM ExperienceEvent類別相關聯的欄位。

下表概述體驗事件結構描述的欄位(*xdm ExperienceEvent欄位*)以及它們應該對應的對應Target欄位(*Target請求欄位*)。 此外，也提供部分對應的其他附註。

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| xdm ExperienceEvent欄位 | Target請求欄位 | 注释 |
| ------------------------- | -------------------- | ----- |
| **`id`** | 唯一請求識別碼 |
| **`dataSource`** |  | 已設定為所有使用者端的「1」。 |
| `dataSource._id` | 系統產生的值，無法與要求一併傳入。 | 此資料來源的唯一識別碼。 這將由建立資料來源的個人或系統提供。 |
| `dataSource.code` | 系統產生的值，無法與要求一併傳入。 | 完整@id的捷徑。 至少可以使用其中一個程式碼或@id。 有時候，此程式碼會稱為資料來源整合程式碼。 |
| `dataSource.tags` | 系統產生的值，無法與要求一併傳入。 | 標籤可用來指出應用程式應如何使用這些別名來解譯指定資料來源所代表的別名。<br><br>示例：<br><ul><li>`isAVID`：代表Analytics訪客ID的資料來源。</li><li>`isCRSKey`：代表應在CRS中作為索引鍵使用的別名的資料來源。</li></ul>標籤會在建立資料來源時設定，但也會在參照特定資料來源時納入管道訊息中。 |
| **`timestamp`** | 事件時間戳記 |
| **`channel`** | `context.channel` | 僅適用於檢視傳遞。 選項為「Web」和「mobile」，預設值為「Web」。 |
| **`endUserIds`** |
| `endUserIds.experience.tntId` | `tntId/mboxPC` |
| `endUserIds.experience.mcId` | `marketingCloudVisitorId` | Experience CloudID (ECID)也稱為MCID，並將繼續用於名稱空間。 |
| **`environment`** |
| `environment.browserDetails.userAgent` | `mboxRequest.userAgent` |
| `environment.browserDetails.viewPortHeight` | `mboxRequest.browserHeight` |
| `environment.browserDetails.viewPortWidth` | `mboxRequest.browserWidth` |
| `environment.operatingSystem` | `deviceAtlas.osName` |
| `environment.operatingSystemVersion` | `deviceAtlas.osVersion` |
| `environment.viewportHeight` | `mboxRequest.screenHeight` |
| `environment.viewportWidth` | `mboxRequest.screenWidth` |
| `environment.colorDepth` | `mboxRequest.colorDepth` |
| `environment.carrier` | 根據請求的IP位址解析的行動電信業者名稱。 |
| `environment.ipV4` | `mboxRequest.ipAddress` （若為V4格式） |
| `environment.ipV6` | `mboxRequest.ipAddress` （若為V6格式） |
| **`experience`** |
| `experience.target.clientCode` | `mboxRequest.client` |
| `experience.target.mboxName` | `mboxRequest.mboxName` |
| `experience.target.mboxVersion` | `mboxRequest.mboxVersion` |
| `experience.target.sessionId` | `mboxRequest.sessionId` |
| `experience.target.environmentID` | 適用於客戶定義環境（例如開發、qa或生產環境）的Target內部對應。 |
| `experience.target.supplementalDataID` | 用於將Target事件與Analytics事件拼接的識別碼 |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` | 訪客已符合資格的活動清單（陣列） |
| `experience.target.activities[i].activityID` | 訪客符合資格的任何給定活動的ID |
| `experience.target.activities[i].version` | 訪客符合資格的任何給定活動的版本 |
| `experience.target.activities[i].activityEvents` | 包含使用者透過此事件點選的活動事件的詳細資料。 |
| **`device`** |
| `device.typeIDService` | `XDMDevice.Device.TypeIDService.typeIDService_deviceatlas` |
| `device.type` | 下列屬性之一 `deviceAtlas` （或NULL）： <ul><li>`type_mobile`</li><li>`type_tablet`</li><li>`type_desktop`</li><li>`type_ereader`</li><li>`type_television`</li><li>`type_settop`</li><li>`type_mediaplayer`</li></ul> |
| `device.typeID` | （空字串） |
| `device.manufacturer` | `deviceAtlas.manufacturer` |
| `device.model` | `deviceAtlas.model` |
| `device.modelNumber` | （空字串） |
| `device.screenHeight` | `deviceAtlas.displayHeight` |
| `device.screenWidth` | `deviceAtlas.displayWidth` |
| `device.colorDepth` | `deviceAtlas.displayColorDepth` |
| **`placeContext`** |
| `placeContext.geo.id` | 隨機UUID （必要） |
| `placeContext.geo.city` | 根據請求的IP位址解析的城市名稱。 |
| `placeContext.geo.countryCode` | 根據請求的IP位址解析的國家代碼。 |
| `placeContext.geo.dmaId` | 根據請求的IP位址解析指定的市場區碼。 |
| `placeContext.geo.postalCode` | 根據請求的IP位址解析的郵遞區號。 |
| `placeContext.geo.stateProvince` | 根據請求的IP位址解決的州或省。 |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** |  | 只有在請求中存在訂單詳細資料時才會設定。 |
| `commerce.order.priceTotal` | `mboxRequest.orderTotal` |
| `commerce.order.purchaseOrderNumber` | `mboxRequest.orderId` |
| `commerce.order.purchaseID` | `mboxRequest.orderId` |
| **`web`** |
| `web.withWebPageDetails.url` | `mboxURL.context.address.url` |
| `web.webReferrer.url` | `mboxReferrer.context.address.url` |
| **`identityMap`** |
| `identityMap.TNTID` | `tntId.mboxPC` |
| `identityMap.ECID` | `marketingCloudVisitorId` |

{style="table-layout:auto"}
