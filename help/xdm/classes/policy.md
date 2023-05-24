---
title: 原則類別
description: 本檔案提供Experience Data Model (XDM)中原則類別的概觀。
exl-id: 56cc8c69-84a0-493e-85c5-e0cd994e4bee
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 7%

---

# [!UICONTROL 原則] 類別

在Experience Data Model (XDM)中， [!UICONTROL 原則] class會擷取定義保單的最小屬性集。

![](../images/classes/policy.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `assignedBeneficiary` | 陣列 [[!UICONTROL 個人]](../data-types/person.md) 資料型別 | 擷取指定給保單的受益人（或受益人）。 |
| `benefitAmount` | [[!UICONTROL 货币]](../data-types/currency.md) | 根據政策條款支付的金額。 |
| `location` | [[!UICONTROL 郵寄地址]](../data-types/postal-address.md) | 保單核發地點。 |
| `owner` | [!UICONTROL 对象] | 擷取保單持有人設定檔資訊。 |
| `owner.faxPhone` | [[!UICONTROL 电话号码]](../data-types/phone-number.md) | 擁有者的傳真電話號碼。 |
| `owner.homeAddress` | [[!UICONTROL 郵寄地址]](../data-types/postal-address.md) | 擁有者的住家地址。 |
| `owner.homePhone` | [[!UICONTROL 电话号码]](../data-types/phone-number.md) | 擁有者的住家電話號碼。 |
| `owner.mobilePhone` | [[!UICONTROL 电话号码]](../data-types/phone-number.md) | 擁有者的行動電話號碼。 |
| `owner.personalEmail` | [[!UICONTROL 电子邮件地址]](../data-types/email-address.md) | 擁有者的個人電子郵件地址。 |
| `ID` | [!UICONTROL 字符串] | 保單的識別碼。 |
| `_id` | [!UICONTROL 字符串] | 記錄的唯一、系統產生的字串識別碼。 此欄位用於追蹤個別記錄的唯一性、防止資料重複，以及在下游服務中查詢該記錄。<br><br>由於此欄位是系統產生的，因此在資料擷取期間不會向其提供明確值。 不過，您仍然可以視需要選擇提供自己的唯一ID值。 |
| `endDate` | [!UICONTROL 日期時間] | 保單承保結束（或結束）的日期。 |
| `hasAssignedBeneficiary` | [!UICONTROL 布尔型] | 指出原則是否已指定受益人。 |
| `name` | [!UICONTROL 字符串] | 保單的名稱。 |
| `startDate` | [!UICONTROL 日期時間] | 保單承保開始（或開始）的日期。 |
| `type` | [!UICONTROL 字符串] | 住家、汽車、租借者或船隻等保單型別。 |

{style="table-layout:auto"}
