---
description: 本页介绍从Adobe Experience Platform导出到目标的数据中的消息格式和配置文件转换。
title: 消息格式
exl-id: ab05d34e-530f-456c-b78a-7f3389733d35
source-git-commit: b5d8a1c31705ffe72dadc4fff8626acb7081444a
workflow-type: tm+mt
source-wordcount: '2488'
ht-degree: 0%

---

# 消息格式

## 先决条件 — Adobe Experience Platform概念 {#prerequisites}

要了解Adobe端的消息格式以及用户档案配置和转换过程，请熟悉以下Experience Platform概念：

* **体验数据模型(XDM)**。 [XDM概述](../../../../xdm/home.md)和[如何在Adobe Experience Platform中创建XDM架构](../../../../xdm/tutorials/create-schema-ui.md)。
* **类**。 [在UI中创建和编辑类](../../../../xdm/ui/resources/classes.md)。
* **IdentityMap**。 标识映射表示Adobe Experience Platform中所有最终用户标识的映射。 请参阅`xdm:identityMap`XDM字段词典[中的](../../../../xdm/schema/field-dictionary.md)。
* **区段成员资格**。 [segmentMembership](../../../../xdm/schema/field-dictionary.md) XDM属性通知配置文件是哪些受众的成员。 对于`status`字段中的三个不同值，请阅读有关[受众成员资格详细信息架构字段组](../../../../xdm/field-groups/profile/segmentation.md)的文档。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值均区分大小写&#x200B;****。 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 支持的集成类型 {#supported-integration-types}

有关哪些类型的集成支持此页面上描述的功能，请参阅下表。

| 集成类型 | 支持功能 |
|---|---|
| 实时（流）集成 | 是 |
| 基于文件（批处理）的集成 | 是（下面图中仅步骤1和2） |

## 概述 {#overview}

本页介绍从Adobe Experience Platform导出到目标的数据中的消息格式和配置文件转换。

Adobe Experience Platform会以各种数据格式将数据导出到大量目标。 目标类型的一些示例包括广告平台(Google)、社交网络(Facebook)和云存储位置(Amazon S3、Azure事件中心)。

Experience Platform可以调整导出用户档案的消息格式，以与您这边的预期格式匹配。 要了解此自定义设置，请务必了解以下概念：

