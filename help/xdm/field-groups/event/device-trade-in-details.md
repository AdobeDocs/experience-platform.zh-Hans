---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；ExperienceEvent；欄位；結構；結構描述；結構描述設計；欄位群組；欄位群組；裝置；交易；交易；
solution: Experience Platform
title: 裝置折舊換新詳細資料結構描述欄位群組
description: 本檔案提供「裝置以舊換新詳細資訊」結構描述欄位群組的概觀。
exl-id: 744557be-0297-453f-9134-9d0f4ef2df4d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 2%

---

# [!UICONTROL 裝置折舊換新細節] 結構描述欄位群組

>[!NOTE]
>
>數個結構描述欄位群組的名稱已變更。 檢視檔案： [欄位群組名稱更新](../name-updates.md) 以取得詳細資訊。

[!UICONTROL 裝置折舊換新細節] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md). 它提供單一欄位(`deviceTradeInDetails`)以舊換新交易，包括折舊換新價值、原始裝置ID和新裝置ID。

![裝置折舊換新詳細資料結構](../../images/field-groups/device-trade-in-details.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `tradeInValue` | [货币](../../data-types/currency.md) | 交易的裝置值。 |
| `newDeviceID` | 字符串 | 交易的新裝置ID。 |
| `originalDeviceID` | 字符串 | 交易的裝置識別碼。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.schema.json)
