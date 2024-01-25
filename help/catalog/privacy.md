---
keywords: Experience Platform；主页；热门主题；数据湖隐私；身份命名空间；隐私；数据湖
solution: Experience Platform
title: 数据湖中的隐私请求处理
description: Adobe Experience Platform Privacy Service会根据法律和组织隐私法规处理客户访问、选择退出销售或删除其个人数据的请求。 本文档介绍了与处理存储在数据湖中的客户数据的隐私请求相关的基本概念。
exl-id: c06b0a44-be1a-4938-9c3e-f5491a3dfc19
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1429'
ht-degree: 1%

---

# 数据湖中的隐私请求处理

Adobe Experience Platform [!DNL Privacy Service] 处理客户访问、选择退出销售或删除其个人数据的请求，如法律和组织隐私法规所述。

本文档介绍了与处理存储在数据湖中的客户数据的隐私请求相关的基本概念。

>[!NOTE]
>
>本指南仅介绍如何在Experience Platform中针对Data Lake发出隐私请求。 如果您还计划对Real-time Customer Profile数据存储提出隐私请求，请参阅以下指南： [个人资料的隐私请求处理](../profile/privacy.md) 以及本教程。
>
>有关如何为其他Adobe Experience Cloud应用程序提出隐私请求的步骤，请参阅 [Privacy Service文档](../privacy-service/experience-cloud-apps.md).

## 快速入门

建议您实际了解以下内容 [!DNL Experience Platform] 阅读本指南之前的服务：

* [[!DNL Privacy Service]](../privacy-service/home.md)：管理客户跨多个Adobe Experience Cloud应用程序访问、选择退出销售或删除其个人数据的请求。
* [[!DNL Catalog Service]](home.md)：记录系统中数据位置和族系的系统 [!DNL Experience Platform]. 提供可用于更新数据集元数据的API。
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
* [[!DNL Identity Service]](../identity-service/home.md)：通过跨设备和系统桥接身份，解决了客户体验数据碎片化带来的根本挑战。

## 了解标识命名空间 {#namespaces}

Adobe Experience Platform [!DNL Identity Service] 跨系统和设备桥接客户身份数据。 [!DNL Identity Service] 使用身份命名空间，通过将身份值与原始系统相关联，来为身份值提供上下文。 命名空间可以表示通用概念，例如电子邮件地址（“电子邮件”），也可以将身份与特定应用程序关联，例如Adobe Advertising Cloud ID (“AdCloud”)或Adobe Target ID (“TNTID”)。

[!DNL Identity Service] 维护全局定义（标准）和用户定义（自定义）身份命名空间的存储。 标准命名空间适用于所有组织（例如，“Email”和“ECID”），而您的组织也可以创建自定义命名空间以满足其特定需求。

有关中身份命名空间的更多信息 [!DNL Experience Platform]，请参见 [身份命名空间概述](../identity-service/features/namespaces.md).

## 向数据集添加身份数据

在为数据湖创建隐私请求时，必须为每位客户提供有效的身份值（及其关联的命名空间），以便找到其数据并相应地对其进行处理。 因此，所有服从隐私请求的数据集都必须在其关联的XDM架构中包含身份描述符。

>[!NOTE]
>
>任何基于不支持身份描述符元数据的架构的数据集（例如临时数据集）当前无法在隐私请求中处理。

