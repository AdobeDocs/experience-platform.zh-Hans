---
title: Adobe Analytics ExperienceEvent完整擴充功能結構描述欄位群組
description: 本檔案提供Adobe Analytics ExperienceEvent Full Extension結構描述欄位群組的概觀。
exl-id: b5e17f4a-a582-4059-bbcb-435d46932775
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 8%

---

# [!UICONTROL Adobe Analytics ExperienceEvent完整擴充功能] 結構描述欄位群組

[!UICONTROL Adobe Analytics ExperienceEvent完整擴充功能] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md)，會擷取Adobe Analytics所收集的一般量度。

本檔案說明Analytics擴充功能欄位群組的結構和使用案例。

>[!NOTE]
>
>由於此欄位群組中重複元素的大小和數量，本指南中顯示的許多欄位已收合以節省空間。 若要探索此欄位群組的完整結構，您可以 [在平台UI中查詢 ](../../ui/explore.md) 或檢視中完整的結構描述 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

## 欄位群組結構

欄位群組提供單一 `_experience` 物件對應到結構描述，而結構描述本身包含單一 `analytics` 物件。

![Analytics欄位群組的頂層欄位](../../images/field-groups/analytics-full-extension/full-schema.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `customDimensions` | 对象 | 擷取Analytics追蹤的自訂維度。 請參閱 [下方的子區段](#custom-dimensions) 以取得此物件內容的詳細資訊。 |
| `endUser` | 对象 | 擷取觸發事件之一般使用者的網路互動細節。 請參閱 [下方的子區段](#end-user) 以取得此物件內容的詳細資訊。 |
| `environment` | 对象 | 擷取關於觸發事件的瀏覽器和作業系統的資訊。 請參閱 [下方的子區段](#environment) 以取得此物件內容的詳細資訊。 |
| `event1to100`<br><br>`event101to200`<br><br>`event201to300`<br><br>`event301to400`<br><br>`event401to500`<br><br>`event501to100`<br><br>`event601to700`<br><br>`event701to800`<br><br>`event801to900`<br><br>`event901to1000` | 对象 | 欄位群組提供物件欄位，可擷取最多1000個自訂事件。 請參閱 [下方的子區段](#events) 以取得這些欄位的詳細資訊。 |
| `session` | 对象 | 擷取觸發事件的工作階段相關資訊。 請參閱 [下方的子區段](#session) 以取得此物件內容的詳細資訊。 |

{style="table-layout:auto"}

## `customDimensions` {#custom-dimensions}

`customDimensions` 擷取自訂 [維度](https://experienceleague.adobe.com/docs/analytics/components/dimensions/overview.html?lang=zh-Hans) Analytics所追蹤的專案。

![customdimensions欄位](../../images/field-groups/analytics-full-extension/customDimensions.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `eVars` | 对象 | 可擷取最多250個轉換變數的物件([eVar](https://experienceleague.adobe.com/docs/analytics/components/dimensions/evar.html?lang=zh-CN))。 此物件的屬性會加上金鑰 `eVar1` 至 `eVar250` 和僅接受字串作為其資料型別。 |
| `hierarchies` | 对象 | 可擷取最多五個自訂階層變數的物件([hiers](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html))。 此物件的屬性會加上金鑰 `hier1` 至 `hier5`，這些物件本身便具有下列子屬性：<ul><li>`delimiter`：用來產生下方所提供清單的原始分隔字元 `values`.</li><li>`values`：階層層級名稱的分隔清單，以字串表示。</li></ul> |
| `listProps` | 对象 | 擷取最多75個的物件 [清單屬性](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html#list-props). 此物件的屬性會加上金鑰 `prop1` 至 `prop75`，這些物件本身便具有下列子屬性：<ul><li>`delimiter`：用來產生下方所提供清單的原始分隔字元 `values`.</li><li>`values`：Prop的分隔值清單，以字串表示。</li></ul> |
| `lists` | 对象 | 可擷取最多三個的物件 [清單](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/list.html). 此物件的屬性會加上金鑰 `list1` 至 `list3`. 這些屬性各自包含一個 `list` 陣列 [[!UICONTROL 金鑰值組]](../../data-types/key-value-pair.md) 資料型別。 |
| `props` | 对象 | 擷取最多75個的物件 [prop](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html). 此物件的屬性會加上金鑰 `prop1` 至 `prop75` 和僅接受字串作為其資料型別。 |
| `postalCode` | 字符串 | 使用者端提供的郵遞區號或郵遞區號。 |
| `stateProvince` | 字符串 | 使用者端提供的州或省位置。 |

{style="table-layout:auto"}

## `endUser` {#end-user}

`endUser` 擷取觸發事件之一般使用者的網路互動細節。

![一般使用者欄位](../../images/field-groups/analytics-full-extension/endUser.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `firstWeb` | [[!UICONTROL 網頁資訊]](../../data-types/web-information.md) | 與來自此一般使用者的第一個體驗事件的網頁、連結和反向連結相關的資訊。 |
| `firstTimestamp` | 整数 | 此一般使用者的第一個ExperienceEvent的Unix時間戳記。 |

## `environment` {#environment}

`environment` 擷取有關觸發事件的瀏覽器和作業系統的資訊。

![環境欄位](../../images/field-groups/analytics-full-extension/environment.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `browserIDStr` | 字符串 | 用於瀏覽器的Adobe Analytics識別碼(又稱為 [瀏覽器型別維度](https://experienceleague.adobe.com/docs/analytics/components/dimensions/browser-type.html?lang=zh-Hans))。 |
| `operatingSystemIDStr` | 字符串 | 所用作業系統的Adobe Analytics識別碼(又稱為 [作業系統型別維度](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-system-types.html?lang=zh-Hans))。 |

## 自訂事件欄位 {#events}

Analytics擴充功能欄位群組提供10個物件欄位，可擷取最多100個物件欄位 [自訂事件量度](https://experienceleague.adobe.com/docs/analytics/components/metrics/custom-events.html?lang=zh-Hans) 每個欄位群組，共1000個。

每個頂層事件物件都包含其各自範圍的個別事件物件。 例如， `event101to200` 包含作為輸入碼的事件 `event101` 至 `event200`.

每個偶數物件會使用 [[!UICONTROL 測量]](../../data-types/measure.md) 資料型別，提供唯一識別碼和可量化的值。

![自訂事件欄位](../../images/field-groups/analytics-full-extension/event-vars.png)

## `session` {#session}

`session` 擷取觸發事件的工作階段的相關資訊。

![工作階段欄位](../../images/field-groups/analytics-full-extension/session.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `search` | [[!UICONTROL  搜索]](../../data-types/search.md) | 擷取與工作階段專案的網頁或行動搜尋相關的資訊。 |
| `web` | [[!UICONTROL 網頁資訊]](../../data-types/web-information.md) | 擷取工作階段專案的連結點按次數、網頁詳細資訊、反向連結資訊和瀏覽器詳細資訊。 |
| `depth` | 整数 | 一般使用者目前的作業階段深度（例如頁碼）。 |
| `num` | 整数 | 一般使用者目前的作業階段編號。 |
| `timestamp` | 整数 | 工作階段專案的Unix時間戳記。 |

## 后续步骤

本檔案說明Analytics擴充功能欄位群組的結構和使用案例。 如需欄位群組本身的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

如果您使用此欄位群組來使用Adobe Experience Platform Web SDK收集Analytics資料，請參閱以下指南： [設定資料串流](../../../edge/datastreams/overview.md) 以瞭解如何將資料對應至伺服器端的XDM。
