---
solution: Experience Platform
title: 同意字串資料型別
description: 本檔案提供同意字串XDM資料型別的概觀。
exl-id: 288ec79e-074a-4d72-9c5f-e9cd8485b804
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 3%

---

# [!UICONTROL 同意字串] 資料型別

[!UICONTROL 同意字串] 是標準XDM資料型別，說明代表客戶同意的字串值。 其中包含內容相關資訊，例如同意字串的標準(例如 [IAB透明與同意架構(TCF) 2.0](../field-groups/profile/iab.md))。

![](../images/data-types/consent-string.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `consentStandard` | 字符串 | 同意字串的標準。 這有助於判斷同意管理服務所設定的同意字串格式。 |
| `consentStandardVersion` | 字符串 | 同意標準的版本，用來精確定義同意管理服務所設定的同意字串格式。 |
| `consentStringValue` | 字符串 | 同意管理服務所提供的完整同意字串。 `consentStandard` 和 `consentStandardVersion` 協助定義如何剖析此字串。 |
| `containsPersonalData` | 布尔值 | 此欄位為true時，表示需要處理此同意字串以進行同意執行。 |
| `gdprApplies` | 布尔值 | 當此欄位為true時，表示同意和個人資料會一起出現。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.schema.json)
