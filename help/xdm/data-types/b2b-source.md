---
title: B2B來源資料型別
description: 本檔案提供B2B來源體驗資料模型(XDM)資料型別的概觀。
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: e602f78470fe4eeb2a42e6333ba52096d8a9fe8a
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 2%

---

# [!UICONTROL B2B來源] 資料型別

[!UICONTROL B2B來源] 是標準的體驗資料模型(XDM)資料型別，代表B2B實體(例如 [帳戶](../classes/b2b/business-account.md)，和 [商機](../classes/b2b/business-opportunity.md)，或 [行銷活動](../classes/b2b/business-campaign.md))。

當僅依賴字串型識別碼時，多個系統之間的ID可能會重疊（例如，機會可能會在一個CRM系統上獲得字串ID，但同一ID可能會引用完全不同的機會）。 這可能會導致合併中的資料發生衝突 [即時客戶個人檔案](../../profile/home.md).

此 [!UICONTROL B2B來源] 資料型別可讓您使用實體的原始字串ID，並將其與來源特定的內容資訊結合，以確保無論其來源為何，在Platform系統中都保持完全唯一。

![B2B來源結構](../images/data-types/b2b-source.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `sourceID` | 字符串 | 來源記錄的唯一ID。 |
| `sourceInstanceID` | 字符串 | 來源資料的執行個體或組織ID。 |
| `sourceKey` | 字符串 | 由以下專案組成的唯一識別碼 `sourceId`， `sourceInstanceId`、和 `sourceType` 以下列格式串連在一起： `[sourceID]@[sourceInstanceID].[sourceType]`.<br><br>某些來源聯結器(如Marketo)會自動為特定識別碼串連此值。 其他必須使用 [資料準備 `concat` 函式](../../data-prep/functions.md#string)例如： `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | 字符串 | 提供來源資料的平台名稱。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
