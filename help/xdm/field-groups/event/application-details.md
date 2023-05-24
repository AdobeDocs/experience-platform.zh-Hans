---
title: 應用程式詳細資料結構欄位群組
description: 本檔案提供「應用程式詳細資訊」結構描述欄位群組的概觀。
exl-id: 5df99f9a-b36a-4c2b-a4a4-d3cf054f09b8
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 2%

---

# [!UICONTROL 應用程式詳細資料] 結構描述欄位群組

[!UICONTROL 應用程式詳細資料] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md). 欄位群組提供單一 `application` 將物件變更為結構描述，以擷取應用程式相關詳細資訊，例如當機、功能使用、啟動和升級。

![](../../images/field-groups/application-details.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `application` | [[!UICONTROL 应用程序]](../../data-types/financial-account.md) | 擷取和事件相關的應用程式資訊，包括應用程式名稱、應用程式版本、安裝、啟動、當機和關閉。 可能是事件鎖定的應用程式（例如傳送的推播通知目的地），或是產生事件的應用程式（例如點選或登入）。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json).
