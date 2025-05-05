---
description: Experience PlatformDestination SDK使用Pebble模板，允许您将从Experience Platform导出的数据转换为目标所需的格式。
title: Destination SDK中支持的转换函数
exl-id: 36f761c7-9d76-41fe-b05f-d4cad655ddd2
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 2%

---

# Destination SDK中支持的转换函数

Experience PlatformDestination SDK使用[[!DNL Pebble] 模板](https://pebbletemplates.io/)，允许您将从Experience Platform导出的数据转换为目标所需的格式。

与[!DNL Pebble]提供的现成版本相比，Experience Platform[!DNL Pebble]实现有一些更改。 此外，除了[!DNL Pebble]提供的现成函数之外，Adobe还创建了一些可与Destination SDK一起使用的其他函数。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值均区分大小写&#x200B;**&#x200B;**。 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 使用位置 {#where-to-use}

为从Experience Platform导出到目标的数据创建消息转换模板[&#128279;](../../testing-api/streaming-destinations/create-template.md)时，请使用此页上下面列出的受支持的函数。

消息转换模板在流目标的[目标服务器配置](templating-specs.md)中使用。

## 先决条件 {#prerequisites}

要了解此参考页中的概念和函数，请先阅读[消息格式](message-format.md)文档。 您需要先了解Experience Platform中配置文件[&#128279;](message-format.md#profile-structure)的结构，然后才能使用[!DNL Pebble]模板转换和导出的数据。

在继续使用下面记录的功能之前，请查看[使用模板语言进行标识、属性和受众成员资格转换](message-format.md#using-templating)一节中的模板化示例。 这里的示例开始非常简单，复杂性也增加了。

## 支持的[!DNL Pebble]函数 {#supported-functions}

在[!DNL Pebble]标记部分中，Destination SDK仅支持：

* [筛选器](https://pebbletemplates.io/wiki/tag/filter/)
* [&#128279;](https://pebbletemplates.io/wiki/tag/for/)的
* [if](https://pebbletemplates.io/wiki/tag/if/)
* [设置](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>在模板中迭代使用&#x200B;*数组*&#x200B;或&#x200B;*映射*&#x200B;元素时，使用`for`是不同的。 循环访问数组时，可以直接获取元素。 循环访问映射时，将获得每个映射项，每个映射项都有一个键值对。
>
> * 有关数组元素的示例，请考虑[identityMap](message-format.md#identities)命名空间中的标识，在该命名空间中，您可以对`identityMap.gaid`、`identityMap.email`等元素进行迭代。
> * 有关映射元素的示例，请考虑[segmentMembership](message-format.md#segment-membership)。

从[!DNL Pebble]筛选器部分中，Destination SDK支持所有函数。 下面的进一步示例说明如何在Destination SDK中使用`date`函数。

在[!DNL Pebble]函数部分中，Adobe *不*&#x200B;支持[范围](https://pebbletemplates.io/wiki/function/range/)函数。

## 如何使用`date`函数的示例 {#date-function}

若要举例说明[!DNL Pebble]函数在Destination SDK中的使用方式，请参阅下面如何使用日期函数（[链接，位于Pebble文档](https://pebbletemplates.io/wiki/filter/date/)中）转换时间戳的格式。

### 用例

您想要将`lastQualificationTime`时间戳从Experience Platform导出的默认[ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)值更改为目标首选的其他值。

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

除了[!DNL Pebble]提供的现成函数之外，请参阅下面的Adobe创建的其他函数，这些函数可用于数据导出。

### `addedSegments`和`removedSegments`函数 {#addedsegments-removedsegments-functions}

#### 用例

可以使用此函数来获取在配置文件中添加或删除的受众列表。

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

### Added and removed audiences filters {#added-and-removed-segmnts-filters}

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

您现在知道Destination SDK支持哪些[!DNL Pebble]函数，以及如何使用它们调整导出数据的格式以满足您的需求。 接下来，您应该查看以下页面：

* [创建和测试消息转换模板](../../testing-api/streaming-destinations/create-template.md)
* [呈现模板API操作](../../testing-api/streaming-destinations/render-template-api.md)
