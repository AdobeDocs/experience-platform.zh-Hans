---
keywords: Experience Platform；配置文件；实时客户配置文件；疑难解答；API；同意；同意；首选项；首选项；privacyOptOuts；marketingPreferences；optOutType；basisOfProcessing；同意；同意
title: 同意和偏好设置数据类型
description: “隐私同意、个性化和营销偏好设置”数据类型旨在支持从您的数据操作中收集由同意管理平台(CMP)和其他源生成的客户权限和偏好设置。
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '2034'
ht-degree: 1%

---

# [!UICONTROL 同意和偏好设置] 数据类型

此 [!UICONTROL 隐私、个性化和营销偏好设置的同意] 数据类型(以下简称“ ”[!UICONTROL 同意和偏好设置] 数据类型”)是 [!DNL Experience Data Model] (XDM)数据类型，旨在支持从您的数据操作中收集由同意管理平台(CMP)和其他源生成的客户权限和偏好设置。

本文档介绍了提供的字段的结构和预期用途。 [!UICONTROL 同意和偏好设置] 数据类型。

## 先决条件 {#prerequisites}

本文档要求您对XDM和中的架构的使用有一定的了解 [!DNL Experience Platform]. 请在继续之前查看以下文档：

* [XDM 系统概述](https://www.adobe.com/go/xdm-home-en)
* [模式组合基础](https://www.adobe.com/go/xdm-schema-best-practices-en)

## 数据类型结构 {#structure}

>[!IMPORTANT]
>
>此 [!UICONTROL 同意和偏好设置] 数据类型旨在涵盖一系列同意和偏好管理用例。 因此，本文档以一般术语说明了数据类型字段的使用，并仅就应如何解释这些字段的使用提出建议。 请咨询您的隐私法律团队，以使数据类型结构符合您的组织如何解释并向您的客户展示这些同意和偏好设置选择。

此 [!UICONTROL 同意和偏好设置] 数据类型提供了多个用于捕获的字段 **同意** 和 **偏好设置** 信息。

同意是一个选项，允许客户指定如何使用其数据。 大多数同意书都有一个法律含义，即有些司法管辖区要求先获得许可，数据才能以特定方式使用，或者如果不需要肯定性同意，则要求客户可以选择停止使用（选择退出）。

首选项是一个选项，允许客户指定如何处理其品牌体验的不同方面。 这些规则分为两类：

* **个性化偏好设置**：有关品牌应如何个性化向客户提供体验的首选项。
* **营销偏好设置**：有关品牌是否允许通过各种渠道联系客户的首选项。

以下屏幕截图显示了数据类型的结构在Platform UI中的表示方式：

![](../images/data-types/consents.png)

>[!TIP]
>
>请参阅指南，网址为 [探索XDM资源](../ui/explore.md) 有关如何在Platform UI中查找任何XDM资源并检查其结构的步骤，请参见。

以下JSON显示了以下数据类型的示例： [!UICONTROL 同意和偏好设置] 数据类型可以处理。 以下各节提供了有关每个字段的特定用法的信息。

```json
{
  "consents": {
    "collect": {
      "val": "VI",
    },
    "adID": {
      "idType": "IDFA",
      "val": "y"
    },
    "share": {
      "val": "y",
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "u"
      },
      "push": {
        "val": "n",
        "reason": "Too Frequent",
        "time": "2019-01-01T15:52:25+00:00"
      }
    },
    "metadata": {
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

>[!TIP]
>
>您可以为在Experience Platform中定义的任何XDM架构生成示例JSON数据，以帮助可视化应如何映射客户同意和偏好设置数据。 有关更多信息，请参阅以下文档：
>
>* [在UI中生成示例数据](../ui/sample.md)
>* [在API中生成示例数据](../api/sample-data.md)


## `consents` {#choices}

`consents` 包含多个描述客户同意和偏好设置的字段。 以下各小节将更详细地描述这些字段。

```json
"consents": {
  "collect": {
    "val": "VI",
  },
  "adID": {
    "idType": "IDFA",
    "val": "y"
  },
  "share": {
    "val": "y",
  },
  "personalize": {
    "content": {
      "val": "y"
    }
  },
  "marketing": {
    "preferred": "email",
    "any": {
      "val": "u"
    },
    "email": {
      "val": "n",
      "reason": "Too Frequent",
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

### `collect`

`collect` 表示客户同意收集其数据。

```json
"collect": {
  "val": "y"
}
```

| 属性 | 描述 |
| --- | --- |
| `val` | 此用例的客户提供的同意选择。 请参阅 [附录](#choice-values) 以获取接受的值和定义。 |

{style="table-layout:auto"}

### `adID`

`adID` 表示客户同意是否可以使用广告商ID在此设备上跨应用程序链接客户。

```json
"adID": {
  "idType": "IDFA",
  "val": "y"
}
```

| 属性 | 描述 |
| --- | --- |
| `idType` | 广告ID类型： `IDFA` 广告商的Apple ID或 `GAID` Google (也称为Android广告商ID (AAID))的信息。 |
| `val` | 此用例的客户提供的同意选择。 请参阅 [附录](#choice-values) 以获取接受的值和定义。 |

{style="table-layout:auto"}

### `share`

`share` 表示客户同意其数据可以与第二方或第三方共享（或出售给）。

```json
"share": {
  "val": "y"
}
```

| 属性 | 描述 |
| --- | --- |
| `val` | 此用例的客户提供的同意选择。 请参阅 [附录](#choice-values) 以获取接受的值和定义。 |

{style="table-layout:auto"}

### `personalize` {#personalize}

`personalize` 捕获客户对其数据可用于个性化的方式的偏好。 客户可以选择退出特定的个性化用例，或完全选择退出个性化。

>[!IMPORTANT]
>
>`personalize` 不包括营销用例。 例如，如果客户选择不对所有渠道进行个性化，则他们不应停止通过这些渠道接收通信。 相反，他们收到的消息应该是通用的，而不是基于其用户档案。
>
>同一，如果客户选择不进行所有渠道的直接营销(通过 `marketing`，在中说明 [下一节](#marketing))，则即使允许个性化，该客户也不应收到任何消息。

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `content` | 表示客户对您的网站或应用程序上的个性化内容的偏好。 |
| `val` | 指定用例的客户提供的个性化偏好设置。 如果不必提示客户提供同意，则此字段的值应指示进行个性化的基础。 请参阅 [附录](#choice-values) 以获取接受的值和定义。 |

{style="table-layout:auto"}

### `marketing` {#marketing}

`marketing` 捕获客户关于其数据可用于哪些营销目的的偏好。 客户可以选择退出特定的营销用例，或完全选择退出直接营销。

```json
"marketing": {
  "preferred": "email",
  "any": {
    "val": "u"
  },
  "email": {
    "val": "n",
    "reason": "Too Frequent"
  },
  "push": {
    "val": "y"
  },
  "sms": {
    "val": "y"
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `preferred` | 指示客户接收通信的首选渠道。 请参阅 [附录](#preferred-values) 以获取接受的值。 |
| `any` | 表示客户对整个直接营销的偏好。 此字段中提供的同意首选项被视为任何营销渠道的“默认”首选项，除非被下提供的其他子字段覆盖 `marketing`. 如果您计划使用更细粒度的同意选项，建议您排除此字段。<br><br>如果该值设置为 `n`，则所有更具体的个性化设置都应忽略。 如果该值设置为 `y`，则所有细粒度个性化选项也应视为 `y`，除非明确设置为 `n`. 如果未设置该值，则每个个性化选项的值都应按指定接受。 |
| `email` | 指示客户是否同意接收电子邮件。 |
| `push` | 指示客户是否允许接收推送通知。 |
| `sms` | 指示客户是否同意接收短信。 |
| `val` | 客户提供的指定用例的偏好设置。 如果不必提示客户提供同意，则此字段的值应指示进行营销用例的基础。 请参阅 [附录](#choice-values) 以获取接受的值和定义。 |
| `time` | 营销偏好设置更改时间的ISO 8601时间戳（如果适用）。 请注意，如果任何单个首选项的时间戳与下提供的时间戳相同 `metadata`，则不会为该首选项设置此字段。 |
| `reason` | 当客户选择退出营销用例时，此字符串字段表示客户选择退出的原因。 |

{style="table-layout:auto"}

### `metadata`

`metadata` 捕获有关客户同意和偏好设置的一般元数据（只要上次更新它们）。

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| 属性 | 描述 |
| --- | --- |
| `time` | 上次更新任何客户同意和偏好设置的ISO 8601时间戳。 此字段可用于代替向单个首选项应用时间戳，以减少负载和复杂性。 提供 `time` 单个首选项下的值将覆盖 `metadata` 该特定首选项的时间戳。 |

{style="table-layout:auto"}

## 使用数据类型引入数据 {#ingest}

要使用 [!UICONTROL 同意和偏好设置] 数据类型要从客户那里摄取同意数据，您必须根据包含该数据类型的架构创建一个数据集。

请参阅上的教程 [在UI中创建架构](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) 有关如何向字段分配数据类型的步骤。 创建包含字段的架构后，使用 [!UICONTROL 同意和偏好设置] 数据类型，请参阅 [创建数据集](../../catalog/datasets/user-guide.md#create) 在数据集用户指南中，按照使用现有架构创建数据集的步骤进行操作。

>[!IMPORTANT]
>
>如果要将同意数据发送到 [!DNL Real-Time Customer Profile]，您需要创建 [!DNL Profile] — 启用的架构基于 [!DNL XDM Individual Profile] 包含 [!UICONTROL 同意和偏好设置] 数据类型。 您基于该架构创建的数据集也必须启用 [!DNL Profile]. 有关以下内容的特定步骤，请参阅以上链接的教程 [!DNL Real-Time Customer Profile] 架构和数据集的要求。
>
>此外，还必须确保将合并策略配置为优先考虑包含最新同意和偏好设置数据的数据集，以便正确更新客户配置文件。 请参阅概述，位于 [合并策略](../../rtcdp/profile/merge-policies.md) 了解更多信息。

## 处理同意和偏好设置更改

当客户在您的网站上更改其同意或偏好设置时，应使用收集这些更改并立即实施 [Adobe Experience Platform Web SDK](../../edge/consent/supporting-consent.md). 如果客户选择退出数据收集，则必须立即停止所有数据收集。 如果客户选择退出个性化，则他们访问的下一个页面上不应存在个性化。

## 附录 {#appendix}

以下各节提供了关于 [!UICONTROL 同意和偏好设置] 数据类型。

### 接受的值 `val` {#choice-values}

下表概述了接受的值 `val`：

| 值 | 标题 | 描述 |
| --- | --- | --- |
| `y` | 是（选择加入） | 客户已选择加入以获得同意或偏好设置。 换句话说，他们 **do** 同意使用相关同意或偏好设置所指示的数据。 |
| `n` | 否（选择退出） | 客户已选择退出同意或偏好设置。 换句话说，他们 **不要** 同意使用相关同意或偏好设置所指示的数据。 |
| `p` | 等待验证 | 系统尚未收到最终同意或偏好设置值。 这通常用作需要两步验证的同意的一部分。 例如，如果客户选择接收电子邮件，则该同意将设置为 `p` 直到他们选择电子邮件中的链接以验证他们提供了正确的电子邮件地址，届时同意将更新为 `y`.<br><br>如果此同意或偏好设置不使用两集验证过程，则 `p` 选项可用于指示客户尚未响应同意提示。 例如，您可以自动将值设置为 `p` 在网站第一页上，客户尚未响应同意提示。 在不要求明确同意的管辖区，您还可以使用它来表示客户没有明确选择退出（换言之，假定同意）。 |
| `u` | 未知 | 客户的同意或偏好设置信息未知。 |
| `dy` | 默认为“是（选择启用）” | 客户自己未提供同意值，默认情况下会被视为选择加入（“是”）。 换言之，在客户表示不同意见之前，将假定客户同意。<br><br>请注意，如果法律或公司隐私策略的更改导致某些或所有用户的默认值发生更改，则必须手动更新包含默认值的所有用户档案。 |
| `dn` | 默认为“否”（选择退出） | 客户本身未提供同意值，并默认被视为选择退出（“否”）。 换言之，在客户表示不同意见之前，我们假定客户已拒绝同意。<br><br>请注意，如果法律或公司隐私策略的更改导致某些或所有用户的默认值发生更改，则必须手动更新包含默认值的所有用户档案。 |
| `LI` | 合法利益 | 为特定目的收集和处理此数据的合法商业利益超过了它对个人造成的潜在伤害。 |
| `CT` | 合同 | 为特定目的收集数据是履行与个人的合同义务所必需的。 |
| `CP` | 遵守法律义务 | 为特定目的收集数据是履行业务的法律义务所必需的。 |
| `VI` | 个人切身利益 | 为了保护个人的切身利益，需要为特定目的收集数据。 |
| `PI` | 公共利益 | 为了公众利益或行使官方权力，需要为特定目的收集数据。 |

{style="table-layout:auto"}

### 接受的值 `preferred` {#preferred-values}

下表概述了接受的值 `preferred`：

| 值 | 描述 |
| --- | --- |
| `email` | 电子邮件 messages. |
| `push` | 推送通知. |
| `inApp` | 应用程序内消息. |
| `sms` | 短信消息. |
| `phone` | 电话呼叫交互。 |
| `phyMail` | 实体邮件。 |
| `inVehicle` | 车内信息。 |
| `inHome` | 家庭留言。 |
| `iot` | 物联网(IoT)消息。 |
| `social` | 社交媒体内容。 |
| `other` | 不适合标准类别的渠道。 |
| `none` | 无首选渠道。 |
| `unknown` | 首选渠道未知。 |

{style="table-layout:auto"}

### 完整 [!UICONTROL 同意和偏好设置] 架构 {#full-schema}

查看的完整架构 [!UICONTROL 同意和偏好设置] 数据类型，请参阅 [官方XDM存储库](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-preferences.schema.json).