* Adobe Experience Platform中的源(1)和目标(2) XDM架构
* 合作伙伴端的预期消息格式(3)，以及
* XDM架构和预期消息格式之间的转换层，可通过创建[消息转换模板](#using-templating)来定义该转换层。

![架构到JSON的转换](../../assets/functionality/destination-server/transformations-3-steps.png)

Experience Platform使用XDM架构以一致且可重用的方式描述数据结构。

<!--

Users who want to activate data to your destination need to map the fields in their Experience Platform datasets to a schema that translates to your destination's expected format. Adobe will create a custom field group for your company to add to the target schema. The fields in the field group depend on the profile attribute fields that you can receive.

-->

**Source XDM架构(1)**：此项目是指客户在Experience Platform中使用的架构。 在Experience Platform中，在激活目标工作流的[映射步骤](../../../ui/activate-segment-streaming-destinations.md#mapping)中，客户将字段从其XDM架构映射到目标的目标架构(2)。

**目标XDM架构(2)**：根据目标预期格式的JSON标准架构(3)以及目标可以解释的属性，您可以在目标XDM架构中定义配置文件属性和身份。 您可以在目标配置的[schemaConfig](../../functionality/destination-configuration/schema-configuration.md)和[identityNamespaces](../../functionality/destination-configuration/identity-namespace-configuration.md)对象中执行此操作。

**目标配置文件属性的JSON标准架构(3)**：此示例表示您的平台支持的所有配置文件属性及其类型（例如：对象、字符串、数组）的[JSON架构](https://json-schema.org/learn/miscellaneous-examples.html)。 目标可以支持的示例字段可以是`firstName`、`lastName`、`gender`、`email`、`phone`、`productId`、`productName`等。 您需要[消息转换模板](#using-templating)来定制从Experience Platform导出的数据，使其符合您的预期格式。

根据上述架构转换，下面说明了源XDM架构与合作伙伴端示例架构之间的配置文件配置更改方式：

![转换消息示例](../../assets/functionality/destination-server/transformations-with-examples.png)

## 快速入门 — 转换三个基本属性 {#getting-started}

为了演示配置文件转换过程，以下示例在Adobe Experience Platform中使用了三个常见的配置文件属性：**名字**、**姓氏**&#x200B;和&#x200B;**电子邮件地址**。

>[!NOTE]
>
>在&#x200B;**激活目标工作流**&#x200B;的[映射](../../../ui/activate-segment-streaming-destinations.md#mapping)步骤中，客户将属性从源XDM架构映射到Adobe Experience Platform UI中的合作伙伴XDM架构。

假设您的平台可以接收如下消息格式：

```shell
POST https://YOUR_REST_API_URL/users/
Content-Type: application/json
Authorization: Bearer YOUR_REST_API_KEY

{
  "attributes":
    {
      "first_name": "Yours",
      "last_name": "Truly",
      "external_id": "yourstruly@adobe.com"
    }
}
```

考虑到报文格式，相应的转换如下：

| Adobe端的合作伙伴XDM架构中的属性 | 转换 | 您这边HTTP消息中的属性 |
|---------|----------|---------|
| `_your_custom_schema.firstName` | `attributes.first_name` | `first_name` |
| `_your_custom_schema.lastName` | `attributes.last_name` | `last_name` |
| `personalEmail.address` | `attributes.external_id` | `external_id` |

{style="table-layout:auto"}

## Experience Platform中的配置文件结构 {#profile-structure}

要进一步了解页面上下文的示例，请务必了解Experience Platform中的用户档案结构。

配置文件包含3个部分：

* `segmentMembership` （始终显示在配置文件中）
   * 此部分包含配置文件中存在的所有受众。 受众可以具有以下两种状态之一：`realized`或`exited`。
* `identityMap` （始终显示在配置文件中）
   * 此部分包含配置文件中存在的所有身份(电子邮件、Google GAID、Apple IDFA等)，以及映射为在激活工作流中导出的用户。
* 属性（根据目标配置，这些属性可能出现在配置文件中）。 要注意的是，预定义属性和自由格式属性之间也存在一些细微差异：
   * 对于&#x200B;*自由格式属性*，如果配置文件中存在该属性，则它们包含`.value`路径（请参阅示例1中的`lastName`属性）。 如果它们不在配置文件中，则不会包含`.value`路径（请参阅示例1中的`firstName`属性）。
   * 对于&#x200B;*预定义属性*，这些属性不包含`.value`路径。 配置文件中存在的所有映射属性都将出现在属性映射中。 不存在属性（请参阅示例2 — 配置文件上不存在`firstName`属性）。

请参阅下面两个Experience Platform中的配置文件示例：

### 具有自由格式属性的`segmentMembership`、`identityMap`和属性的示例1 {#example-1}

```json
{
  "segmentMembership": {
    "ups": {
      "11111111-1111-1111-1111-111111111111": {
        "lastQualificationTime": "2019-04-15T02:41:50.000+0000",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "mobileIds": [
      {
        "id": "e86fb215-0921-4537-bc77-969ff775752c"
      }
    ]
  },
  "attributes": {
    "firstName": {
    },
    "lastName": {
      "value": "lastName"
    }
  }
}
```

### 示例2，具有预定义属性的`segmentMembership`、`identityMap`和属性 {#example-2}

```json
{
  "segmentMembership": {
    "ups": {
      "11111111-1111-1111-1111-111111111111": {
        "lastQualificationTime": "2019-04-15T02:41:50.000+0000",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "mobileIds": [
      {
        "id": "e86fb215-0921-4537-bc77-969ff775752c"
      }
    ]
  },
  "attributes": {
    "lastName": "lastName"
  }
}
```

## 使用模板语言进行身份、属性和受众成员资格转换 {#using-templating}

Adobe使用[Pebble templates](https://pebbletemplates.io/)（与[Jinja](https://jinja.palletsprojects.com/en/2.11.x/)类似的模板语言）将字段从Experience Platform XDM架构转换为目标支持的格式。

此部分提供了多个如何进行这些转换的示例 — 从输入XDM模式通过模板，然后输出到目标接受的有效负载格式。 下面的示例通过提高复杂性来显示，如下所示：

1. 简单转换示例。 了解模板化如何与[配置文件属性](#attributes)、[受众成员资格](#segment-membership)和[标识](#identities)字段的简单转换一起使用。
2. 合并上述字段的模板的复杂性增加：[创建发送受众和标识的模板](./message-format.md#segments-and-identities)和[创建发送区段、标识和配置文件属性的模板](#segments-identities-attributes)。
3. 包含聚合键的模板。 在目标配置中使用[可配置的聚合](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation)时，Experience Platform会根据受众ID、受众状态或身份命名空间等条件对导出到目标的配置文件进行分组。

### 配置文件属性 {#attributes}

要转换导出到目标的配置文件属性，请参阅下面的JSON和代码示例。

>[!IMPORTANT]
>
>有关Adobe Experience Platform中所有可用配置文件属性的列表，请参阅[XDM字段字典](../../../../xdm/schema/field-dictionary.md)。


**输入**

配置文件1：

```json
{
    "attributes": {
        "firstName": {
            "value": "Hermione"
    },
    "birthDate": {}
  }
}
```

配置文件2：

```json
{
  "attributes": {
    "firstName": {
      "value": "Harry"
    },
    "birthDate": {
        "value": "1980/07/31"
    }
  }
}
```

**模板**

>[!IMPORTANT]
>
>对于您使用的所有模板，在`""`目标服务器配置[中插入](../../functionality/destination-server/templating-specs.md)模板[之前，必须转义非法字符，如双引号](../../authoring-api/destination-server/create-destination-server.md)。 有关转义双引号的更多信息，请参阅[JSON标准](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/)中的第9章。

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            {% for attribute in profile.attributes %}
            "{{ attribute.key }}":
                {% if attribute.value is empty %}
                    null
                {% else %}
                    "{{ attribute.value.value }}"
                {% endif %}
            {% if not loop.last %},{% endif %}
            {% endfor %}
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**结果**


```json
{
    "profiles": [
        {
            "firstName": "Hermione",
            "birthDate": null
        },
        {
            "firstName": "Harry",
            "birthDate": "1980/07/31"
        }
    ]
}
```

### 受众会员资格 {#audience-membership}

[segmentMembership](../../../../xdm/schema/field-dictionary.md) XDM属性通知配置文件是哪些受众的成员。
对于`status`字段中的三个不同值，请阅读有关[受众成员资格详细信息架构字段组](../../../../xdm/field-groups/profile/segmentation.md)的文档。

**输入**

配置文件1：

```json
{
  "segmentMembership": {
    "ups": {
      "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "8f812592-3f06-416b-bd50-e7831848a31a": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      }
    }
  }
}
```

配置文件2：

```json
{
  "segmentMembership": {
    "ups": {
      "32396e4b-16f6-4033-9702-fc69b5e24e7c": {
        "lastQualificationTime": "2021-08-20T17:23:04Z",
        "status": "realized"
      },
      "af854278-894a-4192-a96b-320fbf2623fd": {
        "lastQualificationTime": "2021-08-20T16:44:37Z",
        "status": "realized"
      },
      "66505bf9-bc08-4bac-afbc-8b6706650ea4": {
        "lastQualificationTime": "2019-08-20T17:23:04Z",
        "status": "realized"
      }
    }
  }
}
```

**模板**

>[!IMPORTANT]
>
>对于您使用的所有模板，在`""`目标服务器配置[中插入](../../functionality/destination-server/templating-specs.md)模板[之前，必须转义非法字符，如双引号](../../authoring-api/destination-server/create-destination-server.md)。 有关转义双引号的更多信息，请参阅[JSON标准](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/)中的第9章。


```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                {% for segment in profile.segmentMembership.ups | added %}
                "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ],
                "remove": [
                {# Alternative syntax for filtering audiences by status: #}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ]
            }
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**结果**

```json
{
    "profiles": [
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "32396e4b-16f6-4033-9702-fc69b5e24e7c",
                    "af854278-894a-4192-a96b-320fbf2623fd",
                    "66505bf9-bc08-4bac-afbc-8b6706650ea4"
                ],
                "remove": [
                ]
            }
        }
    ]
}
```

### 身份标识 {#identities}

有关Experience Platform中标识的信息，请参阅[标识命名空间概述](../../../../identity-service/features/namespaces.md)。

**输入**

配置文件1：

```json
{
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    }
}
```

配置文件2：

```json
{
    "identityMap": {
        "email": [
            {
                "id": "jane.doe@example.com"
            }
        ]
    }
}
```

**模板**

>[!IMPORTANT]
>
>对于您使用的所有模板，在`""`目标服务器配置[中插入](../../functionality/destination-server/templating-specs.md)模板[之前，必须转义非法字符，如双引号](../../authoring-api/destination-server/create-destination-server.md)。 有关转义双引号的更多信息，请参阅[JSON标准](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/)中的第9章。

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}

                {# Add a comma only if you have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}

                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ]
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**结果**

```json
{
    "profiles": [
        {
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ]
        },
        {
            "identities": [
                {
                    "type": "email",
                    "id": "jane.doe@example.com"
                }
            ]
        }
    ]
}
```

### 创建用于发送受众和身份的模板 {#segments-and-identities}

此部分提供了Adobe XDM架构与合作伙伴目标架构之间常用转换的示例。
以下示例显示了如何转换受众成员资格和身份格式并将它们输出到您的目标。

**输入**

配置文件1：

```json
{
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            },
            "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
              "lastQualificationTime": "2019-11-20T13:15:49Z",
              "status": "realized"
            },
            "8f812592-3f06-416b-bd50-e7831848a31a": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "exited"
            }
        }
    }
}
```

配置文件2：

```json
{
    "identityMap": {
        "email": [
            {
                "id": "jane.doe@example.com"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2021-08-31T10:01:42Z",
                "status": "realized"
            }
        }
    }
}
```

**模板**

>[!IMPORTANT]
>
>对于您使用的所有模板，在`""`目标服务器配置[中插入](../../functionality/destination-server/templating-specs.md)模板[之前，必须转义非法字符，如双引号](../../authoring-api/destination-server/create-destination-server.md)。 有关转义双引号的更多信息，请参阅[JSON标准](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/)中的第9章。

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
                
                {# Add a comma only if you have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}
                
                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    {% for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ],
                "remove": [
                    {# Alternative syntax for filtering audiences by status: #}
                    {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ]
            }
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**结果**

以下`json`表示从Adobe Experience Platform中导出的数据。

```json
{
    "profiles": [
        {
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "identities": [
                {
                    "type": "email",
                    "id": "jane.doe@example.com"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075"
                ],
                "remove": []
            }
        }
    ]
}
```

### 创建用于发送区段、身份和配置文件属性的模板 {#segments-identities-attributes}

此部分提供了Adobe XDM架构与合作伙伴目标架构之间常用转换的示例。

另一个常见用例是导出包含受众成员资格、身份（例如：电子邮件地址、电话号码、广告ID）和配置文件属性的数据。 要以这种方式导出数据，请参阅以下示例：

**输入**

配置文件1：

```json
{
    "attributes": {
        "firstName": {
            "value": "Hermione"
        },
        "birthDate": {}
    },
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            },
            "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
              "lastQualificationTime": "2019-11-20T13:15:49Z",
              "status": "realized"
            },
            "8f812592-3f06-416b-bd50-e7831848a31a": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "exited"
            }
        }
    }
}
```

配置文件2：

```json
{
    "attributes": {
        "firstName": {
            "value": "Harry"
        },
        "birthDate": {
            "value": "1980/07/31"
        }
    },
    "identityMap": {
        "email": [
            {
                "id": "harry.p@example.com"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            }
        }
    }
}
```

**模板**

>[!IMPORTANT]
>
>对于您使用的所有模板，在`""`目标服务器配置[中插入](../../functionality/destination-server/templating-specs.md)模板[之前，必须转义非法字符，如双引号](../../authoring-api/destination-server/create-destination-server.md)。 有关转义双引号的更多信息，请参阅[JSON标准](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/)中的第9章。

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "attributes": {
            {% for attribute in profile.attributes %}
                "{{ attribute.key }}":
                    {% if attribute.value is empty %}
                        null
                    {% else %}
                        "{{ attribute.value.value }}"
                    {% endif %}
                {% if not loop.last %},{% endif %}
            {% endfor %}
            },
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}

                {# Add a comma only if we have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}

                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                {% for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ],
                "remove": [
                {# Alternative syntax for filtering audiences by status: #}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ]
            }
        }
    ]
}
```