本节介绍将身份描述符添加到现有数据集的XDM架构的步骤。 如果您已经有一个数据集具有身份描述符，则可以向前跳到 [下一节](#nested-maps).

>[!IMPORTANT]
>
>在决定要将哪些架构字段设置为身份时，请记住 [使用嵌套映射类型字段的限制](#nested-maps).

有两种方法可以将身份描述符添加到数据集架构：

* [使用UI](#identity-ui)
* [使用 API](#identity-api)

### 使用UI {#identity-ui}

在 [!DNL Experience Platform]用户界面， **[!UICONTROL 架构]** 工作区允许您编辑现有的XDM架构。 要向架构中添加身份描述符，请从列表中选择架构并按照以下步骤操作 [将架构字段设置为标识字段](../xdm/tutorials/create-schema-ui.md#identity-field) 在 [!DNL Schema Editor] 教程。

将架构中的相应字段设置为身份字段后，您可以转到以下内容的下一部分： [提交隐私请求](#submit).

### 使用 API {#identity-api}

>[!NOTE]
>
>本节假设您知道数据集XDM架构的唯一URI ID值。 如果您不知道此值，可以使用 [!DNL Catalog Service] API。 在阅读 [快速入门](./api/getting-started.md) 在开发人员指南的部分中，遵循中概述的步骤 [列表](./api/list-objects.md) 或 [查找](./api/look-up-object.md) [!DNL Catalog] 对象以查找数据集。 架构ID位于 `schemaRef.id`
>
>本节还假定您知道如何调用架构注册表API。 有关使用API的重要信息，包括了解 `{TENANT_ID}` 以及容器的概念，请参见 [快速入门](../xdm/api/getting-started.md) API指南的部分。

POST您可以通过对数据集的XDM架构添加标识描述符，方法是向 `/descriptors` 中的端点 [!DNL Schema Registry] API。

**API格式**

```http
POST /descriptors
```

**请求**

以下请求在示例架构中的“电子邮件地址”字段中定义标识描述符。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '
      {
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/personalEmail/address",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

| 属性 | 描述 |
| --- | --- |
| `@type` | 正在创建的描述符的类型。 对于身份描述符，该值必须为“xdm：descriptorIdentity”。 |
| `xdm:sourceSchema` | 数据集XDM架构的唯一URI ID。 |
| `xdm:sourceVersion` | 中指定的XDM架构的版本 `xdm:sourceSchema`. |
| `xdm:sourceProperty` | 描述符所应用到的架构字段的路径。 |
| `xdm:namespace` | 其中一项 [标准身份命名空间](../privacy-service/api/appendix.md#standard-namespaces) 识别者 [!DNL Privacy Service]，或由您的组织定义的自定义命名空间。 |
| `xdm:property` | “xdm：id”或“xdm：code”，具体取决于下使用的命名空间 `xdm:namespace`. |
| `xdm:isPrimary` | 可选的布尔值。 如果为true，则表示该字段是主标识。 架构只能包含一个主标识。 如果不包含，则默认为false。 |

**响应**

成功的响应返回HTTP状态201 （已创建）以及新创建的描述符的详细信息。

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## 提交请求 {#submit}

>[!NOTE]
>
>本节介绍如何设置Data Lake隐私请求的格式。 强烈建议您查阅 [[!DNL Privacy Service] UI](../privacy-service/ui/overview.md) 或 [[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) 有关如何提交隐私作业的完整步骤的文档，包括如何在请求负载中正确格式化提交的用户身份数据。

以下部分概述了如何使用对数据湖提出隐私请求 [!DNL Privacy Service] ui或API。

>[!IMPORTANT]
>
>无法保证隐私请求可能需要多长时间才能完成。 如果在请求仍在处理期间数据湖内发生更改，则无法保证这些记录是否也得到处理。

### 使用UI

在UI中创建作业请求时，请确保选择 **[!UICONTROL AEP数据湖]** 下 **[!UICONTROL 产品]** 以便处理存储在数据湖中的数据的作业。

![显示在隐私请求创建对话框中选择的Data Lake产品的图像](./images/privacy/product-value.png)

### 使用 API

在API中创建作业请求时，任何 `userIDs` 提供的必须使用特定的 `namespace` 和 `type` 取决于它们应用到的数据存储。 数据湖必须使用ID `unregistered` 为其 `type` 值和 `namespace` 与以下值之一匹配的值 [隐私标签](#privacy-labels) 添加到适用数据集的属性。

此外， `include` 请求有效负载的数组必须包含请求所针对的不同数据存储的产品值。 向数据湖发出请求时，数组必须包含值 `aepDataLake`.

以下请求使用未注册的数据湖创建新的隐私作业 `email_label` 命名空间。 它还包含中数据湖的产品值 `include` 数组：

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
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          },
          {
            "namespace": "email_label",
            "value": "jdoe@example.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

>[!IMPORTANT]
>
>Platform处理所有隐私请求 [沙盒](../sandboxes/home.md) 属于您的组织。 因此，任何 `x-sandbox-name` 请求中包含的标头将被系统忽略。

## 正在处理删除请求

时间 [!DNL Experience Platform] 接收来自的删除请求 [!DNL Privacy Service]， [!DNL Platform] 将确认发送至 [!DNL Privacy Service] 请求已收到，并且受影响的数据已标记为删除。 然后，这些记录会在七天内从数据湖中删除。 在这七天窗口内，数据将被软删除，因此任何用户都无法访问 [!DNL Platform] 服务。

如果您还包含 `ProfileService` 或 `identity` 在隐私请求中，会单独处理关联的数据。 请参阅以下部分 [删除配置文件请求处理](../profile/privacy.md#delete) 以了解更多信息。

## 后续步骤

通过阅读本文档，您已了解与处理Data Lake的隐私请求相关的重要概念。 建议您继续阅读本指南中提供的文档，以加深您对如何管理身份数据和创建隐私作业的了解。

查看文档 [实时客户个人资料的隐私请求处理](../profile/privacy.md) 以了解有关以下项的隐私请求的处理步骤： [!DNL Profile] 商店。

## 附录

以下部分包含有关在数据湖中处理隐私请求的其他信息。

### 为嵌套映射类型字段设置标签 {#nested-maps}

需要注意的是，有两种嵌套映射类型字段不支持隐私标签：

* 数组类型字段中的映射类型字段
* 另一个映射类型字段中的映射类型字段

上述两个示例的隐私作业处理最终都将失败。 因此，建议您避免使用嵌套的映射类型字段来存储专用客户数据。 相关使用者ID应作为非映射数据类型存储在中 `identityMap` 字段（本身为映射类型字段），或者 `endUserID` 基于时间序列的数据集的字段。
