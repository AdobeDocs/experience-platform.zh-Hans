---
keywords: Experience Platform；主页；热门主题；数据湖隐私；身份命名空间；隐私；数据湖
solution: Experience Platform
title: 数据湖中的隐私请求处理
topic-legacy: overview
description: Adobe Experience Platform Privacy Service会根据法律和组织隐私法规的规定处理客户访问、选择退出销售或删除其个人数据的请求。 本文档介绍与处理存储在数据湖中的客户数据的隐私请求相关的基本概念。
exl-id: c06b0a44-be1a-4938-9c3e-f5491a3dfc19
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 1%

---

# 中的隐私请求处理 [!DNL Data Lake]

Adobe Experience Platform [!DNL Privacy Service] 处理客户访问、选择退出销售或删除其个人数据的请求，这些请求符合法律和组织隐私法规的规定。

本文档介绍与处理存储在 [!DNL Data Lake].

>[!NOTE]
>
>本指南仅介绍如何在Experience Platform中对数据湖发出隐私请求。 如果您还计划为实时客户资料数据存储提出隐私请求，请参阅 [配置文件的隐私请求处理](../profile/privacy.md) 除了本教程之外，
>
>有关如何为其他Adobe Experience Cloud应用程序发出隐私请求的步骤，请参阅 [Privacy Service文档](../privacy-service/experience-cloud-apps.md).

## 快速入门

建议您对以下方面有一定的了解 [!DNL Experience Platform] 服务：

* [[!DNL Privacy Service]](../privacy-service/home.md):管理客户在Adobe Experience Cloud应用程序中访问、选择退出销售或删除其个人数据的请求。
* [[!DNL Catalog Service]](home.md):数据位置和谱系的记录系统 [!DNL Experience Platform]. 提供可用于更新数据集元数据的API。
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
* [[!DNL Identity Service]](../identity-service/home.md):通过跨设备和系统桥接身份，解决客户体验数据碎片化所带来的根本难题。

## 了解身份命名空间 {#namespaces}

Adobe Experience Platform [!DNL Identity Service] 跨系统和设备连接客户身份数据。 [!DNL Identity Service] 使用身份命名空间，通过将身份值与其源系统相关联来提供与身份值相关的上下文。 命名空间可以表示一个通用概念，如电子邮件地址（“电子邮件”），或将标识与特定应用程序(如Adobe Advertising Cloud ID(“AdCloud”)或Adobe Target ID(“TNTID”))相关联。

[!DNL Identity Service] 维护全局定义（标准）和用户定义（自定义）身份命名空间的存储。 标准命名空间适用于所有组织（例如，“电子邮件”和“ECID”），而您的组织也可以创建自定义命名空间以满足其特定需求。

有关 [!DNL Experience Platform]，请参阅 [身份命名空间概述](../identity-service/namespaces.md).

## 向数据集添加身份数据

在为 [!DNL Data Lake]，必须为每个客户提供有效的标识值（及其关联的命名空间），以便找到其数据并进行相应处理。 因此，所有遵循隐私请求的数据集都必须在其关联的XDM架构中包含标识描述符。

>[!NOTE]
>
>当前不支持身份描述符元数据的任何基于架构的数据集（例如临时数据集）在隐私请求中无法处理。

