---
title: 在Reactor API中篩選回應
description: 瞭解在Reactor API中列出資源時如何篩選結果。
exl-id: 8a91f3dd-4ead-4a10-abb1-e71acb0d73b6
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 1%

---

# 在Reactor API中篩選回應

在Reactor API中使用清單(GET)端點時，您可能會發現有必要將傳回的結果限製為記錄子集。 為了完成這點，許多API的清單端點都支援依特定屬性篩選的功能。 如果您想改向API提出結構化查詢，請參閱以下指南： [搜尋](./search.md).

## 篩選語法

以下範例說明如何為GET請求實作篩選器。

**API格式**

若要篩選指定清單端點的回應，您必須提供 `filter` 請求路徑中的查詢引數。

>[!NOTE]
>
>下面的範本使用方括弧(`[]`)和空格字元來增加可讀性。 實際上，這些字元必須是URI編碼，如中所述 [RFC 3986](https://tools.ietf.org/html/rfc3986). 本指南稍後會顯示正確編碼的請求路徑的範例。
>
>請注意，如果篩選器的結構不正確，則不會套用任何篩選器並傳回完整結果集。

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE}
```

| 属性 | 描述 |
| --- | --- |
| `{ENDPOINT}` | Reactor API中支援篩選引數的清單端點。 |
| `{ATTRIBUTE_NAME}` | 篩選結果所依據的特定屬性的名稱。 請記住，不同的端點支援不同的篩選屬性。 如需可用篩選屬性的清單，請參閱您正在使用的端點的參考指南。 |
| `{OPERATOR}` | 決定如何根據提供的評估結果的運運算元 `{VALUE}`. 支援的運運算元列於 [附錄部分](#supported-operators). |
| `{VALUE}` | 用來比較傳回結果的值。 使用比較相等時 `EQ` 運運算元，值必須是完全相符且區分大小寫的專案，才能包含在回應中。 |

{style="table-layout:auto"}

**请求**

以下範例請求會套用篩選器（需要程式庫的），以擷取已發佈程式庫的清單 `state` 屬性等於 `published`.

在URI編碼之前，請求路徑中此篩選器的語法如下所示：

`https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter[state]=EQ published`

路徑和查詢引數經過URI編碼後，便可用於API請求，如下所示：

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter%5Bstate%5D=EQ%20published \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

## 篩選多個值 {#multiple-values}

若要依單一屬性的多個值篩選，請以逗號分隔清單的形式提供這些值。

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE_1},{VALUE_2}
```

## 使用多個篩選器

若要套用多個屬性的篩選器，請提供 `filter` 每個屬性的引數。 引數必須以&amp;符號分隔(`&`)個字元。

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME_1}]={OPERATOR} {VALUE}&filter[{ATTRIBUTE_NAME_2}]={OPERATOR} {VALUE}
```

>[!NOTE]
>
>如果您在相同要求的多個篩選條件中指定相同的屬性，則只會套用最後為該屬性提供的篩選條件。

## 附录

下節包含在Reactor API中使用篩選器的其他資訊。

### 支援的篩選器運運算元 {#operators}

下表列出篩選引數支援的運運算元值。 請記住，根據您篩選依據的屬性，並非所有可用的篩選運運算元都適用，例如對字串屬性使用「小於」或「大於」運運算元。

| 操作员 | 描述 |
| --- | --- |
| `EQ` | 屬性必須等於提供的值。 |
| `NOT` | 屬性不得等於提供的值。 |
| `LT` | 屬性必須小於提供的值。 |
| `GT` | 屬性必須大於提供的值。 |
| `BETWEEN` | 屬性必須落在指定的值範圍內。 使用此運運算元時， [兩個值](#multiple-values) 必須提供以指示所需範圍的最小值和最大值。 |
| `CONTAINS` | 屬性必須包含提供的值，例如字串屬性中的一組字元。 |
