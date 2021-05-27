---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 实时客户资料中的隐私请求处理
type: Documentation
description: Adobe Experience Platform Privacy Service会按照许多隐私法规的规定处理客户访问、选择退出销售或删除其个人数据的请求。 本文档介绍了与处理实时客户资料的隐私请求相关的基本概念。
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: e94482532e0c5698cfe5e51ba260f89c67fa64f0
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile]中的隐私请求处理

Adobe Experience Platform [!DNL Privacy Service]会按照隐私法规(如《通用数据保护条例》(GDPR)和[!DNL California Consumer Privacy Act](CCPA))的规定，处理客户访问、选择退出销售或删除其个人数据的请求。

本文档介绍与在Adobe Experience Platform中处理[!DNL Real-time Customer Profile]隐私请求相关的基本概念。

>[!NOTE]
>
>本指南仅介绍如何在Experience Platform中对配置文件数据存储进行隐私请求。 如果您还计划为平台数据湖发出隐私请求，除本教程外，请参阅数据湖](../catalog/privacy.md)中[隐私请求处理指南。
>
>有关如何为其他Adobe Experience Cloud应用程序发出隐私请求的步骤，请参阅[Privacy Service文档](../privacy-service/experience-cloud-apps.md)。

## 入门指南

在阅读本指南之前，建议您对以下[!DNL Experience Platform]服务有一定的了解：

* [[!DNL Privacy Service]](../privacy-service/home.md):管理客户在Adobe Experience Cloud应用程序中访问、选择退出销售或删除其个人数据的请求。
* [[!DNL Identity Service]](../identity-service/home.md):通过跨设备和系统桥接身份，解决客户体验数据碎片化所带来的根本难题。
* [[!DNL Real-time Customer Profile]](home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

## 了解身份命名空间 {#namespaces}

Adobe Experience Platform [!DNL Identity Service]跨系统和设备桥接客户身份数据。 [!DNL Identity Service] 使用 **身** 份名称，通过将身份值与其原始系统相关联，来提供身份值的上下文。命名空间可以表示一个通用概念，如电子邮件地址（“电子邮件”），或将标识与特定应用程序(如Adobe Advertising Cloud ID(“AdCloud”)或Adobe Target ID(“TNTID”))相关联。

Identity Service维护全局定义（标准）和用户定义（自定义）身份命名空间的存储区。 标准命名空间适用于所有组织（例如，“电子邮件”和“ECID”），而您的组织也可以创建自定义命名空间以满足其特定需求。

有关[!DNL Experience Platform]中身份命名空间的更多信息，请参阅[身份命名空间概述](../identity-service/namespaces.md)。

## 提交请求 {#submit}

以下各节概述了如何使用[!DNL Privacy Service] API或UI向[!DNL Real-time Customer Profile]发出隐私请求。 在阅读这些部分之前，强烈建议您查看[Privacy ServiceAPI](../privacy-service/api/getting-started.md)或[Privacy ServiceUI](../privacy-service/ui/overview.md)文档，以了解有关如何提交隐私作业的完整步骤，包括如何以请求负载正确设置提交的用户身份数据的格式。

>[!IMPORTANT]
>
>Privacy Service只能使用不执行身份拼合的合并策略处理[!DNL Profile]数据。 如果您使用UI确认是否正在处理隐私请求，请确保使用策略，其中“[!DNL None]”作为[!UICONTROL ID拼合]类型。 换言之，您不能使用将[!UICONTROL ID拼合]设置为“[!UICONTROL 专用图]”的合并策略。
>
>![](./images/privacy/no-id-stitch.png)
>
>另外，请务必注意，无法保证完成隐私请求所花费的时间。 如果在请求仍在处理时，[!DNL Profile]数据中发生更改，则无法保证是否处理了这些记录。

### 使用 API

在API中创建作业请求时，`userIDs`中提供的任何ID都必须使用特定的`namespace`和`type`。 必须为`namespace`值提供由[!DNL Identity Service]识别的有效[标识命名空间](#namespaces)，而`type`必须为`standard`或`unregistered`（对于标准命名空间和自定义命名空间，分别为）。

>[!NOTE]
>
>您可能需要为每个客户提供多个ID，具体取决于身份图以及Platform数据集中配置文件片段的分发方式。 有关更多信息，请参阅下一节[配置文件片段](#fragments)。

此外，请求有效负载的`include`数组必须包含请求所针对的不同数据存储的产品值。 向[!DNL Data Lake]发出请求时，阵列必须包含值“ProfileService”。

以下请求会为[!DNL Profile]存储中的单个客户数据创建新的隐私作业。 在`userIDs`数组中为客户提供了两个标识值；一个使用标准`Email`标识命名空间，另一个使用自定义`Customer_ID`命名空间。 它还包括`include`数组中[!DNL Profile](`ProfileService`)的产品值：

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
    "regulation": "ccpa"
}'
```

### 使用UI

在UI中创建作业请求时，请务必在&#x200B;**[!UICONTROL 产品]**&#x200B;下选择&#x200B;**[!UICONTROL AEP Data Lake]**&#x200B;和/或&#x200B;**[!UICONTROL 配置文件]**，以便分别处理存储在[!DNL Data Lake]或[!DNL Real-time Customer Profile]中的数据的作业。

<img src="images/privacy/product-value.png" width="450"><br>

## 隐私请求中的配置文件片段 {#fragments}

在[!DNL Profile]数据存储中，单个客户的个人数据通常由多个配置文件片段组成，这些片段通过身份图与人员关联。 在向[!DNL Profile]存储发出隐私请求时，请务必注意，请求仅在配置文件片段级别处理，而不是在整个配置文件级别处理。

例如，假设您将客户属性数据存储在三个单独的数据集中，这些数据集使用不同的标识符将该数据与各个客户关联：

| 数据集名称 | 主标识字段 | 存储的属性 |
| --- | --- | --- |
| 数据集1 | `customer_id` | `address` |
| 数据集2 | `email_id` | `firstName`、`lastName` |
| 数据集3 | `email_id` | `mlScore` |

其中一个数据集使用`customer_id`作为其主要标识符，而另两个数据集则使用`email_id`。 如果要仅使用`email_id`作为用户ID值发送隐私请求（访问或删除），则将仅处理`firstName`、`lastName`和`mlScore`属性，而`address`不会受到影响。

要确保您的隐私请求处理所有相关的客户属性，您必须为可能存储这些属性的所有适用数据集提供主标识值（每个客户最多9个ID）。 有关通常标记为身份的字段的更多信息，请参阅[架构组合基础知识](../xdm/schema/composition.md#identity)中有关标识字段的部分。

>[!NOTE]
>
>如果您使用不同的[沙盒](../sandboxes/home.md)来存储[!DNL Profile]数据，则必须对每个沙盒发出单独的隐私请求，并在`x-sandbox-name`标头中指示相应的沙盒名称。

## 删除请求处理

当[!DNL Experience Platform]收到来自[!DNL Privacy Service]的删除请求时，[!DNL Platform]向[!DNL Privacy Service]发送确认，确认该请求已被接收，且受影响的数据已被标记为删除。 隐私作业完成后，将从[!DNL Data Lake]或[!DNL Profile]存储中删除记录。 删除作业仍在处理，但数据会被软删除，因此任何[!DNL Platform]服务都无法访问。 有关跟踪作业状态的更多信息，请参阅[[!DNL Privacy Service] 文档](../privacy-service/home.md#monitor)。

>[!IMPORTANT]
>
>成功的删除请求会删除客户（或一组客户）收集的属性数据，但请求不会删除在身份图中建立的关联。
>
>例如，使用客户`email_id`和`customer_id`的删除请求会删除这些ID下存储的所有属性数据。 但是，随后在同一`customer_id`下摄取的任何数据仍将与相应的`email_id`关联，因为关联仍然存在。

在将来的版本中， [!DNL Platform]将在数据被实际删除后向[!DNL Privacy Service]发送确认。

## 后续步骤

阅读本文档后，您便了解了处理[!DNL Experience Platform]中的隐私请求所涉及的重要概念。 建议您继续阅读本指南中提供的文档，以加深对如何管理身份数据和创建隐私作业的了解。

有关处理[!DNL Platform]资源中[!DNL Profile]未使用的隐私请求的信息，请参阅数据湖](../catalog/privacy.md)中有关[隐私请求处理的文档。
