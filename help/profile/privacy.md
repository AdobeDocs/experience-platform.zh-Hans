---
keywords: Experience Platform；首页；热门话题
solution: Experience Platform
title: 实时客户配置文件中的隐私请求处理
type: Documentation
description: Adobe Experience Platform Privacy Service会处理客户访问、选择退出销售或删除其个人数据的请求，如大量隐私法规所述。 本文档介绍了与处理实时客户个人资料的隐私请求相关的基本概念。
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: 6eaa384feb1b84e6081f03cb4de9687ad26f437d
workflow-type: tm+mt
source-wordcount: '1757'
ht-degree: 1%

---

# 在[!DNL Real-Time Customer Profile]中处理隐私请求

Adobe Experience Platform [!DNL Privacy Service]处理客户访问、选择退出销售或删除其个人数据的请求，这些请求由隐私法规(如《通用数据保护条例》(GDPR)和[!DNL California Consumer Privacy Act] (CCPA)规定。

本文档介绍了与在Adobe Experience Platform中处理[!DNL Real-Time Customer Profile]的隐私请求相关的基本概念。

>[!NOTE]
>
>本指南仅涵盖如何在Experience Platform中针对配置文件数据存储区提出隐私请求。 如果您还计划提出针对Experience Platform数据湖的隐私请求，请参阅本教程和关于在数据湖](../catalog/privacy.md)中处理[隐私请求的指南。
>
>有关如何为其他Adobe Experience Cloud应用程序提出隐私请求的步骤，请参阅[Privacy Service文档](../privacy-service/experience-cloud-apps.md)。

>[!IMPORTANT]
>
>本指南中的隐私请求&#x200B;**不**&#x200B;涵盖B2B非人员实体。

## 快速入门

本指南要求您对以下[!DNL Experience Platform]个组件有一定的了解：

* [[!DNL Privacy Service]](../privacy-service/home.md)：管理客户跨多个Adobe Experience Cloud应用程序访问、选择退出销售或删除其个人数据的请求。
* [[!DNL Identity Service]](../identity-service/home.md)：通过跨设备和系统桥接身份，解决了客户体验数据碎片化带来的基本挑战。
* [[!DNL Real-Time Customer Profile]](home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

## 了解身份标识命名空间 {#namespaces}

Adobe Experience Platform [!DNL Identity Service]跨系统和设备桥接客户身份数据。 [!DNL Identity Service]使用&#x200B;**身份命名空间**&#x200B;将身份值与其原始系统相关联，从而为其提供上下文。 命名空间可以表示通用概念，例如电子邮件地址（“电子邮件”），也可以将身份与特定应用程序关联，例如Adobe Advertising Cloud ID (“AdCloud”)或Adobe Target ID (“TNTID”)。

Identity Service维护全局定义（标准）和用户定义（自定义）身份命名空间的存储。 标准命名空间适用于所有组织（例如，“Email”和“ECID”），而您的组织也可以创建自定义命名空间以满足其特定需求。

有关[!DNL Experience Platform]中身份命名空间的更多信息，请参阅[身份命名空间概述](../identity-service/features/namespaces.md)。

## 提交请求 {#submit}

以下各节概述了如何使用[!DNL Privacy Service] API或UI为[!DNL Real-Time Customer Profile]提出隐私请求。 在阅读这些部分之前，您应该查看或了解[Privacy Service API](../privacy-service/api/getting-started.md)或[Privacy Service UI](../privacy-service/ui/overview.md)文档。 本文档提供了有关如何提交隐私作业的完整步骤，包括如何在请求负载中正确格式化提交的用户身份数据。

>[!IMPORTANT]
>
>Privacy Service只能使用不执行身份拼接的合并策略处理[!DNL Profile]数据。 有关详细信息，请参阅[合并策略限制](#merge-policy-limitations)部分。
>
>请注意，隐私请求在法规要求内异步处理，完成所需时间可能会有所不同。 如果在请求仍在处理时您的[!DNL Profile]数据发生了更改，则不能保证也会在该请求中处理这些传入记录。 只有请求隐私作业时保存在数据湖或配置文件存储中的配置文件才会被删除。 如果您在删除作业期间摄取与删除请求的主题相关的配置文件数据，则无法保证所有配置文件片段都会被删除。
>您有责任在删除请求时了解Experience Platform或配置文件服务中的任何传入数据，因为这些数据将插入记录存储中。 您必须谨慎接收已被删除或正在删除的数据。

### 使用 API

在API中创建作业请求时，`userIDs`中提供的任何ID都必须使用特定的`namespace`和`type`。 必须为`namespace`值提供[!DNL Identity Service]识别的有效[标识命名空间](#namespaces)，而`type`必须为`standard`或`unregistered`（分别用于标准命名空间和自定义命名空间）。

>[!NOTE]
>
>您可能需要为每个客户提供多个ID，具体取决于身份图以及您的配置文件片段在Experience Platform数据集中的分配方式。 有关详细信息，请参阅下一节[配置文件片段](#fragments)。

此外，请求有效负载的`include`数组必须包含请求所接收的不同数据存储的产品值。 要删除与标识关联的配置文件数据，数组必须包含值`ProfileService`。 要删除客户的标识图关联，数组必须包含值`identity`。

>[!NOTE]
>
>有关在`include`数组中使用`ProfileService`和`identity`所产生的影响的更多详细信息，请参阅本文档后面有关[配置文件请求和身份请求](#profile-v-identity)的部分。

以下请求为[!DNL Profile]存储区中的单个客户数据创建新的隐私作业。 在`userIDs`数组中为客户提供了两个标识值；一个使用标准`Email`标识命名空间，另一个使用自定义`Customer_ID`命名空间。 它还包含`include`数组中[!DNL Profile] (`ProfileService`)的产品值：

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
>Experience Platform跨所有属于您组织的[沙盒](../sandboxes/home.md)处理隐私请求。 因此，请求中包含的任何`x-sandbox-name`标头都会被系统忽略。

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

在UI中创建作业请求时，请确保选择&#x200B;**[!UICONTROL 产品]**&#x200B;下的&#x200B;**[!UICONTROL AEP Data Lake]**&#x200B;和/或&#x200B;**[!UICONTROL 配置文件]**，以便分别处理存储在数据湖或[!DNL Real-Time Customer Profile]中的数据的作业。

![正在用户界面中创建访问作业请求，并在“产品”下选择“配置文件”选项](./images/privacy/product-value.png)

## 隐私请求中的配置文件片段 {#fragments}

在[!DNL Profile]数据存储中，单个客户的个人数据通常由多个配置文件片段组成，这些片段通过身份图与人员关联。 向[!DNL Profile]存储区发出隐私请求时，请务必注意，请求仅在配置文件片段级别进行处理，而不是整个配置文件。

例如，考虑这样一种情况：您将客户属性数据存储到三个单独的数据集中，这几个数据集使用不同的标识符将该数据与单个客户关联：

| 数据集名称 | 主要身份标识字段 | 存储的属性 |
| --- | --- | --- |
| 数据集1 | `customer_id` | `address` |
| 数据集2 | `email_id` | `firstName`、`lastName` |
| 数据集3 | `email_id` | `mlScore` |

其中一个数据集使用`customer_id`作为其主要标识符，而另外两个数据集使用`email_id`。 如果您只使用`email_id`作为用户ID值来发送隐私请求（访问或删除），则只会处理`firstName`、`lastName`和`mlScore`属性，而`address`不会受到影响。

为确保您的隐私请求能够处理所有相关客户属性，您必须为可能存储了这些属性的所有适用数据集提供主标识值（每个客户最多九个ID）。 有关通常标记为标识的字段的更多信息，请参阅架构组合](../xdm/schema/composition.md#identity)的[基础知识中有关标识字段的部分。

## 正在处理删除请求 {#delete}

当[!DNL Experience Platform]收到来自[!DNL Privacy Service]的删除请求时，[!DNL Experience Platform]向[!DNL Privacy Service]发送确认，确认已收到该请求并且受影响的数据已标记为删除。 隐私作业完成后，记录将被删除。

>[!IMPORTANT]
>
>隐私删除请求不是即时发出的，并且可能会因涉及的服务和其他影响因素（例如地理位置）而异。 完成隐私作业的时间范围介于15天到45天之间，但并不保证会实现。

根据您在个人资料的隐私请求(`ProfileService`)中是否还包含Identity Service (`identity`)和数据湖(`aepDataLake`)作为产品，可能会在不同时间从系统中删除与个人资料相关的不同数据集：

| 包含的产品 | 效应 |
| --- | --- |
| 仅`ProfileService` | 一旦Privacy Service发送删除请求已完成确认，则会立即将该配置文件视为已删除。 但是，个人资料的身份图仍然会保留，并且个人资料有可能在摄取具有相同身份的新数据时进行重构。 与个人资料关联的无法识别个人身份的数据也保留在数据湖中。 |
| `ProfileService` 和 `identity` | 一旦Privacy Service发送删除请求已完成确认，则会立即删除用户档案及其关联的身份图。 与个人资料关联的无法识别个人身份的数据也保留在数据湖中。 |
| `ProfileService` 和 `aepDataLake` | 一旦Privacy Service发送删除请求已完成确认，则会立即删除用户档案。 但是，个人资料的身份图仍然会保留，并且个人资料有可能在摄取具有相同身份的新数据时进行重构。<br><br>当Data Lake产品回应收到请求且当前正在处理时，与配置文件关联的数据将被软删除，因此任何[!DNL Experience Platform]服务都无法访问。 作业完成后，数据将从数据湖中完全删除。 |
| `ProfileService`、`identity`和`aepDataLake` | 一旦Privacy Service发送删除请求已完成确认，则会立即删除用户档案及其关联的身份图。<br><br>当Data Lake产品回应收到请求且当前正在处理时，与配置文件关联的数据将被软删除，因此任何[!DNL Experience Platform]服务都无法访问。 作业完成后，数据将从数据湖中完全删除。 |

有关跟踪作业状态的详细信息，请参阅[[!DNL Privacy Service] 文档](../privacy-service/home.md#monitor)。

### 配置文件请求与身份请求 {#profile-v-identity}

如果对配置文件(`ProfileService`)而不是标识服务(`identity`)发出删除请求，则生成的作业将删除为客户（或客户组）收集的属性数据，但不会删除在标识图中建立的关联。

例如，使用客户的`email_id`和`customer_id`的删除请求将删除这些ID下存储的所有属性数据。 但是，此后在同一`customer_id`下摄取的任何数据都将仍然与相应的`email_id`关联，因为该关联仍然存在。

要删除给定客户的配置文件和所有标识关联，请确保在删除请求中同时包含配置文件和标识服务作为目标产品。

### 合并策略限制 {#merge-policy-limitations}

Privacy Service只能使用不执行身份拼接的合并策略处理[!DNL Profile]数据。 如果您使用UI确认是否正在处理您的隐私请求，请确保您使用的是将&#x200B;**[!DNL None]**&#x200B;用作其[!UICONTROL ID拼接]类型的策略。 换句话说，您不能使用[!UICONTROL ID拼接]设置为[!UICONTROL 专用图形]的合并策略。

>![合并策略的ID拼接设置为None](./images/privacy/no-id-stitch.png)

## 后续步骤

通过阅读本文档，您已了解[!DNL Experience Platform]中处理隐私请求涉及的重要概念。 要加深您对如何管理身份数据和创建隐私作业的了解，请继续阅读本指南中提供的文档。

有关处理[!DNL Profile]未使用的[!DNL Experience Platform]资源的隐私请求的信息，请参阅有关在数据湖](../catalog/privacy.md)中处理[隐私请求的文档。
