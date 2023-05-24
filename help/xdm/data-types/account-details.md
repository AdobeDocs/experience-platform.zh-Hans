---
title: 帳戶詳細資料資料型別
description: 本檔案提供Account Details Experience Data Model (XDM)資料型別的概述。
exl-id: 17254393-263e-4000-9bd2-815a9e842533
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 5%

---

# [!UICONTROL 帳戶詳細資料] 資料型別

[!UICONTROL 帳戶詳細資料] 是標準的體驗資料模型(XDM)資料型別，可描述與業務組織相關的詳細資訊。

![資料型別結構](../images/data-types/account-details.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `annualRevenue` | [[!UICONTROL 货币]](./currency.md) | 預估的組織年收入金額。 |
| `DUNSNumber` | 字符串 | 組織的Dun &amp; Bradstreet D-U-N-S編號。 這是指派給Dun &amp; Bradstreet資料庫中每個商業地點的非指示性九位數數字，具有唯一、單獨和相異的操作，並完全由Dun &amp; Bradstreet維護。 |
| `NAICSCode` | 字符串 | 該組織在北美產業分類系統中的分類。 |
| `NAICSDescription` | 字符串 | 組織的企業營運的簡短說明（根據其NAICS代碼）。 |
| `SICCode` | 字符串 | 組織的標準產業分類(SIC)代碼。 這是四位數的代碼，會根據公司的業務活動來分類其所屬的產業。 |
| `SICDescription` | 字符串 | 組織的企業營運的簡短說明（根據其SIC代碼）。 |
| `companyProductAndServices` | 字符串 | 組織正在交易或做生意的產品和服務。 |
| `facebookPageUrl` | 字符串 | 指向組織Facebook帳戶的網站連結。 |
| `industry` | 字符串 | 此組織所屬的產業。 這是自由格式的欄位，建議在查詢中使用結構化值或使用 `xdm:classifier` 屬性。 |
| `jigsaw` | 字符串 | 組織的Data.com索引鍵。 |
| `linkedinPageUrl` | 字符串 | 指向組織LinkedIn帳戶的網站連結。 |
| `logoUrl` | 字符串 | 要與Salesforce執行個體的URL結合的路徑(例如， `https://yourInstance.salesforce.com/`)產生URL以請求與組織相關聯的社交網路設定檔影像。 產生的URL會傳回HTTP重新導向（代碼302）至組織的社交網路設定檔影像。 |
| `marketSegment` | 字符串 | 組織參與的已命名市場區段。 這是自由格式的欄位，建議在查詢中使用結構化值或使用 `xdm:identifier` 屬性。 |
| `numberOfEmployees` | 整数 | 組織的員工人數。 |
| `organizationType` | 字符串 | 說明組織型別的標籤。 |
| `primaryEmailDomain` | 字符串 | 組織用於其人員的主要電子郵件網域。 |
| `rating` | 双精度 | 此組織的計算分數或星級評等。 `1` 表示最大可能的評等，以及 `0` 為可能的最低評等。 |
| `tickerSymbol` | 字符串 | 此帳戶的股市符號。 最多20個字元。 |
| `twitterHandleUrl` | 字符串 | 指向組織的twitter控制碼的網站連結。 |
| `website` | 字符串 | 組織網站的URL。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.schema.json)
