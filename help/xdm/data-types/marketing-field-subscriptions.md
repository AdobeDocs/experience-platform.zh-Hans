---
solution: Experience Platform
title: 包含订阅数据类型的一般营销首选项字段
topic-legacy: overview
description: 本文档概述了包含订阅XDM数据类型的通用营销首选项字段。
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
source-git-commit: bccf97d85421fcb2f8fe153ad0ddbef4975b6f7e
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 2%

---

# [!UICONTROL 包含订阅的通用营销首选项字段] 数据类型

[!UICONTROL 包含订阅的通用营销首选项字段] 是一种标准XDM数据类型，用于描述客户对特定营销首选项的选择。

>[!NOTE]
>
>此数据类型旨在用于使用 [[!UICONTROL 同意和首选项] 字段组](../field-groups/profile/consents.md) 作为基线。
>
>如果您不需要 `subscriptions` 映射到特定营销首选项字段时，您可以使用 [基本营销字段数据类型](./marketing-field.md) 中。

![](../images/data-types/marketing-field-subscriptions.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `reason` | 字符串 | 当客户选择退出营销用例时，此字符串字段表示客户选择退出的原因。 |
| `subscriptions` | 地图 | 特定订阅的客户营销偏好图。 请参阅 [订阅](#subscriptions) 以了解更多信息。 |
| `time` | DateTime | 营销首选项更改时的ISO 8601时间戳（如果适用）。 |
| `val` | 字符串 | 客户为此营销用例提供的首选项选择。 请参阅 [下一部分](#val) 以了解接受的值和定义。 |

{style=&quot;table-layout:auto&quot;}

## `val` {#val}

下表概述了 `val`:

| 值 | 标题 | 描述 |
| --- | --- | --- |
| `y` | 是（选择加入） | 客户已选择使用该首选项。 换句话说，他们 **do** 同意使用其数据（如相关首选项所示）。 |
| `n` | 否（选择退出） | 客户已选择退出该首选项。 换句话说，他们 **不** 同意使用其数据（如相关首选项所示）。 |
| `p` | 待验证 | 系统尚未收到最终的偏好值。 这通常用作需要两步验证的同意的一部分。 例如，如果客户选择接收电子邮件，则同意将设置为 `p` 直到他们选择电子邮件中的链接以验证他们提供了正确的电子邮件地址，此时同意将更新为 `y`.<br><br>如果此首选项不使用两套验证过程，则 `p` 相反，可以使用选择指示客户尚未响应同意提示。 例如，您可以自动将值设置为 `p` 在网站的第一页上，客户响应同意提示之前。 在不需要明确同意的司法管辖区中，您还可以使用它来指示客户未明确选择退出（换言之，假设同意）。 |
| `u` | Unknown | 客户的首选项信息未知。 |
| `dy` | 默认为“是”（选择加入） | 客户本身未提供同意值，默认情况下会被视为选择加入（“是”）。 换言之，在客户另有指示之前，会假定客户同意。<br><br>请注意，如果法律或贵公司隐私政策的更改导致某些或所有用户的默认值发生更改，则必须手动更新包含默认值的所有用户档案。 |
| `dn` | 默认为否（选择退出） | 客户本身未提供同意值，默认情况下会被视为选择退出（“否”）。 换言之，假定客户拒绝同意，直到他们另有指示。<br><br>请注意，如果法律或贵公司隐私政策的更改导致某些或所有用户的默认值发生更改，则必须手动更新包含默认值的所有用户档案。 |
| `LI` | 合法利益 | 为特定目的收集和处理这些数据的正当商业利益，超过了这些数据对个人的潜在损害。 |
| `CT` | 合同 | 为达到指定目的而收集数据，是为了履行与个人的合同义务。 |
| `CP` | 遵守法律义务 | 为达到指定目的而收集数据，是为了履行业务的法律义务。 |
| `VI` | 个人的重大利益 | 为了保护个人的重大利益，需要为特定目的收集数据。 |
| `PI` | 公共利益 | 为特定目的收集数据是为了公共利益或行使官方权力而执行一项任务所必需的。 |

{style=&quot;table-layout:auto&quot;}

## `subscriptions` {#subscriptions}

有些企业允许客户选择加入与特定营销渠道关联的不同订阅。 例如，银行公司可能允许客户订阅超支帐户的电话警报，或接收忠诚计划优惠的销售电话。

以下JSON表示电话呼叫营销渠道的营销字段示例，该渠道包含 `subscriptions` 地图。 中的每个键 `subscriptions` 对象表示营销渠道的单个订阅。 反过来，每个订阅都包含一个选择加入值(`val`)。

```json
"email-marketing-field": {
  "val": "y",
  "time": "2019-01-01T15:52:25+00:00",
  "subscriptions": {
    "loyalty-offers": {
      "val": "y",
      "type": "sales",
      "topics": ["discounts", "early-access"],
      "subscribers": {
        "jdoe@example.com": {
          "time": "2019-01-01T15:52:25+00:00",
          "source": "website"
        }
      }
    },
    "newsletters": {
      "val": "y",
      "type": "advertising",
      "topics": ["hardware"],
      "subscribers": {
        "jdoe@example.com": {
          "time": "2021-01-01T08:32:53+07:00",
          "source": "website"
        },
        "tparan@example.com": {
          "time": "2020-02-03T07:54:21+07:00",
          "source": "call center"
        }
      }
    }
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `val` | 的 [同意值](#val) 订购。 |
| `type` | 订阅类型。 这可以是任何描述性字符串，前提是它不超过15个字符。 |
| `topics` | 一组字符串，表示客户订阅的目标区域，可用于发送相关内容。 |
| `subscribers` | 可选的映射类型字段，表示订阅了特定订阅的标识符集（如电子邮件地址或电话号码）。 此对象中的每个键都表示相关的标识符，并包含两个子属性： <ul><li>`time`:身份订阅时的ISO 8601时间戳（如果适用）。</li><li>`source`:订阅者源自的源。 这可以是任何描述性字符串，前提是它不超过15个字符。</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 其他资源

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
