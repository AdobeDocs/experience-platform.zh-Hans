---
keywords: Experience Platform；主页；热门主题；数据湖隐私；身份命名空间；隐私；数据湖
solution: Experience Platform
title: 数据湖中的隐私请求处理
topic: overview
description: Adobe Experience Platform Privacy Service处理客户访问、选择退出出售或删除其法律和组织隐私法规规定的个人数据的请求。 此文档涵盖与处理存储在数据湖中的客户数据的隐私请求相关的基本概念。
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '1285'
ht-degree: 0%

---


# 在[!DNL Data Lake]中处理隐私请求

Adobe Experience Platform[!DNL Privacy Service]处理客户访问、销选择退出售或删除其个人数据的请求，这些请求由法律和组织隐私法规规定。

此文档涵盖与处理存储在[!DNL Data Lake]中的客户数据的隐私请求相关的基本概念。

## 入门指南

在阅读本指南之前，建议您对以下[!DNL Experience Platform]服务有正确的了解：

* [[!DNL Privacy Service]](../privacy-service/home.md):管理跨Adobe Experience Cloud应用程序访问、选择退出销售或删除其个人数据的客户请求。
* [[!DNL Catalog Service]](home.md):数据位置和谱系的记录系统 [!DNL Experience Platform]。提供可用于更新数据集元数据的API。
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
* [[!DNL Identity Service]](../identity-service/home.md):通过跨设备和系统桥接身份，解决客户体验数据碎片化带来的根本挑战。

## 了解身份命名空间{#namespaces}

Adobe Experience Platform[!DNL Identity Service]跨系统和设备连接客户身份数据。 [!DNL Identity Service] 使用身份命名空间将身份值与其来源系统关联，从而提供与身份值相关的上下文。命名空间可以表示一个通用概念，如电子邮件地址（“电子邮件”），或将标识与特定应用程序(如Adobe Advertising CloudID(“AdCloud”)或Adobe TargetID(“TNTID”))关联。

[!DNL Identity Service] 维护全局定义（标准）和用户定义（自定义）标识命名空间的存储。标准命名空间适用于所有组织（例如，“电子邮件”和“ECID”），而您的组织也可以创建自定义命名空间以满足其特定需求。

有关[!DNL Experience Platform]中的标识命名空间的详细信息，请参阅[标识命名空间概述](../identity-service/namespaces.md)。

## 向数据集添加标识数据

为[!DNL Data Lake]创建隐私请求时，必须为每个客户提供有效身份值(及其关联命名空间)，以便找到其数据并相应地处理它们。 因此，所有受隐私请求约束的数据集都必须在其关联的XDM模式中包含标识描述符。

>[!NOTE]
>
>当前无法在隐私请求中处理任何基于不支持身份描述符元数据的模式集（如临时数据集）。

