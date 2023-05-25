---
description: Experience PlatformDestination SDK使用Pebble模板，允许您将从Experience Platform导出的数据转换为目标所需的格式。
title: Destination SDK中支持的转换函数
source-git-commit: ab87a2b7190a0365729ba7bad472fde7a489ec02
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 3%

---


# Destination SDK中支持的转换函数

Experience PlatformDestination SDK使用 [[!DNL Pebble] 模板](https://pebbletemplates.io/)，允许您将从Experience Platform导出的数据转换为目标所需的格式。

Experience Platform [!DNL Pebble] 与提供的现成版本相比，实施有一些变化 [!DNL Pebble]. 此外，除了提供的开箱即用功能外， [!DNL Pebble]，Adobe创建了一些可与Destination SDK一起使用的其他函数。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值包括 **区分大小写**. 为避免区分大小写错误，请完全按照文档中所示使用参数名称和值。

## 使用位置 {#where-to-use}

在以下情况下，请使用本页下面列出的受支持函数 [创建消息转换模板](../../testing-api/streaming-destinations/create-template.md) 从Experience Platform导出到目标的数据。

消息转换模板用于 [目标服务器配置](templating-specs.md) 适用于流式传输目标。

## 先决条件 {#prerequisites}

要了解此参考页面中的概念和函数，请阅读 [消息格式](message-format.md) 文档优先。 您需要了解 [用户档案的结构](message-format.md#profile-structure) 在Experience Platform中，然后才能使用 [!DNL Pebble] 用于转换和导出数据的模板。

在继续使用下面记录的功能之前，请查看部分中的模板示例 [使用模板语言进行身份、属性和区段成员资格转换](message-format.md#using-templating). 这里的示例开始非常简单，复杂性也增加了。

## 支持 [!DNL Pebble] 函数 {#supported-functions}

从 [!DNL Pebble] 标记部分，Destination SDK仅支持：

* [filter](https://pebbletemplates.io/wiki/tag/filter/)
* [for](https://pebbletemplates.io/wiki/tag/for/)
* [如果](https://pebbletemplates.io/wiki/tag/if/)
* [set](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>使用 `for` 迭代时不同 *数组* 或 *映射* 元素之间的关联。 遍历数组时，可以直接获取元素。 循环遍历映射时，将获取每个映射条目，每个条目都有一个键值对。
>
> * 有关数组元素的示例，请考虑以下对象中的标识： [identitymap](message-format.md#identities) 命名空间，您可以在其中循环访问元素，例如 `identityMap.gaid`， `identityMap.email`，或类似内容。
> * 有关映射元素的示例，请考虑 [segmentMembership](message-format.md#segment-membership).


从 [!DNL Pebble] 过滤器部分，Destination SDK支持所有函数。 下面的示例进一步说明了 `date` 函数可在Destination SDK中使用。

从 [!DNL Pebble] 函数部分，Adobe执行 *非* 支持 [范围](https://pebbletemplates.io/wiki/function/range/) 函数。

## 示例 `date` 函数已使用 {#date-function}

举例说明 [!DNL Pebble] 函数在Destination SDK中使用，请参阅下面日期函数的使用方式([Pebble文档的链接](https://pebbletemplates.io/wiki/filter/date/))用于转换时间戳的格式。

### 用例

您希望更改 `lastQualificationTime` 默认时间戳 [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) Experience Platform导出到您的目标首选的其他值的值。

### 示例

#### 输入

```json
{
"lastQualificationTime": "2022-02-08T18:34:24.000+0000"
}
```

#### 格式

```java
{{ lastQualificationTime | date(existingFormat="yyyy-MM-dd'T'HH:mm:sss.SSSX", format="yyyy-MM-dd'T'HH:mm:ssX") }}
```

#### 输出

```json
{
"lastQualificationTime": "2022-02-21T18:34:24Z"
}
```

## Adobe添加的函数 {#functions-added-by-adobe}

除了提供的现成功能外， [!DNL Pebble]，请参阅下面由Adobe创建的其他函数，这些函数可用于数据导出。

### `addedSegments` 和 `removedSegments` 函数 {#addedsegments-removedsegments-functions}

#### 用例

可使用这些函数获取在配置文件中添加或删除的区段的列表。

#### 示例

##### 输入

```json
{
  "identityMap": {
    "myIdNamespace": [
      {
        "id": "external_id1"
      },
      {
        "id": "external_id2"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "111111": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "222222": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      },
      "333333": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      }
    }
  }
}
```

##### 格式

```java
added: {% for s in addedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}; removed: {% for s in removedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}
```

##### 输出

```json
added: <111111><333333>; removed: <222222>
```

<!--

### Added and removed segments filters {#added-and-removed-segmnts-filters}

#### Use case {#use-case}

These filters are similar to `addedSegments` and `removedSegments`, described above. The only difference is that they are implemented as filters as opposed to functions.

#### Example {#example}

##### Input {#input}

```json
{
  "identityMap": {
    "myIdNamespace": [
      {
        "id": "external_id1"
      },
      {
        "id": "external_id2"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "111111": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "222222": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      },
      "333333": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      }
    }
  }
}
```

##### Format {#format}

```java
added: {% for s in input.profile.segmentMembership.ups | added %}<{{s.key}}>{% endfor %};|removed: {% for s in input.profile.segmentMembership.ups | removed %}<{{s.key}}>{% endfor %};
```

##### Output {#output}

```json
added: <111111><333333>;|removed: <222222>;
```

-->

## 后续步骤 {#next-steps}

您现在知道了 [!DNL Pebble] Destination SDK中支持函数，以及如何使用它们调整导出数据的格式以满足您的需求。 接下来，您应该查看以下页面：

* [创建和测试消息转换模板](../../testing-api/streaming-destinations/create-template.md)
* [渲染模板API操作](../../testing-api/streaming-destinations/render-template-api.md)
