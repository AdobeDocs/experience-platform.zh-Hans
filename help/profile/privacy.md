---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 实时客户配置文件中的隐私请求处理
type: Documentation
description: Adobe Experience Platform Privacy Service会处理客户访问、选择退出销售或删除其个人数据的请求，如大量隐私法规所述。 本文档介绍了与处理实时客户个人资料的隐私请求相关的基本概念。
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1743'
ht-degree: 0%

---

# 隐私请求处理位置 [!DNL Real-Time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] 处理客户访问、选择退出销售或删除其个人数据的请求，隐私法规(例如《通用数据保护条例》(GDPR)和 [!DNL California Consumer Privacy Act] (CCPA)。

本文档介绍了与处理隐私请求相关的基本概念 [!DNL Real-Time Customer Profile] 在Adobe Experience Platform中。

>[!NOTE]
>
>本指南仅涵盖如何对Experience Platform中的配置文件数据存储进行隐私请求。 如果您还计划向Platform数据湖提出隐私请求，请参阅以下内容的指南： [数据湖中的隐私请求处理](../catalog/privacy.md) 以及本教程。
>
>有关如何为其他Adobe Experience Cloud应用程序提出隐私请求的步骤，请参阅 [Privacy Service文档](../privacy-service/experience-cloud-apps.md).

>[!IMPORTANT]
>
>本指南中的隐私请求可以 **非** 涵盖B2B非个人实体。

## 快速入门

本指南要求您对以下内容有一定的了解 [!DNL Platform] 组件：