本节将介绍如何向现有数据集的XDM架构添加身份描述符。 如果您已经有一个包含身份描述符的数据集，则可以跳到 [下一部分](#nested-maps).

>[!IMPORTANT]
>
>在决定要设置为标识的架构字段时，请记住 [使用嵌套映射类型字段的限制](#nested-maps).

向数据集架构添加标识描述符的方法有两种：

* [使用UI](#identity-ui)
* [使用 API](#identity-api)

### 使用UI {#identity-ui}

在 [!DNL Experience Platform ]用户界面， **[!UICONTROL 模式]** 工作区允许您编辑现有的XDM模式。 要向架构添加标识描述符，请从列表中选择架构，然后按照 [将架构字段设置为标识字段](../xdm/tutorials/create-schema-ui.md#identity-field) 在 [!DNL Schema Editor] 教程。

在架构中将相应字段设置为标识字段后，您可以转到 [提交隐私请求](#submit).

### 使用 API {#identity-api}

>[!NOTE]
>
>本节假定您知道数据集XDM架构的唯一URI ID值。 如果您不知道此值，可以使用 [!DNL Catalog Service] API。 阅读 [入门](./api/getting-started.md) ，请按照 [列表](./api/list-objects.md) 或 [查找](./api/look-up-object.md) [!DNL Catalog] 查找数据集的对象。 架构ID可在 `schemaRef.id`
>
>本节还假定您知道如何调用架构注册表API。 有关使用API的重要信息，包括了解您的 `{TENANT_ID}` 容器的概念，请参阅 [入门](../xdm/api/getting-started.md) 部分。

您可以通过向 `/descriptors` 的端点 [!DNL Schema Registry] API。

**API格式**

```http
POST /descriptors
```

**请求**

以下请求在示例架构的“email address”字段上定义标识描述符。

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
| `@type` | 正在创建的描述符的类型。 对于身份描述符，值必须为“xdm:descriptorIdentity”。 |
| `xdm:sourceSchema` | 数据集XDM架构的唯一URI ID。 |
| `xdm:sourceVersion` | 中指定的XDM架构版本 `xdm:sourceSchema`. |
| `xdm:sourceProperty` | 描述符所应用的架构字段的路径。 |
| `xdm:namespace` | 其中一个 [标准身份命名空间](../privacy-service/api/appendix.md#standard-namespaces) 确认 [!DNL Privacy Service]，或由您的组织定义的自定义命名空间。 |
| `xdm:property` | “xdm:id”或“xdm:code”，具体取决于 `xdm:namespace`. |
| `xdm:isPrimary` | 可选布尔值。 如果为true，则表示字段是主标识。 架构只能包含一个主标识。 如果未包含，则默认为false。 |

**响应**

成功的响应会返回HTTP状态201（已创建）以及新创建描述符的详细信息。

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
>本节介绍如何设置隐私请求的格式 [!DNL Data Lake]. 强烈建议您查看 [[!DNL Privacy Service] UI](../privacy-service/ui/overview.md) 或 [[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) 有关如何提交隐私作业的完整步骤文档，包括如何以请求负载正确设置已提交的用户身份数据的格式。

以下部分概述如何为 [!DNL Data Lake] 使用 [!DNL Privacy Service] UI或API。

>[!IMPORTANT]
>
>无法保证完成隐私请求所花费的时间。 如果在请求仍在处理期间数据湖中发生了更改，则也无法保证是否会处理这些记录。

### 使用UI

在UI中创建作业请求时，请务必选择 **[!UICONTROL AEP Data Lake]** 和/或 **[!UICONTROL 用户档案]** 在 **[!UICONTROL 产品]** 以便处理存储在 [!DNL Data Lake] 或 [!DNL Real-time Customer Profile]，分别为。

<img src="images/privacy/product-value.png" width="450"><br>

### 使用 API

在API中创建作业请求时，任何 `userIDs` 必须使用 `namespace` 和 `type` 具体取决于应用到的数据存储。 的ID [!DNL Data Lake] 必须使用 `unregistered` 为 `type` 值和 `namespace` 与其中一个匹配的值 [隐私标签](#privacy-labels) 已添加到适用数据集的数据集。

此外， `include` 请求有效负载的数组必须包含对请求进行的不同数据存储的产品值。 向 [!DNL Data Lake]，则数组必须包含值 `aepDataLake`.

以下请求会为 [!DNL Data Lake]，使用未注册的 `email_label` 命名空间。 它还包括 [!DNL Data Lake] 在 `include` 数组：

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
>平台处理所有 [沙箱](../sandboxes/home.md) 属于您的组织。 因此， `x-sandbox-name` 系统将忽略请求中包含的标头。

## 删除请求处理

When [!DNL Experience Platform] 从接收删除请求 [!DNL Privacy Service], [!DNL Platform] 向发送确认 [!DNL Privacy Service] 请求已收到且受影响的数据已标记为删除。 然后，将从 [!DNL Data Lake] 七天之内。 在这七天的时间范围内，数据会被软删除，因此任何用户都无法访问 [!DNL Platform] 服务。

在未来版本中， [!DNL Platform] 将向发送确认函 [!DNL Privacy Service] 数据被物理删除后。

## 后续步骤

通过阅读本文档，您了解了处理 [!DNL Data Lake]. 建议您继续阅读本指南中提供的文档，以加深对如何管理身份数据和创建隐私作业的了解。

请参阅 [实时客户资料的隐私请求处理](../profile/privacy.md) 有关处理隐私请求的步骤，请参阅 [!DNL Profile] 存储。

## 附录

以下部分包含有关在 [!DNL Data Lake].

### 标记嵌套的映射类型字段 {#nested-maps}

请务必注意，有两种嵌套的映射类型字段不支持隐私标签设置：

* 数组类型字段中的映射类型字段
* 另一个映射类型字段中的映射类型字段

以上两个示例中任何一个的隐私作业处理最终都将失败。 因此，建议您避免使用嵌套的映射类型字段存储专用客户数据。 相关消费者ID应作为非映射数据类型存储在 `identityMap` 字段（本身是映射类型字段），用于基于记录的数据集，或 `endUserID` 字段。
