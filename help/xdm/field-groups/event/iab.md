---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；ExperienceEvent；欄位；結構；結構描述；結構描述設計；欄位群組；欄位群組；iab；tcf；同意；
solution: Experience Platform
title: 事件結構描述的IAB TCF 2.0同意欄位群組
description: 本檔案提供XDM ExperienceEvent類別的IAB TCF 2.0同意結構描述欄位群組概覽。
exl-id: c236d0d4-27bd-45d7-a912-d0e93a609254
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# [!UICONTROL IAB TCF 2.0同意] 事件結構描述的欄位群組

>[!IMPORTANT]
>
>本檔案涵蓋 [!UICONTROL IAB TCF 2.0同意] xdm ExperienceEvent類別的結構描述欄位群組。 只有在您想要追蹤一段時間內同意變更事件時，才應使用此欄位群組。
>
>請注意，自動執行工作流程不會遵循事件資料中記錄的同意值。 為了進行自動強制執行，同意值必須擷取到XDM個人設定檔類別中，並啟用即時客戶設定檔。
>
>若為XDM個別設定檔類別的欄位群組，請參閱下列內容 [檔案](../profile/iab.md) 而非。

[!UICONTROL IAB TCF 2.0同意] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md) 用於擷取時間戳記系列IAB同意字串，以追蹤隨著時間變化的同意變更模式。

![](../../images/field-groups/iab-event.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `consentStrings` | 陣列 [同意字串](../../data-types/consent-string.md) | 與事件相關的一組同意字串值。 |

{style="table-layout:auto"}

請參閱指南： [平台中的IAB TCF 2.0支援](../../../landing/governance-privacy-security/consent/iab/overview.md) 以取得此欄位群組使用案例的詳細資訊。 如需欄位群組本身的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
