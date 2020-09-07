---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;consent;Consent;preferences;Preferences;privacyOptOuts;marketingPreferences;optOutType;basisOfProcessing;consent;Consent
solution: Adobe Experience Platform
title: 隐私混合概述
description: 隐私／营销偏好（同意）混合是一种体验数据模型(XDM)混合，旨在支持CMP和客户其他来源生成的用户权限和偏好的收集。 此文档涵盖混合物提供的各种字段的结构和预期用途。
topic: guide
translation-type: tm+mt
source-git-commit: 172710c62b6f60de74e05364edb1191fbba0ff64
workflow-type: tm+mt
source-wordcount: '1827'
ht-degree: 1%

---


# [!DNL Privacy Consent] 混音概述

混 [!DNL Privacy/Marketing Preferences (Consent)] 音(以下称“混音[!DNL Privacy Consent] ”)是一种(XDM)混音， [!DNL Experience Data Model] 旨在支持由CMP和来自客户的其他来源生成的用户权限和偏好的集合。 此文档涵盖混合物提供的各种字段的结构和预期用途。

## 先决条件 {#prerequisites}

此文档要求对(XDM) [!DNL Experience Data Model] 和中模式的使用有所了解 [!DNL Experience Platform]。 请在继续之前查看以下文档：

* [XDM系统概述](http://www.adobe.com/go/xdm-home-en)
* [模式合成基础](http://www.adobe.com/go/xdm-schema-best-practices-en)

## 模式示例 {#schema}

>[!NOTE]
>
>以下示例旨在说明通过mixin发送到的 [!DNL Platform] 文档 [!DNL Privacy Consent] 的结构，以便提供本下一节的上下文，该章节解释了mixin提供的主要字段。 附录中提供了模式结构的完整示 [例](#full-schema) ，供参考。

以下JSON显示了混音可处理的数 [!DNL Privacy Consent] 据类型示例。 下一节提供了有关这些字段具体用途的信息。

```json
{
  "xdm:privacyOptOuts": [
     {
        "xdm:optOutType": "general_opt_out",
        "xdm:optOutValue": "in",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "legitimate_interest"
     },
     {
        "xdm:optOutType": "device_linking",
        "xdm:optOutValue": "not_provided",
        "xdm:basisOfProcessing": "vital_interest"
     },
     {
        "xdm:optOutType": "anonymous_analysis",
        "xdm:optOutValue": "out"
     }
  ],
  "xdm:personalizationPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "consent"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in"
        },
        {
           "xdm:type": "push_notifications",
           "xdm:choice": "out",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00"
        }
     ]
  },
  "xdm:marketingPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in",
           "xdm:subscriptions": {
              "weekly_mailer": {
                 "xdm:choice": "out",
                 "xdm:timestamp": "2019-02-03T15:52:25+00:00"
              },
              "daily_newsletter": {
                 "xdm:choice": "pending"
              }
           }
        },
        {
           "xdm:type": "iot",
           "xdm:choice": "out",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:subscriptions": {
              "out_of_milk": {
                 "xdm:choice": "in"
              }
           }
        }
     ]
  },
  "xdm:version": "1.0.0",
  "xdm:timestamp": "2019-01-01T15:52:25+00:00",
  "xdm:userLocale": "UK",
  "xdm:localeSource": "ip"
}
```

## 字段 {#fields}

以下各节介绍混合中提供的每个主要字段的使 [!DNL Privacy Consent] 用情况，以及子字段的结构。

### xdm:privacyOptOuts {#privacyOptOuts}

`xdm:privacyOptOuts` 是表示客户选择的常规退出设置的阵列。 此阵列中可以包括多个对象，每个对象表示特定退出类型以及客户为该类型选择的首选项。

```json
"xdm:privacyOptOuts": [
     {
        "xdm:optOutType": "general_opt_out",
        "xdm:optOutValue": "in",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "legitimate_interest"
     },
     {
        "xdm:optOutType": "device_linking",
        "xdm:optOutValue": "not_provided",
        "xdm:basisOfProcessing": "vital_interest"
     },
     {
        "xdm:optOutType": "anonymous_analysis",
        "xdm:optOutValue": "out"
     }
  ]
```

| 属性 | 描述 |
| --- | --- |
| `xdm:optOutType` | 选择退出的类型。 有关已接 [受的值](#optOutType-values) 和定义，请参阅附录。 |
| `xdm:optOutValue` | 客户为此特定选择退出类型选择的选定首选项。 有关已接 [受的值](#choice-optOutValue-values) 和定义，请参阅附录。 |
| `xdm:timestamp` | 选择退出首选项更改时的ISO 8601时间戳（如果适用）。 |
| `xdm:basisOfProcessing` | 指示收集和处理数据的隐私相关依据。 默认情况下，此字段设置 `consent`为，这表示仅当用户提供同意时（如所示）才应处理数 `xdm:optOutValue`据。<br><br>在某些情况下，系统不会提示客户同意进行数据处理。 `xdm:basisOfProcessing` 在这些情况下，必须包含在选择退出对象中，指明未提供同意提示的原因。 有关已接 [受的值](#basisOfProcessing-values) 和定义，请参阅附录。 |

### xdm：个性化首选项 {#personalizationPreferences}

`xdm:personalizationPreferences` 捕获客户偏好，以确定其数据可通过哪些方式进行个性化。 用户可选择退出以使用特定个性化用例，或选择退出完全个性化。

>[!IMPORTANT]
>
>`xdm:personalizationPreferences` 不涵盖营销用例。 例如，如果客户选择取消电子邮件的个性化，他们不会停止接收电子邮件。 相反，他们收到的电子邮件将是通用的，而不是基于用户档案。
>
>通过同一示例，如果客户选择退出电子邮件营销( `xdm:marketingPreferences`通过下一节 [中介绍)](#marketingPreferences)，则即使允许电子邮件个性化，该客户也不会收到任何电子邮件。

```json
"xdm:personalizationPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "consent"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in"
        },
        {
           "xdm:type": "push_notifications",
           "xdm:choice": "out",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00"
        }
     ]
  }
```

| 属性 | 描述 |
| --- | --- |
| `xdm:default` | 此对象中提供的数据代表客户整体的个性化偏好。 |
| `xdm:details` | 一组对象，每个对象对应客户为其提供偏好的特定个性化类型。 |
| `xdm:choice` | 客户提供的同意偏好一般性或特定的个性化类型，具体取决于具体的个性化类型是 `xdm:default` 分别 `xdm:details`根据还是提供。 有关已接 [受的值](#choice-optOutValue-values) 和定义，请参阅附录。 |
| `xdm:type` | 阵列中的 `xdm:details` 对象必须提供此字段以指示客户提供同意数据的特定个性化用例。 有关已接 [受的值](#type-values) 和定义，请参阅附录。 |
| `xdm:timestamp` | 选择退出首选项更改时的ISO 8601时间戳（如果适用）。 |
| `xdm:basisOfProcessing` | 指示收集和处理数据的隐私相关依据。 默认情况下，此字段设置 `consent`为，这表示仅当用户提供同意时（如所示）才应处理数 `xdm:choice`据。<br><br>在某些情况下，系统不会提示客户同意个性化。 `xdm:basisOfProcessing` 在这些情况下，必须包含在选择退出对象中，指明未提供同意提示的原因。 有关已接 [受的值](#basisOfProcessing-values) 和定义，请参阅附录。 |


### xdm:marketingPreferences {#marketingPreferences}

`xdm:marketingPreferences` 捕获客户关于其数据可用于哪些营销目的的偏好。 用户可选择退出以使用特定的营销用例，或选择退出完全使用直接营销。

```json
"xdm:marketingPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in",
           "xdm:subscriptions": {
              "weekly_mailer": {
                 "xdm:choice": "out",
                 "xdm:timestamp": "2019-02-03T15:52:25+00:00"
              },
              "daily_newsletter": {
                 "xdm:choice": "pending"
              }
           }
        },
        {
           "xdm:type": "iot",
           "xdm:choice": "out",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:subscriptions": {
              "out_of_milk": {
                 "xdm:choice": "in"
              }
           }
        }
     ]
  }
```

| 属性 | 描述 |
| --- | --- |
| `xdm:default` | 此对象中提供的数据代表客户对直接营销的总体偏好。 |
| `xdm:details` | 一组对象，每个特定营销用例由客户提供偏好。 |
| `xdm:choice` | 客户提供的同意偏好一般性营销或特定营销用例，具体取决于是根据还是 `xdm:default` 分别 `xdm:details`提供。 有关已接 [受的值](#choice-optOutValue-values) 和定义，请参阅附录。 |
| `xdm:subscriptions` | 其密钥表示公司特定订阅的对象，如邮寄列表或新闻稿。 每个订阅对象应依次包 `xdm:choice` 含相关订阅的值。 |
| `xdm:type` | 阵列中的 `xdm:details` 对象必须提供此字段以指明客户提供同意数据的特定营销用例。 有关已接 [受的值](#type-values) 和定义，请参阅附录。 |
| `xdm:timestamp` | 选择退出首选项更改时的ISO 8601时间戳（如果适用）。 |
| `xdm:basisOfProcessing` | 指示收集和处理数据的隐私相关依据。 默认情况下，此字段设置 `consent`为，这表示仅当用户提供同意时（如所示）才应处理数 `xdm:choice`据。<br><br>在某些情况下，客户不会被提示同意直接营销。 `xdm:basisOfProcessing` 在这些情况下，必须包含在选择退出对象中，指明未提供同意提示的原因。 有关已接 [受的值](#basisOfProcessing-values) 和定义，请参阅附录。 |

## 使用混合素摄取同意数据 {#ingest}

要使用混音符 [!DNL Privacy Consent] 从客户处获取同意数据，您必须将混音符添加到新模式或现有模式，并基于该创建数据集。

有关如何向 [模式添加混音的步骤](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) ，请参阅在UI中创建模式的教程。 mixin[!DNL  Privacy Consent] 与基于类或的模式兼 [!DNL XDM Individual Profile] 容 [!DNL XDM ExperienceEvent]。

创建包含混合的模式 [!DNL Privacy Consent] 后，请参阅数据集用户指 [南中有关创建数据集](../../catalog/datasets/user-guide.md#create) 的部分，按照步骤使用现有模式创建数据集。

>[!IMPORTANT]
>
>如果要向其发送同意数 [!DNL Real-time Customer Profile]据，则需要根据包含混 [!DNL Profile]合的类创建启用 [!DNL XDM Individual Profile] 模式的 [!DNL Privacy Consent] 值。 您根据该模式创建的数据集也必须启用 [!DNL Profile]。 有关与要求相关的特定步骤，请参阅以上 [!DNL Real-time Customer Profile] 教程。

## 附录 {#appendix}

以下各节提供了有关混音的其他参 [!DNL Privacy Consent] 考信息。

### xdm:optOutType的已接受值 {#optOutType-values}

下表概述了以下的已接受值 `xdm:optOutType`:

| 值 | 描述 |
| --- | --- |
| `general_opt_out` | 数据不能用于任何目的。 这通常会阻止数据收集，除非处理基础不是“同意”。<br><br>使用此选择退出类型时，接受的值 `in` 并获 `out` 得以下上下文含义：<ul><li>`in`:用户 **已经同意** ，其数据将用于一般处理。</li><li>`out`:用户不 **同意他们** 用于一般处理的数据。</li></ul>有关详细信息，请 [参阅xdm:optOutValue的已接受值](#choice-optOutValue-values) ，下表。 |
| `anonymous_analysis` | 该数据不能用于不需要任何类型的用户ID的通用Web度量，如查看特定页面的次数。 |
| `device_linking` | 访客使用的来自一个设备的数据不能与来自同一访客使用的另一个设备的数据组合。 设备使用通用用户名或电子邮件地址等技术进行链接，通常通过Adobe设备合作社或专用设备图表。 |
| `pseudonymous_analysis` | 这些数据不能用于Adobe Analytics提供的网络指标，该指标要求使用假名ID来识别用户通过网站（如流失报告）的路径、建立会话以及用于归因。 |
| `sales_sharing_opt_out` | 数据不能用于销售目的或与第三方共享。<br><br>使用此选择退出类型时，接受的值 `in` 并获 `out` 得以下上下文含义：<ul><li>`in`:用户 **已同意** ，其数据将用于销售和共享目的。</li><li>`out`:用户不 **同意他们** 的数据用于销售和共享目的。</li></ul>有关详细信息，请 [参阅xdm:optOutValue的已接受值](#choice-optOutValue-values) ，下表。 |

### xdm:basisOfProcessing的已接受值 {#basisOfProcessing-values}

下表概述了以下的已接受值 `xdm:basisOfProcessing`:

| 值 | 描述 |
| --- | --- |
| `consent` **（默认）** | 允许为指定目的收集数据，因为个人已经提供明确权限。 如果没有提供其 `xdm:basisOfProcessing` 他值，则此为默认值。 <br><br>**重要说明**:只有将 `xdm:choice` 和 `xdm:optOutValue` 的值设置为 `xdm:basisOfProcessing` 时，才接受 `consent`。 如果将此表中概述的任何其他值用 `xdm:basisOfProcessing` 于替代，则忽略个人的同意选择。 |
| `compliance` | 为达到特定目的而收集数据，是为了履行企业的法律义务。 |
| `contract` | 为达到指定目的而收集数据是为了履行与个人的合同义务。 |
| `legitimate_interest` | 出于特定目的收集和处理这些数据的正当商业利益，超过了数据对个人的潜在损害。 |
| `public_interest` | 为特定目的收集数据，必须为公共利益或行使官方权力而进行任务。 |
| `vital_interest` | 为了保护个人的切身利益，必须收集特定目的的数据。 |

### xdm:choice和xdm:optOutValue的已接受值 {#choice-optOutValue-values}

下表概述了和的已接受 `xdm:choice` 值 `xdm:optOutValue`:

| 值 | 描述 |
| --- | --- |
| `pending` | 系统尚未从客户处接收同意优先信息。 可在获得同意后用于网站的第一页。 它还可用于指示同意是&quot;假定的&quot;，而不是明确提供的。 |
| `in` | 用户已选择同意首选项。 换言之，他们 **同意** ，使用其数据，如所涉同意偏好所示。 |
| `out` | 用户已选择退出同意首选项。 换言之，他们 **不同意** ，如所涉同意偏好所示，使用其数据。 |
| `not_applicable` | 相关的同意偏好不适用于客户。 |
| `not_provided` | 客户未提供任何同意优先信息。 |
| `unknown` | 客户的同意偏好信息未知。 |

### xdm:type的已接受值 {#type-values}

下表概述了以下的已接受值 `xdm:type`:

| 值 | 描述 |
| --- | --- |
| `ads` | 可从无关网站查看的广告。 |
| `content` | 网站上显示的内容。 |
| `customer_support` | 与客户支持相关的数据。 |
| `email` | 电子邮件消息. |
| `iot` | 与“物联网”(IoT)相关的数据。 |
| `in_app_messages` | 应用程序内消息. |
| `in_home` | 家庭内消息。 |
| `in_store` | 店内消息。 |
| `in_vehicle` | 车内消息。 |
| `offers` | 特别优惠。 |
| `phone_calls` | 与电话通话互动相关的数据。 |
| `push_notifications` | 推送通知. |
| `sms` | 短信消息. |
| `social_media` | 社交媒体内容。 |
| `snail_mail` | 通过传统邮政投放发送的信息。 |
| `third_party_content` | 网站上显示的由不相关实体提供的内容或文章。 |
| `third_party_offers` | 优惠或广告显示在您网站广告服务中的不相关实体。 |

### 完整 [!DNL Privacy Consent] 模式 {#full-schema}

以下JSON表示在模式注 [!DNL Privacy Consent] 册表中显示的完整模式:

```json
{
  "meta:license": [
    "Copyright 2019 Adobe Systems Incorporated. All rights reserved.",
    "This work is licensed under a Creative Commons Attribution 4.0 International (CC BY 4.0) license",
    "you may not use this file except in compliance with the License. You may obtain a copy",
    "of the License at https://creativecommons.org/licenses/by/4.0/"
  ],
  "$id": "https://ns.adobe.com/xdm/context/consent-preferences",
  "$schema": "http://json-schema.org/draft-06/schema#",
  "title": "Privacy/Marketing Preferences (Consent)",
  "description": "This schema captures privacy, personalization and marketing preferences (consents).",
  "type": "object",
  "meta:extensible": true,
  "meta:abstract": true,
  "definitions": {
    "consentValue": {
      "type": "string",
      "enum": [
        "not_provided",
        "pending",
        "in",
        "out",
        "unknown",
        "not_applicable"
      ],
      "meta:enum": {
        "not_provided": "Not provided",
        "pending": "Pending verification",
        "in": "Opt-in",
        "out": "Opt-out",
        "unknown": "Unknown",
        "not_applicable": "Not Applicable"
      }
    },
    "basisOfProcessing": {
      "title": "Basis Of Processing",
      "type": "string",
      "description": "Basis of Processing",
      "enum": [
        "consent",
        "legitimate_interest",
        "contract",
        "vital_interest",
        "compliance",
        "public_interest"
      ],
      "meta:enum": {
        "consent": "User Consent",
        "legitimate_interest": "Legitimate Interest",
        "contract": "Contract",
        "vital_interest": "Vital Interest of the Individual",
        "compliance": "Compliance with a Legal Obligation",
        "public_interest": "Public Interest"
      }
    },
    "timestamp": {
      "title": "Preference timestamp",
      "description": "Timestamp of this specific opt out or preference.",
      "type": "string",
      "format": "date-time"
    },
    "consent-preferences": {
      "properties": {
        "xdm:privacyOptOuts": {
          "title": "Privacy Preferences",
          "description": "Encapsulates data privacy preferences.",
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "xdm:optOutType": {
                "title": "Opt-out type",
                "type": "string",
                "description": "The type of user permission.",
                "enum": [
                  "general_opt_out",
                  "sales_sharing_opt_out",
                  "anonymous_analysis",
                  "pseudonymous_analysis",
                  "device_linking"
                ],
                "meta:enum": {
                  "general_opt_out": "General opt-out",
                  "sales_sharing_opt_out": "Sales/sharing opt-out",
                  "anonymous_analysis": "Anonymous Analysis",
                  "pseudonymous_analysis": "Pseudonymous Analysis",
                  "device_linking": "Device Linking"
                }
              },
              "xdm:optOutValue": {
                "title": "Opt Out Value",
                "description": "The value of the specific opt out.",
                "$ref": "#/definitions/consentValue"
              },
              "xdm:basisOfProcessing": {
                "$ref": "#/definitions/basisOfProcessing"
              },
              "xdm:timestamp": {
                "$ref": "#/definitions/timestamp"
              }
            }
          }
        },
        "xdm:personalizationPreferences": {
          "title": "Personalization Preferences",
          "description": "User's Personalization Preferences",
          "type": "object",
          "properties": {
            "xdm:default": {
              "title": "Global Personalization Preferences",
              "description": "User's Default Personalization Preference",
              "type": "object",
              "properties": {
                "xdm:choice": {
                  "title": "Default Personalization Preferences Value",
                  "description": "The default value for personalization",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                }
              }
            },
            "xdm:details": {
              "title": "Itemized Personalization Preferences",
              "description": "Preferences for specific types of personalization",
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "meta:enum": {
                    "content": "Personalize Content",
                    "in_app": "Personalize In App Messages",
                    "offers": "Personalize Offers",
                    "email": "Personalize eMail",
                    "snail_mail": "Personalize Regular Mail",
                    "phone_calls": "Personalize Phone Calls",
                    "push_notifications": "Personalize Push Notifications",
                    "sms": "Personalize SMS",
                    "customer_support": "Personalize Customer Support",
                    "in_store": "Personalize In Store",
                    "in_vehicle": "Personalize In Vehicle",
                    "in_home": "Personalize In Home",
                    "iot": "Personalize IoT",
                    "social_media": "Personalize Social Media",
                    "third_party_offers": "Personalize Third-party Offers",
                    "third_party_content": "Personalize Third-party Content",
                    "ads": "Personalize My Business's Ads on Other Sites"
                  }
                },
                "xdm:choice": {
                  "title": "Personalization Preference Value",
                  "description": "The value for this specific personalization preference",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                }
              }
            }
          }
        }
      },
      "xdm:marketingPreferences": {
        "title": "Marketing Preferences",
        "description": "User's Direct Marketing Preferences",
        "type": "object",
        "properties": {
          "xdm:default": {
            "title": "Default Direct Marketing Preference",
            "description": "User's Default Marketing Preference",
            "type": "object",
            "properties": {
              "xdm:choice": {
                "title": "Default Marketing Preferences Value",
                "description": "The default value for direct marketing preferences",
                "$ref": "#/definitions/consentValue"
              },
              "xdm:basisOfProcessing": {
                "$ref": "#/definitions/basisOfProcessing"
              },
              "xdm:timestamp": {
                "$ref": "#/definitions/timestamp"
              }
            }
          },
          "xdm:details": {
            "title": "Itemized Direct Marketing Preferences",
            "description": "Preferences for specific types of direct marketing",
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "xdm:type": {
                  "title": "Marketing Preference",
                  "type": "string",
                  "description": "The specific marketing preference.",
                  "enum": [
                    "email",
                    "push_notifications",
                    "in_app_messages",
                    "sms",
                    "phone_calls",
                    "snail_mail",
                    "in_vehicle_messages",
                    "in_home_messages",
                    "iot",
                    "social_media"
                  ],
                  "meta:enum": {
                    "email": "Receive eMail",
                    "push_notifications": "Receive Push Notifications",
                    "in_app_messages": "Receive In App Messages",
                    "sms": "Receive SMS",
                    "phone_calls": "Receive Phone Calls",
                    "snail_mail": "Receive Regular Mail",
                    "in_vehicle_messages": "Receive In Vehicle Messages",
                    "in_home_messages": "Receive In Home Messages",
                    "iot": "Receive IoT",
                    "social_media": "Receive Social Media Messages"
                  }
                },
                "xdm:choice": {
                  "title": "Marketing Preference Value",
                  "description": "The value for this specific marketing preference",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                },
                "xdm:subscriptions": {
                  "title": "Company-specific subscriptions",
                  "description": "Company-specific subscriptions, such as mailing lists or newsletters",
                  "type": "object",
                  "meta:xdmType": "map",
                  "additionalProperties": {
                    "xdm:choice": {
                      "title": "Marketing Preference Value",
                      "description": "The value for this specific marketing preference",
                      "$ref": "#/definitions/consentValue"
                    },
                    "xdm:timestamp": {
                      "$ref": "#/definitions/timestamp"
                    }
                  }
                }
              }
            }
          }
        }
      },
      "xdm:timestamp": {
        "title": "Consent Preferences timestamp",
        "description": "Timestamp of the complete set of user consent preferences.",
        "type": "string",
        "format": "date-time"
      },
      "xdm:version": {
        "title": "Preferences Version",
        "description": "Version of the Privacy Preferences Standard",
        "type": "string"
      },
      "xdm:userLocale": {
        "title": "User Locale",
        "description": "User location or jurisdiction that applies to the consents for this user",
        "type": "string"
      },
      "xdm:localeSource": {
        "title": "Locale Source",
        "description": "Method used to determine the user's locale",
        "enum": [
          "ip",
          "gps",
          "user_provided",
          "website_location",
          "inferred",
          "other"
        ],
        "meta:enum": {
          "ip": "IP Address",
          "gps": "Device GPS",
          "user_provided": "User Provided",
          "website_location": "Website eTDL",
          "inferred": "Inferred",
          "other": "Other"
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context"
    },
    {
      "$ref": "#/definitions/consent-preferences"
    }
  ],
  "meta:status": "experimental"
}
```