* [[!DNL Privacy Service]](../privacy-service/home.md)：管理客户跨多个Adobe Experience Cloud应用程序访问、选择退出销售或删除其个人数据的请求。
* [[!DNL Identity Service]](../identity-service/home.md)：通过跨设备和系统桥接身份，解决了客户体验数据碎片化带来的根本挑战。
* [[!DNL Real-Time Customer Profile]](home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

## 了解标识命名空间 {#namespaces}

Adobe Experience Platform [!DNL Identity Service] 跨系统和设备桥接客户身份数据。 [!DNL Identity Service] 用途 **身份命名空间** 为标识值提供上下文，方法是将其与原始系统相关联。 命名空间可以表示通用概念，例如电子邮件地址（“电子邮件”），也可以将身份与特定应用程序关联，例如Adobe Advertising Cloud ID (“AdCloud”)或Adobe Target ID (“TNTID”)。

Identity Service维护全局定义（标准）和用户定义（自定义）身份命名空间的存储。 标准命名空间适用于所有组织（例如，“Email”和“ECID”），而您的组织也可以创建自定义命名空间以满足其特定需求。

有关中身份命名空间的更多信息 [!DNL Experience Platform]，请参见 [身份命名空间概述](../identity-service/features/namespaces.md).

## 提交请求 {#submit}

以下部分概述了如何针对以下对象发出隐私请求： [!DNL Real-Time Customer Profile] 使用 [!DNL Privacy Service] API或UI。 在阅读这些部分之前，您应该回顾或了解 [PRIVACY SERVICEAPI](../privacy-service/api/getting-started.md) 或 [PRIVACY SERVICEUI](../privacy-service/ui/overview.md) 文档。 本文档提供了有关如何提交隐私作业的完整步骤，包括如何在请求负载中正确格式化提交的用户身份数据。

>[!IMPORTANT]
>
>Privacy Service只能处理 [!DNL Profile] 使用不执行身份拼接的合并策略的数据。 请参阅以下部分 [合并策略限制](#merge-policy-limitations) 以了解更多信息。
>
>请注意，隐私请求在法规要求内异步处理，完成所需时间可能会有所不同。 如果更改 [!DNL Profile] 数据当请求仍在处理时，并不保证这些传入记录也将在该请求中处理。 只有请求隐私作业时保存在数据湖或配置文件存储中的配置文件才会被删除。 如果您在删除作业期间摄取与删除请求的主题相关的配置文件数据，则无法保证所有配置文件片段都会被删除。
>您有责任在删除请求时了解Platform或Profile Service中的任何传入数据，因为该数据将插入到您的记录存储中。 您必须谨慎接收已被删除或正在删除的数据。

### 使用API

在API中创建作业请求时，中提供的任何ID `userIDs` 必须使用特定的 `namespace` 和 `type`. 有效的 [身份命名空间](#namespaces) 识别者 [!DNL Identity Service] 必须提供 `namespace` 值，而 `type` 必须是 `standard` 或 `unregistered` （分别用于标准和自定义命名空间）。

>[!NOTE]
>
>您可能需要为每个客户提供多个ID，具体取决于身份图以及配置文件片段在Platform数据集中的分发方式。 请参阅下一部分 [配置文件片段](#fragments) 以了解更多信息。

此外， `include` 请求有效负载的数组必须包含请求所针对的不同数据存储的产品值。 要删除与标识关联的配置文件数据，数组必须包含值 `ProfileService`. 要删除客户的身份图关联，数组必须包含值 `identity`.

>[!NOTE]
>
>请参阅以下部分 [配置文件请求和身份请求](#profile-v-identity) 本文档后面部分，详细了解使用 `ProfileService` 和 `identity` 内部 `include` 数组。

以下请求在中为单个客户的数据创建新的隐私作业 [!DNL Profile] 商店。 在以下位置为客户提供了两个标识值： `userIDs` 数组；一个使用标准 `Email` 身份命名空间和使用自定义命名空间的其他命名空间 `Customer_ID` 命名空间。 它还包括的产品价值 [!DNL Profile] (`ProfileService`) `include` 数组：

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "Email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "Customer_ID",
            "value": "12345678",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["ProfileService","identity"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

>[!IMPORTANT]
>
>Platform处理所有隐私请求 [沙盒](../sandboxes/home.md) 属于您的组织。 因此，任何 `x-sandbox-name` 请求中包含的标头将被系统忽略。

**产品响应**

对于配置文件服务，隐私作业完成后，将以JSON格式返回响应，其中包含有关所请求用户ID的信息。

```json
{
    "privacyResponse": {
        "jobId": "7467850f-9698-11ed-8635-355435552164",
        "response": [
            {
                "sandbox": "prod",
                "mergePolicyId": "none",
                "result": {
                    "person": {
                        "gender": "female"           
                    },
                    "personalEmail": {
                        "address": "ajones@acme.com",
                    },
                    "identityMap": {
                        "crmid": [
                            {
                                "id": "5b7db37a-bc7a-46a2-a63e-2cfe7e1cc068"
                            }
                        ]
                    }
                }
            },
            {
                "sandbox": "prod",
                "mergePolicyId": "none",
                "result": {
                    "person": {
                        "gender": "male"
                    },
                    "id": 12345678,
                    "identityMap": {
                        "crmid": [
                            {
                                "id": "e9d439f2-f5e4-4790-ad67-b13dbd89d52e"
                            }
                        ]
                    }
                }
            }
        ]
    }
}
```

### 使用UI

在UI中创建作业请求时，请确保选择 **[!UICONTROL AEP数据湖]** 和/或 **[!UICONTROL 个人资料]** 下 **[!UICONTROL 产品]** 为了处理存储在数据湖中的数据的作业，或者 [!DNL Real-Time Customer Profile]、ID名称和ID名称等。

![正在UI中创建访问作业请求，并在产品下选择配置文件选项](./images/privacy/product-value.png)

## 隐私请求中的配置文件片段 {#fragments}

在 [!DNL Profile] 数据存储时，单个客户的个人数据通常由多个配置文件片段组成，这些片段通过身份图与人员关联。 向发出隐私请求时 [!DNL Profile] 请务必注意，请求仅在配置文件片段级别进行处理，而不是整个配置文件。

例如，考虑这样一种情况：您将客户属性数据存储到三个单独的数据集中，这几个数据集使用不同的标识符将该数据与单个客户关联：

| 数据集名称 | 主要标识字段 | 存储的属性 |
| --- | --- | --- |
| 数据集1 | `customer_id` | `address` |
| 数据集2 | `email_id` | `firstName`、`lastName` |
| 数据集3 | `email_id` | `mlScore` |

其中一个数据集使用 `customer_id` 作为其主要标识符，而其他两个使用 `email_id`. 如果您只使用发送隐私请求（访问或删除）， `email_id` 作为用户ID值，仅 `firstName`， `lastName`、和 `mlScore` 将处理属性，而 `address` 不会受到影响。

为确保您的隐私请求能够处理所有相关客户属性，您必须为可能存储了这些属性的所有适用数据集提供主标识值（每个客户最多九个ID）。 请参阅中有关身份字段的部分 [模式组合基础](../xdm/schema/composition.md#identity) 以了解有关通常标记为标识的字段的更多信息。

## 正在处理删除请求 {#delete}

时间 [!DNL Experience Platform] 接收来自的删除请求 [!DNL Privacy Service]， [!DNL Platform] 将确认发送至 [!DNL Privacy Service] 请求已收到，并且受影响的数据已标记为删除。 隐私作业完成后，记录将被删除。

>[!IMPORTANT]
>
>隐私删除请求不是即时发出的，并且可能会因涉及的服务和其他影响因素（例如地理位置）而异。 完成隐私作业的时间范围介于15天到45天之间，但并不保证会实现。

根据您是否还包含Identity Service (`identity`)和数据湖(`aepDataLake`)作为产品，适用于您的隐私配置文件请求(`ProfileService`)，则与用户档案相关的不同数据集将在不同的时间从系统中删除：

| 包含的产品 | 效应 |
| --- | --- |
| `ProfileService` 仅限 | 用户档案会在Platform发送确认信息确认收到删除请求后立即删除。 但是，个人资料的身份图仍然会保留，并且个人资料有可能在摄取具有相同身份的新数据时进行重构。 与用户档案关联的数据也保留在数据湖中。 |
| `ProfileService` 和 `identity` | 用户档案及其关联的身份图会在Platform发送确认收到删除请求后立即删除。 与用户档案关联的数据将保留在数据湖中。 |
| `ProfileService` 和 `aepDataLake` | 用户档案会在Platform发送确认信息确认收到删除请求后立即删除。 但是，个人资料的身份图仍然会保留，并且个人资料有可能在摄取具有相同身份的新数据时进行重构。<br><br>当Data Lake产品响应请求被接收并且当前正在处理时，与用户档案关联的数据将被软删除，因此任何用户都无法访问 [!DNL Platform] 服务。 作业完成后，数据将从数据湖中完全删除。 |
| `ProfileService`， `identity`、和 `aepDataLake` | 用户档案及其关联的身份图会在Platform发送确认收到删除请求后立即删除。<br><br>当Data Lake产品响应请求被接收并且当前正在处理时，与用户档案关联的数据将被软删除，因此任何用户都无法访问 [!DNL Platform] 服务。 作业完成后，数据将从数据湖中完全删除。 |

请参阅 [[!DNL Privacy Service] 文档](../privacy-service/home.md#monitor) 以了解有关跟踪作业状态的更多信息。

### 配置文件请求与身份请求 {#profile-v-identity}

如果对配置文件提出删除请求(`ProfileService`)而非Identity Service (`identity`)，则生成的作业将删除为客户（或客户集）收集的属性数据，但不会删除在身份图中建立的关联。

例如，使用客户的删除请求 `email_id` 和 `customer_id` 删除存储在这些ID下的所有属性数据。 但是，此后摄取的任何数据均采用 `customer_id` 仍将与相应的关联 `email_id`，因为关联仍然存在。

要删除给定客户的配置文件和所有标识关联，请确保在删除请求中同时包含配置文件和标识服务作为目标产品。

### 合并策略限制 {#merge-policy-limitations}

Privacy Service只能处理 [!DNL Profile] 使用不执行身份拼接的合并策略的数据。 如果您使用UI来确认是否正在处理您的隐私请求，请确保您使用的策略具有 **[!DNL None]** 作为 [!UICONTROL ID拼接] 类型。 换言之，您不能在以下情况下使用合并策略： [!UICONTROL ID拼接] 设置为 [!UICONTROL 专用图].

>![合并策略的ID拼接设置为“无”](./images/privacy/no-id-stitch.png)

## 后续步骤

通过阅读本文档，您已了解在中处理隐私请求涉及的重要概念。 [!DNL Experience Platform]. 要加深您对如何管理身份数据和创建隐私作业的了解，请继续阅读本指南中提供的文档。

有关处理隐私请求的信息 [!DNL Platform] 未使用的资源 [!DNL Profile]，请参阅上的文档 [数据湖中的隐私请求处理](../catalog/privacy.md).
