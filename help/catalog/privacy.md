---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 数据湖中的隐私请求处理
topic: overview
translation-type: tm+mt
source-git-commit: d3584202554baf46aad174d671084751e6557bbc

---


# 数据湖中的隐私请求处理

Adobe Experience Platform隐私服务处理客户访问、选择退出出售或删除其法律和组织隐私法规规定的个人数据的请求。

此文档涵盖与处理存储在数据湖中的客户数据的隐私请求相关的基本概念。

## 入门指南

在阅读本指南之前，建议您对以下Experience Platform服务有一定的了解：

* [隐私服务](../privacy-service/home.md): 管理客户在Adobe Experience Cloud应用程序中访问、选择退出销售或删除其个人数据的请求。
* [目录服务](home.md): Experience Platform中数据位置和世系的记录系统。 提供可用于更新数据集元数据的API。
* [体验数据模型(XDM)系统](../xdm/home.md): Experience Platform组织客户体验数据的标准化框架。
* [身份服务](../identity-service/home.md): 通过跨设备和系统桥接身份，解决客户体验数据碎片化带来的根本挑战。

## 了解身份命名空间 {#namespaces}

Adobe Experience Platform Identity Service跨系统和设备连接客户身份数据。 身份服务 **使用身份命名空间** ，通过将身份值与其来源系统相关联来提供与身份值相关的上下文。 命名空间可以表示一个通用概念，如电子邮件地址（“电子邮件”），或将标识与特定应用程序(如Adobe Advertising Cloud ID(“AdCloud”)或Adobe目标ID(“TNTID”))关联。

Identity Service维护全局定义（标准）和用户定义（自定义）标识命名空间的存储。 标准命名空间适用于所有组织（例如，“电子邮件”和“ECID”），而您的组织也可以创建自定义命名空间以满足其特定需求。

有关Experience Platform中身份命名空间的更多信息，请参阅 [身份命名空间概述](../identity-service/namespaces.md)。

## 向数据集添加标识数据

创建数据湖的隐私请求时，必须为每个客户提供有效的身份值(及其关联命名空间)，以便找到其数据并相应地处理它们。 因此，所有受隐私请求约束的数据集都必须在其关联的 **XDM模式中** ，包含一个标识描述符。

>[!NOTE] 当前无法在隐私请求中处理任何基于不支持身份描述符元数据的模式集（如临时数据集）。

