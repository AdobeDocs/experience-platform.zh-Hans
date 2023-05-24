---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；電話號碼；xdm：phoneNumber；資料型別；資料型別；
solution: Experience Platform
title: 電話號碼資料型別
description: 本檔案提供電話號碼XDM資料型別的概觀。
exl-id: b84e48f9-bbb4-4b8b-9476-4bc1c455ecfd
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# [!UICONTROL 電話號碼] 資料型別

[!UICONTROL 電話號碼] 是說明電話號碼詳細資訊的標準XDM資料型別。

<img src="../images/data-types/phone-number.png" width="600" /><br />

| 属性 | 描述 |
| --- | --- |
| `extension` | 用於從私人交換機、接線生或總機打電話的內部撥號號碼。 |
| `number` | 電話號碼。 請注意，電話號碼為字串，可能包含有意義的字元，例如括弧 `()`，連字型大小 `-`，或字元來表示次撥接識別碼，例如副檔名 `x` 例如， `1-353(0)18391111` 或 `+613 9403600x1234`. |
| `primary` | 表示這是否為個人主要電話號碼的布林值。 不像地址或電子郵件地址，主要電話號碼可以有多個；每個通訊頻道一個。 通訊通道由型別定義（由父屬性的名稱指示）： `textMessaging`， `mobile`， `phone`， `home`， `work`， `unknown`、和 `fax`. |
| `status` | 指出目前是否可以使用電話號碼。 |
| `statusReason` | 目前狀態的說明。 |
| `validity` | 電話號碼的技術正確性等級。 |

{style="table-layout:auto"}

如需電話號碼資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.schema.json)
