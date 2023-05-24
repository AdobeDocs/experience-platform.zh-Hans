---
title: 廣告詳細資料結構欄位群組
description: 本檔案提供「廣告詳細資料」結構欄位群組的概觀。
exl-id: 25de09bd-eedd-489c-9cd5-8acd0c52ddbe
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 8%

---

# [!UICONTROL 廣告詳細資料] 結構描述欄位群組

[!UICONTROL 廣告詳細資料] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md). 欄位群組提供單一 `advertising` 物件放入結構描述，擷取與廣告曝光、點進和歸因相關的資訊。

![欄位群組結構](../../images/field-groups/advertising-details/structure.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `adAssetReference` | 对象 | 擷取有關廣告的資產資訊。 請參閱 [下方的子區段](#adAssetReference) 以取得此物件結構的詳細資訊。 |
| `adAssetViewDetails` | 对象 | 擷取廣告播放的檢視詳細資料。 請參閱 [下方的子區段](#adAssetViewDetails) 以取得此物件結構的詳細資訊。 |
| `adViewability` | 对象 | 擷取一般使用者看到的曝光次數，例如播放器音量、資料庫版本、視窗狀態和廣告檢視區維度。 請參閱 [下方的子區段](#adViewability) 以取得此物件結構的詳細資訊。 |
| `clicks` | [[!UICONTROL 測量]](../../data-types/measure.md) | 廣告上的點按動作次數。 |
| `completes` | [[!UICONTROL 測量]](../../data-types/measure.md) | 定時媒體資產觀看至完成的次數。 這並不一定表示使用者看完整段影片，因為他們可能略過前面。 |
| `conversions` | [[!UICONTROL 測量]](../../data-types/measure.md) | 預先定義的動作（或動作）觸發效能評估事件的次數。 |
| `federated` | [[!UICONTROL 測量]](../../data-types/measure.md) | 指出體驗事件是否透過資料同盟（例如客戶之間的資料共用）建立。 |
| `firstQuartiles` | [[!UICONTROL 測量]](../../data-types/measure.md) | 數位影片廣告以正常速度播放其長度的25%的次數。 |
| `impressions` | [[!UICONTROL 測量]](../../data-types/measure.md) | 傳送給可能檢視的一般使用者的廣告曝光次數。 |
| `midpoints` | [[!UICONTROL 測量]](../../data-types/measure.md) | 數位影片廣告以正常速度播放其長度的50%的次數。 |
| `starts` | [[!UICONTROL 測量]](../../data-types/measure.md) | 數位視訊廣告開始播放的次數。 |
| `thirdQuartiles` | [[!UICONTROL 測量]](../../data-types/measure.md) | 數位影片廣告以正常速度播放其長度的75%的次數。 |
| `timePlayed` | [[!UICONTROL 測量]](../../data-types/measure.md) | 一般使用者在特定的定時媒體資產上所花費的時間。 |
| `downloadedPlayback` | 布尔值 | 當設定為 `true`，表示點選是由於播放已下載的廣告工作階段所產生。 |

{style="table-layout:auto"}

## `adAssetReference` {#adAssetReference}

此 `adAssetReference` 物件會擷取與廣告相關的資產資訊。

![adAssetReference結構](../../images/field-groups/advertising-details/adAssetReference.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `_dc.title` | 字符串 | 易記且易讀的廣告資產名稱。 |
| `_xmpDM.duration` | 整数 | 資產長度或持續時間（以秒為單位）。 |
| `_id` | 字符串 | 廣告資產的唯一識別碼，位於 [Ad-ID標準](https://datatracker.ietf.org/doc/html/rfc8107). |
| `advertiser` | 字符串 | 广告中展现的产品所属的公司或品牌. |
| `campaign` | 字符串 | 广告营销活动的 ID. |
| `creativeID` | 字符串 | 广告创作的 ID. |
| `creativeURL` | 字符串 | 广告创作的 URL. |
| `placementID` | 字符串 | 广告的版面 ID. |
| `siteID` | 字符串 | 广告网站的 ID. |

{style="table-layout:auto"}

## `adAssetViewDetails` {#adAssetViewDetails}

此 `adAssetViewDetails` 物件會擷取廣告播放的檢視詳細資料。

![adAssetViewDetails結構](../../images/field-groups/advertising-details/adAssetViewDetails.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `adBreak` | [[!UICONTROL 廣告插播]](../../data-types/ad-break.md) | 說明如何將計時廣告插入計時媒體。 |
| `index` | 整数 | 上層廣告插播內的廣告索引。 例如，第一個廣告有索引 `0` 而第二個廣告則有索引 `1`. |
| `playerName` | 字符串 | 负责呈现广告的播放器的名称. |

{style="table-layout:auto"}

## `adViewability` {#adViewability}

此 `adViewability` object會擷取一般使用者看到的曝光次數，例如播放器音量、資料庫版本、視窗狀態和廣告檢視區維度。

![adViewability結構](../../images/field-groups/advertising-details/adViewability.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `implementationDetails` | [[!UICONTROL 实施详细信息]](../../data-types/implementation-details.md) | 用於測量可見度量度的資料庫名稱和版本。 |
| `measuredAdNotVisible` | [[!UICONTROL 測量]](../../data-types/measure.md) | 表示在曝光時由可檢視度資料庫測量出的廣告不可見。 |
| `measuredMuted` | [[!UICONTROL 測量]](../../data-types/measure.md) | 表示廣告在曝光時由可檢視度資料庫測量為靜音。 |
| `unmeasurableIframe` | [[!UICONTROL 測量]](../../data-types/measure.md) | 表示廣告會顯示在非使用中視窗中，由閱聽時間的可檢視度資料庫測量。 |
| `unmeasurableOther` | [[!UICONTROL 測量]](../../data-types/measure.md) | 指出由於iframe內所顯示的廣告，可檢視度資料庫無法正確執行測量。 |
| `viewabilityEligibleImpressions` | [[!UICONTROL 測量]](../../data-types/measure.md) | 使用者透過檢測的可檢視度資料庫對廣告的閱聽。 |
| `viewabilityCompletes` | [[!UICONTROL 測量]](../../data-types/measure.md) | 對於被視為可檢視的一般使用者在可檢視度資料庫完成時的廣告完成度。 |
| `viewableFirstQuartiles` | [[!UICONTROL 測量]](../../data-types/measure.md) | 對於被視為可檢視的一般使用者在可檢視度資料庫播放至第一個四分位時的第一四分位廣告。 |
| `viewableImpressions` | [[!UICONTROL 測量]](../../data-types/measure.md) | 對於被視為可檢視的一般使用者在可檢視度資料庫播放兩秒後對廣告的閱聽。 |
| `viewableMidpoints` | [[!UICONTROL 測量]](../../data-types/measure.md) | 對於被視為可檢視的一般使用者在可檢視度資料庫播放至中點時的廣告中點。 |
| `viewableThirdQuartiles` | [[!UICONTROL 測量]](../../data-types/measure.md) | 對於被視為可檢視的一般使用者在可檢視度資料庫播放至第三個四分位時的第三四分位廣告。 |
| `activeWindow` | 布尔值 | 指出廣告是否顯示在使用者裝置的作用中視窗。 |
| `adHeight` | 整数 | 播放器的垂直畫素數（在執行階段測量）。 如果播放器有額外控制或縮圖，這可能會大於廣告大小。 |
| `adUnitDepth` | 整数 | 發佈者可將廣告單位內嵌於容器(iFrames)中，以限制廣告僅能存取頁面程式碼。 此值說明廣告單位顯示在多少個容器內。 |
| `adWidth` | 整数 | 播放器的水準畫素數（在執行階段測量）。 如果播放器有額外控制或縮圖，這可能會大於廣告大小。 |
| `measurementEligible` | 布尔值 | 廣告是否符合可檢視度測量的資格。 如果單位有受支援的創意格式和標籤型別，廣告即符合資格。 |
| `percentViewable` | 整数 | 測量時被視為可檢視的廣告中的畫素百分比。 |
| `playerVolume` | 整数 | 播放器音量百分比（在執行階段測量），其中 `0` 已設為靜音且 `100` 是最大磁碟區。 |
| `viewable` | 布尔值 | 表示在執行階段是否可檢視廣告。 當顯示廣告的至少50%可見至少一秒時，顯示廣告會被視為可檢視。 當視訊播放至少連續兩秒並看到至少50%的廣告時，視訊廣告會被視為可檢視。 |
| `viewportHeight` | 整数 | 在執行階段測量顯示體驗的視窗垂直大小（畫素）。 若為網頁檢視事件，此值表示瀏覽器檢視區高度。 |
| `viewportWidth` | 整数 | 在執行階段測量顯示體驗的視窗水準大小（畫素）。 若為網頁檢視事件，此值表示瀏覽器檢視區寬度。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-advertising.schema.json).
