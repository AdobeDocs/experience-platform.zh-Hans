---
keywords: Experience Platform；首頁；熱門主題；結構描述；結構描述；XDM；欄位；結構描述；電子郵件地址；xdm：emailAddress；電子郵件；電子郵件地址；資料型別；資料型別；
solution: Experience Platform
title: 電子郵件地址資料型別
description: 本檔案提供電子郵件地址XDM資料型別的概觀。
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# [!UICONTROL 電子郵件地址] 資料型別

[!UICONTROL 電子郵件地址] 是標準的體驗資料模型(XDM)資料型別，可描述電子郵件地址的詳細資訊。

<img src="../images/data-types/email-address.png" width="450" /><br />

| 属性 | 描述 |
| --- | --- |
| `address` | RFC2822和後續標準中通常定義的電子郵件的技術地址(例如， `name@domain.com`)。<br><br>在XDM中，電子郵件地址必須包含有效的頂層網域，才能通過驗證。 請參閱下列內容 [檔案](https://data.iana.org/TLD/tlds-alpha-by-domain.txt) 以取得網際網路號碼指派機構(IANA)所定義的有效上層網域完整清單。 |
| `label` | 可能有的其他顯示資訊。 例如，如果電子郵件的Microsoft Outlook豐富地址顯示為 `John Smith smithjr@company.uk`， `John Smith` 會放置在此欄位中。 |
| `primary` | 指出這是否為個人的主要電子郵件地址。 設定檔只能有一個 `primary` 指定時間點的電子郵件地址。 |
| `status` | 指出目前是否可以使用電子郵件地址 |
| `statusReason` | 目前專案的說明 `status`. |
| `type` | 帳戶與個人建立關聯的方式(例如 `work` 或 `personal`)。 |

{style="table-layout:auto"}


有關電子郵件地址資料型別的更多詳細資訊，請參閱公共XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
