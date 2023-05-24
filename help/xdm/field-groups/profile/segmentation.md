---
keywords: Experience Platform；首頁；熱門主題；結構描述；結構描述；XDM；個人設定檔；欄位；結構描述；結構描述；區段；segmentMembership；區段會籍；結構描述設計；對應；對應；
solution: Experience Platform
title: 區段會籍詳細資料結構欄位群組
description: 本檔案提供「區段成員資格詳細資訊」結構描述欄位群組的概觀。
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
source-git-commit: 229dd08bc5d5dfab068db3be84ad20d10992fd31
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 1%

---


# [!UICONTROL 區段會籍細節] 結構描述欄位群組

>[!NOTE]
>
>數個結構描述欄位群組的名稱已變更。 檢視檔案： [欄位群組名稱更新](../name-updates.md) 以取得詳細資訊。

[!UICONTROL 區段會籍細節] 是的標準結構描述欄位群組 [[!DNL XDM Individual Profile] 類別](../../classes/individual-profile.md). 欄位群組提供單一對應欄位，可擷取關於區段會籍的資訊，包括個人屬於哪些區段、上次資格取得時間以及會籍有效期至。

>[!WARNING]
>
>而 `segmentMembership` 欄位必須使用此欄位群組手動新增到您的設定檔結構描述，您不應嘗試手動填入或更新此欄位。 系統會自動更新 `segmentMembership` 在執行分段工作時，對應每個設定檔。

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `segmentMembership` | 地图 | 描述個人區段會籍的地圖物件。 此物件的結構將於下文詳細說明。 |

{style="table-layout:auto"}

範例如下 `segmentMembership` 系統已針對特定設定檔填入的對應。 區段會籍會依名稱空間排序，如物件的根層級索引鍵所示。 反過來，每個名稱空間底下的個別索引鍵代表設定檔所屬區段的ID。 每個區段物件都包含數個子欄位，提供有關成員資格的進一步詳細資訊：

```json
{
  "xdm:segmentMembership": {
    "AAM": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "xdm:version": "15",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2019-04-26T15:52:25+00:00",
        "xdm:status": "realized",
        "xdm:payload": {
          "xdm:payloadBooleanValue": true,
          "xdm:payloadType": "boolean"
        }
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "xdm:version": "3",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2018-04-27T15:52:25+00:00",
        "xdm:status": "realized",
        "xdm:payload": {
          "xdm:payloadPropensityValue": 0.5,
          "xdm:payloadType": "propensity"
        }
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "xdm:version": "1",
        "xdm:lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "xdm:validUntil": "2017-12-26T15:52:25+00:00",
        "xdm:status": "exited"
      }
    }
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `xdm:version` | 此設定檔符合資格的區段版本。 |
| `xdm:lastQualificationTime` | 此設定檔上次符合區段資格的時間戳記。 |
| `xdm:validUntil` | 區塊會籍何時不應再被假定為有效的時間戳記。 對於外部對象，若未設定此欄位，則區段會籍將僅保留30天，從 `lastQualificationTime`. |
| `xdm:status` | 字串欄位，指出是否已將區段會籍實現為目前請求的一部分。 接受下列值： <ul><li>`realized`：設定檔符合區段的資格。</li><li>`exited`：設定檔正在退出區段，做為目前請求的一部分。</li></ul> |
| `xdm:payload` | 部分割槽段會籍包含說明與會籍直接相關之其他值的裝載。 每個成員資格只能提供一個指定型別的裝載。 `xdm:payloadType` 指示裝載型別(`boolean`， `number`， `propensity`，或 `string`)，而其同層級屬性則提供裝載型別的值。 |

{style="table-layout:auto"}

>[!NOTE]
>
>任何位於中的區段會籍 `exited` 超過30天的狀態，根據 `lastQualificationTime`，可能會刪除。

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
