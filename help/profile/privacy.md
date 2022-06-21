---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 实时客户资料中的隐私请求处理
type: Documentation
description: Adobe Experience Platform Privacy Service会按照许多隐私法规的规定处理客户访问、选择退出销售或删除其个人数据的请求。 本文档介绍了与处理实时客户资料的隐私请求相关的基本概念。
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: 1686ff1684080160057462e9aa40819a60bf6b75
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 0%

---

# 中的隐私请求处理 [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] 处理客户访问、选择退出销售或删除其个人数据的请求(如《通用数据保护条例》(GDPR)等隐私法规中所述)，并 [!DNL California Consumer Privacy Act] (CCPA)。

本文档介绍与处理 [!DNL Real-time Customer Profile] 在Adobe Experience Platform。

>[!NOTE]
>
>本指南仅介绍如何在Experience Platform中对配置文件数据存储进行隐私请求。 如果您还计划针对平台数据湖发出隐私请求，请参阅 [数据湖中的隐私请求处理](../catalog/privacy.md) 除了本教程之外，
>
>有关如何为其他Adobe Experience Cloud应用程序发出隐私请求的步骤，请参阅 [Privacy Service文档](../privacy-service/experience-cloud-apps.md).

## 快速入门

建议您对以下方面有一定的了解 [!DNL Experience Platform] 服务：

