---
keywords: Experience Platform；配置文件；实时客户配置文件；故障诊断；API；同意；同意；首选项；首选项；privacyOptOuts;marketingPreferences;optOutType;basisOfProcessing；同意
title: 同意和首选项数据类型
description: “隐私、个性化和营销首选项的同意”数据类型旨在支持收集由同意管理平台(CMP)和其他来自您数据操作来源的客户权限和首选项。
topic-legacy: guide
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2058'
ht-degree: 2%

---

# [!UICONTROL 同意和首选项] 数据类型

的 [!UICONTROL 隐私、个性化和营销首选项的同意] 数据类型(以下简称“[!UICONTROL 同意和首选项] 数据类型”)是 [!DNL Experience Data Model] (XDM)数据类型，用于支持由同意管理平台(CMP)和其他来自您数据操作来源的来源生成的客户权限和首选项的收集。

本文档介绍由 [!UICONTROL 同意和首选项] 数据类型。

## 先决条件 {#prerequisites}

本文档需要对XDM以及在 [!DNL Experience Platform]. 在继续操作之前，请查看以下文档：

* [XDM系统概述](https://www.adobe.com/go/xdm-home-en)
* [架构组合的基础知识](https://www.adobe.com/go/xdm-schema-best-practices-en)

## 数据类型结构 {#structure}

>[!IMPORTANT]
>
>的 [!UICONTROL 同意和首选项] 数据类型旨在涵盖一系列同意和首选项管理用例。 因此，本文档以一般术语介绍了数据类型字段的使用情况，并仅就如何解释这些字段的使用提出建议。 请咨询您的隐私法律团队，将数据类型的结构与贵组织如何解释并向客户展示这些同意和首选项选择保持一致。

的 [!UICONTROL 同意和首选项] 数据类型提供了多个用于捕获的字段 **同意** 和 **偏好** 信息。

同意是允许客户指定如何使用其数据的选项。 大多数同意具有法律方面的内容，因为某些司法辖区需要获得许可才能以特定方式使用数据，或者要求客户有权在不需要肯定同意的情况下停止使用（选择退出）。

首选项是一个选项，允许客户指定如何处理其品牌体验的不同方面。 这分为两类：

* **个性化首选项**:有关品牌应如何个性化交付给客户的体验的首选项。
* **营销首选项**:关于是否允许品牌通过各种渠道联系客户的首选项。

以下屏幕截图显示了数据类型结构在Platform UI中的显示方式：

![](../images/data-types/consents.png)

>[!TIP]
>
>请参阅 [浏览XDM资源](../ui/explore.md) 要了解如何查找任何XDM资源并在Platform UI中检查其结构的步骤，请访问。

以下JSON显示了 [!UICONTROL 同意和首选项] 数据类型可以处理。 以下各节提供了有关每个字段具体用途的信息。

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
>您可以为在Experience Platform中定义的任何XDM架构生成示例JSON数据，以便帮助可视化应如何映射客户同意和首选项数据。 有关更多信息，请参阅以下文档：
>
>* [在UI中生成示例数据](../ui/sample.md)
>* [在API中生成示例数据](../api/sample-data.md)


## `consents` {#choices}

`consents` 包含多个描述客户同意和偏好的字段。 以下各小节进一步详细介绍了这些字段。

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
| `val` | 客户为此用例提供的同意选择。 请参阅 [附录](#choice-values) 以了解接受的值和定义。 |

{style=&quot;table-layout:auto&quot;}

### `adID`

`adID` 表示客户同意是否可以使用广告商ID在此设备上的各个应用程序中链接客户。

```json
"adID": {
  "idType": "IDFA",
  "val": "y"
}
```

| 属性 | 描述 |
| --- | --- |
| `idType` | 广告ID类型， `IDFA` (适用于广告商或Apple `GAID` (对于Google的广告商ID，也称为Android广告商ID(AAID))。 |
| `val` | 客户为此用例提供的同意选择。 请参阅 [附录](#choice-values) 以了解接受的值和定义。 |

{style=&quot;table-layout:auto&quot;}

### `share`

`share` 表示客户同意是否可以与第二方或第三方共享（或出售给）其数据。

```json
"share": {
  "val": "y"
}
```

| 属性 | 描述 |
| --- | --- |
| `val` | 客户为此用例提供的同意选择。 请参阅 [附录](#choice-values) 以了解接受的值和定义。 |

{style=&quot;table-layout:auto&quot;}

### `personalize` {#personalize}

`personalize` 可捕获客户的偏好，以确定其数据可用于个性化的方式。 客户可以选择退出特定的个性化用例，或完全退出个性化。

>[!IMPORTANT]
>
>`personalize` 不包括营销用例。 例如，如果客户选择退出所有渠道的个性化，则他们不应停止通过这些渠道接收通信。 相反，他们收到的消息应是通用的，而不应基于其用户档案。
>
>同一示例中，如果客户选择退出所有渠道的直接营销(通过 `marketing`，详见 [下一部分](#marketing))，则客户即使允许进行个性化，也不应收到任何消息。

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `content` | 表示客户在您的网站或应用程序上对个性化内容的偏好。 |
| `val` | 客户为指定用例提供的个性化首选项。 如果客户无需获得同意，则此字段的值应指示进行个性化的基础。 请参阅 [附录](#choice-values) 以了解接受的值和定义。 |

{style=&quot;table-layout:auto&quot;}

### `marketing` {#marketing}

`marketing` 捕获客户有关其数据可用于哪些营销目的的偏好。 客户可以选择退出特定营销用例，或完全退出直接营销。

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
| `preferred` | 指示客户接收通信的首选渠道。 请参阅 [附录](#preferred-values) 的值。 |
| `any` | 代表客户对整体直接营销的偏好。 此字段中提供的同意首选项将被视为任何营销渠道的“默认”首选项，除非被下提供的其他子字段覆盖 `marketing`. 如果您计划使用更详细的同意选项，建议您排除此字段。<br><br>如果将值设置为 `n`，则应忽略所有更具体的个性化设置。 如果将值设置为 `y`，则所有更细粒度的个性化选项也应被视为 `y`，除非明确设置为 `n`. 如果未设置该值，则应按照指定的方式处理每个个性化选项的值。 |
| `email` | 指示客户是否同意接收电子邮件。 |
| `push` | 指示客户是否允许接收推送通知。 |
| `sms` | 指示客户是否同意接收短信。 |
| `val` | 客户提供的特定用例首选项。 如果客户不必被提示提供同意，则此字段的值应指示进行营销用例的依据。 请参阅 [附录](#choice-values) 以了解接受的值和定义。 |
| `time` | 营销首选项更改时的ISO 8601时间戳（如果适用）。 请注意，如果任何单个首选项的时间戳与 `metadata`，则不会为该首选项设置此字段。 |
| `reason` | 当客户选择退出营销用例时，此字符串字段表示客户选择退出的原因。 |

{style=&quot;table-layout:auto&quot;}

### `metadata`

`metadata` 在上次更新时捕获有关客户同意和首选项的常规元数据。

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| 属性 | 描述 |
| --- | --- |
| `time` | 上次更新客户同意和首选项的ISO 8601时间戳。 为了减少负载和复杂性，可以使用此字段，而不是将时间戳应用到单个首选项。 提供 `time` 单个首选项下的值将覆盖 `metadata` 该特定首选项的时间戳。 |

{style=&quot;table-layout:auto&quot;}

## 使用数据类型摄取数据 {#ingest}

为了使用 [!UICONTROL 同意和首选项] 数据类型以从客户那里摄取同意数据，您必须根据包含该数据类型的架构创建数据集。

请参阅 [在UI中创建架构](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) 有关如何将数据类型分配给字段的步骤。 创建包含字段的架构后，便可使用 [!UICONTROL 同意和首选项] 数据类型，请参阅 [创建数据集](../../catalog/datasets/user-guide.md#create) 在数据集用户指南中，按照使用现有架构创建数据集的步骤操作。

>[!IMPORTANT]
>
>如果您要将同意数据发送到 [!DNL Real-Time Customer Profile]，则需要您创建 [!DNL Profile]启用的架构基于 [!DNL XDM Individual Profile] 包含类 [!UICONTROL 同意和首选项] 数据类型。 您基于该架构创建的数据集还必须在 [!DNL Profile]. 有关与 [!DNL Real-Time Customer Profile] 架构和数据集的要求。
>
>此外，您还必须确保将合并策略配置为对包含最新同意和首选项数据的数据集优先级，以便正确更新客户配置文件。 请参阅 [合并策略](../../rtcdp/profile/merge-policies.md) 以了解更多信息。

## 处理同意和首选项更改

当客户在您的网站上更改其同意或首选项时，应收集并立即使用 [Adobe Experience Platform Web SDK](../../edge/consent/supporting-consent.md). 如果客户选择退出数据收集，则所有数据收集必须立即停止。 如果客户选择退出个性化，则他们访问的下一个页面上不应存在个性化。

## 附录 {#appendix}

以下各节提供了有关 [!UICONTROL 同意和首选项] 数据类型。

### 的接受值 `val` {#choice-values}

下表概述了 `val`:

| 值 | 标题 | 描述 |
| --- | --- | --- |
| `y` | 是（选择加入） | 客户已选择同意或首选项。 换句话说，他们 **do** 同意使用其数据（如相关同意或首选项所示）。 |
| `n` | 否（选择退出） | 客户已选择退出同意或首选项。 换句话说，他们 **不** 同意使用其数据（如相关同意或首选项所示）。 |
| `p` | 待验证 | 系统尚未收到最终同意或偏好值。 这通常用作需要两步验证的同意的一部分。 例如，如果客户选择接收电子邮件，则同意将设置为 `p` 直到他们选择电子邮件中的链接以验证他们提供了正确的电子邮件地址，此时同意将更新为 `y`.<br><br>如果此同意或首选项不使用两套验证流程，则 `p` 相反，可以使用选择指示客户尚未响应同意提示。 例如，您可以自动将值设置为 `p` 在网站的第一页上，客户响应同意提示之前。 在不需要明确同意的司法管辖区中，您还可以使用它来指示客户未明确选择退出（换言之，假设同意）。 |
| `u` | 未知 | 客户的同意或首选项信息未知。 |
| `dy` | 默认为“是”（选择加入） | 客户本身未提供同意值，默认情况下会被视为选择加入（“是”）。 换言之，在客户另有指示之前，会假定客户同意。<br><br>请注意，如果法律或贵公司隐私政策的更改导致某些或所有用户的默认值发生更改，则必须手动更新包含默认值的所有用户档案。 |
| `dn` | 默认为否（选择退出） | 客户本身未提供同意值，默认情况下会被视为选择退出（“否”）。 换言之，假定客户拒绝同意，直到他们另有指示。<br><br>请注意，如果法律或贵公司隐私政策的更改导致某些或所有用户的默认值发生更改，则必须手动更新包含默认值的所有用户档案。 |
| `LI` | 合法利益 | 为特定目的收集和处理这些数据的正当商业利益，超过了这些数据对个人的潜在损害。 |
| `CT` | 合同 | 为达到指定目的而收集数据，是为了履行与个人的合同义务。 |
| `CP` | 遵守法律义务 | 为达到指定目的而收集数据，是为了履行业务的法律义务。 |
| `VI` | 个人的重大利益 | 为了保护个人的重大利益，需要为特定目的收集数据。 |
| `PI` | 公共利益 | 为特定目的收集数据是为了公共利益或行使官方权力而执行一项任务所必需的。 |

{style=&quot;table-layout:auto&quot;}

### 的接受值 `preferred` {#preferred-values}

下表概述了 `preferred`:

| 值 | 描述 |
| --- | --- |
| `email` | 电子邮件消息. |
| `push` | 推送通知. |
| `inApp` | 应用程序内消息. |
| `sms` | 短信消息. |
| `phone` | 电话互动。 |
| `phyMail` | 实物邮件。 |
| `inVehicle` | 车内消息。 |
| `inHome` | 家庭内消息。 |
| `iot` | 物联网(IoT)消息。 |
| `social` | 社交媒体内容。 |
| `other` | 不适合标准类别的渠道。 |
| `none` | 没有首选渠道。 |
| `unknown` | 首选渠道未知。 |

{style=&quot;table-layout:auto&quot;}

### 完整 [!UICONTROL 同意和首选项] 模式 {#full-schema}

查看 [!UICONTROL 同意和首选项] 数据类型，请参阅 [官方XDM存储库](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-preferences.schema.json).
