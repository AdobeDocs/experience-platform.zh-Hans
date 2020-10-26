---
keywords: Experience Platform;home;popular topics;data lake privacy;identity namespaces;privacy;data lake
solution: Experience Platform
title: 数据湖中的隐私请求处理
topic: overview
description: Adobe Experience Platform Privacy Service处理客户访问、选择退出出售或删除其法律和组织隐私法规规定的个人数据的请求。 此文档涵盖与处理存储在数据湖中的客户数据的隐私请求相关的基本概念。
translation-type: tm+mt
source-git-commit: 066337419431db24bde0a8d0d30b85132d08f43c
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 0%

---


# 在 [!DNL Data Lake]

Adobe Experience Platform [!DNL Privacy Service] 处理客户访问、选择退出出售或删除其法律和组织隐私法规规定的个人数据的请求。

此文档涵盖与处理存储在中的客户数据的隐私请求相关的基本概念 [!DNL Data Lake]。

## 入门指南

在阅读本指南之前，建议您对以下服 [!DNL Experience Platform] 务有一定的了解：

* [[!DNL Privacy Service]](../privacy-service/home.md):管理跨Adobe Experience Cloud应用程序访问、选择退出销售或删除其个人数据的客户请求。
* [[!DNL Catalog Service]](home.md):数据位置和谱系的记录系统 [!DNL Experience Platform]。 提供可用于更新数据集元数据的API。
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
* [[!DNL Identity Service]](../identity-service/home.md):通过跨设备和系统桥接身份，解决客户体验数据碎片化带来的根本挑战。

## 了解身份命名空间 {#namespaces}

Adobe Experience Platform [!DNL Identity Service] 将跨系统和设备的客户身份数据建立桥梁。 [!DNL Identity Service] 使用身份命名空间将身份值与其来源系统关联，从而提供与身份值相关的上下文。 命名空间可以表示一个通用概念，如电子邮件地址（“电子邮件”），或将标识与特定应用程序(如Adobe Advertising CloudID(“AdCloud”)或Adobe TargetID(“TNTID”))关联。

[!DNL Identity Service] 维护全局定义（标准）和用户定义（自定义）标识命名空间的存储。 标准命名空间适用于所有组织（例如，“电子邮件”和“ECID”），而您的组织也可以创建自定义命名空间以满足其特定需求。

有关中的标识命名空间的详 [!DNL Experience Platform]细信息，请参 [阅标识命名空间概述](../identity-service/namespaces.md)。

## 向数据集添加标识数据

在创建隐私请求时，必 [!DNL Data Lake]须为每位客户提供有效的身份值(及其关联命名空间)，以便找到其数据并相应地处理它们。 因此，所有受隐私请求约束的数据集都必须在其关联的XDM模式中包含标识描述符。

>[!NOTE]
>
>当前无法在隐私请求中处理任何基于不支持身份描述符元数据的模式集（如临时数据集）。

