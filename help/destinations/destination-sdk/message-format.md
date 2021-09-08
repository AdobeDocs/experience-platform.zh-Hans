---
description: 将本页面上的内容与合作伙伴目标的其余配置选项结合使用。 本页介绍从Adobe Experience Platform导出到目标的数据的消息传送格式，而其他页面则介绍有关连接到您的目标并进行身份验证的特定信息。
seo-description: Use the content on this page together with the rest of the configuration options for partner destinations. This page addresses the messaging format of data exported from Adobe Experience Platform to destinations, while the other page addresses specifics about connecting and authenticating to your destination.
seo-title: Message format
title: 消息格式
source-git-commit: d60933d2083b7befcfa8beba4b1630f372c08cfa
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 3%

---

# 消息格式

## 先决条件 — Adobe Experience Platform概念 {#prerequisites}

要了解Adobe方面的流程，请熟悉以下Experience Platform概念：

* **体验数据模型(XDM)**。[XDM概](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hans) 述和  [如何在Adobe Experience Platform中创建XDM架构](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en)。
* **类**。[在UI中创建和编辑类](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/classes.html?lang=en)。
* **字段组**。[字段组定](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#field-group) 义以及 [有关字段组的更多信息](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en#field-group)。
* **IdentityMap**。标识映射表示Adobe Experience Platform中所有最终用户标识的映射。 请参阅[XDM字段词典](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en)中的`xdm:identityMap`。
* **区段成员资格**。[segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) XDM属性会通知配置文件是其成员的区段。 有关`status`字段中的三个不同值，请阅读[区段成员资格详细信息架构字段组](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html)中的文档。

## 概述 {#overview}

将本页中的内容与合作伙伴目标](./configuration-options.md)的其余[配置选项一起使用。 本页介绍从Adobe Experience Platform导出到目标的数据的消息传送格式，而其他页面则介绍有关连接到您的目标并进行身份验证的特定信息。

Adobe Experience Platform以各种数据格式将数据导出到大量目标。 目标类型的一些示例包括广告平台(Google)、社交网络(Facebook)、云存储位置(Amazon S3、Azure事件中心)。

Experience Platform可以调整导出的消息格式，使其与一侧的预期格式匹配。 要了解此自定义设置，以下概念非常重要：
* Adobe Experience Platform中的源(1)和目标(2)XDM模式
* 合作伙伴端(3)上的消息格式，以及
* 两个之间的转换层，可通过创建[消息转换模板](./message-format.md#using-templating)来定义。

![架构到JSON转换](./assets/transformations-3-steps.png)

Experience Platform 会使用架构，以便以可重用的一致方式描述数据结构。

要将数据激活到目标的用户需要将其Experience Platform中数据集所使用的字段映射到将转换为目标预期格式的架构。 Adobe将为您的公司创建一个自定义字段组，以将其添加到目标架构。 字段组中的字段取决于您能够收到的配置文件属性字段。

**源XDM架构(1)**:这是指客户在Experience Platform中使用的架构。在Experience Platform中，在激活目标工作流的[映射步骤](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en#mapping)中，客户会将其源架构中的字段映射到目标架构(2)。

**目标XDM架构(2)**:根据您与Adobe共享的JSON标准架构(3),Adobe的团队将为您的目标创建自定义架构。请注意，在项目](./overview.md#phased-approach)的未来阶段，您将能够自行为目标创建自定义架构。[

**目标配置文件属性的JSON标准架构(3)**:请与我们共享一个 [JSON](https://json-schema.org/learn/miscellaneous-examples.html) 架构，其中包含您的平台支持的所有配置文件属性及其类型(例如：对象、字符串、数组)。目标可支持的示例字段可能为`firstName`、`lastName`、`gender`、`email`、`phone`、`productId`、`productName`等。

根据上述架构转换，以下是源XDM架构与合作伙伴端示例架构之间消息结构的更改方式：

![转换消息示例](./assets/transformations-with-examples.png)

<br> 


## 入门 — 转换三个基本属性 {#getting-started}

为了演示转换过程，以下示例使用了Adobe Experience Platform中的三个常用配置文件属性：**名字**、**姓氏**&#x200B;和&#x200B;**电子邮件地址**。

>[!NOTE]
>
>客户将源XDM架构的属性映射到Adobe Experience Platform UI中合作伙伴XDM架构的&#x200B;**激活目标工作流](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate-destinations.html#mapping)的[映射**&#x200B;步骤中的。

假设您的平台可以接收如下消息格式：

```curl
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

| Adobe端合作伙伴XDM架构中的属性 | 转换 | HTTP消息中的属性 |
|---------|----------|---------|
| `_your_custom_schema.firstName` | ` attributes.first_name` | `first_name` |
| `_your_custom_schema.lastName` | `attributes.last_name` | `last_name` |
| `personalEmail.address` | `attributes.external_id` | `external_id` |

## 对身份、属性和区段成员资格转换使用模板语言 {#using-templating}

Adobe使用类似于[Jinja](https://jinja.palletsprojects.com/en/2.11.x/)的模板语言将XDM架构中的字段转换为目标支持的格式。

本节提供了一些示例，说明如何从输入XDM架构、模板，以及如何将这些转换输出为目标接受的有效负载格式。 以下示例按日益复杂的情况排序，如下所示：

1. 简单的转换示例。 了解模板如何与[配置文件属性](./message-format.md#attributes)、[区段成员资格](./message-format.md#segment-membership)和[Identity](./message-format.md#identities)字段的简单转换一起使用。
2. 组合上述字段的模板的复杂性增加了示例：[创建用于发送区段和标识的模板](./message-format.md#segments-and-identities)和[创建用于发送区段、标识和配置文件属性的模板](./message-format.md#segments-identities-attributes)。
3. 深入研究，展示两个行业合作伙伴的模板示例。

### 配置文件属性 {#attributes}

要转换导出到目标的配置文件属性，请参阅下面的JSON和代码示例。


>[!IMPORTANT]
>
>有关Adobe Experience Platform中所有可用配置文件属性的列表，请参阅[XDM字段词典](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en)。



**输入**

用户档案1:

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

用户档案2:

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
>对于您使用的所有模板，在[目标服务器配置](./server-and-template-configuration.md#template-specs)中插入模板之前，必须对非法字符进行转义，如双引号`""`。 有关转义双引号的更多信息，请参阅[JSON standard](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf)中的第9章。

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

### 区段成员资格 {#segment-membership}

[segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) XDM属性会通知配置文件是其成员的区段。
有关`status`字段中的三个不同值，请阅读[区段成员资格详细信息架构字段组](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html)中的文档。

**输入**

用户档案1:

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
        "status": "existing"
      },
      "8f812592-3f06-416b-bd50-e7831848a31a": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      }
    }
  }
}
```

用户档案2:

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
        "status": "existing"
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
>对于您使用的所有模板，在[目标服务器配置](./server-and-template-configuration.md#template-specs)中插入模板之前，必须对非法字符进行转义，如双引号`""`。 有关转义双引号的更多信息，请参阅[JSON standard](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf)中的第9章。

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
                {# Alternative syntax for filtering segments by status: #}
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

### 标识 {#identities}

有关Experience Platform中身份的信息，请参阅[身份命名空间概述](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=zh-Hans)。

**输入**

用户档案1:

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

用户档案2:

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
>对于您使用的所有模板，在[目标服务器配置](./server-and-template-configuration.md#template-specs)中插入模板之前，必须对非法字符进行转义，如双引号`""`。 有关转义双引号的更多信息，请参阅[JSON standard](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf)中的第9章。

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


### 创建用于发送区段和标识的模板 {#segments-and-identities}

本节提供了AdobeXDM架构与合作伙伴目标架构之间常用转换的示例。
以下示例向您展示了如何转换区段成员资格和标识格式，并将它们输出到您的目标。

**输入**

用户档案1:

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
              "status": "existing"
            },
            "8f812592-3f06-416b-bd50-e7831848a31a": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "exited"
            }
        }
    }
}
```

用户档案2:

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
>对于您使用的所有模板，在[目标服务器配置](./server-and-template-configuration.md#template-specs)中插入模板之前，必须对非法字符进行转义，如双引号`""`。 有关转义双引号的更多信息，请参阅[JSON standard](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf)中的第9章。

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
                    {# Alternative syntax for filtering segments by status: #}
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

下面的`json`表示从Adobe Experience Platform中导出的数据。

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

本节提供了AdobeXDM架构与合作伙伴目标架构之间常用转换的示例。

另一个常见用例是导出包含区段成员资格和标识的数据(例如：电子邮件地址、电话号码、广告ID)和配置文件属性。 要以这种方式导出数据，请参阅以下示例：

**输入**

用户档案1:

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
              "status": "existing"
            },
            "8f812592-3f06-416b-bd50-e7831848a31a": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "exited"
            }
        }
    }
}
```

用户档案2:

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
>对于您使用的所有模板，在[目标服务器配置](./server-and-template-configuration.md#template-specs)中插入模板之前，必须对非法字符进行转义，如双引号`""`。 有关转义双引号的更多信息，请参阅[JSON standard](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf)中的第9章。

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
                {# Alternative syntax for filtering segments by status: #}
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

下面的`json`表示从Adobe Experience Platform中导出的数据。

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

### 引用：转换模板中使用的上下文和函数

向模板提供的上下文包含`input`（此调用中导出的配置文件/数据）和`destination`(有关Adobe向其发送数据的目标的数据，对所有配置文件均有效)。

下表提供了上述示例中函数的说明。

| 函数 | 描述 |
|---------|----------|
| `input.profile` | 配置文件，表示为[JsonNode](http://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html)。 遵循本页上面进一步提到的合作伙伴XDM架构。 |
| `destination.segmentAliases` | 从Adobe Experience Platform命名空间中的区段ID映射到合作伙伴系统中的区段别名。 |
| `destination.segmentNames` | 从Adobe Experience Platform命名空间中的区段名称映射到合作伙伴系统中的区段名称。 |
| `addedSegments(listOfSegments)` | 仅返回状态为`realized`或`existing`的区段。 |
| `removedSegments(listOfSegments)` | 仅返回状态为`exited`的区段。 |

<!--

## What Adobe needs from you to set up your destination {#what-adobe-needs}

Based on the transformations outlined in the sections above, Adobe needs the following information to set up your destination:

* Considering *all* the fields that your platform can receive, Adobe needs the standard JSON schema that corresponds to your expected message format. Having the template allows Adobe to define transformations and to create a custom XDM schema for your company, which customers would use to export data to your destination.

-->