本节将逐步介绍向现有数据集的XDM模式添加标识描述符的步骤。 如果已有带有标识描述符的数据集，可跳到下一节[](#nested-maps)。

>[!IMPORTANT]
>
>在确定要设置为标识的模式字段时，请牢记使用嵌套映射类型字段](#nested-maps)的[限制。

有两种方法可将标识描述符添加到数据集模式:

* [使用UI](#identity-ui)
* [使用API](#identity-api)

### 使用UI {#identity-ui}

在[!DNL Experience Platform ]用户界面中，**[!UICONTROL 模式]**&#x200B;工作区允许您编辑现有XDM模式。 要向模式添加标识描述符，请从列表中选择该模式，然后按照[教程中将模式字段设置为标识字段](../xdm/tutorials/create-schema-ui.md#identity-field)的步骤操作。[!DNL Schema Editor]

在将模式中的相应字段设置为标识字段后，您可以继续执行有关[提交隐私请求](#submit)的下一节。

### 使用API {#identity-api}

>[!NOTE]
>
>本节假定您知道数据集的XDM模式的唯一URI ID值。 如果您不知道此值，可以使用[!DNL Catalog Service] API检索它。 在阅读开发人员指南的[getting started](./api/getting-started.md)部分后，按照[listing](./api/list-objects.md)或[查找](./api/look-up-object.md) [!DNL Catalog]对象中概述的步骤查找数据集。 模式ID位于`schemaRef.id`下
>
> 此部分包括对模式注册表API的调用。 有关使用API的重要信息(包括了解您的`{TENANT_ID}`和容器概念)，请参阅开发人员指南的[入门](../xdm/api/getting-started.md)部分。

可以通过向[!DNL Schema Registry] API中的`/descriptors`端点发出POST请求，将标识描述符添加到数据集的XDM模式。

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
| `xdm:sourceVersion` | `xdm:sourceSchema`中指定的XDM模式版本。 |
| `xdm:sourceProperty` | 模式符所应用的描述符字段的路径。 |
| `xdm:namespace` | 由[!DNL Privacy Service]识别的[标准标识命名空间](../privacy-service/api/appendix.md#standard-namespaces)或由您的组织定义的自定义命名空间。 |
| `xdm:property` | 根据`xdm:namespace`下使用的命名空间符，可选择“xdm:id”或“xdm:code”。 |
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

## 提交请求{#submit}

>[!NOTE]
>
>本节介绍如何设置[!DNL Data Lake]的隐私请求的格式。 强烈建议您查看[[!DNL Privacy Service] UI](../privacy-service/ui/overview.md)或[[!DNL Privacy Service] API](../privacy-service/api/getting-started.md)文档，了解有关如何提交隐私作业的完整步骤，包括如何在请求负载中正确设置提交的用户身份数据的格式。

以下部分概述了如何使用[!DNL Privacy Service] UI或API向[!DNL Data Lake]发出隐私请求。

>[!IMPORTANT]
>
>无法保证完成隐私请求所花费的时间。 如果在请求仍在处理时数据湖中发生更改，则也无法保证是否处理了这些记录。

### 使用UI

在UI中创建作业请求时，请务必在&#x200B;**[!UICONTROL 产品]**&#x200B;下选择&#x200B;**[!UICONTROL AEP用户档案湖]**&#x200B;和／或&#x200B;****，以分别处理存储在[!DNL Data Lake]或[!DNL Real-time Customer Profile]中的数据的作业。

<img src="images/privacy/product-value.png" width="450"><br>

### 使用API

在API中创建作业请求时，提供的任何`userIDs`必须使用特定的`namespace`和`type`，具体取决于它们所应用的数据存储。 [!DNL Data Lake]的ID必须对其`type`值使用“未注册”，并且`namespace`值与已添加到适用数据集的[隐私标签](#privacy-labels)中的一个匹配。

此外，请求有效负荷的`include`数组必须包含请求所针对的不同数据存储的产品值。 向[!DNL Data Lake]发出请求时，阵列必须包含值`aepDataLake`。

以下请求使用未注册的“email_label”命名空间为[!DNL Data Lake]创建新的隐私作业。 它还包括`include`阵列中[!DNL Data Lake]的产品值：

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

当[!DNL Experience Platform]收到来自[!DNL Privacy Service]的删除请求时，[!DNL Platform]会向[!DNL Privacy Service]发送确认，确认已收到该请求，且受影响的数据已被标记为删除。 然后，在七天内从[!DNL Data Lake]中删除记录。 在这七天的窗口期间，数据被软删除，因此任何[!DNL Platform]服务都无法访问。

在将来的版本中，[!DNL Platform]将在数据被物理删除后向[!DNL Privacy Service]发送确认信息。

## 后续步骤

通过阅读此文档，您了解了处理[!DNL Data Lake]隐私请求时涉及的重要概念。 建议您继续阅读本指南中提供的文档，以加深您对如何管理身份数据和创建隐私工作的理解。

有关处理[!DNL Profile]商店隐私请求的步骤，请参见[实时客户用户档案的隐私请求处理文档](../profile/privacy.md)。

## 附录

以下部分包含有关处理[!DNL Data Lake]中的隐私请求的其他信息。

### 标记嵌套映射类型字段{#nested-maps}

请务必注意，有两种嵌套的映射类型字段不支持隐私标签：

* 数组类型字段中的映射类型字段
* 另一个映射类型字段中的映射类型字段

上述两个示例中的任何一个的隐私作业处理最终都将失败。 因此，建议您避免使用嵌套的映射类型字段存储私人客户数据。 对于基于记录的数据集，相关的消费者ID应作为非映射数据类型存储在`identityMap`字段（本身是映射类型字段）中，对于基于时间序列的数据集，应作为`endUserID`字段存储。