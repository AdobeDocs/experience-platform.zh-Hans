---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；位址；xdm：位址；資料型別；資料型別；
solution: Experience Platform
title: 郵寄地址資料型別
description: 本檔案提供郵寄地址XDM資料型別的概觀。
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# [!UICONTROL 郵寄地址] 資料型別

[!UICONTROL 郵寄地址] 是標準XDM資料型別，說明郵寄地址的詳細資訊。

<img src="../images/data-types/postal-address.png" width="450" /><br />

| 属性 | 描述 |
| --- | --- |
| `city` | 城市名稱。 |
| `country` | 政府管理地區的名稱。 這是自由格式的欄位，可以有任何語言的國家/地區名稱。 |
| `countryCode` | 兩個字元 <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> 國家/地區的代碼。 |
| `createdByBatchID` | 建立地址記錄之擷取批次檔案的ID。 |
| `dmaID` | Nielsen媒體研究指定的市場區域。 |
| `label` | 地址的自由格式名稱。 |
| `lastVerifiedDate` | 上次驗證該地址仍與該人員相關聯的日期。 |
| `modifiedByBatchID` | 上次修改記錄之擷取批次檔案的ID。 |
| `msaID` | 進行觀察的美國大都會統計區域。 |
| `postOfficeBox` | 地址的郵政信箱。 |
| `postalCode` | 地點的郵遞區號。 郵遞區號並非適用於所有國家/地區。 在某些國家/地區，這僅包含部分郵遞區號。 |
| `primary` | 表示這是否為個人主要地址的布林值。 設定檔只能有一個 `primary` 指定時間點的位址。 |
| `region` | 地址的地區、國家或地區部分。 |
| `repositoryCreatedBy` | 建立記錄的使用者ID。 |
| `repositoryLastModifiedBy` | 上次修改記錄的使用者ID。 |
| `stateProvince` | 觀察的州或省的部分。 格式會遵循 [ISO 3166-2 （國家/地區和細分）](https://www.unece.org/cefact/locode/subdivisions.html) 標準。 |
| `status` | 指出目前是否可以使用地址。 |
| `statusReason` | 目前專案的說明 `status`. |
| `street1` — `street4` | 這四個欄位的用途是包含主要街道層級資訊、公寓號碼、街道號碼和街道名稱。 `street2` 至 `street4` 是選用專案。 |

{style="table-layout:auto"}

如需郵寄地址資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.schema.json)