**结果**

以下`json`表示从Adobe Experience Platform中导出的数据。

```json
{
    "profiles": [
        {
            "attributes": {
                "firstName": "Hermione",
                "birthDate": null
            },
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "attributes": {
                "firstName": "Harry",
                "birthDate": "1980/07/21"
            },
            "identities": [
                {
                    "type": "email",
                    "id": "harry.p@example.com"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075"
                ],
                "remove": []
            }
        }
    ]
}
```

### 在模板中包含Aggregation Key，以访问按不同条件分组的导出用户档案 {#template-aggregation-key}

在目标配置中使用[可配置的聚合](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation)时，可以根据受众ID、受众别名、受众成员资格或身份命名空间等条件对导出到目标的配置文件进行分组。

在消息转换模板中，您可以访问上述聚合键，如以下部分中的示例所示。 使用聚合密钥构造从Experience Platform导出的HTTP消息，以匹配目标所需的格式和速率限制。

#### 在模板中使用受众ID聚合密钥 {#aggregation-key-segment-id}

如果您使用[可配置的聚合](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation)并将`includeSegmentId`设置为true，则导出到目标的HTTP消息中的用户档案将按受众ID进行分组。 请参阅下文，了解如何在模板中访问受众ID。

**输入**

请考虑以下四个配置文件，其中：

