---
keywords: Experience Platform；首页；热门话题
title: Identity Service中的隐私请求处理
description: Adobe Experience Platform Privacy Service会处理客户访问、选择退出销售或删除其个人数据的请求，如大量隐私法规所述。 本文档介绍了与处理Identity Service的隐私请求相关的基本概念。
exl-id: ab84450b-1a4b-4fdd-b77d-508c86bbb073
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 1%

---

# 在[!DNL Identity Service]中处理隐私请求

Adobe Experience Platform [!DNL Privacy Service]处理客户访问、选择退出销售或删除其个人数据的请求，这些请求由隐私法规(如《通用数据保护条例》(GDPR)和[!DNL California Consumer Privacy Act] (CCPA)规定。

本文档介绍了与在Adobe Experience Platform中处理[!DNL Identity Service]的隐私请求相关的基本概念。

>[!NOTE]
>
>本指南仅介绍如何在Experience Platform中对Identity数据存储区发出隐私请求。 如果您还计划提出Experience Platform数据湖或[!DNL Real-Time Customer Profile]的隐私请求，请参阅关于数据湖中[隐私请求处理的指南](../catalog/privacy.md)，以及本教程之外的关于配置文件[隐私请求处理](../profile/privacy.md)的指南。
>
>有关如何为其他Adobe Experience Cloud应用程序提出隐私请求的步骤，请参阅[Privacy Service文档](../privacy-service/experience-cloud-apps.md)。

## 快速入门

在阅读本指南之前，建议您实际了解以下[!DNL Experience Platform]服务：

* [[!DNL Privacy Service]](../privacy-service/home.md)：管理客户跨多个Adobe Experience Cloud应用程序访问、选择退出销售或删除其个人数据的请求。
* [[!DNL Identity Service]](../identity-service/home.md)：通过跨设备和系统桥接身份，解决了客户体验数据碎片化带来的基本挑战。
* [[!DNL Real-Time Customer Profile]](home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

## 了解身份标识命名空间 {#namespaces}

Adobe Experience Platform [!DNL Identity Service]跨系统和设备桥接客户身份数据。 [!DNL Identity Service]使用&#x200B;**身份命名空间**&#x200B;将身份值与其原始系统相关联，从而为其提供上下文。 命名空间可以表示通用概念，例如电子邮件地址（“电子邮件”），也可以将身份与特定应用程序关联，例如Adobe Advertising Cloud ID (“AdCloud”)或Adobe Target ID (“TNTID”)。

Identity Service维护全局定义（标准）和用户定义（自定义）身份命名空间的存储。 标准命名空间适用于所有组织（例如，“Email”和“ECID”），而您的组织也可以创建自定义命名空间以满足其特定需求。

有关[!DNL Experience Platform]中身份命名空间的更多信息，请参阅[身份命名空间概述](../identity-service/features/namespaces.md)。

## 提交请求 {#submit}

以下各节概述了如何使用[!DNL Privacy Service] API或UI为[!DNL Identity Service]提出隐私请求。 在阅读这些部分之前，强烈建议您查看[Privacy Service API](../privacy-service/api/getting-started.md)或[Privacy Service UI](../privacy-service/ui/overview.md)文档，以了解有关如何提交隐私作业的完整步骤，包括如何正确格式化请求负载中的用户数据。

### 使用 API

在API中创建作业请求时，`userIDs`中提供的任何ID都必须使用特定的`namespace`和`type`。 必须为`namespace`值提供[!DNL Identity Service]识别的有效[标识命名空间](#namespaces)，而`type`必须为`standard`或`unregistered`（分别用于标准命名空间和自定义命名空间）。

此外，请求有效负载的`include`数组必须包含请求所接收的不同数据存储的产品值。 向[!DNL Identity]发出请求时，数组必须包含值`Identity`。

以下请求根据GDPR为[!DNL Identity]存储中的单个客户数据创建新的隐私作业。 为`userIDs`数组中的客户提供了两个标识值；一个使用标准`Email`标识命名空间，另一个使用`ECID`命名空间，它还包含`include`数组中[!DNL Identity] (`Identity`)的产品值：

>[!TIP]
>
>在使用GDPR删除身份时，必须将身份符号指定为命名空间，而不是显示名称。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer <key>' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: acp_privacy_ui_gdpr' \
  -H 'x-gw-ims-org-id: sample@AdobeOrg' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "sample@AdobeOrg"
      }
    ],
    "users": [
      {
        "key": "bob",
        "action": ["delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "bob@adobe.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "123451234512345123451234512345",
            "isDeletedClientSide": false
          }
        ]
      }
    ],
    "include": ["Identity"],
    "regulation": "gdpr"
}'
```

### 使用UI

>[!TIP]
>
>在使用GDPR删除身份时，必须将身份符号指定为命名空间，而不是显示名称。

在UI中创建作业请求时，请确保选择&#x200B;**[!UICONTROL 产品]**&#x200B;下的&#x200B;**[!UICONTROL 标识]**，以便处理存储在[!DNL Identity Service]中的数据的作业。

![identity-gdpr](./images/identity-gdpr.png)

## 正在处理删除请求

当[!DNL Experience Platform]收到来自[!DNL Privacy Service]的删除请求时，[!DNL Experience Platform]向[!DNL Privacy Service]发送确认，确认已收到该请求并且受影响的数据已标记为删除。 个人身份的删除基于提供的命名空间和/或ID值。 此外，还会删除与给定组织关联的所有沙盒。

根据您是否还在Identity Service (`identity`)的隐私请求中包含了实时客户档案(`ProfileService`)和数据湖(`aepDataLake`)作为产品，与标识相关的不同数据集可能会在不同的时间从系统中删除：

| 包含的产品 | 效应 |
| --- | --- |
| 仅`identity` | 当Experience Platform发送确认消息确认已收到删除请求时，会立即删除提供的身份。 从该身份图构建的配置文件仍会保留，但不会由于接收到新数据而更新，因为身份关联现已移除。 与用户档案关联的数据也保留在数据湖中。 |
| `identity` 和 `ProfileService` | 当Experience Platform发送确认消息确认已收到删除请求时，会立即删除提供的身份。 与用户档案关联的数据将保留在数据湖中。 |
| `identity` 和 `aepDataLake` | 当Experience Platform发送确认消息确认已收到删除请求时，会立即删除提供的身份。 从该身份图构建的配置文件仍会保留，但不会由于接收到新数据而更新，因为身份关联现已移除。<br><br>当Data Lake产品回应收到请求且当前正在处理时，与配置文件关联的数据将被软删除，因此任何[!DNL Experience Platform]服务都无法访问。 作业完成后，数据将从数据湖中完全删除。 |
| `identity`、`ProfileService`和`aepDataLake` | 当Experience Platform发送确认消息确认已收到删除请求时，会立即删除提供的身份。<br><br>当Data Lake产品回应收到请求且当前正在处理时，与配置文件关联的数据将被软删除，因此任何[!DNL Experience Platform]服务都无法访问。 作业完成后，数据将从数据湖中完全删除。 |

有关跟踪作业状态的详细信息，请参阅[[!DNL Privacy Service] 文档](../privacy-service/home.md#monitor)。

## 后续步骤

通过阅读本文档，您已了解[!DNL Identity Service]中处理隐私请求涉及的重要概念。 有关处理其他[!DNL Experience Cloud]应用程序的隐私请求的信息，请参阅[[!DNL Privacy Service] 和 [!DNL Experience Cloud] 应用程序](../privacy-service/experience-cloud-apps.md)上的文档。
