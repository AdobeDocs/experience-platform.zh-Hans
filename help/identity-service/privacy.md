---
keywords: Experience Platform；主页；热门主题
title: Identity Service中的隐私请求处理
description: Adobe Experience Platform Privacy Service会按照许多隐私法规的规定处理客户访问、选择退出销售或删除其个人数据的请求。 本文档介绍与处理Identity Service的隐私请求相关的基本概念。
exl-id: ab84450b-1a4b-4fdd-b77d-508c86bbb073
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 0%

---

# 中的隐私请求处理 [!DNL Identity Service]

Adobe Experience Platform [!DNL Privacy Service] 处理客户访问、选择退出销售或删除其个人数据的请求(如《通用数据保护条例》(GDPR)等隐私法规中所述)，并 [!DNL California Consumer Privacy Act] (CCPA)。

本文档介绍与处理 [!DNL Identity Service] 在Adobe Experience Platform。

>[!NOTE]
>
>本指南仅介绍如何在Experience Platform中对身份数据存储进行隐私请求。 如果您还计划对Platform数据湖或 [!DNL Real-Time Customer Profile]，请参阅 [数据湖中的隐私请求处理](../catalog/privacy.md) 和 [配置文件的隐私请求处理](../profile/privacy.md) 除了本教程之外，
>
>有关如何为其他Adobe Experience Cloud应用程序发出隐私请求的步骤，请参阅 [Privacy Service文档](../privacy-service/experience-cloud-apps.md).

## 快速入门

建议您对以下方面有一定的了解 [!DNL Experience Platform] 服务：

* [[!DNL Privacy Service]](../privacy-service/home.md):管理客户在Adobe Experience Cloud应用程序中访问、选择退出销售或删除其个人数据的请求。
* [[!DNL Identity Service]](../identity-service/home.md):通过跨设备和系统桥接身份，解决客户体验数据碎片化所带来的根本难题。
* [[!DNL Real-Time Customer Profile]](home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

## 了解身份命名空间 {#namespaces}

Adobe Experience Platform [!DNL Identity Service] 跨系统和设备连接客户身份数据。 [!DNL Identity Service] 使用 **身份命名空间** 通过将身份值与其原籍系统联系起来，提供身份值的上下文。 命名空间可以表示一个通用概念，如电子邮件地址（“电子邮件”），或将标识与特定应用程序(如Adobe Advertising Cloud ID(“AdCloud”)或Adobe Target ID(“TNTID”))相关联。

Identity Service维护全局定义（标准）和用户定义（自定义）身份命名空间的存储区。 标准命名空间适用于所有组织（例如，“电子邮件”和“ECID”），而您的组织也可以创建自定义命名空间以满足其特定需求。

有关 [!DNL Experience Platform]，请参阅 [身份命名空间概述](../identity-service/namespaces.md).

## 提交请求 {#submit}

以下各节将简要介绍如何对 [!DNL Identity Service] 使用 [!DNL Privacy Service] API或UI。 在阅读这些部分之前，强烈建议您查看 [Privacy ServiceAPI](../privacy-service/api/getting-started.md) 或 [Privacy ServiceUI](../privacy-service/ui/overview.md) 有关如何提交隐私作业的完整步骤文档，包括如何以请求负载正确设置用户数据格式。

### 使用 API

在API中创建作业请求时， `userIDs` 必须使用特定 `namespace` 和 `type`. 有效 [标识命名空间](#namespaces) 确认 [!DNL Identity Service] 必须为 `namespace` 值，而 `type` 必须为 `standard` 或 `unregistered` （分别用于标准和自定义命名空间）。

此外， `include` 请求有效负载的数组必须包含对请求进行的不同数据存储的产品值。 在向 [!DNL Identity]，则数组必须包含值 `Identity`.

以下请求会根据GDPR为 [!DNL Identity] 存储。 在 `userIDs` 数组；使用标准 `Email` 标识命名空间，而另一个使用 `ECID` 命名空间中，它还包含 [!DNL Identity] (`Identity`) `include` 数组：

>[!TIP]
>
>使用API删除自定义命名空间时，必须将身份符号指定为命名空间，而不是显示名称。

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
>使用UI删除自定义命名空间时，必须将身份符号指定为命名空间，而不是显示名称。 此外，您无法在非生产沙箱的UI中删除自定义命名空间。

在UI中创建作业请求时，请务必选择 **[!UICONTROL 身份]** 在 **[!UICONTROL 产品]** 以便处理存储在 [!DNL Identity Service].

![identity-gdpr](./images/identity-gdpr.png)

## 删除请求处理

When [!DNL Experience Platform] 从接收删除请求 [!DNL Privacy Service], [!DNL Platform] 向发送确认 [!DNL Privacy Service] 请求已收到且受影响的数据已标记为删除。 单个身份的删除基于提供的命名空间和/或ID值。 此外，与给定IMS组织关联的所有沙箱都会被删除。

根据您是否还包含实时客户资料(`ProfileService`)和数据湖(`aepDataLake`)作为您的Identity Service隐私请求中的产品(`identity`)，则会在可能不同的时间从系统中删除与身份相关的不同数据集：

| 包含的产品 | 效果 |
| --- | --- |
| `identity` 仅 | 一旦平台发送确认消息，确认已收到删除请求，则与提供的身份关联的身份图会立即删除。 使用该身份图构建的用户档案仍将保留，但由于现在删除了身份关联，因此在摄取新数据时不会更新。 与用户档案关联的数据也会保留在数据湖中。 |
| `identity` 和 `ProfileService` | 一旦Platform发送确认消息，确认已收到删除请求，则会立即删除身份图及其关联配置文件。 与用户档案关联的数据将保留在数据湖中。 |
| `identity` 和 `aepDataLake` | 一旦平台发送确认消息，确认已收到删除请求，则与提供的身份关联的身份图会立即删除。 使用该身份图构建的用户档案仍将保留，但由于现在删除了身份关联，因此在摄取新数据时不会更新。<br><br>当数据湖产品响应收到请求且当前正在处理时，与用户档案关联的数据将被软删除，因此任何用户都无法访问 [!DNL Platform] 服务。 作业完成后，数据将完全从数据湖中删除。 |
| `identity`, `ProfileService`, 和 `aepDataLake` | 一旦Platform发送确认消息，确认已收到删除请求，则会立即删除身份图及其关联配置文件。<br><br>当数据湖产品响应收到请求且当前正在处理时，与用户档案关联的数据将被软删除，因此任何用户都无法访问 [!DNL Platform] 服务。 作业完成后，数据将完全从数据湖中删除。 |

请参阅 [[!DNL Privacy Service] 文档](../privacy-service/home.md#monitor) 以了解有关跟踪作业状态的更多信息。

## 后续步骤

阅读本文档后，您便了解了 [!DNL Identity Service]. 有关处理其他隐私请求的信息 [!DNL Experience Cloud] 应用程序，请参阅 [[!DNL Privacy Service] and [!DNL Experience Cloud] 应用程序](../privacy-service/experience-cloud-apps.md).