本节将逐步介绍向现有数据集的XDM模式添加标识描述符的步骤。 如果已有带有标识描述符的数据集，可跳到下一 [节](#nested-maps)。

>[!IMPORTANT] 在确定要设置为标识的模式字段时，请记 [住使用嵌套映射类型字段的限制](#nested-maps)。

有两种方法可将标识描述符添加到数据集模式:

* [使用UI](#identity-ui)
* [使用API](#identity-api)

### 使用UI {#identity-ui}

在Experience Platform用户界面中，您可 _[!UICONTROL Schemas]_以通过工作区编辑现有的XDM模式。 要向模式添加标识描述符，请从列表中选择模式，然后按照“模式编辑[器”教程中将模式字段设置为标识](../xdm/tutorials/create-schema-ui.md#identity-field)字段的步骤进行操作。

在将模式中的相应字段设置为标识字段后，您可以继续执行下一节提交隐 [私请求](#submit)。

### 使用API {#identity-api}

>[!NOTE] 本节假定您知道数据集的XDM模式的唯一URI ID值。 如果您不知道此值，可以使用Catalog Service API检索它。 阅读开发人 [员指南](./api/getting-started.md) 的入门部分后，请按照中概述的步骤列出或查 [找Catalog对象](./api/list-objects.md) , [](./api/look-up-object.md) 以找到您的数据集。 模式ID可在 `schemaRef.id`
>
> 此部分包括对模式注册表API的调用。 有关使用API的重要信息(包括了解您 `{TENANT_ID}` 和容器概念)，请参 [阅开发人员](../xdm/api/getting-started.md) 指南的入门部分。

可以通过向模式注册表API中的端点发出POST请求，将标识描述符添 `/descriptors` 加到数据集的XDM模式。

**API格式**

```http
POST /descriptors
```

**请求**

以下请求在示例模式的“电子邮件地址”字段上定义标识描述符。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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
| `@type` | 所创建描述符的类型。 对于标识描述符，该值必须为“xdm:descriptorIdentity”。 |
| `xdm:sourceSchema` | 数据集XDM模式的唯一URI ID。 |
| `xdm:sourceVersion` | 中指定的XDM模式版本 `xdm:sourceSchema`。 |
| `xdm:sourceProperty` | 模式符所应用的描述符字段的路径。 |
| `xdm:namespace` | 隐私服 [务可识别的标准身份命名空间](../privacy-service/api/appendix.md#standard-namespaces) 之一，或您的组织定义的自定义命名空间。 |
| `xdm:property` | “xdm:id”或“xdm:code”，具体取决于使用的命名空间 `xdm:namespace`。 |
| `xdm:isPrimary` | 可选布尔值。 如果为true，则表示字段是主标识。 模式只能包含一个主标识。 如果不包括，则默认为false。 |

**响应**

成功的响应返回HTTP状态201（已创建）和新创建描述符的详细信息。

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

>[!NOTE] 本节介绍如何格式化数据湖的隐私请求。 强烈建议您查看隐私服务 [UI](../privacy-service/ui/overview.md) 或 [](../privacy-service/api/getting-started.md) 隐私服务API文档，了解如何提交隐私作业的完整步骤，包括如何在请求负载中正确设置提交的用户身份数据的格式。

以下部分概述了如何使用隐私服务UI或API向数据湖发出隐私请求。

### 使用UI

在UI中创建作业请求时，请务必在 **产品下选择** AEP Data Lake和／或 **用户档案**__ ，以便分别处理存储在“数据湖”或“实时客户”用户档案中的数据的作业。

<img src="images/privacy/product-value.png" width="450"><br>

### 使用API

在API中创建作业请求时，提 `userIDs` 供的任何作业请求都必须使用特 `namespace` 定 `type` 的，具体取决于它们所应用的数据存储。 数据湖的ID必须使用“未注册”作为其 `type` 值，并且值 `namespace` 与已添加到适用数据集的 [隐私标签之一](#privacy-labels) 匹配。

此外，请求 `include` 有效负荷的数组必须包含请求所针对的不同数据存储的产品值。 向数据湖发出请求时，数组必须包含值“aepDataLake”。

以下请求使用未注册的“email_label”命名空间为数据湖创建新的隐私作业。 它还包括阵列中数据湖的产品 `include` 值：

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

## 删除请求处理

当Experience Platform从隐私服务收到删除请求时，平台会向隐私服务发送确认消息，确认该请求已收到且受影响的数据已标记为删除。 然后在七天内从数据湖中删除记录。 在这七天的时间内，数据会被软删除，因此任何平台服务都无法访问。

在将来的版本中，平台将在数据被物理删除后向隐私服务发送确认信息。

## 后续步骤

通过阅读此文档，您了解了处理数据湖隐私请求时涉及的重要概念。 建议您继续阅读本指南中提供的文档，以加深您对如何管理身份数据和创建隐私工作的理解。

有关处理文档 [商店隐私请求的步骤](../profile/privacy.md) ，请参阅实时用户档案的隐私请求处理用户档案。

## 附录

以下部分包含有关在数据湖中处理隐私请求的其他信息。

### 标记嵌套的映射类型字段 {#nested-maps}

请务必注意，有两种嵌套的映射类型字段不支持隐私标签：

* 数组类型字段中的映射类型字段
* 另一个映射类型字段中的映射类型字段

上述两个示例中的任何一个的隐私作业处理最终都将失败。 因此，建议您避免使用嵌套的映射类型字段存储私人客户数据。 对于基于记录的数据集，相关的消费者ID应 `identityMap` 作为字段（本身是映射类型字段）或基于时间序列的数据集 `endUserID` 的字段内的非映射数据类型存储。