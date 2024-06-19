---
solution: Experience Platform
title: 同意和偏好设置架构字段组
description: 了解同意和偏好设置架构字段组。
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: b08c6cf12a38f79e019544dea91913a77bd6490a
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# [!UICONTROL 同意和偏好设置] 字段组

[!UICONTROL 同意和偏好设置] 是的标准字段组 [[!DNL XDM Individual Profile] 类](../../classes/individual-profile.md) 捕获单个客户的同意和偏好设置信息。

>[!NOTE]
>
>由于此字段组仅与 [!DNL XDM Individual Profile]，它不能用于 [!DNL XDM ExperienceEvent] 模式。 如果您想在体验事件架构中包含同意和偏好设置数据，请添加 [[!UICONTROL 隐私、个性化和营销偏好设置的同意] 数据类型](../../data-types/consents.md) 到架构中 [自定义字段组](../../ui/resources/field-groups.md#create) 而是。

## 字段组结构 {#structure}

此 [!UICONTROL 同意和偏好设置] 字段组提供单个对象类型字段， `consents`，以获取同意和偏好设置信息。 此字段可扩展 [[!UICONTROL 隐私、个性化和营销偏好设置的同意] 数据类型](../../data-types/consents.md)，删除 `adID` 字段并添加 `idSpecific` 映射字段。

![](../../images/field-groups/consent.png)

>[!TIP]
>
>请参阅指南，网址为 [探索XDM资源](../../ui/explore.md) ，以了解有关如何在Platform UI中查找任何XDM资源并检查其结构的步骤。

以下JSON显示了以下数据类型的一个示例： [!UICONTROL 同意和偏好设置] 字段组可以处理。 有关如何使用字段组提供的大多数字段的信息，请参阅 [同意和偏好设置数据类型](../../data-types/consents.md). 以下子部分重点介绍字段组添加到数据类型的唯一属性。

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
>您可以为在Experience Platform中定义的任何XDM架构生成示例JSON数据，以帮助可视化应如何映射客户同意和偏好设置数据。 有关更多信息，请参阅以下文档：
>
>* [在UI中生成示例数据](../../ui/sample.md)
>* [在API中生成示例数据](../../api/sample-data.md)

### `idSpecific`

`idSpecific` 当特定同意或偏好设置并非普遍适用于客户，而是仅限于单个设备或ID时可以使用。 例如，客户可以选择不接收发往一个地址的电子邮件，而可能允许发往另一个地址的电子邮件。

>[!IMPORTANT]
>
>渠道级别的同意和偏好设置（即下提供的同意和偏好设置） `consents` 外部 `idSpecific`)适用于该渠道中的所有ID。 因此，无论遵循等效的特定于ID还是特定于设备的设置，所有渠道级别的同意和偏好设置都会直接产生作用：
>
>* 如果客户在渠道级别选择退出，则任何等效的同意或偏好设置在 `idSpecific` 将被忽略。
>* 如果未设置渠道级别的同意或偏好设置，或者客户已选择加入，则等效的同意或偏好设置位于 `idSpecific` 荣誉。

中的各个键 `idSpecific` 对象表示Adobe Experience Platform Identity服务识别的特定身份命名空间。 虽然您可以定义自己的自定义命名空间来对不同的标识符进行分类，但建议您使用Identity Service提供的标准命名空间之一来减少实时客户档案的存储大小。 有关身份命名空间的更多信息，请参见 [身份命名空间概述](../../../identity-service/features/namespaces.md) 在Identity Service文档中。

每个命名空间对象的键表示客户为其设置了首选项的唯一标识值。 每个标识值都可以包含一组完整的同意和偏好设置，其格式与相同 `consents`.

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

范围 `marketing` 中提供的对象 `idSpecific` 部分， `any` 和 `preferred` 不支持字段。 这些字段只能在用户级别配置。 此外， `idSpecific` 营销偏好设置 `email`， `sms`、和 `push` 不支持 `subscriptions` 字段。

此外，只有在 `idSpecific` 部分： `adID`. 此字段将在以下子部分中介绍。

#### `adID`

此 `adID` 同意表示客户同意是否可以使用广告商ID（IDFA或GAID）在此设备上跨应用程序链接客户。 此值只能在 `ECID` 中的身份命名空间 `idSpecific` 部分，并且不能为其他命名空间或此字段组的用户级别设置。

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

要使用 [!UICONTROL 同意和偏好设置] 字段组要从客户那里摄取同意数据，您必须根据包含该字段组的架构创建数据集。

请参阅上的教程 [在UI中创建架构](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) 有关如何将字段组分配给字段的步骤。 创建包含字段的架构后，使用 [!UICONTROL 同意和偏好设置] 字段组，请参阅关于 [创建数据集](../../../catalog/datasets/user-guide.md#create) 在数据集用户指南中，按照使用现有架构创建数据集的步骤进行操作。

>[!IMPORTANT]
>
>如果要将同意数据发送至 [!DNL Real-Time Customer Profile]，您需要创建 [!DNL Profile] — 启用的架构基于 [!DNL XDM Individual Profile] 包含 [!UICONTROL 同意和偏好设置] 字段组。 还必须启用您根据该架构创建的数据集 [!DNL Profile]. 有关以下内容的特定步骤，请参阅以上链接的教程 [!DNL Real-Time Customer Profile] 架构和数据集的要求。
>
>此外，您还必须确保将合并策略配置为优先考虑包含最新同意和偏好设置数据的数据集，以便正确更新客户配置文件。 有关更多详细信息，请参阅 [合并策略](../../../rtcdp/profile/merge-policies.md) 以了解更多信息。

## 处理同意和偏好设置更改

当客户在您的网站上更改其同意或偏好设置时，应使用收集这些更改并立即实施 [Adobe Experience Platform Web SDK](../../../web-sdk/commands/setconsent.md). 如果客户选择退出数据收集，则必须立即停止所有数据收集。 如果客户选择退出个性化，则他们访问的下一个页面上应该不会显示个性化。

## 后续步骤

本文档介绍了 [!UICONTROL 同意和偏好设置] 字段组。 有关字段组提供的其他字段的更多信息，请参阅 [[!UICONTROL 隐私、个性化和营销偏好设置的同意] 数据类型](../../data-types/consents.md).
