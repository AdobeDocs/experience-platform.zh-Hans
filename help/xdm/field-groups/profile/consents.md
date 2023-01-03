---
solution: Experience Platform
title: 同意和首选项架构字段组
topic-legacy: overview
description: 本文档概述了同意和首选项架构字段组。
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# [!UICONTROL 同意和首选项] 字段组

[!UICONTROL 同意和首选项] 是的标准字段组 [[!DNL XDM Individual Profile] 类](../../classes/individual-profile.md) 来捕获个人客户的同意和首选项信息。

>[!NOTE]
>
>由于此字段组仅与 [!DNL XDM Individual Profile]，不能用于 [!DNL XDM ExperienceEvent] 模式。 如果要在体验事件架构中包含同意和首选项数据，请添加 [[!UICONTROL 隐私、个性化和营销首选项的同意] 数据类型](../../data-types/consents.md) 通过使用 [自定义字段组](../../ui/resources/field-groups.md#create) 中。

## 字段组结构 {#structure}

的 [!UICONTROL 同意和首选项] 字段组提供单个对象类型字段， `consents`，以捕获同意和首选项信息。 此字段将扩展 [[!UICONTROL 隐私、个性化和营销首选项的同意] 数据类型](../../data-types/consents.md)，删除 `adID` 字段和添加 `idSpecific` 映射字段。

![](../../images/field-groups/consent.png)

>[!TIP]
>
>请参阅 [浏览XDM资源](../../ui/explore.md) 要了解如何查找任何XDM资源并在Platform UI中检查其结构的步骤，请访问。

以下JSON显示了 [!UICONTROL 同意和首选项] 字段组可以处理。 有关如何使用字段组提供的大多数字段的信息，请参阅 [同意和首选项数据类型](../../data-types/consents.md). 以下子部分重点介绍字段组添加到数据类型的唯一属性。

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
>* [在API中生成示例数据](../../api/sample-data.md)


### `idSpecific`

`idSpecific` 当特定同意或首选项并非普遍适用于客户，但仅限于单个设备或ID时，可以使用。 例如，客户可以选择不接收指向一个地址的电子邮件，而可能允许向另一个地址发送电子邮件。

>[!IMPORTANT]
>
>渠道级别同意和首选项(即 `consents` 外部 `idSpecific`)应用于该渠道中的所有ID。 因此，无论是接受对等的ID还是设备特定的设置，所有渠道级别的同意和首选项都会直接影响：
>
>* 如果客户在渠道级别选择退出，则 `idSpecific` 将被忽略。
>* 如果未设置渠道级别的同意或首选项，或者客户已选择加入，则 `idSpecific` 很荣幸。


中的每个键 `idSpecific` 对象表示由Adobe Experience Platform Identity Service识别的特定身份命名空间。 虽然您可以定义自己的自定义命名空间以对不同的标识符进行分类，但建议您使用Identity Service提供的标准命名空间之一来减小实时客户配置文件的存储大小。 有关身份命名空间的更多信息，请参阅 [身份命名空间概述](../../../identity-service/namespaces.md) （在Identity Service文档中）。

每个命名空间对象的键表示客户为其设置首选项的唯一标识值。 每个标识值可以包含一组完整的同意和首选项，格式与 `consents`.

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
  "ECID": {
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

在 `marketing` 在 `idSpecific` , `any` 和 `preferred` 不支持字段。 这些字段只能在用户级别配置。 此外， `idSpecific` 营销首选项 `email`, `sms`和 `push` 不支持 `subscriptions` 字段。

此外，还有一个同意，该同意仅可在 `idSpecific` 部分： `adID`. 下文小节将介绍此字段。

#### `adID`

的 `adID` 同意表示客户同意是否可以使用广告商ID（IDFA或GAID）在此设备上的多个应用程序中链接客户。 此值只能在 `ECID` 标识命名空间 `idSpecific` ，不能为其他命名空间或此字段组的用户级别设置。

```json
"idSpecific": {
  "ECID": {
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
>
>您不应直接设置此值，因为Adobe Experience Platform Mobile SDK会在适当时自动设置此值。

## 使用字段组摄取数据 {#ingest}

为了使用 [!UICONTROL 同意和首选项] 字段组以从客户那里摄取同意数据，则必须基于包含该字段组的架构创建数据集。

请参阅 [在UI中创建架构](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) 有关如何将字段组分配给字段的步骤。 创建包含字段的架构后，便可使用 [!UICONTROL 同意和首选项] 字段组，请参阅 [创建数据集](../../../catalog/datasets/user-guide.md#create) 在数据集用户指南中，按照使用现有架构创建数据集的步骤操作。

>[!IMPORTANT]
>
>如果您要将同意数据发送到 [!DNL Real-Time Customer Profile]，则需要您创建 [!DNL Profile]启用的架构基于 [!DNL XDM Individual Profile] 包含类 [!UICONTROL 同意和首选项] 字段组。 您基于该架构创建的数据集还必须在 [!DNL Profile]. 有关与 [!DNL Real-Time Customer Profile] 架构和数据集的要求。
>
>此外，您还必须确保将合并策略配置为对包含最新同意和首选项数据的数据集优先级，以便正确更新客户配置文件。 请参阅 [合并策略](../../../rtcdp/profile/merge-policies.md) 以了解更多信息。

## 处理同意和首选项更改

当客户在您的网站上更改其同意或首选项时，应收集并立即使用 [Adobe Experience Platform Web SDK](../../../edge/consent/supporting-consent.md). 如果客户选择退出数据收集，则所有数据收集必须立即停止。 如果客户选择退出个性化，则他们访问的下一个页面上不应存在个性化。

## 后续步骤

本文档介绍了 [!UICONTROL 同意和首选项] 字段组。 有关字段组提供的其他字段的详细信息，请参阅 [[!UICONTROL 隐私、个性化和营销首选项的同意] 数据类型](../../data-types/consents.md).
