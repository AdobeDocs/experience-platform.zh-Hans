---
solution: Experience Platform
title: 隐私/个性化/营销首选项（同意）架构字段组
topic-legacy: overview
description: 本文档概述了隐私/个性化/营销首选项（同意）架构字段组。
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '2304'
ht-degree: 2%

---

# [!UICONTROL 隐私/个性化/营销首选项（同意）] 字段组

[!UICONTROL 隐私/个性化/营销首选项（同意）] (以下简称 [!DNL Privacy & Consents] 字段组)是类的标准字段组 [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md)，用于捕获客户同意和首选项信息。

>[!NOTE]
>
>由于此字段组仅与[!DNL XDM Individual Profile]兼容，因此不能将其用于[!DNL XDM ExperienceEvent]架构。 如果要在体验事件架构中包含同意和首选项数据，请改用[自定义字段组](../../ui/resources/field-groups.md#create)将[[!UICONTROL 隐私、个性化和营销首选项的同意]数据类型](../../data-types/consents.md)添加到架构中。

## 字段组结构 {#structure}

>[!IMPORTANT]
>
>[!DNL Consents & Preferences]字段组旨在涵盖一系列同意和首选项管理用例。 因此，本文档以一般术语介绍了字段组字段的使用情况，并仅就如何解释这些字段的使用提出建议。 请咨询您的隐私法律团队，将字段组的结构与贵组织如何解释并向客户展示这些同意和首选项选择保持一致。

[!DNL Consents & Preferences]字段组提供了多个用于捕获&#x200B;**consent**&#x200B;和&#x200B;**preference**&#x200B;信息的字段。

同意是允许客户指定如何使用其数据的选项。 大多数同意具有法律方面的内容，因为某些司法辖区需要获得许可才能以特定方式使用数据，或者要求客户有权在不需要肯定同意的情况下停止使用（选择退出）。

首选项是一个选项，允许客户指定如何处理其品牌体验的不同方面。 这分为两类：

* **个性化首选项**:有关品牌应如何个性化交付给客户的体验的首选项。
* **营销首选项**:关于是否允许品牌通过各种渠道联系客户的首选项。

以下屏幕截图显示了字段组结构在平台UI中的显示方式：

![](../../images/field-groups/consent.png)

>[!TIP]
>
>有关如何查找任何XDM资源并在平台UI中检查其结构的步骤，请参阅[探索XDM资源](../../ui/explore.md)指南。

以下JSON显示了[!DNL Consents & Preferences]字段组可处理的数据类型示例。 以下各节提供了有关每个字段具体用途的信息。

```json
{
  "consents": {
    "collect": {
      "val": "VI"
    },
    "share": {
      "val": "y"
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "y"
      },
      "email": {
        "val": "y"
      }
    },
    "idSpecific": {
      "ECID": {
        "37784337855396895622558625508046772577": {
          "adID": {
            "val": "n",
          },
          "share": {
            "val": "n"
          },
          "marketing": {
            "push": {
              "val": "n",
              "time": "2020-09-30T01:02:33+00:00",
              "reason": "not relevant"
            }
          }
        }
      },
      "email": {
        "john@xyz.com": {
          "marketing": {
            "email": {
              "val": "y"
            }
          }
        }
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
>* [在UI中生成示例数据](../../ui/sample.md)
* [在API中生成示例数据](../../api/sample-data.md)


## 现场用例

以下各节提供了这些字段的预期用例。

### `collect`

`collect` 表示客户同意收集其数据。

```json
"collect" : {
  "val": "y"
}
```

| 属性 | 描述 |
| --- | --- |
| `val` | 客户为此用例提供的同意选择。 有关已接受的值和定义，请参阅[附录](#choice-values)。 |

{style=&quot;table-layout:auto&quot;}

### `share`

`share` 表示客户同意是否可以与第二方或第三方共享（或出售给）其数据。

```json
"share" : {
  "val": "y"
}
```

| 属性 | 描述 |
| --- | --- |
| `val` | 客户为此用例提供的同意选择。 有关已接受的值和定义，请参阅[附录](#choice-values)。 |

{style=&quot;table-layout:auto&quot;}

### `personalize` {#personalize}

`personalize` 可捕获客户的偏好，以确定其数据可用于个性化的方式。客户可以选择退出特定的个性化用例，或完全退出个性化。

>[!IMPORTANT]
`personalize` 不包括营销用例。例如，如果客户选择退出所有渠道的个性化，则他们不应停止通过这些渠道接收通信。 相反，他们收到的消息应是通用的，而不应基于其用户档案。
同一示例中，如果客户选择退出所有渠道的直接营销（通过`marketing`，如[下一节](#marketing)中所述），则该客户即使允许个性化，也不应收到任何消息。

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
| `val` | 客户为指定用例提供的个性化首选项。 如果客户无需获得同意，则此字段的值应指示进行个性化的基础。 有关已接受的值和定义，请参阅[附录](#choice-values)。 |

{style=&quot;table-layout:auto&quot;}

### `marketing` {#marketing}

`marketing` 捕获客户有关其数据可用于哪些营销目的的偏好。客户可以选择退出特定营销用例，或完全退出直接营销。

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
| `preferred` | 指示客户接收通信的首选渠道。 有关已接受的值，请参阅[附录](#preferred-values)。 |
| `any` | 代表客户对整体直接营销的偏好。 除非被`marketing`下提供的其他子字段覆盖，否则此字段中提供的同意首选项将被视为任何营销渠道的“默认”首选项。 如果您计划使用更详细的同意选项，建议您排除此字段。<br><br>如果将该值设置为，则 `n`应忽略所有更具体的个性化设置。如果将该值设置为`y`，则所有更细粒度的个性化选项也应当被视为`y`，除非明确设置为`n`。 如果未设置该值，则应按照指定的方式处理每个个性化选项的值。 |
| `email` | 指示客户是否同意接收电子邮件。 客户还可以为此渠道中的单个订阅提供首选项。 有关更多信息，请参阅下面[subscriptions](#subscriptions)部分。 |
| `push` | 指示客户是否允许接收推送通知。 客户还可以为此渠道中的单个订阅提供首选项。 有关更多信息，请参阅下面[subscriptions](#subscriptions)部分。 |
| `sms` | 指示客户是否同意接收短信。 客户还可以为此渠道中的单个订阅提供首选项。 有关更多信息，请参阅下面[subscriptions](#subscriptions)部分。 |
| `val` | 客户提供的特定用例首选项。 如果客户不必被提示提供同意，则此字段的值应指示进行营销用例的依据。 有关已接受的值和定义，请参阅[附录](#choice-values)。 |
| `time` | 营销首选项更改时的ISO 8601时间戳（如果适用）。 请注意，如果任何单个首选项的时间戳与`metadata`下提供的时间戳相同，则不为该首选项设置此字段。 |
| `reason` | 当客户选择退出营销用例时，此字符串字段表示客户选择退出的原因。 |

{style=&quot;table-layout:auto&quot;}

#### `subscriptions` {#subscriptions}

`marketing`对象的`email`、`push`和`sms`属性能够表示这些单独渠道的客户订阅。 这可以通过向相关营销渠道添加`subscriptions`属性来完成。

```json
"marketing": {
  "email": {
    "val": "y",
    "subscriptions": {
      "daily-mail": {
        "val": "y",
        "type": "paid",
        "subscribers": {
          "john@xyz.com": {
            "time": "2019-01-01T15:52:25+00:00",
            "source": "website"
          }
        }
      },
      "shipped": {
        "val": "y",

        "subscribers": {
          "john@xyz.com": {
            "time": "2021-01-01T08:32:53+07:00",
            "source": "website"
          },
          "jane@xyz.com": {
            "time": "2020-02-03T07:54:21+07:00",
            "source": "call center",
          }
        }
      }
    }
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `type` | 订阅类型。 这可以是任何描述性字符串，前提是它不超过15个字符。 |
| `subscribers` | 可选的映射类型字段，表示订阅了特定订阅的标识符集（如电子邮件地址或电话号码）。 此对象中的每个键都表示相关的标识符，并包含两个子属性： <ul><li>`time`:身份订阅时的ISO 8601时间戳（如果适用）。</li><li>`source`:订阅者源自的源。这可以是任何描述性字符串，前提是它不超过15个字符。</li></ul> |

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
| `time` | 上次更新客户同意和首选项的ISO 8601时间戳。 为了减少负载和复杂性，可以使用此字段，而不是将时间戳应用到单个首选项。 在单个首选项下提供`time`值将覆盖该特定首选项的`metadata`时间戳。 |

{style=&quot;table-layout:auto&quot;}

### `idSpecific`

`idSpecific` 当特定同意或首选项并非普遍适用于客户，但仅限于单个设备或ID时，可以使用。例如，客户可以选择不接收指向一个地址的电子邮件，而可能允许向另一个地址发送电子邮件。

>[!IMPORTANT]
渠道级别同意和首选项（即在`idSpecific`以外的`consents`下提供的首选项）适用于该渠道中的ID。 因此，无论是接受对等的ID还是设备特定的设置，所有渠道级别的同意和首选项都会直接影响：
* 如果客户已在渠道级别选择退出，则会忽略`idSpecific`中的任何对等同意或首选项。
* 如果未设置渠道级别的同意或首选项，或者客户已选择加入，则符合`idSpecific`中的等同同意或首选项。


`idSpecific`对象中的每个键都表示由Adobe Experience Platform Identity Service识别的特定身份命名空间。 虽然您可以定义自己的自定义命名空间以对不同的标识符进行分类，但建议您使用Identity Service提供的标准命名空间之一来减小实时客户配置文件的存储大小。 有关身份命名空间的更多信息，请参阅Identity Service文档中的[身份命名空间概述](../../../identity-service/namespaces.md)。

每个命名空间对象的键表示客户为其设置首选项的唯一标识值。 每个标识值可以包含一组完整的同意和首选项，格式与`consents`相同。

```json
"idSpecific": {
  "email": {
    "jdoe@example.com": {
      "marketing": {
        "email": {
          "val": "n"
        }
      }
    }
  },
  "ECID" : {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

在`idSpecific`部分中提供的`marketing`对象中，不支持`any`和`preferred`字段。 这些字段只能在用户级别配置。 此外，`email`、`sms`和`push`的`idSpecific`营销首选项不支持`subscriptions`字段。

此外，还有一个同意仅可在`idSpecific`部分中提供：`adID`。 下文小节将介绍此字段。

#### `adID`

`adID`同意表示客户同意是否可以使用广告商ID（IDFA或GAID）在此设备上的各个应用程序中链接客户。 此值只能在`idSpecific`部分的`ECID`标识命名空间下进行配置，不能为其他命名空间或此字段组的用户级别设置。

```json
"idSpecific": {
  "ECID" : {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

>[!NOTE]
您不应直接设置此值，因为Adobe Experience Platform Mobile SDK会在适当时自动设置此值。

## 使用字段组摄取数据 {#ingest}

要使用[!DNL Consents & Preferences]字段组从客户那里摄取同意数据，您必须基于包含该字段组的架构创建数据集。

有关如何将字段组分配给字段的步骤，请参阅有关在UI](http://www.adobe.com/go/xdm-schema-editor-tutorial-en)中创建架构的教程。 [创建包含字段（包含[!DNL Consents & Preferences]字段组）的架构后，请参阅数据集用户指南中[创建数据集](../../../catalog/datasets/user-guide.md#create)部分，以按照使用现有架构创建数据集的步骤操作。

>[!IMPORTANT]
如果要向[!DNL Real-time Customer Profile]发送同意数据，则需要根据包含[!DNL Consents & Preferences]字段组的[!DNL XDM Individual Profile]类创建启用[!DNL Profile]的架构。 还必须为[!DNL Profile]启用您基于该架构创建的数据集。 有关架构和数据集的[!DNL Real-time Customer Profile]要求的具体步骤，请参阅上面链接的教程。
此外，您还必须确保将合并策略配置为对包含最新同意和首选项数据的数据集优先级，以便正确更新客户配置文件。 有关更多信息，请参阅[合并策略](../../../rtcdp/profile/merge-policies.md)的概述。

## 处理同意和首选项更改

当客户在您的网站上更改其同意或首选项时，应使用[Adobe Experience Platform Web SDK](../../../edge/consent/supporting-consent.md)收集并立即强制执行这些更改。 如果客户选择退出数据收集，则所有数据收集必须立即停止。 如果客户选择退出个性化，则他们访问的下一个页面上不应存在个性化。

## 附录 {#appendix}

以下各节提供了有关[!DNL Consents & Preferences]字段组的其他参考信息。

### `val` {#choice-values}的已接受值

下表概述了`val`的接受值：

| 值 | 标题 | 描述 |
| --- | --- | --- |
| `y` | 是 | 客户已选择同意或首选项。 换言之，他们&#x200B;**do**&#x200B;同意使用其数据，如相关同意或偏好所示。 |
| `n` | 否 | 客户已选择退出同意或首选项。 换言之，他们&#x200B;**不**&#x200B;同意使用其数据，如相关同意或偏好所示。 |
| `p` | 待验证 | 系统尚未收到最终同意或偏好值。 这通常用作需要两步验证的同意的一部分。 例如，如果客户选择接收电子邮件，则该同意将设置为`p`，直到他们选择电子邮件中的链接来验证他们是否提供了正确的电子邮件地址，此时同意将更新为`y`。<br><br>如果此同意或首选项不使用两套验证过程，则 `p` 可以使用选择指示客户尚未响应同意提示。例如，您可以在客户响应同意提示之前，在网站的首页上自动将值设置为`p`。 在不需要明确同意的司法管辖区中，您还可以使用它来指示客户未明确选择退出（换言之，假设同意）。 |
| `u` | Unknown | 客户的同意或首选项信息未知。 |
| `LI` | 合法利益 | 为特定目的收集和处理这些数据的正当商业利益，超过了这些数据对个人的潜在损害。 |
| `CT` | 合同 | 为达到指定目的而收集数据，是为了履行与个人的合同义务。 |
| `CP` | 遵守法律义务 | 为达到指定目的而收集数据，是为了履行业务的法律义务。 |
| `VI` | 个人的重大利益 | 为了保护个人的重大利益，需要为特定目的收集数据。 |
| `PI` | 公共利益 | 为特定目的收集数据是为了公共利益或行使官方权力而执行一项任务所必需的。 |

{style=&quot;table-layout:auto&quot;}

### `preferred` {#preferred-values}的已接受值

下表概述了`preferred`的接受值：

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

### 完整[!DNL Consents & Preferences]架构{#full-schema}

要查看[!DNL Consents & Preferences]字段组的完整架构，请参阅[官方XDM存储库](https://github.com/adobe/xdm/blob/master/components/datatypes/consent-preferences.schema.json)。
