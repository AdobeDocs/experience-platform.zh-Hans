---
keywords: 電子郵件；電子郵件；電子郵件；電子郵件目的地
title: 電子郵件行銷目的地概觀
type: Tutorial
description: 電子郵件服務提供者(ESP)可讓您管理電子郵件行銷活動，例如傳送促銷電子郵件行銷活動。 瞭解哪些ESP受支援作為Experience Platform目的地。
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: 29c02cf977863a348252f9a8b40b3b6ec8a83a9c
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 4%

---

# 電子郵件行銷目的地概觀 {#email-marketing-destinations}

## 概述 {#overview}

電子郵件服務提供者(ESP)可讓您管理電子郵件行銷活動，例如傳送促銷電子郵件行銷活動。 Adobe Experience Platform可讓您啟用電子郵件行銷目的地的區段，以與ESP整合。

## 支援的電子郵件行銷目的地 {#supported-destinations}

Adobe Experience Platform支援下列電子郵件行銷目的地：

* [Adobe Campaign](adobe-campaign.md)
* [Adobe Campaign Managed Cloud Services](adobe-campaign-managed-services.md)
* [(API)OracleEloqua](oracle-eloqua-api.md)
* [(API) [!DNL Salesforce Marketing Cloud]](salesforce-marketing-cloud-exact-target.md)
* [（檔案） Oracle Eloqua](oracle-eloqua.md)
* [（檔案） [!DNL Salesforce Marketing Cloud]](salesforce-marketing-cloud.md)
* [[!DNL Salesforce Marketing Cloud Account Engagement]](salesforce-marketing-cloud-account-engagement.md)
* [oracleResponsys](oracle-responsys.md)
* [SendGrid](sendgrid.md)

## 連線至新的電子郵件行銷目的地 {#connect-destination}

若要將區段傳送至行銷活動的電子郵件行銷目的地，平台必須先連線至目的地。 請參閱 [目的地建立教學課程](../../ui/connect-destination.md) 以取得設定新目的地的詳細資訊。

## 在電子郵件行銷目的地啟用對象時的最佳實務 {#best-practices}

### 身分選擇 {#identity}

Adobe建議您從 [聯合結構描述](../../../profile/home.md#profile-fragments-and-union-schemas). 這是將您的使用者身分識別作為輸入資料的欄位。 最常見的情況是，此欄位是電子郵件地址，但也可以是忠誠度方案ID或電話號碼。 請參閱下表，瞭解結構描述中最常見的唯一識別碼及其XDM欄位。

| 唯一識別碼 | 統一結構描述中的XDM欄位 |
|----------------- | ---------------------------|
| Email Address | `personalEmail.address` |
| Phone | `mobilePhone.number` |
| 熟客方案ID | `Customer-defined XDM field` |

{style="table-layout:auto"}

### 其他目的地屬性 {#other-destination-attributes}

在「結構描述」欄位選取器中，選擇要匯出至電子郵件目的地的其他欄位。 部分建議選項包括：

| 架构 | XDM欄位 |
|------ | ---------|
| 名字 | `person.name.firstName` |
| 姓氏 | `person.name.lastName` |
| Phone | `mobilePhone.number` |
| 地址城市 | `homeAddress.city` |
| 地址狀態 | `homeAddress.stateProvince` |
| 地址郵遞區號 | `homeAddress.postalCode` |
| 生日 | `person.birthDayAndMonth` |
| 区段会员资格 | `segmentMembership.status` |

{style="table-layout:auto"}

## 對電子郵件行銷目的地啟用區段 {#activate}

目錄中的部分電子郵件行銷目的地會透過與目的地的API整合，以串流方式匯出設定檔。

其他目的地會將檔案匯出至雲端儲存位置。 匯出完成後，您需要從雲端儲存位置將資料匯入電子郵件行銷目的地。

請依照 [支援的電子郵件行銷目的地](#supported-destinations) 區段，以瞭解如何對每個電子郵件行銷目的地啟用區段。

## 其他资源 {#additional-resources}

* [啟用對象資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md)
* [使用流量服務API建立電子郵件行銷目的地並啟用資料](../../api/connect-activate-batch-destinations.md)
