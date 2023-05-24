---
title: 外部來源系統稽核屬性資料型別
description: 本檔案提供外部來源系統稽核屬性Experience Data Model (XDM)資料型別的概述。
exl-id: ebdd8707-9675-4232-a5b7-4e4a481d706a
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 2%

---

# [!UICONTROL 外部來源系統稽核屬性] 資料型別

>[!NOTE]
>
>此資料型別僅適用於可存取Adobe Real-time Customer Data Platform B2B版本的組織。

[!UICONTROL 外部來源系統稽核屬性] 是標準的體驗資料模型(XDM)資料型別，可擷取有關外部來源系統的稽核細節。

![](../images/data-types/external-source-system-audit-attributes.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL B2B來源]](./b2b-source.md) | 用於稽核之來源的複合識別碼。 |
| `createdBy` | 字符串 | 建立此記錄的使用者名稱。 |
| `createdDate` | 日期時間 | 建立此記錄的日期。 |
| `externalID` | 字符串 | 來源的外部唯一識別碼。 如有需要，可使用此值來協助識別和重複資料刪除。 |
| `lastActivityDate` | 日期時間 | 來源系統的上次活動日期。 |
| `lastReferencedDate` | 日期時間 | 來源系統的最後參考日期。 |
| `lastUpdatedBy` | 字符串 | 上次更新此記錄的人員姓名。 |
| `lastUpdatedDate` | 日期時間 | 來源系統的上次更新日期。 |
| `lastViewedDate` | 日期時間 | 來源系統的上次檢視日期。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)
