---
keywords: Experience Platform;用户档案；实时客户用户档案；疑难解答；API；同意；同意；首选项；首选项；隐私选择退出；营销首选项；选择退出类型；基准选择处理；同意
title: 同意和首选项数据类型
description: “同意隐私、个性化和营销首选项”数据类型旨在支持收集由同意管理平台(CMP)和您数据操作中的其他来源生成的客户权限和首选项。
topic-legacy: guide
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1837'
ht-degree: 1%

---

# [!DNL Consents & Preferences] 数据类型

[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences]数据类型（以下称“[!DNL Consents & Preferences]数据类型”）是[!DNL Experience Data Model](XDM)数据类型，用于支持收集由同意管理平台(CMP)和您数据操作中的其他源生成的客户权限和偏好。

此文档涵盖[!DNL Consents & Preferences]数据类型提供的字段的结构和预期用途。

## 先决条件 {#prerequisites}

此文档需要对XDM和[!DNL Experience Platform]中模式的使用有效的了解。 在继续之前，请查看以下文档：

* [XDM系统概述](http://www.adobe.com/go/xdm-home-en)
* [模式合成基础](http://www.adobe.com/go/xdm-schema-best-practices-en)

## 数据类型结构{#structure}

>[!IMPORTANT]
>
>[!DNL Consents & Preferences]数据类型旨在涵盖一系列同意和偏好管理使用案例。 因此，本文档用一般术语描述数据类型字段的使用，并仅就如何解释这些字段的使用提出建议。 请咨询您的隐私法律团队，使数据类型结构与您的组织如何解释和向客户展示这些同意和偏好选择保持一致。

[!DNL Consents & Preferences]数据类型提供了若干字段，用于捕获&#x200B;**connence**&#x200B;和&#x200B;**preference**&#x200B;信息。

同意是允许客户指定其数据的使用方式的选项。 大多数同意具有法律方面，因为某些司法辖区要求在数据以特定方式使用之前获得许可，或要求客户有权（如果不需要肯定同意）停止选择退出这种使用。

首选项是一个选项，允许客户指定如何处理品牌体验的不同方面。 这属于两个类别:

* **个性化首选项**:关于品牌如何个性化向客户提供体验的偏好。
* **营销首选项**:关于是否允许品牌通过各种渠道联系客户的偏好。

以下屏幕截图显示了数据类型结构在平台UI中的显示方式：

![](../images/data-types/consents.png)

>[!TIP]
>
>有关如何查找任何XDM资源并在平台UI中检查其结构的步骤，请参阅[探索XDM资源](../ui/explore.md)指南。

以下JSON显示了[!DNL Consents & Preferences]数据类型可以处理的数据类型的示例。 以下各节提供了有关这些字段具体用途的信息。

```json
{
  "consents": {
    "collect": {
      "val": "y",
    },
    "adID": {
      "val": "VI"
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
>您可以为在Experience Platform中定义的任何XDM模式生成示例JSON数据，以帮助可视化如何映射客户同意和偏好数据。 有关更多信息，请参阅以下文档：
>
>* [在UI中生成示例数据](../ui/sample.md)
>* [在API中生成示例数据](../api/sample-data.md)


## `consents` {#choices}

`consents` 包含描述客户同意和偏好的几个字段。以下各小节将进一步详细介绍这些字段。

```json
"consents": {
  "collect": {
    "val": "y",
  },
  "adID": {
    "val": "VI"
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
"collect" : {
  "val": "y"
}
```

| 属性 | 描述 |
| --- | --- |
| `val` | 客户为此用例提供的同意选择。 有关已接受的值和定义，请参见[附录](#choice-values)。 |

### `adID`

`adID` 表示客户同意是否可以使用广告商ID（IDFA或GAID）在此设备上的多个应用程序中链接客户。

```json
"adID" : {
  "val": "y"
}
```

| 属性 | 描述 |
| --- | --- |
| `val` | 客户为此用例提供的同意选择。 有关已接受的值和定义，请参见[附录](#choice-values)。 |

### `share`

`share` 表示客户同意与（或售予）第二方或第三方共享其数据。

```json
"share" : {
  "val": "y"
}
```

| 属性 | 描述 |
| --- | --- |
| `val` | 客户为此用例提供的同意选择。 有关已接受的值和定义，请参见[附录](#choice-values)。 |

### `personalize` {#personalize}

`personalize` 捕获客户的偏好，以了解其数据可以通过哪些方式进行个性化。客户可以选择退出针对特定的个性化使用案例，或选择退出者完全个性化。

>[!IMPORTANT]
>
>`personalize` 不涵盖营销使用案例。例如，如果客户选择退出所有渠道的个性化，则不应停止通过这些渠道接收通信。 相反，他们收到的消息应是通用的，而不是基于他们的用户档案。
>
>通过同一示例，如果客户选择退出所有渠道的直接营销（通过`marketing`，在[下一节](#marketing)中说明），则即使允许个性化，该客户也不应接收任何消息。

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `content` | 表示客户对您网站或应用程序上的个性化内容的偏好。 |
| `val` | 客户为指定用例提供的个性化首选项。 如果客户不必被提示提供同意，则此字段的值应指示进行个性化的基础。 有关已接受的值和定义，请参见[附录](#choice-values)。 |

### `marketing` {#marketing}

`marketing` 捕获客户关于其数据可用于哪些营销目的的偏好。客户可以选择退出使用特定的营销用例，或选择退出完全使用直接营销。

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
| `preferred` | 指示客户接收通信的首选渠道。 有关已接受的值，请参见[附录](#preferred-values)。 |
| `any` | 代表客户对直接营销的整体偏好。 此字段中提供的同意首选项被视为任何营销渠道的“默认”首选项，除非由`marketing`下提供的其他子字段覆盖。 如果您计划使用更精细的同意选项，建议您排除此字段。<br><br>如果将值设置为，则 `n`应忽略所有更具体的个性化设置。如果将值设置为`y`，则所有更细粒度的个性化选项也应视为`y`，除非明确设置为`n`。 如果取消设置该值，则每个个性化选项的值应按指定的方式显示。 |
| `email` | 指示客户是否同意接收电子邮件。 |
| `push` | 指示客户是否允许接收推送通知。 |
| `sms` | 指示客户是否同意接收短信。 |
| `val` | 客户为指定用例提供的首选项。 如果客户不必被提示提供同意，则此字段的值应指明进行市场营销用例的依据。 有关已接受的值和定义，请参见[附录](#choice-values)。 |
| `time` | 市场营销首选项更改时的ISO 8601时间戳（如果适用）。 请注意，如果任何单个首选项的时间戳与`metadata`下提供的时间戳相同，则不会为该首选项设置此字段。 |
| `reason` | 当客户选择退出营销用例时，此字符串字段表示客户选择退出的原因。 |

### `metadata`

`metadata` 在上次更新客户同意和偏好时捕获有关这些同意和偏好的一般元数据。

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| 属性 | 描述 |
| --- | --- |
| `time` | 上次更新客户同意和首选项时的ISO 8601时间戳。 可以使用此字段，而不是将时间戳应用到单个首选项，以减少负载和复杂性。 在单个首选项下提供`time`值将覆盖该特定首选项的`metadata`时间戳。 |

## 使用数据类型{#ingest}收录数据

要使用[!DNL Consents & Preferences]数据类型从客户那里收集同意数据，您必须根据包含该数据类型的模式创建数据集。

有关如何将模式类型分配给字段的步骤，请参阅有关在UI](http://www.adobe.com/go/xdm-schema-editor-tutorial-en)中创建数据的教程。 [创建包含数据类型为[!DNL Consents & Preferences]的字段的模式后，请参阅数据集用户指南中[创建数据集](../../catalog/datasets/user-guide.md#create)部分，按照步骤使用现有模式创建数据集。

>[!IMPORTANT]
>
>如果要将同意数据发送到[!DNL Real-time Customer Profile]，则需要根据包含[!DNL Consents & Preferences]数据类型的[!DNL XDM Individual Profile]类创建启用[!DNL Profile]的模式。 还必须为[!DNL Profile]启用您基于该模式创建的数据集。 有关与模式和数据集的[!DNL Real-time Customer Profile]要求相关的具体步骤，请参阅上面链接的教程。
>
>此外，您还必须确保将合并策略配置为优先处理包含最新同意和首选项数据的数据集，以便正确更新客户用户档案。 有关详细信息，请参阅[合并策略](../../rtcdp/profile/merge-policies.md)的概述。

## 处理同意和首选项更改

当客户在您的网站上更改其同意或偏好时，应使用[Adobe Experience Platform Web SDK](../../edge/consent/supporting-consent.md)收集并立即实施这些更改。 如果客户选择退出数据收集，则必须立即停止所有数据收集。 如果客户选择退出个性化，那么他们访问的下一页上不应出现个性化。

## 附录 {#appendix}

以下各节提供了有关[!DNL Consents & Preferences]数据类型的其他参考信息。

### `val` {#choice-values}的已接受值

下表概述了`val`的已接受值：

| 值 | 标题 | 描述 |
| --- | --- | --- |
| `y` | 是 | 客户已选择同意或偏好。 换句话说，他们&#x200B;**do**&#x200B;同意使用其数据，如有关同意或偏好所示。 |
| `n` | 否 | 客户已选择不同意或拒绝。 换句话说，他们&#x200B;**不**&#x200B;同意使用其数据，这些数据由有关的同意或偏好所指示。 |
| `p` | 待验证 | 系统尚未收到最终同意或偏好值。 这通常是需要两步核查的同意的一部分。 例如，如果客户选择接收电子邮件，则该同意将设置为`p`，直到他们选择电子邮件中的链接以验证他们提供了正确的电子邮件地址，此时该同意将更新为`y`。<br><br>如果此同意或偏好不使用两组验证过程，则 `p` 该选择可用于指示客户尚未响应同意提示。例如，您可以在客户响应同意提示之前，在网站的第一页自动将值设置为`p`。 在不需要明确同意的司法管辖区，您还可以使用它指示客户未明确选择退出（即假定客户同意）。 |
| `u` | Unknown | 客户同意或偏好信息未知。 |
| `LI` | 合法利益 | 为特定目的收集和处理这些数据的合法商业利益超过数据对个人的潜在伤害。 |
| `CT` | 合同 | 为达到指定目的而收集数据，是为了履行与个人的合同义务。 |
| `CP` | 遵守法律义务 | 为达到特定目的而收集数据，是为了履行业务的法律义务。 |
| `VI` | 个人的切身利益 | 为了保护个人的切身利益，需要为特定目的收集数据。 |
| `PI` | Public Interest | 为特定目的收集数据，是为了公共利益或行使官方权力而进行任务。 |

### `preferred` {#preferred-values}的已接受值

下表概述了`preferred`的已接受值：

| 值 | 描述 |
| --- | --- |
| `email` | 电子邮件消息. |
| `push` | 推送通知. |
| `inApp` | 应用程序内消息. |
| `sms` | 短信消息. |
| `phone` | 电话互动。 |
| `phyMail` | 实际邮件。 |
| `inVehicle` | 车内消息。 |
| `inHome` | 家庭内消息。 |
| `iot` | 物联网(IoT)消息。 |
| `social` | 社交媒体内容。 |
| `other` | 不符合标准渠道的类别。 |
| `none` | 无首选渠道。 |
| `unknown` | 首选渠道未知。 |

### 完整[!DNL Consents & Preferences]模式{#full-schema}

要视图[!DNL Consents & Preferences]数据类型的完整模式，请参阅[官方XDM存储库](https://github.com/adobe/xdm/blob/master/components/datatypes/consent-preferences.schema.json)。
