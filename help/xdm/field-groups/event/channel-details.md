---
keywords: Experience Platform；首頁；熱門主題；綱要；綱要；XDM；ExperienceEvent；欄位；綱要；綱要；綱要設計；欄位群組；欄位群組；
solution: Experience Platform
title: 管道詳細資料結構欄位群組
description: 本檔案提供「管道詳細資料」結構描述欄位群組的概觀。
exl-id: b8ec2f57-6882-466e-9b22-61fb2178fb1e
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 1%

---

# [!UICONTROL 管道詳細資料] 結構描述欄位群組

>[!NOTE]
>
>數個結構描述欄位群組的名稱已變更。 檢視檔案： [欄位群組名稱更新](../name-updates.md) 以取得詳細資訊。

[!UICONTROL 管道詳細資料] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md)，用於說明頻道資訊，例如ID、頻道型別、媒體型別和位置型別。

![](../../images/field-groups/channel-details.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `channel` | [體驗管道](../../data-types/experience-channel.md) | 說明產品退貨、保固註冊及購物車/訂單流程的物件。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.schema.json)
