---
keywords: Experience Platform；首頁；熱門主題；對應csv；對應csv檔案；將csv檔案對應到xdm；將csv對應到xdm；ui指南；對應程式；對應；資料準備；資料準備；
solution: Experience Platform
title: 使用「資料準備」處理資料格式
description: 本檔案概述在「資料準備」中如何處理不同的資料型別。
exl-id: 4ad253b7-3f83-48cd-9c46-8b5ba627c09e
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 13%

---

# 使用「資料準備」處理資料格式

「資料準備」可以強健地處理擷取到Adobe Experience Platform中的不同格式資料。 本檔案概述使用「資料準備」處理不同資料格式的方式。

## 布林值 {#booleans}

如果來源型別是字串，而目標型別是布林值，資料準備可以自動剖析值並將來源值轉換為布林值。

值 `y`， `yes`， `Y`， `YES`， `on`， `ON`， `true`、和 `TRUE` 會自動剖析為 `true`.

值 `n`， `N`， `no`， `NO`， `off`， `OFF`， `false`、和 `FALSE` 會自動剖析為 `false`.

## 日期 {#dates}

「資料準備」支援日期函式，包括字串和日期時間物件。

### 日期函式格式

date函式會將字串和日期時間物件轉換為ISO 8601格式化的ZonedDateTime物件。

**格式**

```http
date({DATE}, {FORMAT}, {DEFAULT_DATE})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATE}` | 必需。代表日期的字串。 |
| `{FORMAT}` | 可选. 代表來源日期格式的字串。 有關字串格式的更多資訊，請參閱 [日期/時間格式字串區段](#format). |
| `{DEFAULT_DATE}` | 可选. 如果提供的日期為Null，則會傳回預設日期。 |

例如，運算式 `date(orderDate, "yyyy-MM-dd")` 將轉換 `orderDate` 「2020年12月31日」的值轉換為「2020-12-31」的日期時間值。

### 日期函式轉換

當來自傳入資料的字串欄位對應到使用Experience Data Model (XDM)的結構描述中的日期欄位時，應明確提及日期格式。 如果未明確提及，「資料準備」會嘗試透過將輸入資料與以下格式比對來轉換輸入資料。 找到相符的格式後，它將停止評估任何後續格式。

```console
"yyyy-MM-dd HH:mm:ssZ",
"yyyy-MM-dd HH:mm:ss.SSSZ",
"yyyy-MM-dd HH:mm:ss.SSS",
"yyyy-MM-dd'T'HH:mm:ss.SSSX",
"yyyy-MM-dd'T'HH:mm:ss'Z'",
"yyyy-MM-dd",
"yyyy/MM/dd",
"yyyy.MM.dd",
"yyyy-MMM-dd",
"yyyyMMdd",
"MM-dd-yyyy",
"MMddyyyy",
"M/dd/yyyy",
"dd.M.yyyy",
"M/dd/yyyy hh:mm:ss a",
"dd.M.yyyy hh:mm:ss a",
"dd.MMM.yyyy",
"dd-MMM-yyyy"
```

>[!IMPORTANT]
>
> 「資料準備」會儘可能將字串轉換為日期。 不過，這些轉換可能會導致不良的結果。 例如，字串值「12112020」符合模式「MMddyyyy」，但使用者可能希望以模式「ddMMyyyy」讀取日期。 因此，使用者應明確提及字串的日期格式。

### 日期/時間格式字串 {#format}

下表顯示已為格式字串定義哪些圖樣字母。 請注意，字母區分大小寫。

| 符號 | 含义 | 演示文稿 | 示例 |
| ------ | ------- | ------------ | ------- |
| G | 時代 | 文本 | AD； Anno Domini； A |
| Y | 年，根據ISO周 | 数值 | 1996; 96 |
| y | 年 | 数值 | 2004; 04 |
| M/L | 月份 | 數字/文字 | 7；07；7月；7月；J |
| w | 一年中的周 | 数值 | 27 |
| W | 當月第幾週 | 数值 | 3 |
| D | 一年當中的第幾天 | 数值 | 189 |
| d | 日期 | 数值 | 10 |
| F | 一個月中的星期幾 | 数值 | 2 |
| E | 一週中某天的名稱 | 文本 | 星期二；星期二 |
| u | 星期幾（以數字表示）。 1代表星期一， ...， 7代表星期日 | 数值 | 1 |
| a | AM/PM標籤 | 文本 | 下午 |
| H | 一天中的小時(0-23) | 数值 | 0 |
| k | 一天中的小時(1-24) | 数值 | 24 |
| K | 上午/下午的小時(0-11) | 数值 | 0 |
| h | 上午/下午的小時(1-12) | 数值 | 12 |
| m | 一小時中的分鐘 | 数值 | 38 |
| s | 一分鐘中的秒 | 数值 | 44 |
| S | 毫秒 | 数值 | 245 |
| z | 时区 | 一般時區 | 太平洋標準時間；PST；GMT-08:00 |
| Z | 时区 | rfc 822時區 | -0800 |
| X | 时区 | iso 8601時區 | -08; -0800; -08:00 |
| V | 時區ID | 文本 | 美洲/洛杉磯 |
| O | 時區位移 | 文本 | GMT+8 |
| Q/q | 季別 | 數字/文字 | 第3季；第3季；03；第3季 |

## 地图 {#maps}

地圖目前不支援 [!DNL Data Prep].
