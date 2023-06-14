---
keywords: Experience Platform；主页；热门主题
title: Identity Service中的隐私请求处理
description: Adobe Experience Platform Privacy Service会处理客户访问、选择退出销售或删除其个人数据的请求，如许多隐私法规所述。 本文档介绍了与处理Identity Service的隐私请求相关的基本概念。
exl-id: ab84450b-1a4b-4fdd-b77d-508c86bbb073
source-git-commit: 1930d235b57b59f9967f9f53c8c1faf25cea9051
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 0%

---

# 中的隐私请求处理 [!DNL Identity Service]

Adobe Experience Platform [!DNL Privacy Service] 处理客户访问、选择退出销售或删除其个人数据的请求，这些请求由隐私法规(例如《通用数据保护条例》(GDPR)和 [!DNL California Consumer Privacy Act] (CCPA)。

本文档介绍了与处理隐私请求相关的基本概念 [!DNL Identity Service] 在Adobe Experience Platform中。

>[!NOTE]
>
>本指南仅介绍如何在Experience Platform中对Identity数据存储区发出隐私请求。 如果您还计划向Platform Data Lake提出隐私请求，或者 [!DNL Real-Time Customer Profile]，请参阅指南，了解有关 [数据湖中的隐私请求处理](../catalog/privacy.md) 以及指南 [配置文件的隐私请求处理](../profile/privacy.md) 以及本教程。
>
>有关如何为其他Adobe Experience Cloud应用程序提出隐私请求的步骤，请参阅 [Privacy Service文档](../privacy-service/experience-cloud-apps.md).

## 快速入门

建议您实际了解以下内容 [!DNL Experience Platform] 在阅读本指南之前，请先参阅以下内容：

* [[!DNL Privacy Service]](../privacy-service/home.md)：管理客户跨Adobe Experience Cloud应用程序访问、选择退出销售或删除其个人数据的请求。
* [[!DNL Identity Service]](../identity-service/home.md)：通过跨设备和系统桥接身份，解决客户体验数据碎片化带来的根本挑战。
* [[!DNL Real-Time Customer Profile]](home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

## 了解身份命名空间 {#namespaces}

Adobe Experience Platform [!DNL Identity Service] 跨系统和设备桥接客户身份数据。 [!DNL Identity Service] 用途 **身份命名空间** 为标识值提供上下文，方法是将标识值与其来源系统相关联。 命名空间可以表示电子邮件地址（“电子邮件”）等通用概念，也可以将身份与特定应用程序相关联，例如Adobe Advertising Cloud ID (“AdCloud”)或Adobe Target ID (“TNTID”)。

Identity Service维护全局定义的（标准）和用户定义的（自定义）身份命名空间存储。 标准命名空间适用于所有组织（例如，“Email”和“ECID”），而您的组织也可以创建自定义命名空间以满足其特定需求。

有关中标识命名空间的更多信息 [!DNL Experience Platform]，请参见 [身份命名空间概述](../identity-service/namespaces.md).

## 提交请求 {#submit}

以下各节概述了如何针对以下对象提出隐私请求 [!DNL Identity Service] 使用 [!DNL Privacy Service] API或用户界面。 在阅读这些部分之前，强烈建议您查看 [PRIVACY SERVICEAPI](../privacy-service/api/getting-started.md) 或 [PRIVACY SERVICEUI](../privacy-service/ui/overview.md) 有关如何提交隐私作业的完整步骤（包括如何正确格式化请求负载中的用户数据）的文档。

### 使用 API

在API中创建作业请求时，中提供的任何ID `userIDs` 必须使用特定 `namespace` 和 `type`. 有效 [身份命名空间](#namespaces) 识别者 [!DNL Identity Service] 必须提供 `namespace` 值，而 `type` 必须是 `standard` 或 `unregistered` （分别用于标准和自定义命名空间）。

此外， `include` 请求有效负载的数组必须包含请求所针对的不同数据存储的产品值。 向发出请求时 [!DNL Identity]，数组必须包含值 `Identity`.

以下请求根据GDPR为中的单个客户数据创建新的隐私作业 [!DNL Identity] 商店。 在以下位置为客户提供了两个标识值： `userIDs` 数组；一个使用标准 `Email` 身份命名空间，而另一个使用 `ECID` 命名空间，它还包含的产品价值 [!DNL Identity] (`Identity`)中 `include` 数组：

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
>使用UI删除自定义命名空间时，必须将身份符号指定为命名空间，而不是显示名称。 此外，您无法删除非生产沙盒的UI中的自定义命名空间。

在UI中创建作业请求时，请确保选择 **[!UICONTROL 身份]** 下 **[!UICONTROL 产品]** 以便处理存储在中的数据的作业 [!DNL Identity Service].

![identity-gdpr](./images/identity-gdpr.png)

## 正在处理删除请求

时间 [!DNL Experience Platform] 接收来自的删除请求 [!DNL Privacy Service]， [!DNL Platform] 将确认发送至 [!DNL Privacy Service] 请求已收到，且受影响的数据已标记为删除。 个人身份的删除基于提供的命名空间和/或ID值。 此外，还会删除与给定组织关联的所有沙盒。

根据您是否还包含实时客户资料(`ProfileService`)和数据湖(`aepDataLake`)作为产品添加到Identity Service隐私请求中(`identity`)，则与身份相关的不同数据集将在不同的时间从系统中删除：

| 包含的产品 | 效果 |
| --- | --- |
| `identity` 仅限 | 当Platform发送确认消息确认已收到删除请求时，会立即删除提供的身份。 从该身份图构建的配置文件仍会保留，但不会由于摄取新数据而更新，因为身份关联现已移除。 与用户档案关联的数据也保留在数据湖中。 |
| `identity` 和 `ProfileService` | 当Platform发送确认消息确认已收到删除请求时，会立即删除提供的身份。 与配置文件关联的数据将保留在数据湖中。 |
| `identity` 和 `aepDataLake` | 当Platform发送确认消息确认已收到删除请求时，会立即删除提供的身份。 从该身份图构建的配置文件仍会保留，但不会由于摄取新数据而更新，因为身份关联现已移除。<br><br>当Data Lake产品响应请求已收到且当前正在处理时，与用户档案关联的数据将被软删除，因此任何用户都无法访问 [!DNL Platform] 服务。 作业完成后，数据将从数据湖中完全删除。 |
| `identity`, `ProfileService`, 和 `aepDataLake` | 当Platform发送确认消息确认已收到删除请求时，会立即删除提供的身份。<br><br>当Data Lake产品响应请求已收到且当前正在处理时，与用户档案关联的数据将被软删除，因此任何用户都无法访问 [!DNL Platform] 服务。 作业完成后，数据将从数据湖中完全删除。 |

请参阅 [[!DNL Privacy Service] 文档](../privacy-service/home.md#monitor) 以了解有关跟踪作业状态的更多信息。

## 后续步骤

通过阅读本文档，您已经了解中处理隐私请求涉及的重要概念。 [!DNL Identity Service]. 有关处理其他隐私请求的信息 [!DNL Experience Cloud] 应用程序，请参阅文档： [[!DNL Privacy Service] and [!DNL Experience Cloud] 应用程序](../privacy-service/experience-cloud-apps.md).