本节将逐步介绍向现有数据集的XDM模式添加标识描述符的步骤。 如果已有带有标识描述符的数据集，可跳到下一 [节](#nested-maps)。

>[!IMPORTANT]
>
>在确定要设置为标识的模式字段时，请记 [住使用嵌套映射类型字段的限制](#nested-maps)。

有两种方法可将标识描述符添加到数据集模式:

* [使用UI](#identity-ui)
* [使用API](#identity-api)

### 使用UI {#identity-ui}

在用 [!DNL Experience Platform ]户界面中， **[!UICONTROL 模式工]** 作区允许您编辑现有XDM模式。 要向模式添加标识描述符，请从列表中选择模式，然后按照教程中 [将模式字段设置为标识字段](../xdm/tutorials/create-schema-ui.md#identity-field) 的步 [!DNL Schema Editor] 骤操作。

在将模式中的相应字段设置为标识字段后，您可以继续执行下一节提交隐 [私请求](#submit)。

### 使用API {#identity-api}

>[!NOTE]
>
>本节假定您知道数据集的XDM模式的唯一URI ID值。 如果您不知道此值，可以使用API检索 [!DNL Catalog Service] 它。 阅读开发人 [员指南](./api/getting-started.md) 的入门部分后，请按照中概述的步骤 [列出](./api/list-objects.md) 或查 [找对象以找到](./api/look-up-object.md)[!DNL Catalog] 您的数据集。 模式ID可在 `schemaRef.id`
>
> 此部分包括对模式注册表API的调用。 有关使用API的重要信息(包括了解您 `{TENANT_ID}` 和容器概念)，请参 [阅开发人员](../xdm/api/getting-started.md) 指南的入门部分。

您可以通过向API中的端点发出模式请求，将标识描述符添加 `/descriptors` 到数据集的XDM [!DNL Schema Registry] POST。

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
| `xdm:namespace` | 可识别 [的标准身份命名空间](../privacy-service/api/appendix.md#standard-namespaces) , [!DNL Privacy Service]或组织定义的自定义命名空间。 |
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

>[!NOTE]
>
>本节介绍如何设置隐私请求的格式 [!DNL Data Lake]。 强烈建议您查看UI [[!DNL Privacy Service] 或API](../privacy-service/ui/overview.md) 文 [[!DNL Privacy Service] ](../privacy-service/api/getting-started.md) 档，了解如何提交隐私作业的完整步骤，包括如何在请求负载中正确设置提交的用户身份数据的格式。

以下部分概述了如何使用UI或API [!DNL Data Lake] 提 [!DNL Privacy Service] 出隐私请求。

>[!IMPORTANT]
>
>无法保证完成隐私请求所花费的时间。 如果在请求仍在处理时数据湖中发生更改，则也无法保证是否处理了这些记录。

### 使用UI

在UI中创建作业请求时，请务必在“产 **[!UICONTROL 品”下选]** 择AEP **[!UICONTROL Data Lake和／或]** 用户档案 **[!UICONTROL ，以便分别]** 处理存储在或中的 [!DNL Data Lake][!DNL Real-time Customer Profile]数据的作业。

<img src="images/privacy/product-value.png" width="450"><br>

### 使用API

在API中创建作业请求时，提 `userIDs` 供的任何作业请求都必须使用特 `namespace` 定 `type` 的，具体取决于它们所应用的数据存储。 ID的值 [!DNL Data Lake] 必须使用“未注册” `type` 作为值，并且值 `namespace` 与已添加到适用数据集 [的隐私标签](#privacy-labels) 之一匹配。

此外，请求 `include` 有效负荷的数组必须包含请求所针对的不同数据存储的产品值。 向阵列发出请 [!DNL Data Lake]求时，阵列必须包含该值 `aepDataLake`。

以下请求使用未注册的“email_label” [!DNL Data Lake]命名空间为用户创建新的隐私作业。 它还包括阵列中的 [!DNL Data Lake] 产品 `include` 值：

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

当 [!DNL Experience Platform] 收到来自的删除请 [!DNL Privacy Service]求 [!DNL Platform] 时，会发送确认， [!DNL Privacy Service] 确认该请求已接收且受影响的数据已标记为删除。 然后在七天内将记录 [!DNL Data Lake] 从中删除。 在这七天的窗口期内，数据会被软删除，因此任何服务都无法访问 [!DNL Platform] 它。

在以后的版本中， [!DNL Platform] 将在实际删除 [!DNL Privacy Service] 数据后向其发送确认信息。

## 后续步骤

通过阅读此文档，您了解了处理隐私请求的重要概念 [!DNL Data Lake]。 建议您继续阅读本指南中提供的文档，以加深您对如何管理身份数据和创建隐私工作的理解。

有关处理商店 [隐私请求的步骤](../profile/privacy.md) ，请参阅实时客户隐私请求处理文档 [!DNL Profile] 用户档案。

## 附录

以下部分包含有关处理隐私请求的其他信息，请参阅 [!DNL Data Lake]。

### 标记嵌套的映射类型字段 {#nested-maps}

请务必注意，有两种嵌套的映射类型字段不支持隐私标签：

* 数组类型字段中的映射类型字段
* 另一个映射类型字段中的映射类型字段

上述两个示例中的任何一个的隐私作业处理最终都将失败。 因此，建议您避免使用嵌套的映射类型字段存储私人客户数据。 对于基于记录的数据集，相关的消费者ID应 `identityMap` 作为字段（本身是映射类型字段）或基于时间序列的数据集 `endUserID` 的字段内的非映射数据类型存储。