* 前两个受众属于受众ID为`788d8874-8007-4253-92b7-ee6b6c20c6f3`的受众
* 第三个配置文件是受众ID为`8f812592-3f06-416b-bd50-e7831848a31a`的受众的一部分
* 第四个配置文件是上述两个受众的一部分。

配置文件1：

```json
{
   "attributes":{
      "firstName":{
         "value":"Hermione"
      }
   },
   "segmentMembership":{
      "ups":{
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

配置文件2：

```json
{
   "attributes":{
      "firstName":{
         "value":"Harry"
      }
   },
   "segmentMembership":{
      "ups":{
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

配置文件3：

```json
{
   "attributes":{
      "firstName":{
         "value":"Tom"
      }
   },
   "segmentMembership":{
      "ups":{
         "8f812592-3f06-416b-bd50-e7831848a31a":{
            "lastQualificationTime":"2021-02-20T12:00:00Z",
            "status":"realized"
         }
      }
   }
}
```

配置文件4：

```json
{
   "attributes":{
      "firstName":{
         "value":"Jerry"
      }
   },
   "segmentMembership":{
      "ups":{
         "8f812592-3f06-416b-bd50-e7831848a31a":{
            "lastQualificationTime":"2021-02-20T12:00:00Z",
            "status":"realized"
         },
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

**模板**

>[!IMPORTANT]
>
>对于您使用的所有模板，在`""`目标服务器配置[中插入](../../functionality/destination-server/templating-specs.md)模板[之前，必须转义非法字符，如双引号](../../authoring-api/destination-server/create-destination-server.md)。 有关转义双引号的更多信息，请参阅[JSON标准](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/)中的第9章。

请注意以下如何在模板中使用`audienceId`来访问受众ID。 此示例假定您将`audienceId`用于目标分类中的受众成员资格。 您可以改用任何其他字段名称，具体取决于您自己的分类。

```python
{
    "audienceId": "{{ input.aggregationKey.segmentId }}",
    "profiles": [
        {% for profile in input.profiles %}
        {
            "first_name": "{{ profile.attributes.firstName.value }}"
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**结果**

将用户档案导出到目标后，会根据其受众ID将其分为两个组。

```json
{
   "audienceId":"788d8874-8007-4253-92b7-ee6b6c20c6f3",
   "profiles":[
      {
         "firstName":"Hermione"
      },
      {
         "firstName":"Harry"
      },
      {
         "firstName":"Jerry"
      }
   ]
}
```

```json
{
   "audienceId":"8f812592-3f06-416b-bd50-e7831848a31a",
   "profiles":[
      {
         "firstName":"Tom"
      },
      {
         "firstName":"Jerry"
      }
   ]
}
```

#### 在模板中使用受众别名聚合密钥 {#aggregation-key-segment-alias}

如果您使用[可配置的聚合](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation)并将`includeSegmentId`设置为true，则还可以访问模板中的受众别名。

将以下行添加到模板，以访问按受众别名分组的导出用户档案。

```python
customerList={{input.aggregationKey.segmentAlias}}
```

#### 在模板中使用受众状态聚合密钥 {#aggregation-key-segment-status}

如果您使用[可配置的聚合](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation)并将`includeSegmentId`和`includeSegmentStatus`设置为true，则可以在模板中访问受众状态。 这样，您就可以根据是否应从区段中添加或删除用户档案，对导出到目标的HTTP消息中的用户档案进行分组。

可能的值包括：

* 已实现
* 已退出

将以下行添加到模板中，根据上述值在区段中添加或删除用户档案：

```python
action={% if input.aggregationKey.segmentStatus == "exited" %}REMOVE{% else %}ADD{% endif%}
```

#### 在模板中使用身份命名空间聚合密钥 {#aggregation-key-identity}

下面是一个示例，其中目标配置中的[可配置聚合](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation)设置为按身份命名空间聚合导出的配置文件，格式为`"namespaces": ["email", "phone"]`和`"namespaces": ["GAID", "IDFA"]`。 有关分组的更多详细信息，请参阅`groups`创建目标配置[文档中的](../../authoring-api/destination-configuration/create-destination-configuration.md)参数。

**输入**

配置文件1：

```json
{
   "identityMap":{
      "email":[
         {
            "id":"e1@example.com"
         },
         {
            "id":"e2@example.com"
         }
      ],
      "phone":[
         {
            "id":"+40744111222"
         }
      ],
      "IDFA":[
         {
            "id":"AEBE52E7-03EE-455A-B3C4-E57283966239"
         }
      ],
      "GAID":[
         {
            "id":"e4fe9bde-caa0-47b6-908d-ffba3fa184f2"
         }
      ]
   }
}
```

配置文件2：

```json
{
   "identityMap":{
      "email":[
         {
            "id":"e3@example.com"
         }
      ],
      "phone":[
         {
            "id":"+40744333444"
         },
         {
            "id":"+40744555666"
         }
      ],
      "IDFA":[
         {
            "id":"134GHU45-34HH-GHJ7-K0H8-LHN665998NN0"
         }
      ],
      "GAID":[
         {
            "id":"47bh00i9-8jv6-334n-lll8-nb7f24sghg76"
         }
      ]
   }
}
```

**模板**

>[!IMPORTANT]
>
>对于您使用的所有模板，在`""`目标服务器配置[中插入](../../functionality/destination-server/templating-specs.md)模板[之前，必须转义非法字符，如双引号](../../authoring-api/destination-server/create-destination-server.md)。 有关转义双引号的更多信息，请参阅[JSON标准](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/)中的第9章。

请注意，下面的模板中使用了`input.aggregationKey.identityNamespaces`

```python
{
            "profiles": [
            {% for profile in input.profiles %}
            {
                {% for ns in input.aggregationKey.identityNamespaces %}
                "{{ns}}": [
                    {% for id in profile.identityMap[ns] %}
                    "{{id.id}}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ]{% if not loop.last %},{% endif %}
                {% endfor %}
            }{% if not loop.last %},{% endif %}
            {% endfor %}
        ]
}
```

**结果**

将用户档案导出到目标时，会根据其身份命名空间将用户档案拆分为两个组。 电子邮件和电话位于一个组中，而GAID和IDFA位于另一个组中。

```json
{
   "profiles":[
      {
         "email":[
            "e1@example.com",
            "e2@example.com"
         ],
         "phone":[
            "+40744111222"
         ]
      },
      {
         "email":[
            "e3@example.com"
         ],
         "phone":[
            "+40744333444",
            "+40744555666"
         ]
      }
   ]
}
```

```json
{
   "profiles":[
      {
         "IDFA":[
            "AEBE52E7-03EE-455A-B3C4-E57283966239"
         ],
         "GAID":[
            "e4fe9bde-caa0-47b6-908d-ffba3fa184f2"
         ]
      },
      {
         "IDFA":[
            "134GHU45-34HH-GHJ7-K0H8-LHN665998NN0"
         ],
         "GAID":[
            "47bh00i9-8jv6-334n-lll8-nb7f24sghg76"
         ]
      }
   ]
}
```

#### 在URL模板中使用聚合密钥 {#aggregation-key-url-template}

根据您的用例，您还可以在URL中使用此处描述的聚合键，如下所示：

```python
https://api.example.com/audience/{{input.aggregationKey.segmentId}}
```

### 引用：转换模板中使用的上下文和函数 {#reference}

提供给模板的上下文包含`input`（此调用中导出的配置文件/数据）和`destination`(有关Adobe将数据发送到的目标的数据，对所有配置文件都有效)。

下表提供了上述示例中函数的说明。

| 函数 | 描述 | 示例 |
|---------|----------|----------|
| `input.profile` | 以[JsonNode](https://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html)表示的配置文件。 遵循此页面上进一步提到的合作伙伴XDM架构。 |  |
| `hasSegments` | 此函数采用命名空间受众ID的映射作为参数。 如果地图中至少有一个受众（无论其状态如何），则函数返回`true`，否则返回`false`。 您可以使用此函数确定是否对受众映射进行迭代。 | `hasSegments(input.profile.segmentMembership)` |
| `destination.namespaceSegmentAliases` | 将特定Adobe Experience Platform命名空间中的受众ID映射到合作伙伴系统中的受众别名。 | `destination.namespaceSegmentAliases["ups"]["seg-id-1"]` |
| `destination.namespaceSegmentNames` | 将特定Adobe Experience Platform命名空间中的受众名称映射到合作伙伴系统中的受众名称。 | `destination.namespaceSegmentNames["ups"]["seg-name-1"]` |
| `destination.namespaceSegmentTimestamps` | 以UNIX时间戳格式返回创建、更新或激活受众的时间。 | <ul><li>`destination.namespaceSegmentTimestamps["ups"]["seg-id-1"].createdAt`：以UNIX时间戳格式返回从`seg-id-1`命名空间创建ID为`ups`的区段的时间。</li><li>`destination.namespaceSegmentTimestamps["ups"]["seg-id-1"].updatedAt`：返回从`seg-id-1`命名空间更新ID为`ups`的受众的时间，格式为UNIX时间戳。</li><li>`destination.namespaceSegmentTimestamps["ups"]["seg-id-1"].mappingCreatedAt`：返回从`seg-id-1`命名空间中将ID为`ups`的受众激活到目标的时间（采用UNIX时间戳格式）。</li><li>`destination.namespaceSegmentTimestamps["ups"]["seg-id-1"].mappingUpdatedAt`：以UNIX时间戳格式返回目标上受众激活更新的时间。</li></ul> |
| `addedSegments(mapOfNamespacedSegmentIds)` | 在所有命名空间中仅返回状态为`realized`的受众。 | `addedSegments(input.profile.segmentMembership)` |
| `removedSegments(mapOfNamespacedSegmentIds)` | 在所有命名空间中仅返回状态为`exited`的受众。 | `removedSegments(input.profile.segmentMembership)` |
| `destination.segmentAliases` | **已弃用。 替换为`destination.namespaceSegmentAliases`** <br><br>将Adobe Experience Platform命名空间中的受众ID映射到合作伙伴系统中的受众别名。 | `destination.segmentAliases["seg-id-1"]` |
| `destination.segmentNames` | **已弃用。 替换为`destination.namespaceSegmentNames`** <br><br>将Adobe Experience Platform命名空间中的受众名称映射到合作伙伴系统中的受众名称。 | `destination.segmentNames["seg-name-1"]` |
| `destination.segmentTimestamps` | **已弃用。 替换为`destination.namespaceSegmentTimestamps`** <br><br>以UNIX时间戳格式返回创建、更新或激活受众的时间。 | <ul><li>`destination.segmentTimestamps["seg-id-1"].createdAt`：返回ID为`seg-id-1`的受众的创建时间（以UNIX时间戳格式）。</li><li>`destination.segmentTimestamps["seg-id-1"].updatedAt`：返回ID为`seg-id-1`的受众的更新时间（以UNIX时间戳格式）。</li><li>`destination.segmentTimestamps["seg-id-1"].mappingCreatedAt`：以UNIX时间戳格式返回ID为`seg-id-1`的受众激活到目标的时间。</li><li>`destination.segmentTimestamps["seg-id-1"].mappingUpdatedAt`：以UNIX时间戳格式返回目标上受众激活更新的时间。</li></ul> |

{style="table-layout:auto"}

## 后续步骤 {#next-steps}

阅读本文档后，您现在了解如何转换从Experience Platform导出的数据。 接下来，请阅读以下页面，以了解有关为目标创建消息转换模板的知识：

* [创建和测试消息转换模板](../../testing-api/streaming-destinations/create-template.md)
* [呈现模板API操作](../../testing-api/streaming-destinations/render-template-api.md)
* [Destination SDK中支持的转换函数](../destination-server/supported-functions.md)

要了解有关其他目标服务器组件的更多信息，请参阅以下文章：

* [使用Destination SDK创建目标的服务器规范](server-specs.md)
* [模板规范](templating-specs.md)
* [文件格式配置](file-formatting.md)
