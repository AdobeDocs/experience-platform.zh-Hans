---
keywords: Experience Platform；配置文件；实时客户配置文件；疑难解答；API；同意；同意；首选项；隐私选择退出；营销偏好设置；选择退出类型；basisOfProcessing；同意；同意
title: 同意和偏好设置数据类型
description: 隐私同意、Personalization和营销偏好设置数据类型旨在支持从您的数据操作中收集由同意管理平台(CMP)和其他源生成的客户权限和偏好设置。
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '2305'
ht-degree: 1%

---

# [!UICONTROL Consents and Preferences]数据类型

[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences]数据类型（以下简称“[!UICONTROL Consents and Preferences]数据类型”）是[!DNL Experience Data Model] (XDM)数据类型，旨在支持从您的数据操作中收集由同意管理平台(CMP)和其他源生成的客户权限和偏好设置。

本文档介绍了[!UICONTROL Consents and Preferences]数据类型提供的字段的结构和预期用途。

## 先决条件 {#prerequisites}

本文档要求您对XDM和架构在[!DNL Experience Platform]中的使用有一定的了解。 请在继续之前查看以下文档：

* [XDM 系统概述](https://www.adobe.com/go/xdm-home-en)
* [架构组合的基础知识](https://www.adobe.com/go/xdm-schema-best-practices-en)

## 数据类型结构 {#structure}

>[!IMPORTANT]
>
>[!UICONTROL Consents and Preferences]数据类型旨在涵盖一系列同意和偏好设置管理用例。 因此，本文档笼统地说明了数据类型字段的用法，并仅就应如何解释这些字段的使用提出了建议。 请咨询您的隐私法律团队，以调整数据类型的结构，使其与您的组织如何解读并向客户展示这些同意和偏好设置选择相对应。

[!UICONTROL Consents and Preferences]数据类型提供了几个用于捕获&#x200B;**同意**&#x200B;和&#x200B;**首选项**&#x200B;信息的字段。

同意是一个选项，允许客户指定如何使用其数据。 大多数同意都有法律含义，其中有些司法管辖区要求先获得许可，然后数据才能以特定方式使用，或者要求客户在不需要明确同意的情况下可以选择停止使用（选择退出）。

偏好设置是一个选项，它允许客户指定应如何处理其品牌体验的不同方面。 这些规则分为两类：

* **Personalization首选项**：关于品牌应如何个性化向客户提供体验的首选项。
* **营销偏好设置**：有关是否允许品牌通过各种渠道联系客户的偏好设置。

以下屏幕截图显示了数据类型的结构在Experience Platform UI中的表示方式：

![](../images/data-types/consents.png)

>[!TIP]
>
>有关如何在Experience Platform UI中查找任何XDM资源并检查其结构的步骤，请参阅关于[探索XDM资源](../ui/explore.md)的指南。

以下JSON显示了[!UICONTROL Consents and Preferences]数据类型可以处理的数据类型示例。 有关这些字段中每个字段的特定用途的信息，请参见以下部分。

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

`consents`包含多个描述客户同意和偏好设置的字段。 这些字段将在以下子部分中详细介绍。

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

`collect`表示客户同意收集其数据。

```json
"collect": {
  "val": "y"
}
```

| 属性 | 描述 |
| --- | --- |
| `val` | 此用例的客户提供的同意选择。 有关接受的值和定义，请参阅[附录](#choice-values)。 |

{style="table-layout:auto"}

### `adID`

`adID`表示客户同意是否可以使用广告商ID在此设备上跨应用程序链接客户。

```json
"adID": {
  "idType": "IDFA",
  "val": "y"
}
```

| 属性 | 描述 |
| --- | --- |
| `idType` | 广告ID类型，可以是Apple的广告商ID的`IDFA`，也可以是Google的广告商ID的`GAID`，也称为Android广告商ID (AAID)。 |
| `val` | 此用例的客户提供的同意选择。 有关接受的值和定义，请参阅[附录](#choice-values)。 |

{style="table-layout:auto"}

### `share`

`share`表示客户同意其数据可以与第二方或第三方共享（或出售给）。

```json
"share": {
  "val": "y"
}
```

| 属性 | 描述 |
| --- | --- |
| `val` | 此用例的客户提供的同意选择。 有关接受的值和定义，请参阅[附录](#choice-values)。 |

{style="table-layout:auto"}

### `personalize` {#personalize}

`personalize`捕获客户对其数据可用于个性化的方式的偏好。 客户可以选择退出特定的个性化用例，或完全选择退出个性化。

>[!IMPORTANT]
>
>`personalize`不包含营销用例。 例如，如果客户选择不为所有渠道进行个性化，则不应停止通过这些渠道接收通信。 相反，他们收到的消息应该是通用的，而不是基于其用户档案。
>
>根据同一示例，如果客户选择退出所有渠道的直销（通过`marketing`，如[下一节](#marketing)中所述），则该客户不应接收任何消息，即使允许个性化设置也是如此。

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `content` | 表示客户对网站或应用程序上的个性化内容的偏好。 |
| `val` | 指定用例的客户提供的个性化偏好设置。 如果不必提示客户提供同意，则此字段的值应指示进行个性化的基础。 有关接受的值和定义，请参阅[附录](#choice-values)。 |

{style="table-layout:auto"}

### `marketing` {#marketing}

`marketing`捕获客户对其数据可用于哪些营销目的的偏好。 客户可以选择退出特定营销用例，或完全选择退出直接营销。

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
| `preferred` | 指示客户接收通信的首选渠道。 请参阅[附录](#preferred-values)以了解接受的值。 |
| `any` | 表示客户对整个直接营销的偏好。 在此字段中提供的同意首选项被视为任何营销渠道的“默认”首选项，除非由`marketing`下提供的其他子字段覆盖。 如果您计划使用更细粒度的同意选项，建议您排除此字段。<br><br>如果该值设置为`n`，则所有更具体的个性化设置都将被忽略。 如果该值设置为`y`，则所有细粒度个性化选项也应视为`y`，除非显式设置为`n`。 如果未设置该值，则每个个性化选项的值都应按指定接受。 |
| `email` | 指示客户是否同意接收电子邮件。 |
| `push` | 指示客户是否允许接收推送通知。 |
| `sms` | 指示客户是否同意接收短信。 |
| `val` | 指定用例的客户提供的首选项。 如果不必提示客户提供同意，此字段的值应指示进行营销用例的基础。 有关接受的值和定义，请参阅[附录](#choice-values)。 |
| `time` | 营销偏好设置更改时间的ISO 8601时间戳（如果适用）。 请注意，如果任何单个首选项的时间戳与`metadata`下提供的时间戳相同，则不会为该首选项设置此字段。 |
| `reason` | 当客户选择退出营销用例时，此字符串字段表示客户选择退出的原因。 |

{style="table-layout:auto"}

### `metadata`

`metadata`捕获有关客户同意和偏好设置的一般元数据，每次更新时都会捕获。

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| 属性 | 描述 |
| --- | --- |
| `time` | 客户同意和偏好设置上次更新的ISO 8601时间戳。 可以使用此字段代替向单个首选项应用时间戳以降低负载和复杂性。 在单个首选项下提供`time`值将覆盖该特定首选项的`metadata`时间戳。 |

{style="table-layout:auto"}

## 使用数据类型摄取数据 {#ingest}

要使用[!UICONTROL Consents and Preferences]数据类型从客户那里摄取同意数据，您必须基于包含该数据类型的架构创建数据集。

有关如何将数据类型分配给字段的步骤，请参阅有关[在UI](https://www.adobe.com/go/xdm-schema-editor-tutorial-en)中创建架构的教程。 创建包含具有[!UICONTROL Consents and Preferences]数据类型的字段的架构后，请参阅数据集用户指南中有关[创建数据集](../../catalog/datasets/user-guide.md#create)的部分，并按照使用现有架构创建数据集的步骤操作。

>[!IMPORTANT]
>
>如果要将同意数据发送到[!DNL Real-Time Customer Profile]，则需要您根据包含[!DNL Profile]数据类型的[!DNL XDM Individual Profile]类创建一个启用[!UICONTROL Consents and Preferences]的架构。 还必须为[!DNL Profile]启用您根据该架构创建的数据集。 请参阅上面链接的教程，了解与架构和数据集的[!DNL Real-Time Customer Profile]要求相关的特定步骤。
>
>此外，您还必须确保将合并策略配置为优先考虑包含最新同意和偏好设置数据的数据集，以便正确更新客户配置文件。 有关详细信息，请参阅有关[合并策略](../../rtcdp/profile/merge-policies.md)的概述。

## 处理同意和偏好设置更改

当客户在您的网站上更改其同意或偏好设置时，应收集这些更改，并通过在所用的数据收集库中设置同意来立即实施这些更改。 如果客户选择退出数据收集，则必须立即停止所有数据收集。 如果客户选择退出个性化，则他们访问的下一个页面上应该不会显示个性化。 请参阅使用JavaScript库的[`setConsent`](/help/collection/js/commands/setconsent.md)或使用标记扩展的[[!UICONTROL Set consent]](/help/tags/extensions/client/web-sdk/actions/set-consent.md)操作。

## 附录 {#appendix}

以下部分提供了有关[!UICONTROL Consents and Preferences]数据类型的其他参考信息。

### `val`的接受值 {#choice-values}

下表概述了`val`的接受值：

| 值 | 标题 | 描述 |
| --- | --- | --- |
| `y` | 是（选择启用） | 客户已选择加入以获得同意或偏好设置。 换言之，他们&#x200B;**do**&#x200B;同意使用相关同意或偏好设置所指示的数据。 |
| `n` | 否（选择退出） | 客户已选择退出同意或偏好设置。 换言之，他们&#x200B;**不**&#x200B;同意使用相关同意或偏好设置所指示的数据。 |
| `p` | 等待验证 | 系统尚未收到最终同意或偏好设置值。 这通常用作需要两步验证的同意的一部分。 例如，如果客户选择接收电子邮件，该同意将设置为`p`，直到他们在电子邮件中选择链接以验证他们提供了正确的电子邮件地址，此时同意将更新为`y`。<br><br>如果此同意或偏好设置未使用两集验证流程，则可能使用`p`选项来指示客户尚未响应同意提示。 例如，在客户响应同意提示之前，您可以在网站的第一个页面上自动将值设置为`p`。 在不要求明确同意的司法辖区中，您还可以使用它来表示客户没有明确选择退出（换言之，假定您同意该选项）。<br><br>虽然可以使用其他机制（如流式摄取）在[!DNL Profile]中摄取此值，但在&#x200B;**上数据收集或同意收集时**&#x200B;不支持[!DNL Edge Network]。 虽然无法显式发送`p`值，但[[!DNL Web SDK]](../../landing/governance-privacy-security/consent/sdk.md)仍处理事件排队，一旦最终用户的同意明确为[!DNL Edge Network]，事件将调度到`in`。 |
| `u` | 未知 | 客户的同意或偏好设置信息未知。 |
| `dy` | 默认为“是（选择启用）” | 客户本身未提供同意值，默认情况下将视为选择加入（“是”）。 换言之，除非客户另有指示，否则将假定客户同意。<br><br>请注意，如果法律或公司隐私策略的更改导致某些或所有用户的默认值发生更改，则必须手动更新包含默认值的所有用户档案。 |
| `dn` | 默认为“否”（选择退出） | 客户本身并未提供同意值，并默认被视为选择退出（“否”）。 换言之，客户被假定已拒绝同意，直到他们表示不同意。<br><br>请注意，如果法律或公司隐私策略的更改导致某些或所有用户的默认值发生更改，则必须手动更新包含默认值的所有用户档案。 |
| `LI` | 合法利益 | 为特定目的收集和处理这些数据的合法商业利益大于其对个人造成的潜在危害。 |
| `CT` | 合同 | 为特定目的收集数据是履行与个人的合同义务所必需的。 |
| `CP` | 遵守法律义务 | 为特定目的收集数据是履行企业法律义务所必需的。 |
| `VI` | 个人切身利益 | 为了保护个人的切身利益，必须收集用于特定目的的数据。 |
| `PI` | 公共利益 | 为特定目的收集数据，是为了执行一项符合公众利益或行使官方权力的任务。 |

{style="table-layout:auto"}

### `preferred`的接受值 {#preferred-values}

下表概述了`preferred`的接受值。 `preferred`值表示客户接收通信的首选渠道，这些通信将告知他们数据收集、隐私政策和个性化选项。

| 值 | 描述 |
| --- | --- |
| `email` | 此首选项表示客户同意通过电子邮件接收消息。 |
| `push` | 此首选项表示客户同意接收推送通知。 这些是直接发送到其设备（通常是移动应用程序）的消息或警报。 |
| `inApp` | 此首选项表示客户同意接收应用程序内消息。 这些消息在移动或Web应用程序中传送，并在用户积极参与应用程序时提供信息。 |
| `sms` | 此首选项表示客户同意通过短信（短信服务）接收消息。 这些是发送到他们手机的短信。 |
| `phone` | 此首选项表示客户同意通过电话呼叫交互接收通信。 |
| `phyMail` | 此首选项表示客户同意通过实体邮件接收材料。 |
| `inVehicle` | 此首选项表示客户同意在车辆中接收通知。 这些消息可以通过车辆信息娱乐系统或其他车辆内通信信道被传送。 |
| `inHome` | 此首选项表示客户同意在家中接收消息。 这些消息可以通过智能家庭设备或其他基于家庭的通信信道来传送。 |
| `iot` | 此首选项表示客户同意接收与物联网(IoT)相关的消息。 这些消息可以通过其环境中连接的设备和系统来传送。 |
| `social` | 此首选项表示客户同意通过社交媒体平台接收通信。 |
| `other` | 此首选项包含不适合标准类别的渠道。 它表示可能特定于特定业务或行业的替代或专用通信渠道。 |
| `none` | 此首选项表示客户没有首选的通信渠道。 |
| `unknown` | 此首选项表示客户的首选通信渠道未知或未指定。 如果客户没有提供明确的同意或偏好设置信息，则可能会发生这种情况。 |

{style="table-layout:auto"}

### 完整[!UICONTROL Consents and Preferences]架构 {#full-schema}

要查看[!UICONTROL Consents and Preferences]数据类型的完整架构，请参阅[官方XDM存储库](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-preferences.schema.json)。
