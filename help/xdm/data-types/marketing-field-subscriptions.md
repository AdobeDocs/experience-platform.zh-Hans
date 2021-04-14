---
solution: Experience Platform
title: 具有订阅数据类型的通用营销首选项字段
topic: 概述
description: 此文档概述了具有订阅XDM数据类型的“通用营销首选项”字段。
translation-type: tm+mt
source-git-commit: 8c5ab298bad69305358ae961ebaf7836a90a0eaa
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 2%

---


# [!UICONTROL Generic Marketing Preference Field with Subscriptions] 数据类型

[!UICONTROL Generic Marketing Preference Field with Subscriptions] 是一种标准XDM数据类型，用于描述客户针对特定营销首选项的选择。

>[!NOTE]
>
>此模式类型旨在用于使用[[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)] mixin](../mixins/profile/consents.md)作为基线来自定义组织的同意的结构。
>
>如果您不需要特定营销首选项字段的`subscriptions`映射，则可以改用[基本营销字段数据类型](./marketing-field.md)。

![](../images/data-types/marketing-field-subscriptions.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `reason` | 字符串 | 当客户选择退出营销用例时，此字符串字段表示客户选择退出的原因。 |
| `subscriptions` | 地图 | 特定订阅的客户营销偏好图。 有关详细信息，请参阅[订阅](#subscriptions)中的一节。 |
| `time` | DateTime | 市场营销首选项更改时的ISO 8601时间戳（如果适用）。 |
| `val` | 字符串 | 客户为此营销用例提供的首选项选择。 请参见[下一节](#val)了解已接受的值和定义。 |

## `val` {#val}

下表概述了`val`的已接受值：

| 值 | 标题 | 描述 |
| --- | --- | --- |
| `y` | 是 | 客户已选择此首选项。 换句话说，他们&#x200B;**do**&#x200B;同意使用其数据，如有关偏好所示。 |
| `n` | 否 | 客户已选择退出此首选项。 换句话说，他们&#x200B;**不**&#x200B;同意使用其数据，如有关偏好所示。 |
| `p` | 待验证 | 系统尚未收到最终的偏好值。 这通常是需要两步核查的同意的一部分。 例如，如果客户选择接收电子邮件，则该同意将设置为`p`，直到他们选择电子邮件中的链接以验证他们提供了正确的电子邮件地址，此时该同意将更新为`y`。<br><br>如果此首选项不使用两组验证过程，则 `p` 该选择可用于指示客户尚未响应同意提示。例如，您可以在客户响应同意提示之前，在网站的第一页自动将值设置为`p`。 在不需要明确同意的司法管辖区，您还可以使用它指示客户未明确选择退出（即假定客户同意）。 |
| `u` | Unknown | 客户的偏好信息未知。 |
| `LI` | 合法利益 | 为特定目的收集和处理这些数据的合法商业利益超过数据对个人的潜在伤害。 |
| `CT` | 合同 | 为达到指定目的而收集数据，是为了履行与个人的合同义务。 |
| `CP` | 遵守法律义务 | 为达到特定目的而收集数据，是为了履行业务的法律义务。 |
| `VI` | 个人的切身利益 | 为了保护个人的切身利益，需要为特定目的收集数据。 |
| `PI` | Public Interest | 为特定目的收集数据，是为了公共利益或行使官方权力而进行任务。 |

## `subscriptions` {#subscriptions}

某些企业允许客选择加入户访问与特定营销渠道关联的不同订阅。 例如，银行公司可能允许客户订阅超支帐户的电话提醒，或接收忠诚项目优惠的销售呼叫。

以下JSON代表包含`subscriptions`映射的电话呼叫营销渠道的示例营销字段。 `subscriptions`对象中的每个键代表营销渠道的单个订阅。 反过来，每个订阅都包含一个选择加入值(`val`)。

```json
"phone-marketing-field": {
  "val": "y",
  "time": "2019-01-01T15:52:25+00:00",
  "subscriptions": {
    "loyalty-offers": {
      "val": "y",
      "type": "sales",
      "subscribers": {
        "123-555-0928": {
          "time": "2019-01-01T15:52:25+00:00",
          "source": "website"
        }
      }
    },
    "overdrawn-account": {
      "val": "y",
      "type": "issues",
      "subscribers": {
        "123-555-0928": {
          "time": "2021-01-01T08:32:53+07:00",
          "source": "website"
        },
        "301-555-1527": {
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
| `type` | 订阅类型。 这可以是任何描述性字符串，前提是该字符串不超过15个字符。 |
| `subscribers` | 可选的映射类型字段，表示订阅特定订阅的一组标识符（例如电子邮件地址或电话号码）。 此对象中的每个键都表示有关的标识符，并包含两个子属性： <ul><li>`time`:身份订阅时的ISO 8601时间戳（如果适用）。</li><li>`source`:用户源的源。这可以是任何描述性字符串，前提是该字符串不超过15个字符。</li></ul> |

## 其他资源

有关数据类型的详细信息，请参阅公共XDM存储库：

* [已填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)