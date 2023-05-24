---
keywords: Experience Platform；首頁；熱門主題；結構描述；結構描述；欄位群組；欄位群組；欄位群組；資料型別；資料型別；資料型別；結構描述設計；資料型別；資料型別；資料型別；資料型別；結構描述；結構描述；結構描述設計；結構描述設計；對應；對應；
solution: Experience Platform
title: XDM欄位型別限制
description: Experience Data Model (XDM)中欄位型別限制的參考，包括它們可以對應的其他序列化格式，以及如何在API中定義自己的欄位型別。
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 4%

---

# XDM欄位型別限制

在Experience Data Model (XDM)結構描述中，欄位的型別會限制欄位可以包含哪種資料。 本檔案提供每個核心欄位型別的概觀，包括它們可以對應的其他序列化格式，以及如何在API中定義自己的欄位型別，以強制執行不同的限制。

## 快速入门

在使用本指南之前，請檢閱 [結構描述組合基本概念](./composition.md) 以瞭解XDM結構描述、類別和結構描述欄位群組。

如果您打算在API中定義自己的欄位型別，強烈建議您從 [Schema Registry開發人員指南](../api/getting-started.md) 瞭解如何建立欄位群組和資料型別，以將您的自訂欄位納入。 如果您使用Experience PlatformUI建立方案，請參閱以下指南： [在UI中定義欄位](../ui/fields/overview.md) 瞭解如何在自訂欄位群組和資料型別中定義的欄位上實作限制。

## 基底結構和範例 {#basic-types}

XDM是以JSON結構描述為基礎建立，因此XDM欄位在定義其型別時繼承類似的語法。 瞭解不同欄位型別在JSON結構描述中的呈現方式，有助於指出每個型別的基本限制。

>[!NOTE]
>
>請參閱 [API基礎指南](../../landing/api-fundamentals.md#json-schema) 以進一步瞭解JSON結構描述和平台API中的其他基礎技術。

下表概述每個XDM型別在JSON結構描述中的表示方式，以及符合型別的範例值：

<table style="table-layout:auto">
  <thead>
    <tr>
      <th>XDM型別</th>
      <th>JSON結構描述</th>
      <th>示例</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>[！UICONTROL字串]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type"： "string"}</pre>
      </td>
      <td><code>"Platinum"</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL雙精度]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type"： "number"}</pre>
      </td>
      <td><code>12925.49</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL Long]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type"： "integer"， "maximum"： 9007199254740991， "minimum"： -9007199254740991 }</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL整數]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type"： "integer"， "maximum"： 2147483648， "minimum"： -2147483648 }</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL Short]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type"： "integer"， "maximum"： 32768， "minimum"： -32768 }</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL位元組]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type"： "integer"， "maximum"： 128， "minimum"： -128 }</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL日期]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type"： "string"， "format"： "date" }</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL日期時間]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type"： "string"， "format"： "date-time" }</pre>
      </td>
      <td><code>"2019-05-15T20:20:39+00:00"</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL布林值]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type"： "string"}</pre>
      </td>
      <td><code>true</code></td>
    </tr>
  </tbody>
</table>

**所有日期格式字串都必須符合ISO 8601標準([RFC 3339,5.6節](https://tools.ietf.org/html/rfc3339#section-5.6))。*

## 將XDM型別對應到其他格式

以下各節說明每個XDM型別如何對應到其他常見的序列化格式：

* [Parquet、Spark SQL和Java](#parquet)
* [Scala、.NET和CosmosDB](#scala)
* [MongoDB、Arospike和Protobuf 2](#mongo)

>[!NOTE]
>
>在下表中列出的標準XDM型別中， [!UICONTROL 地圖] 也包含型別。 當資料以對應到特定值的索引鍵表示，或索引鍵無法合理地包含在靜態結構描述中且必須被視為資料值時，標準結構描述中就會使用對應。
>
>許多標準XDM元件都使用對應型別，您也可以 [定義自訂對應欄位](../tutorials/custom-fields-api.md#custom-maps) 視需要而定。 下表包含對應型別，旨在協助您決定如何將現有資料對應至XDM （如果目前儲存在下列任何格式中）。

### Parquet、Spark SQL和Java {#parquet}

| XDM型別 | Parquet | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL 字符串] | 型別： `BYTE_ARRAY`<br>註解： `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL 双精度] | 类型：`DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL 長] | 类型：`INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL 整数] | 型別： `INT32`<br>註解： `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL 短] | 型別： `INT32`<br>註解： `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL 位元組] | 型別： `INT32`<br>註解： `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL 日期] | 型別： `INT32`<br>註解： `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL 日期時間] | 型別： `INT64`<br>註解： `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL 布尔型] | 类型：`BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL 地图] | `MAP`-annotated group<br><br>(`<key-type>` 必須是 `STRING`) | `MapType`<br><br>(`keyType` 必須是 `StringType`) | `java.util.Map` |

{style="table-layout:auto"}

### Scala、.NET和CosmosDB {#scala}

| XDM型別 | Scala | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL 字符串] | `String` | `System.String` | `String` |
| [!UICONTROL 双精度] | `Double` | `System.Double` | `Number` |
| [!UICONTROL 長] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL 整数] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL 短] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL 位元組] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL 日期] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL 日期時間] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL 布尔型] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL 地图] | `Map` | (不适用) | `object` |

{style="table-layout:auto"}

### MongoDB、Arospike和Protobuf 2 {#mongo}

| XDM型別 | MongoDB | 塞式飛行器 | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL 字符串] | `string` | `String` | `string` |
| [!UICONTROL 双精度] | `double` | `Double` | `double` |
| [!UICONTROL 長] | `long` | `Integer` | `int64` |
| [!UICONTROL 整数] | `int` | `Integer` | `int32` |
| [!UICONTROL 短] | `int` | `Integer` | `int32` |
| [!UICONTROL 位元組] | `int` | `Integer` | `int32` |
| [!UICONTROL 日期] | `date` | `Integer`<br>（Unix毫秒） | `int64`<br>（Unix毫秒） |
| [!UICONTROL 日期時間] | `timestamp` | `Integer`<br>（Unix毫秒） | `int64`<br>（Unix毫秒） |
| [!UICONTROL 布尔型] | `bool` | `Integer`<br>（0/1二進位） | `bool` |
| [!UICONTROL 地图] | `object` | `map` | `map<key_type, value_type>` |

{style="table-layout:auto"}

## 在API中定義XDM欄位型別 {#define-fields}

Schema Registry API可讓您透過使用格式和選擇性限制來定義自訂欄位。 請參閱指南： [定義結構描述登入API中的自訂欄位](../tutorials/custom-fields-api.md) 以取得詳細資訊。
