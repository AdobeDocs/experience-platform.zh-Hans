---
description: Adobe Experience Platform Destination SDK是一組設定API，可讓您根據您選擇的資料和驗證格式，設定Experience Platform的目的地整合模式，以將受眾和設定檔資料傳送至您的端點或儲存位置。 設定儲存在Experience Platform中，並可透過API擷取以取得其他更新。
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 4%

---

# Adobe Experience Platform Destination SDK

Adobe Experience Platform Destination SDK是一套設定API，可讓您根據您選擇的資料和驗證格式，設定Experience Platform的目的地整合模式，以將受眾和設定檔資料傳送至您的端點或儲存位置。 設定儲存在Experience Platform中，並可透過API擷取以取得其他更新。

Destination SDK檔案會提供指示，讓您使用Adobe Experience Platform Destination SDK來設定、測試和發行與Adobe Experience Platform的已生產目的地整合，並讓您的目的地成為不斷成長的目的地目錄的一部分。 使用Destination SDK，您也可以建立自己的自訂私人目的地，以匯出符合您需求的資料。

![Experience PlatformUI的熒幕擷圖，顯示目的地目錄](assets/destinations-catalog-overview.png)

## 產品化和自訂整合 {#productized-custom-integrations}

>[!IMPORTANT]
>
> 建立私人自訂目的地的此功能僅適用於 [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 客戶。

作為Destination SDK合作夥伴，您可以將已生產化的目的地新增至 [Experience Platform目錄](../catalog/overview.md)：

1. 透過預先設定的引數標準化跨客戶的整合設定，並簡化客戶的設定體驗。
2. 在Experience Platform目的地目錄中推出品牌目的地卡，以簡化客戶設定和認知度。
3. 精選並與Adobe Experience Platform和Adobe Real-time Customer Data Platform整合為產品化的目的地。

身為Experience Platform客戶，您也可以撰寫自己的私人自訂目的地，以最符合您的啟用需求。

![總覽圖表顯示目的地開發人員如何與Destination SDK互動，以及Real-Time CDP客戶如何從生產化和私有目的地獲益。](assets/destination-sdk-visual.png)

## 支援的整合型別 {#supported-integration-types}

### 即時（串流）整合 {#real-time-integrations}

透過Destination SDK，Adobe Experience Platform支援與具有REST API端點的目的地即時整合（也稱為串流）。 與Experience Platform的即時整合支援下列功能：

* 訊息轉換和彙總
* 設定檔回填
* 可設定的中繼資料整合，可初始化對象設定和資料傳輸
* 可設定的驗證
* 一套測試和驗證API，可供您測試和迭代目的地設定

### 檔案式整合 {#file-based-integrations}

透過Destination SDK，您也可以設定整合，以定期將檔案匯出至您選擇的儲存位置。 與Experience Platform的檔案式整合支援如下的功能：

* 檔案匯出採用數個支援的格式(CSV、Parquet、JSON)
* 可設定的檔案格式選項，可讓您根據下游需求來建構轉存檔案的格式。

請閱讀中目標端的技術需求 [整合必要條件](integration-prerequisites.md) 文章並閱讀中所有支援的設定 [設定選項](functionality/configuration-options.md) 文章

## 取得Destination SDK的存取權 {#get-access}

Destination SDK存取權會因您身為合作夥伴或Experience Platform、Real-Time CDP客戶的身份而異。 如需詳細資訊，請參閱下表。

| 合作夥伴或客戶的型別 | 如何存取Destination SDK |
---------|----------|
| 獨立軟體廠商(ISV) | 加入 [Adobe技術合作夥伴計畫](https://partners.adobe.com/technologyprogram/experiencecloud.html) 並要求布建Experience Platform沙箱以存取Destination SDK。 |
| 系統整合商(SI) | 您需要在 [Adobe解決方案合作夥伴計畫](https://solutionpartners.adobe.com/home.html)，您就會布建Experience Platform沙箱，並存取Destination SDK。 |
| Experience Platform客戶於 [Real-Time CDP Ultimate套件](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | 依預設，您可以存取Experience Platform沙箱和Destination SDK，讓您為組織建立私人目的地。 |

{style="table-layout:auto"}

## 高階流程 {#process}

以Experience Platform設定目的地的程式概述如下：

1. 如果您是ISV或SI，請參閱 [取得存取權](#get-access) 一節中的資訊。 [Real-Time CDP Ultimate套件](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 客戶可跳過此步驟。
2. [布建Experience Platform沙箱的要求](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) 並啟用目的地編寫許可權。
3. 建置您的整合。 依照產品檔案中的指示進行設定 [串流目的地](guides/configure-destination-instructions.md) 或 [檔案型目的地](guides/configure-file-based-destination-instructions.md).
4. 測試您的整合。 依照產品檔案中的指示進行測試 [串流目的地](testing-api/streaming-destinations/streaming-destination-testing-overview.md) 或 [檔案型目的地](testing-api/batch-destinations/file-based-destination-testing-overview.md).
5. 如果您是ISV或SI，請建立 [產品化整合](./overview.md#productized-custom-integrations)， [提交您的整合](guides/submit-destination.md) 供Adobe檢閱（標準回應時間為5個工作日）。
6. 如果您是建立產品化整合的ISV或SI，請使用 [自助服務檔案程式](docs-framework/documentation-instructions.md) 以建立有關目的地Experience League的產品檔案頁面。
7. 對於產品化整合，一經Adobe核准，您的整合會顯示在 [Experience Platform目錄](../catalog/overview.md).
8. 如果您想要更新整合，請遵循相同程式。

## 参考 {#reference}

Adobe建議您閱讀並瞭解下列Experience Platform檔案：

* [Adobe Experience Platform目的地概觀](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [XDM結構描述組成的基礎](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=zh-Hans)
* [身分名稱空間總覽](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=zh-Hans)
