---
keywords: Experience Platform;用户档案；实时客户用户档案；疑难解答；API；同意；同意；首选项；隐私选择退出；营销首选项；选择退出类型；基础选择处理；同意
title: 同意和首选项数据类型
description: 隐私／营销偏好（同意）数据类型旨在支持收集由同意管理平台(CMP)和您数据操作的其他来源生成的客户权限和偏好。
topic: guide
translation-type: tm+mt
source-git-commit: caebdcd48e03bd8b91da624532569b55d8696fb4
workflow-type: tm+mt
source-wordcount: '2040'
ht-degree: 1%

---


# [!DNL Consents & Preferences] 数据类型

[!DNL Privacy/Marketing Preferences (Consent)]数据类型（以下称“[!DNL Consents & Preferences]数据类型”）是[!DNL Experience Data Model](XDM)数据类型，用于支持收集由同意管理平台(CMP)和您数据操作中的其他来源生成的客户权限和偏好。

此文档涵盖[!DNL Consents & Preferences]数据类型提供的字段的结构和预期用途。

## 先决条件 {#prerequisites}

此文档要求对XDM和[!DNL Experience Platform]中模式的使用进行有效的了解。 请在继续之前查看以下文档：

* [XDM系统概述](http://www.adobe.com/go/xdm-home-en)
* [模式合成基础](http://www.adobe.com/go/xdm-schema-best-practices-en)

## 数据类型结构{#structure}

>[!IMPORTANT]
>
>[!DNL Consents & Preferences]数据类型旨在涵盖一系列同意和偏好管理用例。 因此，此文档用一般术语描述数据类型字段的使用，并仅就如何解释这些字段的使用提出建议。 请咨询您的隐私法律团队，使数据类型的结构与您的组织如何解释并向客户展示这些同意和偏好选择保持一致。

[!DNL Consents & Preferences]数据类型提供几个字段，用于捕获&#x200B;**connection**&#x200B;和&#x200B;**preference**&#x200B;信息。

同意是允许客户指定数据的使用方式的选项。 大多数同意具有法律意义，因为有些司法辖区需要获得许可才能以特定方式使用数据，或者要求客户有权在不需要肯定同意的情况下停止该选择退出使用。

首选项是允许客户指定如何处理品牌体验的不同方面的选项。 这一数字属于两个类别:

* **个性化首选项**:关于品牌如何个性化向客户提供的体验的偏好。
* **营销首选项**:关于是否允许品牌通过各种渠道联系客户的偏好。

以下JSON显示了[!DNL Consents & Preferences]数据类型可以处理的数据类型的示例。 以下各节提供了有关这些字段具体用途的信息。

```json
{
  "xdm:consents": {
    "xdm:collect": {
      "xdm:val": "y",
    },
    "xdm:adID": {
      "xdm:val": "VI"
    },
    "xdm:share": {
      "xdm:val": "y",
    },
    "xdm:personalize": {
      "xdm:content": {
        "xdm:val": "y"
      }
    },
    "xdm:marketing": {
      "xdm:preferred": "email",
      "xdm:any": {
        "xdm:val": "u"
      },
      "xdm:push": {
        "xdm:val": "n",
        "xdm:reason": "Too Frequent",
        "xdm:time": "2019-01-01T15:52:25+00:00"
      }
    },
    "xdm:idSpecific": {
      "email": {
        "jdoe@example.com": {
          "xdm:marketing": {
            "xdm:email": {
              "xdm:val": "n"
            }
          }
        }
      }
    }
  },
  "xdm:metadata": {
    "xdm:time": "2019-01-01T15:52:25+00:00"
  }
}
```

>[!NOTE]
>
>以上示例旨在说明通过[!DNL Consents & Preferences]数据类型发送到[!DNL Platform]的文档的结构，以便提供本其余部分的上下文，该上下文解释了数据类型提供的主要字段。 [附录](#full-schema)中可找到数据类型结构的完整模式，以供参考。

## xdm:conversions {#choices}

`xdm:consents` 包含几个字段，用于描述客户的同意和偏好。下面各小节将进一步详细介绍这些字段。

```json
"xdm:consents": {
  "xdm:collect": {
    "xdm:val": "y",
  },
  "xdm:adID": {
    "xdm:val": "VI"
  },
  "xdm:share": {
    "xdm:val": "y",
  },
  "xdm:personalize": {
    "xdm:content": {
      "xdm:val": "y"
    }
  },
  "xdm:marketing": {
    "xdm:preferred": "email",
    "xdm:any": {
      "xdm:val": "u"
    },
    "xdm:email": {
      "xdm:val": "n",
      "xdm:reason": "Too Frequent",
      "xdm:time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

### xdm：收集

`xdm:collect` 表示客户同意收集其数据。

```json
"xdm:collect" : {
  "xdm:val": "y"
}
```

| 属性 | 描述 |
| --- | --- |
| `xdm:val` | 客户为此使用案例提供的同意选择。 请参见[附录](#choice-values)，了解已接受的值和定义。 |

### xdm:adID

`xdm:adID` 表示客户同意广告商ID（IDFA或GAID）是否可用于在此设备上的多个应用程序中链接客户。

```json
"xdm:adID" : {
  "xdm:val": "y"
}
```

| 属性 | 描述 |
| --- | --- |
| `xdm:val` | 客户为此使用案例提供的同意选择。 请参见[附录](#choice-values)，了解已接受的值和定义。 |

### xdm：共享

`xdm:share` 表示客户同意是否可与第二方或第三方共享（或出售给）其数据。

```json
"xdm:share" : {
  "xdm:val": "y"
}
```

| 属性 | 描述 |
| --- | --- |
| `xdm:val` | 客户为此使用案例提供的同意选择。 请参见[附录](#choice-values)，了解已接受的值和定义。 |

### xdm:personalize {#personalize}

`xdm:personalize` 捕获客户偏好，以确定其数据可通过哪些方式进行个性化。客户可选择退出以使用特定的个性化用例，或选择退出者完全个性化。

>[!IMPORTANT]
>
>`xdm:personalize` 不涵盖营销用例。例如，如果客户选择退出所有渠道的个性化，他们不应停止通过这些渠道接收通信。 相反，他们收到的消息应是通用的，而不是基于其用户档案。
>
>通过同一示例，如果客户退出所有渠道的直接营销（通过[下一节](#marketing)中说明的`xdm:marketing`），则即使允许个性化，该客户也不会收到任何消息。

```json
"xdm:personalize": {
  "xdm:content": {
    "xdm:val": "y",
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `xdm:content` | 表示客户对您网站或应用程序上的个性化内容的偏好。 |
| `xdm:val` | 客户为指定用例提供的个性化首选项。 如果客户无需获得同意，此字段的值应指明进行个性化的依据。 请参见[附录](#choice-values)，了解已接受的值和定义。 |

### xdm:marketing {#marketing}

`xdm:marketing` 捕获客户关于其数据可用于哪些营销目的的偏好。客户可选择退出以使用特定的营销用例，或选择退出完全使用直接营销。

```json
"xdm:marketing": {
  "xdm:preferred": "email",
  "xdm:any": {
    "xdm:val": "u"
  },
  "xdm:email": {
    "xdm:val": "n",
    "xdm:reason": "Too Frequent"
  },
  "xdm:push": {
    "xdm:val": "y"
  },
  "xdm:sms": {
    "xdm:val": "y"
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `xdm:preferred` | 指示客户接收通信的首选渠道。 有关已接受的值，请参见[附录](#preferred-values)。 |
| `xdm:any` | 代表客户对直接营销的总体偏好。 此字段中提供的同意首选项被视为任何营销渠道的“默认”首选项，除非被`xdm:marketing`下提供的其他子字段覆盖。 如果您计划使用更精细的同意选项，建议您排除此字段。<br><br>如果将该值设置为， `n`则应忽略所有更具体的个性化设置。如果将该值设置为`y`，则所有更细粒度的个性化选项也应视为`y`，除非明确设置为`n`。 如果取消设置该值，则每个个性化选项的值应按指定的方式显示。 |
| `xdm:email` | 指示客户是否同意接收电子邮件。 |
| `xdm:push` | 指示客户是否允许接收推送通知。 |
| `xdm:sms` | 指示客户是否同意接收文本消息。 |
| `xdm:val` | 客户为指定用例提供的首选项。 如果客户无需获得同意，则此字段的值应指明进行市场营销的依据。 请参见[附录](#choice-values)，了解已接受的值和定义。 |
| `xdm:time` | 市场营销首选项更改时的ISO 8601时间戳（如果适用）。 请注意，如果任何单个首选项的时间戳与`xdm:metadata`下提供的时间戳相同，则不会为该首选项设置此字段。 |
| `xdm:reason` | 当客户选择退出营销用例时，此字符串字段表示客户选择退出的原因。 |

### xdm:idSpecific

`xdm:idSpecific` 特定同意或偏好并非普遍适用于客户，但仅限于单个设备或ID时，可使用。例如，客户可以接选择退出收到某个地址的电子邮件，同时可能允许另一个地址发送电子邮件。

>[!IMPORTANT]
>
>渠道级同意和偏好（即在`xdm:idSpecific`外的`xdm:consents`下提供的同意和偏好）适用于该渠道中的ID。 因此，无论是采用对等的ID设置还是设备特定设置，所有渠道级同意和首选项都会直接影响：
>
>* 如果客户已在渠道级别退出，则忽略`xdm:idSpecific`中的任何对等同意或偏好。
>* 如果未设置渠道级同意或偏好，或者客户已选择加入，则`xdm:idSpecific`中的对等同意或偏好将被接受。


`xdm:idSpecific`对象中的每个键代表由Adobe Experience Platform标识服务识别的特定标识命名空间。 虽然您可以定义自己的自定义命名空间来对不同的标识符进行分类，但建议您使用标识服务提供的标准命名空间之一来减少实时客户用户档案的存储大小。 有关身份命名空间的详细信息，请参阅Identity Service文档中的[身份命名空间概述](../../identity-service/namespaces.md)。

每个命名空间对象的键代表客户为其设置首选项的唯一标识值。 每个标识值可以包含一组完整的同意和首选项，格式与`xdm:consents`相同。

```json
"xdm:idSpecific": {
  "email": {
    "jdoe@example.com": {
      "xdm:marketing": {
        "xdm:email": {
          "xdm:val": "n"
        }
      }
    }
  }
}
```

## xdm：元数据

`xdm:metadata` 在上次更新客户同意和偏好时捕获有关这些同意和偏好的一般元数据。

```json
"xdm:metadata": {
  "xdm:time": "2019-01-01T15:52:25+00:00",
}
```

| 属性 | 描述 |
| --- | --- |
| `xdm:time` | 上次更新客户的同意和偏好的时间戳。 可以使用此字段，而不是将时间戳应用到单个首选项，以减少负载和复杂性。 在单个首选项下提供`xdm:time`值将覆盖该特定首选项的`xdm:metadata`时间戳。 |

## 使用数据类型{#ingest}摄取数据

要使用[!DNL Consents & Preferences]数据类型从客户处获取同意数据，您必须根据包含该数据类型的模式创建数据集。

有关如何将数据类型分配给字段的步骤，请参阅[在UI](http://www.adobe.com/go/xdm-schema-editor-tutorial-en)中创建模式的教程。 创建包含数据类型为[!DNL Consents & Preferences]的字段的模式后，请参阅数据集用户指南中[创建数据集](../../catalog/datasets/user-guide.md#create)的部分，按照步骤使用现有模式创建数据集。

>[!IMPORTANT]
>
>如果要向[!DNL Real-time Customer Profile]发送同意模式，必须根据[!DNL XDM Individual Profile]类创建启用[!DNL Profile]的数据类型。 [!DNL Consents & Preferences]还必须为[!DNL Profile]启用您根据该模式创建的数据集。 有关模式和数据集[!DNL Real-time Customer Profile]要求的特定步骤，请参阅以上链接的教程。
>
>此外，您还必须确保将合并策略配置为优先处理包含最新同意和偏好数据的数据集，以便正确更新客户用户档案。 有关详细信息，请参阅[合并策略](../../rtcdp/profile/merge-policies.md)的概述。

## 处理同意和偏好更改

当客户在您的网站上更改其同意或偏好时，应使用[Adobe Experience PlatformWeb SDK](../../edge/consent/supporting-consent.md)收集并立即强制执行这些更改。 如果客户选择退出数据收集，则所有数据收集必须立即停止。 如果客户选择退出个性化，那么他们访问的下一页上就不存在个性化。

## 附录 {#appendix}

以下各节提供了有关[!DNL Consents & Preferences]数据类型的其他参考信息。

### xdm:val {#choice-values}的已接受值

下表概述了`xdm:val`的已接受值：

| 值 | 标题 | 描述 |
| --- | --- | --- |
| `y` | 是 | 客户已选择同意或优惠。 换言之，他们&#x200B;**同意使用其数据，如所述同意或偏好所示。** |
| `n` | 否 | 客户已选择不同意或拒绝。 换言之，他们&#x200B;**不同意按照有关同意或偏好来使用其数据。** |
| `p` | 待验证 | 系统尚未收到最终同意或偏好值。 这通常作为需要两步核查的同意的一部分。 例如，如果客户选择接收电子邮件，则该同意会设置为`p`，直到他们选择电子邮件中的链接来验证他们提供了正确的电子邮件地址，此时该同意会将更新为`y`。<br><br>如果此同意或偏好不使用两套验证流程，则 `p` 可选择可用于指示客户尚未响应同意提示。例如，在客户响应同意提示之前，您可以在网站的第一页上自动将值设置为`p`。 在不需要明确同意的司法管辖区，您还可以使用它来指示客户未明确选择退出（换言之，假定客户同意）。 |
| `u` | Unknown | 客户的同意或偏好信息未知。 |
| `LI` | 合法利益 | 出于特定目的收集和处理这些数据的正当商业利益，超过了数据对个人的潜在损害。 |
| `CT` | 合同 | 为达到指定目的而收集数据是为了履行与个人的合同义务。 |
| `CP` | 遵守法律义务 | 为达到特定目的而收集数据，是为了履行企业的法律义务。 |
| `VI` | 个人的切身利益 | 为了保护个人的切身利益，必须收集特定目的的数据。 |
| `PI` | 公共利益 | 为特定目的收集数据，必须为公共利益或行使官方权力而进行任务。 |

### xdm:preferred {#preferred-values}的已接受值

下表概述了`xdm:preferred`的已接受值：

| 值 | 描述 |
| --- | --- |
| `email` | 电子邮件消息. |
| `push` | 推送通知. |
| `inApp` | 应用程序内消息. |
| `sms` | 短信消息. |
| `phone` | 电话通话互动。 |
| `phyMail` | 邮件。 |
| `inVehicle` | 车内消息。 |
| `inHome` | 家庭内消息。 |
| `iot` | 物联网(IoT)消息。 |
| `social` | 社交媒体内容。 |
| `other` | 不符合标准渠道的类别。 |
| `none` | 没有首选渠道。 |
| `unknown` | 首选渠道未知。 |

### 完整[!DNL Consents & Preferences]模式{#full-schema}

要视图[!DNL Consents & Preferences]数据类型的完整模式，请参阅[官方XDM存储库](https://github.com/adobe/xdm/blob/master/components/datatypes/consent-preferences.schema.json)。