* [[!DNL Privacy Service]](../privacy-service/home.md):管理客户在Adobe Experience Cloud应用程序中访问、选择退出销售或删除其个人数据的请求。
* [[!DNL Identity Service]](../identity-service/home.md):通过跨设备和系统桥接身份，解决客户体验数据碎片化所带来的根本难题。
* [[!DNL Real-time Customer Profile]](home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

## 了解身份命名空间 {#namespaces}

Adobe Experience Platform [!DNL Identity Service] 跨系统和设备连接客户身份数据。 [!DNL Identity Service] 使用 **身份命名空间** 通过将身份值与其原籍系统联系起来，提供身份值的上下文。 命名空间可以表示一个通用概念，如电子邮件地址（“电子邮件”），或将标识与特定应用程序(如Adobe Advertising Cloud ID(“AdCloud”)或Adobe Target ID(“TNTID”))相关联。

Identity Service维护全局定义（标准）和用户定义（自定义）身份命名空间的存储区。 标准命名空间适用于所有组织（例如，“电子邮件”和“ECID”），而您的组织也可以创建自定义命名空间以满足其特定需求。

有关 [!DNL Experience Platform]，请参阅 [身份命名空间概述](../identity-service/namespaces.md).

## 提交请求 {#submit}

以下各节将简要介绍如何对 [!DNL Real-time Customer Profile] 使用 [!DNL Privacy Service] API或UI。 在阅读这些部分之前，强烈建议您查看 [Privacy ServiceAPI](../privacy-service/api/getting-started.md) 或 [Privacy ServiceUI](../privacy-service/ui/overview.md) 有关如何提交隐私作业的完整步骤文档，包括如何以请求负载正确设置已提交的用户身份数据的格式。

>[!IMPORTANT]
>
>Privacy Service只能处理 [!DNL Profile] 使用不执行身份拼合的合并策略的数据。 如果您使用UI确认是否正在处理隐私请求，请确保您使用的策略包含“[!DNL None]&quot;作为 [!UICONTROL ID拼合] 类型。 换句话说，您不能使用合并策略， [!UICONTROL ID拼合] 设置为&quot;[!UICONTROL 专用图]&quot;
>
>![合并策略的ID拼合设置为“无”](./images/privacy/no-id-stitch.png)
>
>另外，请务必注意，无法保证完成隐私请求所花费的时间。 如果 [!DNL Profile] 当请求仍在处理时，也无法保证是否处理了这些记录。

### 使用 API

在API中创建作业请求时， `userIDs` 必须使用特定 `namespace` 和 `type`. 有效 [标识命名空间](#namespaces) 确认 [!DNL Identity Service] 必须为 `namespace` 值，而 `type` 必须为 `standard` 或 `unregistered` （分别用于标准和自定义命名空间）。

>[!NOTE]
>
>您可能需要为每个客户提供多个ID，具体取决于身份图以及Platform数据集中配置文件片段的分发方式。 请参阅下一节 [配置文件片段](#fragments) 以了解更多信息。

此外， `include` 请求有效负载的数组必须包含对请求进行的不同数据存储的产品值。 向 [!DNL Data Lake]，则数组必须包含值“ProfileService”。

以下请求会在 [!DNL Profile] 存储。 在 `userIDs` 数组；使用标准 `Email` 标识命名空间，而另一个使用自定义 `Customer_ID` 命名空间。 它还包括 [!DNL Profile] (`ProfileService`) `include` 数组：

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
    "include": ["ProfileService"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

>[!IMPORTANT]
>
>平台处理所有 [沙箱](../sandboxes/home.md) 属于您的组织。 因此， `x-sandbox-name` 系统将忽略请求中包含的标头。

### 使用UI

在UI中创建作业请求时，请务必选择 **[!UICONTROL AEP Data Lake]** 和/或 **[!UICONTROL 用户档案]** 在 **[!UICONTROL 产品]** 以便处理存储在 [!DNL Data Lake] 或 [!DNL Real-time Customer Profile]，分别为。

![在UI中创建访问作业请求，并在产品下选择配置文件选项](./images/privacy/product-value.png)

## 隐私请求中的配置文件片段 {#fragments}

在 [!DNL Profile] 数据存储中，单个客户的个人数据通常由多个配置文件片段组成，这些片段通过身份图与人员关联。 向 [!DNL Profile] 存储，请务必注意，请求仅在配置文件片段级别处理，而不是在整个配置文件级别处理。

例如，假设您将客户属性数据存储在三个单独的数据集中，这些数据集使用不同的标识符将该数据与各个客户关联：

| 数据集名称 | 主标识字段 | 存储的属性 |
| --- | --- | --- |
| 数据集1 | `customer_id` | `address` |
| 数据集2 | `email_id` | `firstName`、`lastName` |
| 数据集3 | `email_id` | `mlScore` |

其中一个数据集使用 `customer_id` 作为主标识符，而其他两个使用 `email_id`. 如果您仅使用 `email_id` 作为用户ID值，仅 `firstName`, `lastName`和 `mlScore` 属性会被处理，而 `address` 不会受到影响。

要确保您的隐私请求处理所有相关的客户属性，您必须为可能存储这些属性的所有适用数据集提供主标识值（每个客户最多9个ID）。 请参阅 [架构组合基础知识](../xdm/schema/composition.md#identity) 有关通常标记为身份的字段的更多信息。

## 删除请求处理

When [!DNL Experience Platform] 从接收删除请求 [!DNL Privacy Service], [!DNL Platform] 向发送确认 [!DNL Privacy Service] 请求已收到且受影响的数据已标记为删除。 然后，将从 [!DNL Data Lake] 或 [!DNL Profile] 完成隐私作业后进行存储。 删除作业仍在处理中，但数据会被软删除，因此任何用户都无法访问 [!DNL Platform] 服务。 请参阅 [[!DNL Privacy Service] 文档](../privacy-service/home.md#monitor) 以了解有关跟踪作业状态的更多信息。

>[!IMPORTANT]
>
>如果对用户档案(`ProfileService`)，但不是Identity Service(`identity`)，则生成的作业将删除客户（或一组客户）收集的属性数据，但不会删除在身份图中建立的关联。
>
>例如，使用客户 `email_id` 和 `customer_id` 删除存储在这些ID下的所有属性数据。 但是，之后在同一数据下摄取的任何数据 `customer_id` 仍将与相应的 `email_id`，因为关联仍然存在。
>
>此外，Privacy Service只能处理 [!DNL Profile] 使用不执行身份拼合的合并策略的数据。 如果您使用UI确认是否正在处理隐私请求，请确保您使用的策略包含“[!DNL None]&quot;作为 [!UICONTROL ID拼合] 类型。 换句话说，您不能使用合并策略， [!UICONTROL ID拼合] 设置为&quot;[!UICONTROL 专用图]&quot;
>
>![合并策略的ID拼合设置为“无”](./images/privacy/no-id-stitch.png)

在未来版本中， [!DNL Platform] 将向发送确认函 [!DNL Privacy Service] 数据被物理删除后。

## 后续步骤

阅读本文档后，您便了解了 [!DNL Experience Platform]. 建议您继续阅读本指南中提供的文档，以加深对如何管理身份数据和创建隐私作业的了解。

有关处理的隐私请求的信息 [!DNL Platform] 未使用的资源 [!DNL Profile]，请参阅 [数据湖中的隐私请求处理](../catalog/privacy.md).
