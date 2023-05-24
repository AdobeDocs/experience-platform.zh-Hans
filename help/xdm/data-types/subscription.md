---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；訂閱；資料型別；資料型別；
solution: Experience Platform
title: 訂閱資料型別
description: 本檔案提供訂閱體驗資料模型(XDM)資料型別的概觀。
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 9%

---

# [!UICONTROL 訂閱] 資料型別

[!UICONTROL 訂閱] 是標準的Experience Data Model (XDM)資料型別，說明軟體、服務或商品的授權權利，這些權利是根據時間或使用情況來使用。

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `device` | [[!UICONTROL 设备]](./device.md) | 說明連結至訂閱之裝置的詳細資料。 |
| `environment` | [[!UICONTROL 环境]](./environment.md) | 包含有關發生事件觀察的周圍情況的資訊，特別詳細說明網路或軟體版本之類的臨時性資訊。 |
| `subscriber` | [[!UICONTROL 人员]](./person.md) | 說明個人。 這也可以代表擔任各種角色的人員，例如客戶、連絡人或擁有者。 |
| `SKU` | 字符串 | 庫存單位(SKU)，產品的唯一識別碼。 |
| `billingPeriod` | 字符串 | 計費之間的持續時間。 |
| `billingStartDate` | 日期 | 第一筆帳單到期日。 日期格式（沒有時間）應遵循 [RFC 3339,5.6節](https://tools.ietf.org/html/rfc3339#section-5.6) 標準。 |
| `category` | 字符串 | 此類訂閱的主要頂層分類。 |
| `chargeMethod` | 字符串 | 設定帳單的方式以向客戶收費。 |
| `contractID` | 字符串 | 適用於規範此訂閱之合約的唯一ID。 |
| `country` | 字符串 | 訂閱合約和協定條款根源的國家/地區。 |
| `endDate` | 日期 | 目前訂閱期限結束的日期。 日期格式（沒有時間）應遵循 [RFC 3339,5.6節](https://tools.ietf.org/html/rfc3339#section-5.6) 標準。 |
| `paymentMethod` | 字符串 | 定期付款的付款方式。 |
| `paymentStatus` | 字符串 | 帳戶的付款狀態。 |
| `planName` | 字符串 | 人類看得懂的訂閱名稱。 |
| `reason` | 字符串 | 成員使用訂閱的一般意圖。 |
| `renew` | 字符串 | 訂閱在結束日期後可能繼續的議定方式。 |
| `revision` | 字符串 | 相同名稱和類別階層的訂閱之間的識別。 |
| `startDate` | 日期 | 訂閱開始日期。 日期格式（沒有時間）應遵循 [RFC 3339,5.6節](https://tools.ietf.org/html/rfc3339#section-5.6) 標準。 |
| `status` | 字符串 | 訂閱的目前狀態。 |
| `subCategory` | 字符串 | 訂閱的特定子分類。 |
| `term` | 整数 | 訂閱期限的數值。 |
| `termUnitOfTime` | 字符串 | 期限期間的時間單位。 |
| `topUp` | 字符串 | 說明在計費期間如何重新購買訂閱之可消耗部分的議定條款。 |
| `type` | 字符串 | 與訂閱所涵蓋人數相關的權益範圍。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)
