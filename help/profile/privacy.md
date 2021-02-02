---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 实时客户用户档案中的隐私请求处理
topic: overview
type: Documentation
description: Adobe Experience Platform Privacy Service处理客户访问、选择退出出售或删除其个人数据的请求，这些请求由众多隐私法规规定。 此文档涵盖与处理实时客户用户档案的隐私请求相关的基本概念。
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 0%

---


# 在[!DNL Real-time Customer Profile]中处理隐私请求

Adobe Experience Platform[!DNL Privacy Service]处理客户访问、选择退出出售或删除其个人数据的请求，这些请求由隐私法规(如一般数据保护规定(GDPR)和[!DNL California Consumer Privacy Act](CCPA))规定。

此文档涵盖与处理[!DNL Real-time Customer Profile]的隐私请求相关的基本概念。

## 入门指南

在阅读本指南之前，建议您对以下[!DNL Experience Platform]服务有正确的了解：

* [[!DNL Privacy Service]](home.md):管理跨Adobe Experience Cloud应用程序访问、选择退出销售或删除其个人数据的客户请求。
* [[!DNL Identity Service]](../identity-service/home.md):通过跨设备和系统桥接身份，解决客户体验数据碎片化带来的根本挑战。
* [[!DNL Real-time Customer Profile]](../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

## 了解身份命名空间{#namespaces}

Adobe Experience Platform[!DNL Identity Service]跨系统和设备连接客户身份数据。 [!DNL Identity Service] 使用 **标** 识名称包，通过将标识值与其来源系统相关来提供标识值的上下文。命名空间可以表示一个通用概念，如电子邮件地址（“电子邮件”），或将标识与特定应用程序(如Adobe Advertising CloudID(“AdCloud”)或Adobe TargetID(“TNTID”))关联。

Identity Service维护全局定义（标准）和用户定义（自定义）标识命名空间的存储。 标准命名空间适用于所有组织（例如，“电子邮件”和“ECID”），而您的组织也可以创建自定义命名空间以满足其特定需求。

有关[!DNL Experience Platform]中的标识命名空间的详细信息，请参阅[标识命名空间概述](../identity-service/namespaces.md)。

## 提交请求{#submit}

以下各节概述了如何使用[!DNL Privacy Service] API或UI向[!DNL Real-time Customer Profile]发出隐私请求。 在阅读这些部分之前，强烈建议您查看[Privacy ServiceAPI](../privacy-service/api/getting-started.md)或[Privacy ServiceUI](../privacy-service/ui/overview.md)文档，了解有关如何提交隐私作业的完整步骤，包括如何在请求负载中正确设置提交的用户身份数据的格式。

>[!IMPORTANT]
>
>Privacy Service只能使用不执行身份拼接的合并策略处理[!DNL Profile]数据。 如果您使用UI确认是否正在处理您的隐私请求，请确保您使用的策略类型为[!UICONTROL ID structing]，类型为“[!DNL None]”。 换言之，您不能使用将[!UICONTROL ID structing]设置为“[!UICONTROL 专用图]”的合并策略。
>
>![](./images/privacy/no-id-stitch.png)
>
>还必须指出，无法保证完成隐私请求所花费的时间。 如果在请求仍在处理时[!DNL Profile]数据中发生更改，则也无法保证是否处理了这些记录。

### 使用API

在API中创建作业请求时，在`userIDs`中提供的任何ID都必须使用特定的`namespace`和`type`。 必须为`namespace`值提供由[!DNL Identity Service]识别的有效[标识命名空间](#namespaces)，而`type`必须为`standard`或`unregistered`(对于标准和自定义命名空间，分别为)。

>[!NOTE]
>
>您可能需要为每个客户提供多个ID，具体取决于标识图以及用户档案片段在平台数据集中的分发方式。 有关详细信息，请参阅下一节[用户档案片段](#fragments)。

此外，请求有效负荷的`include`数组必须包含请求所针对的不同数据存储的产品值。 向[!DNL Data Lake]发出请求时，阵列必须包含值“ProfileService”。

以下请求为[!DNL Profile]商店中单个客户的数据创建新的隐私作业。 在`userIDs`阵列中为客户提供了两个标识值；一个使用标准`Email`标识命名空间，另一个使用自定义`Customer_ID`命名空间。 它还包括`include`阵列中[!DNL Profile](`ProfileService`)的产品值：

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
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
    "include": ["ProfileService"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

### 使用UI

在UI中创建作业请求时，请务必在&#x200B;**[!UICONTROL 产品]**&#x200B;下选择&#x200B;**[!UICONTROL AEP用户档案湖]**&#x200B;和／或&#x200B;****，以分别处理存储在[!DNL Data Lake]或[!DNL Real-time Customer Profile]中的数据的作业。

<img src="images/privacy/product-value.png" width="450"><br>

## 用户档案请求中的数据片段{#fragments}

在[!DNL Profile]用户档案存储中，单个客户的个人数据通常由多个客户片段组成，这些片段通过身份图与个人关联。 在向[!DNL Profile]商店发出隐私请求时，请务必注意，请求仅在用户档案片段级别处理，而不是在整个用户档案处理。

例如，考虑一种情况，即您将客户属性数据存储在三个不同的数据集中，这些数据集使用不同的标识符将该数据与单个客户关联：

| 数据集名称 | 主标识字段 | 存储属性 |
| --- | --- | --- |
| 数据集1 | `customer_id` | `address` |
| 数据集2 | `email_id` | `firstName`、`lastName` |
| 数据集3 | `email_id` | `mlScore` |

其中一个数据集使用`customer_id`作为其主要标识符，而另两个数据集使用`email_id`。 如果仅使用`email_id`作为用户ID值发送隐私请求（访问或删除），则只会处理`firstName`、`lastName`和`mlScore`属性，而不会影响`address`。

要确保您的隐私请求处理所有相关客户属性，您必须为所有可能存储这些属性的适用数据集提供主要标识值（每个客户最多可以提供9个ID）。 有关通常标为标识的字段的详细信息，请参见[模式合成基础知识](../xdm/schema/composition.md#identity)中有关标识字段的部分。

>[!NOTE]
>
>如果使用不同的[沙箱](../sandboxes/home.md)存储[!DNL Profile]数据，则必须对每个沙箱发出单独的隐私请求，并在`x-sandbox-name`标头中指明相应的沙箱名称。

## 删除请求处理

当[!DNL Experience Platform]收到来自[!DNL Privacy Service]的删除请求时，[!DNL Platform]会向[!DNL Privacy Service]发送确认，确认已收到该请求，且受影响的数据已被标记为删除。 隐私作业完成后，将从[!DNL Data Lake]或[!DNL Profile]存储中删除记录。 当删除作业仍在处理时，数据被软删除，因此任何[!DNL Platform]服务都无法访问。 有关跟踪作业状态的详细信息，请参阅[[!DNL Privacy Service] 文档](../privacy-service/home.md#monitor)。

>[!IMPORTANT]
>
>成功的删除请求会删除客户（或客户集）收集的属性数据，但该请求不会删除在标识图中建立的关联。
>
>例如，使用客户的`email_id`和`customer_id`的删除请求将删除存储在这些ID下的所有属性数据。 但是，随后在同一`customer_id`下摄取的任何数据仍与相应的`email_id`相关，因为该关联仍然存在。

在将来的版本中，[!DNL Platform]将在数据被物理删除后向[!DNL Privacy Service]发送确认信息。

## 后续步骤

通过阅读此文档，您了解了处理[!DNL Experience Platform]中的隐私请求所涉及的重要概念。 建议您继续阅读本指南中提供的文档，以加深您对如何管理身份数据和创建隐私工作的理解。

有关处理[!DNL Platform]资源未被[!DNL Profile]使用的隐私请求的信息，请参阅数据湖](../catalog/privacy.md)中有关处理[隐私请求的文档。