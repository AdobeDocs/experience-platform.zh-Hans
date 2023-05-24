---
title: 查詢服務套件
description: 以下檔案概述可用於查詢服務的功能和產品套件，並著重說明隨機查詢和批次查詢之間的差異。
exl-id: ba472d9e-afe6-423d-9abd-13ecea43f04f
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 3%

---

# 查詢服務套件

本檔案概述查詢服務中可用的不同型別的封裝和查詢執行功能。

根據可以執行的查詢模式，Adobe Experience Platform Query Service可以分為兩種功能：

- **臨時查詢** 是用於探索用於驗證、驗證、實驗等擷取資料集的SQL查詢。 這些查詢不會將資料寫回Platform Data Lake。
- **批次查詢** 是用於執行擷取資料集的擷取後處理的SQL查詢。 這些查詢會清除、塑形、操控及擴充資料，而結果會回寫至Platform Data Lake。 這些查詢可作為批次作業進行排程、管理和監視。

查詢服務功能會與下列產品和附加元件一起封裝：

- **平台式應用程式** (Adobe Real-time Customer Data Platform、Adobe Customer Journey Analytics和Adobe Journey Optimizer)：查詢服務執行隨選查詢的存取權，從一開始就有提供平台型應用程式的每個變數和階層。
- **[!DNL Data Distiller]** (可與Adobe Real-Time CDP、Customer Journey Analytics和Adobe Journey Optimizer一起購買的附加元件套件)：提供執行批次查詢的查詢服務存取權 [!DNL Data Distiller].

下表根據封裝方式概述主要查詢服務權益：

| 查詢服務權益 | 與平台型應用程式封裝 | 已封裝 [!DNL Data Distiller] |
|---|---|---|
| 支援的查詢模式 | 僅限特定查詢 | 批次查詢 |
| 支援的使用案例 | <ul><li>探索&#x200B;</li><li>資料探索&#x200B;</li><li>資料驗證</li><li>實驗</li></ul> | <ul><li>清理</li><li>Shaping</li><li>操控</li><li>豐富</li></ul> |
| 支援的語意 | <ul><li>選取查詢</li></ul> | <ul><li>CTAS和ITAS查詢</li></ul> |
| 最長執行時間 | 10 分钟 | 24 小时 |
| 授權量度 | **查詢使用者並行**： <ul><li>1位同時使用者(Real-Time CDP、Adobe Journey Optimizer&#x200B;)</li><li>5個同時使用者(Customer Journey Analytics)&#x200B;</li></ul> **查詢並行**： <ul><li>1個並行執行查詢(所有應用程式&#x200B;)</li></ul> **其他Ad Hoc Query使用者套件附加元件** 可購買以增加客戶的授權特定查詢權益。 <ul><li>每包+5個額外的同時使用者</li><li>每個套件增加1個額外的並行執行查詢</li></ul> | **計算時數**： <ul><li>變數（根據客戶的應用程式許可權設定範圍）</li></ul> **計算時數** 是當執行批次查詢時，查詢服務引擎讀取、處理資料以及將資料寫入資料湖所花費的時間量度。 |
| 查詢執行介面 | <ul><li>查詢服務UI</li><li>協力廠商使用者端UI</li><li>[!DNL PostgresSQL] 使用者端UI</li></ul> | <ul><li>查詢UI </li><li>協力廠商使用者端UI</li><li>[!DNL PostgresSQL] 使用者端UI</li><li>REST API</li></ul> |
| 透過傳回的查詢結果 | 使用者端UI | 衍生資料集儲存在Data Lake中 |
| 結果限制 | <ul><li>查詢UI - 100列</li><li>協力廠商使用者端 — 50,000</li><li>[!DNL PostgresSQL] 使用者端 — 50,000</li></ul> | <ul><li>查詢UI （沒有列數上限）</li><li>協力廠商使用者端（列數沒有上限）</li><li>[!DNL PostgresSQL] 使用者端（列數沒有上限）</li><li>REST API （列數沒有上限）</li></ul> |
| 讀取資料集容量 | 是 | 是 |
| 寫入資料集容量 | 否 | 是 |
| 排程容量 | 否 | 是 |
| 監控容量 | 是 | 是 |
| 查詢警示設定容量 | 否 | 是 |

{style="table-layout:auto"}

## 访问控制

Experience Platform的存取控制需透過 [Adobe Admin Console](https://adminconsole.adobe.com/) 產品設定檔會將使用者與許可權和沙箱連結。 請參閱 [存取控制總覽](../access-control/home.md) 以取得詳細資訊。

為了使用查詢服務， [!DNL Manage Queries] 必須在admin console中啟用許可權。 此許可權可讓使用者執行隨機和批次查詢。 請求存取產品設定檔的詳細指示 [!DNL Manage Queries] 已在下列章節中概述許可權： [管理產品設定檔的許可權](../access-control/ui/permissions.md) 和 [管理產品設定檔的使用者](../access-control/ui/users.md) 檔案。

購買後 [!DNL Data Distiller] 附加元件， [!DNL Write Dataset] 必須授予許可權。 此許可權允許 [!DNL Data Distiller] 執行批次查詢的使用者。

下表概述了 [!DNL Manage Queries] 許可權：

| 权限 | 函数 |
|---|---|
| [!DNL Manage Queries] （沒有寫入資料許可權） | 提供執行特定查詢的存取權 |
| [!DNL Manage Queries] （具有寫入資料許可權） | 提供執行批次查詢的存取權 |

{style="table-layout:auto"}

## 沙箱支援

沙箱是單一Experience Platform執行個體中的虛擬分割區。 每個Platform例項都支援多個生產和非生產沙箱，每個沙箱都維護自己的Platform資源庫。 非生產沙箱可讓您測試功能、執行實驗及進行自訂設定，而不會影響您的生產沙箱。 如需沙箱的詳細資訊，請參閱 [沙箱總覽](../sandboxes/home.md). 所有查詢服務權益會在所有沙箱之間共用

## 后续步骤

閱讀本檔案後，您應該能更清楚瞭解查詢服務中可用的不同封裝型別和查詢執行功能。 若要進一步瞭解查詢服務（例如知名的產業使用案例），請閱讀 [使用案例檔案](./use-cases/abandoned-browse.md). 如需一般資訊，請瀏覽 [查詢服務總覽](./home.md).
