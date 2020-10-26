---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 实时客户用户档案中的隐私请求处理
topic: overview
translation-type: tm+mt
source-git-commit: 066337419431db24bde0a8d0d30b85132d08f43c
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 0%

---


# 隐私请求处理 [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] 处理客户访问、选择退出出售或删除其个人数据的请求，这些请求由隐私法规(如一般数据保护规定(GDPR)和(CCPA)) [!DNL California Consumer Privacy Act] 规定。

本文档涵盖与处理隐私请求相关的基本概念 [!DNL Real-time Customer Profile]。

## 入门指南

在阅读本指南之前，建议您对以下服 [!DNL Experience Platform] 务有一定的了解：

* [[!DNL Privacy Service]](home.md):管理跨Adobe Experience Cloud应用程序访问、选择退出销售或删除其个人数据的客户请求。
* [[!DNL Identity Service]](../identity-service/home.md):通过跨设备和系统桥接身份，解决客户体验数据碎片化带来的根本挑战。
* [[!DNL Real-time Customer Profile]](../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

## 了解身份命名空间 {#namespaces}

Adobe Experience Platform [!DNL Identity Service] 将跨系统和设备的客户身份数据建立桥梁。 [!DNL Identity Service] 使用 **身份命名空间** ，通过将身份值与其来源系统相关联来提供与身份值相关的上下文。 命名空间可以表示一个通用概念，如电子邮件地址（“电子邮件”），或将标识与特定应用程序(如Adobe Advertising CloudID(“AdCloud”)或Adobe TargetID(“TNTID”))关联。

Identity Service维护全局定义（标准）和用户定义（自定义）标识命名空间的存储。 标准命名空间适用于所有组织（例如，“电子邮件”和“ECID”），而您的组织也可以创建自定义命名空间以满足其特定需求。

有关中的标识命名空间的详 [!DNL Experience Platform]细信息，请参 [阅标识命名空间概述](../identity-service/namespaces.md)。

## 提交请求 {#submit}

以下各节概述了如何使用API或UI [!DNL Real-time Customer Profile] 发出 [!DNL Privacy Service] 隐私请求。 在阅读这些部分之前，强烈建议您查看 [Privacy ServiceAPI](../privacy-service/api/getting-started.md) 或 [](../privacy-service/ui/overview.md) Privacy ServiceUI文档，了解如何提交隐私作业的完整步骤，包括如何在请求负载中正确设置提交的用户身份数据的格式。

>[!IMPORTANT]
>
>Privacy Service只能使用不执 [!DNL Profile] 行身份拼接的合并策略处理数据。 如果您使用UI确认是否正在处理您的隐私请求，请确保您使用的策略[!DNL None]为“” [!UICONTROL ID拼接] 。 换言之，您不能使用将ID拼接设 [!UICONTROL 置为] “专用图[!UICONTROL 形”的合并策略]。
>
>![](./images/privacy/no-id-stitch.png)
>
>还必须指出，无法保证完成隐私请求所花费的时间。 如果在请求仍处 [!DNL Profile] 理时数据中发生更改，则也无法保证是否处理了这些记录。

### 使用API

在API中创建作业请求时，中提供的任何ID `userIDs` 都必须使用特定 `namespace` 和 `type`。 必须为 [值提供](#namespaces)[!DNL Identity Service] 可识别的有效标识命名空间，而 `namespace` 该必须 `type` 为或( `standard``unregistered` 分别针对标准命名空间和自定义)。

>[!NOTE]
>
>您可能需要为每个客户提供多个ID，具体取决于标识图以及用户档案片段在平台数据集中的分发方式。 请参阅下一节 [用户档案片段](#fragments) ，以了解更多信息。

此外，请求 `include` 有效负荷的数组必须包含请求所针对的不同数据存储的产品值。 向阵列发出请 [!DNL Data Lake]求时，阵列必须包含值“ProfileService”。

以下请求为商店中单个客户的数据创建新的隐私 [!DNL Profile] 作业。 阵列中为客户提供了两个标识 `userIDs` 值；一个使用标 `Email` 准标识命名空间，另一个使用自定义 `Customer_ID` 命名空间。 它还包括阵列中( [!DNL Profile] )`ProfileService`的产品 `include` 值：

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

在UI中创建作业请求时，请务必在“产 **[!UICONTROL 品”下选]** 择AEP **[!UICONTROL Data Lake和／或]** 用户档案 **[!UICONTROL ，以便分别]** 处理存储在或中的 [!DNL Data Lake][!DNL Real-time Customer Profile]数据的作业。

<img src="images/privacy/product-value.png" width="450"><br>

## 用户档案片段在隐私请求中 {#fragments}

在数 [!DNL Profile] 据存储中，个人客户的个人数据通常由多个用户档案片段组成，这些片段通过身份图与个人相关联。 在向商店发出隐 [!DNL Profile] 私请求时，请务必注意，请求仅在用户档案片段级别处理，而不是在整个用户档案处理。

例如，考虑一种情况，即您将客户属性数据存储在三个不同的数据集中，这些数据集使用不同的标识符将该数据与单个客户关联：

| 数据集名称 | 主标识字段 | 存储属性 |
| --- | --- | --- |
| 数据集1 | `customer_id` | `address` |
| 数据集2 | `email_id` | `firstName`, `lastName` |
| 数据集3 | `email_id` | `mlScore` |

其中一个数据集 `customer_id` 用作其主标识符，而另两个则使用 `email_id`。 如果您仅使用用户ID值发送隐私请求( `email_id` 访问或删除)，则只会 `firstName`处理 `lastName`、和 `mlScore` 属性，而不 `address` 会受到影响。

要确保您的隐私请求处理所有相关客户属性，您必须为所有可能存储这些属性的适用数据集提供主要标识值（每个客户最多可以提供9个ID）。 有关通常标记为身份的字段的 [更多信息](../xdm/schema/composition.md#identity) ，请参阅模式合成基础知识中有关标识字段的部分。

>[!NOTE]
>
>如果使用不同的沙 [箱](../sandboxes/home.md) ，则必须对每个沙 [!DNL Profile] 箱发出单独的隐私请求，并在标头中指明相应的沙箱 `x-sandbox-name` 名称。

## 删除请求处理

当 [!DNL Experience Platform] 收到来自的删除请 [!DNL Privacy Service]求 [!DNL Platform] 时，会发送确认， [!DNL Privacy Service] 确认该请求已接收且受影响的数据已标记为删除。 隐私作业完成后，记录 [!DNL Data Lake] 会 [!DNL Profile] 从或存储中删除。 当删除作业仍在处理时，数据会被软删除，因此任何服务都无法访问 [!DNL Platform] 它。 有关跟踪作 [[!DNL Privacy Service] 业状态](../privacy-service/home.md#monitor) ，请参阅文档。

>[!IMPORTANT]
>
>成功的删除请求会删除客户（或客户集）收集的属性数据，但该请求不会删除在标识图中建立的关联。
>
>例如，使用客户的删除请求并删除 `email_id` 存储在 `customer_id` 这些ID下的所有属性数据。 但是，随后在同一数据下摄取的任何 `customer_id` 数据仍与相应的数据相关联， `email_id`因为该关联仍然存在。

在以后的版本中， [!DNL Platform] 将在实际删除 [!DNL Privacy Service] 数据后向其发送确认信息。

## 后续步骤

通过阅读此文档，您了解了处理中的隐私请求所涉及的重要概念 [!DNL Experience Platform]。 建议您继续阅读本指南中提供的文档，以加深您对如何管理身份数据和创建隐私工作的理解。

有关处理未使用的资源的隐 [!DNL Platform] 私请求的信 [!DNL Profile]息，请参阅数据 [湖中的隐私请求处理文档](../catalog/privacy.md)。