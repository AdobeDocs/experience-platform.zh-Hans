---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；ExperienceEvent；欄位；結構；結構描述；結構描述設計；欄位群組；欄位群組；環境；環境詳細資訊；
solution: Experience Platform
title: 環境詳細資料結構欄位群組
description: 本檔案提供「ExperienceEvent環境詳細資訊」結構描述欄位群組的概觀。
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 1%

---


# [!UICONTROL 環境詳細資訊] 結構描述欄位群組

>[!NOTE]
>
>數個結構描述欄位群組的名稱已變更。 檢視檔案： [欄位群組名稱更新](../name-updates.md) 以取得詳細資訊。

[!UICONTROL 環境詳細資訊] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md) 用於擷取和體驗事件相關的環境詳細資訊相關資訊，例如裝置詳細資訊、瀏覽器資訊、當地時間和其他地理資訊。

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `device` | [设备](../../data-types/device.md) | 說明可跨工作階段追蹤（通常透過Cookie）的已識別裝置、應用程式或裝置瀏覽器執行個體。 |
| `environment` | [环境](../../data-types/environment.md) | 說明事件觀察情境的相關資訊，特別是網路或軟體版本之類的臨時性詳細資訊。 |
| `placeContext` | [地標內容](../../data-types/place-context.md) | 說明與事件觀察相關的暫時性情況。 例如特定地區資訊，例如天氣、當地時間、交通、星期幾、工作日與假日、以及工作時間。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
