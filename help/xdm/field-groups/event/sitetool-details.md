---
title: Sitetool詳細資料結構欄位群組
description: 本檔案提供「Sitetool詳細資訊」結構描述欄位群組的概觀。
exl-id: 472c0a3f-efda-49af-9490-f2de90b348c0
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 4%

---

# [!UICONTROL Sitetool詳細資料] 結構描述欄位群組

[!UICONTROL Sitetool詳細資料] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md). 欄位群組提供單一 `sitetool` 物件變更為結構描述，以擷取sitetool所收集的資訊。

![欄位群組結構](../../images/field-groups/sitetool-details.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `dataGatheringEvent` | 对象 | 指出此事件是否與其他相關詳細資料一起屬於資料收集事件。 包含以下屬性：<ul><li>`data`：（對應）包含所收集的JSON資料，這些資料會隨著測驗、調查或輪詢提交事件而提交。</li><li>`isTrue`：（布林值）指出此事件是否為測驗、調查或輪詢等資料收集事件。</li><li>`score`：（整數）執行者根據事件回應保護的分數。</li></ul> |
| `actor` | 字符串 | 執行此動作的人員/成員。 |
| `actorID` | 字符串 | 執行此動作之人員/成員的唯一識別碼。 |
| `isKeyEvent` | 布尔值 | 指出此事件是否為關鍵事件。 |
| `name` | 字符串 | Sitetool的名稱，例如聊天機器人、調查等。 |
| `section` | 字符串 | Sitetool的相關區段，例如main或sub。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json).
