---
solution: Experience Platform
title: 同意和偏好设置架构字段组
description: 了解“同意和首选项”架构字段组。
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: be35c5398cd96cdfe424c5088db288ba4061ac4a
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# [!UICONTROL 同意和首选项]字段组

[!UICONTROL 同意和首选项]是[[!DNL XDM Individual Profile] 类](../../classes/individual-profile.md)的标准字段组，用于捕获单个客户的同意和首选项信息。

>[!NOTE]
>
>由于该字段组仅与[!DNL XDM Individual Profile]兼容，因此不能用于[!DNL XDM ExperienceEvent]架构。 如果要在体验事件架构中包含同意和偏好设置数据，请改用[自定义字段组](../../ui/resources/field-groups.md#create)将[[!UICONTROL 同意隐私、个性化设置和营销偏好]数据类型](../../data-types/consents.md)添加到架构中。

## 字段组结构 {#structure}

[!UICONTROL 同意和首选项]字段组提供一个对象类型字段`consents`以捕获同意和首选项信息。 此字段扩展了[[!UICONTROL 同意隐私、个性化和营销首选项]数据类型](../../data-types/consents.md)，删除了`adID`字段并添加了`idSpecific`映射字段。

![](../../images/field-groups/consent.png)

>[!TIP]
>
>请参阅[探索XDM资源](../../ui/explore.md)的指南，了解如何查找任何XDM资源并在平台UI中检查其结构的步骤。

The following JSON shows an example of the type of data that the [!UICONTROL Consents and Preferences] field group can process. For information on how to use most of the fields provided by the field group, refer to the guide on the [Consents and Preferences data type](../../data-types/consents.md). The subsections below focus on the unique attributes that the field group adds to the data type.

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
>You can generate sample JSON data for any XDM schema that you define in Experience Platform in order to help visualize how your customer consent and preference data should be mapped. See the following documentation for more information:
>
>* [Generate sample data in the UI](../../ui/sample.md)
>* [在API中生成示例数据](../../api/sample-data.md)

### `idSpecific`

`idSpecific` can be used when a particular consent or preference does not universally apply to a customer, but is restricted to a single device or ID. 例如，客户可以选择不接收发送到某个地址的电子邮件，而允许发送到另一个地址的电子邮件。

>[!IMPORTANT]
>
>Channel-level consents and preferences (i.e. those provided under `consents` outside of `idSpecific`) apply to all IDs within that channel. Therefore, all channel-level consents and preferences directly effect whether equivalent ID- or device-specific settings are honored:
>
>* If the customer has opted out at the channel level, then any equivalent consents or preferences in `idSpecific` are ignored.
>* If the channel-level consent or preference is not set, or the customer has opted in, then the equivalent consents or preferences in `idSpecific` are honored.

Each key in the `idSpecific` object represents a specific identity namespace recognized by Adobe Experience Platform Identity Service. 虽然您可以定义自己的自定义命名空间来对不同的标识符进行分类，但建议您使用身份服务提供的标准命名空间之一来减小Real-Time Customer Profile的存储大小。 有关标识命名空间的详细信息，请参阅标识服务文档中的[标识命名空间概述](../../../identity-service/features/namespaces.md)。

每个命名空间对象的键代表客户为其设置了首选项的唯一标识值。 每个标识值可以包含一组完整的同意和首选项，其格式与`consents`相同。

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

在`idSpecific`部分提供的`marketing`对象中，`any`和`preferred`字段不受支持。 这些字段只能在用户级别配置。 此外，`email`、`sms`和`push`的`idSpecific`营销首选项不支持`subscriptions`字段。

还只能在`idSpecific`部分提供同意： `adID`。 下面的子部分介绍了此字段。

#### `adID`

`adID`同意表示客户同意是否可以使用广告商ID（IDFA或GAID）在此设备上的应用程序间链接客户。 此值只能在`idSpecific`节中的`ECID`标识命名空间下配置，不能为其他命名空间或此字段组的用户级别进行设置。

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
>您不应直接设置此值，因为Adobe Experience Platform Mobile SDK会在适当的时候自动设置它。

## 使用字段组收录数据 {#ingest}

为了使用[!UICONTROL 同意和首选项]字段组从您的客户那里获取同意数据，您必须基于包含该字段组的架构创建数据集。

See the tutorial on [creating a schema in the UI](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) for steps on how to assign field groups to fields. Once you have created a schema containing a field with the [!UICONTROL Consents and Preferences] field group, refer to the section on [creating a dataset](../../../catalog/datasets/user-guide.md#create) in the dataset user guide, following the steps to create a dataset with an existing schema.

>[!IMPORTANT]
>
>If you want to send consent data to [!DNL Real-Time Customer Profile], it is required that you create a [!DNL Profile]-enabled schema based on the [!DNL XDM Individual Profile] class that contains the [!UICONTROL Consents and Preferences] field group. The dataset that you create based on that schema must also be enabled for [!DNL Profile]. Refer to the tutorials linked above for specific steps related to [!DNL Real-Time Customer Profile] requirements for schemas and datasets.
>
>In addition, you must also ensure that your merge policies are configured to prioritize the dataset(s) that contain the latest consent and preference data, in order for customer profiles to be updated correctly. See the overview on [merge policies](../../../rtcdp/profile/merge-policies.md) for more information.

## Handling consent and preference changes

When a customer changes their consents or preferences on your website, these changes should be collected and immediately enforced using the [Adobe Experience Platform Web SDK](../../../web-sdk/commands/setconsent.md). If a customer opts out of data collection, all data collection must immediately cease. If a customer opts out of personalization, then there should be no personalization present on the next page they load.

## 后续步骤

This document covered the structure and use of the [!UICONTROL Consents and Preferences] field group. For more information on the other fields provided by the field group, see the document on the [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] data type](../../data-types/consents.md).
