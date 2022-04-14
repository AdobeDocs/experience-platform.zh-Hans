---
description: Experience PlatformDestination SDK使用Pebble模板，允许您将从Experience Platform导出的数据转换为目标所需的格式。
title: 支持的转换函数Destination SDK
source-git-commit: 840404741da06ba1593b227c7d6ba459b5f43110
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 3%

---

# 支持的转换函数Destination SDK

## 概述 {#overview}

Experience PlatformDestination SDK使用 [[!DNL Pebble] 模板](https://pebbletemplates.io/)，允许您将从Experience Platform导出的数据转换为目标所需的格式。

Experience Platform [!DNL Pebble] 与提供的现成版本相比，实施有一些变化 [!DNL Pebble]. 此外，除了 [!DNL Pebble]，则Adobe已创建了一些其他函数，您可以将其与Destination SDK结合使用。

## 使用位置 {#where-to-use}

在 [创建消息转换模板](./create-template.md) 用于导出到目标的非Experience Platform数据。 在 [目标服务器配置](./server-and-template-configuration.md) 用于流目标。

## 先决条件 {#prerequisites}

要了解此参考页面中的概念和函数，请阅读 [消息格式](/help/destinations/destination-sdk/message-format.md) 文档。 您需要了解 [轮廓结构](/help/destinations/destination-sdk/message-format.md#profile-structure) Experience Platform [!DNL Pebble] 转换和导出数据的模板。

在前进到下面介绍的功能之前，请查看部分中的模板示例 [对身份、属性和区段成员资格转换使用模板语言](/help/destinations/destination-sdk/message-format.md#using-templating). 其中的示例开始非常简单，而且复杂性也增加了。

## 支持 [!DNL Pebble] 函数 {#supported-functions}

从 [!DNL Pebble] 标记部分，Destination SDK仅支持：
* [filter](https://pebbletemplates.io/wiki/tag/filter/)
* [for](https://pebbletemplates.io/wiki/tag/for/)
* [if](https://pebbletemplates.io/wiki/tag/if/)
* [set](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>使用 `for` 在迭代时不同 *阵列* 或 *地图* 模板中的元素。 遍历数组时，可以直接获取元素。 遍历映射时，将获取每个映射条目，该条目具有键值对。
>
> * 有关数组元素的示例，请考虑 [identityMap](./message-format.md#identities) namespace，您可以在其中遍历元素，例如 `identityMap.gaid`, `identityMap.email`、或类似。
> * 有关映射元素的示例，请考虑 [segmentMembership](./message-format.md#segment-membership).


从 [!DNL Pebble] 过滤器部分，Destination SDK支持所有函数。 以下进一步示例显示 `date` 函数。

从 [!DNL Pebble] 函数部分，Adobe执行 *not* 支持 [范围](https://pebbletemplates.io/wiki/function/range/) 函数。

## 示例 `date` 函数 {#date-function}

以说明如何 [!DNL Pebble] 函数在Destination SDK中使用，请参阅下面日期函数([Pebble文档中的链接](https://pebbletemplates.io/wiki/filter/date/))来转换时间戳的格式。

### 用例

要更改 `lastQualificationTime` 默认时间戳 [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) 值。

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

## 按Adobe添加的函数 {#functions-added-by-adobe}

除了 [!DNL Pebble]，请参阅下面的Adobe创建的其他函数，这些函数可用于数据导出。

### `addedSegments` 和 `removedSegments` 函数 {#addedsegments-removedsegments-functions}

#### 用例

这些函数可用于获取已添加到配置文件或从配置文件中删除的区段列表。

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

你现在知道 [!DNL Pebble] Destination SDK中支持函数，以及如何使用函数调整导出数据的格式以符合您的需要。 接下来，您应该查看以下页面：

* [创建和测试消息转换模板](/help/destinations/destination-sdk/create-template.md)
* [渲染模板API操作](/help/destinations/destination-sdk/render-template-api.md)