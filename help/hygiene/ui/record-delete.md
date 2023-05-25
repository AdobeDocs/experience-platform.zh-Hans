---
title: 删除记录
description: 了解如何在Adobe Experience Platform UI中删除记录。
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
hide: true
hidefromtoc: true
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 10%

---

# 删除记录

此 [[!UICONTROL 数据卫生] 工作区](./overview.md) 在Adobe Experience Platform UI中，您可以删除参与Identity Service和Real-Time Customer Profile的记录。 这些记录可以绑定到个人消费者或身份图中包含的任何其他实体。

>[!IMPORTANT]
>
>记录删除请求仅适用于已购买的组织 **AdobeHealth Shield**.
>
>
>记录删除旨在用于数据清理、匿名数据删除或数据最小化。 它们是 **非** 用于数据主体权利请求（合规性），与通用数据保护条例(GDPR)等隐私法规相关。 对于所有合规性用例，使用 [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) 而是。

## 先决条件

删除记录需要深入了解身份字段在Experience Platform中的工作原理。 具体而言，您必须知道要删除其记录的实体的主要标识值，具体取决于从中删除这些记录的数据集（或数据集）。

有关Platform中标识的更多信息，请参阅以下文档：

* [Adobe Experience Platform Identity服务](../../identity-service/home.md)：跨设备和系统桥接身份，根据数据集符合的XDM架构定义的身份字段将数据集链接在一起。
   * [身份命名空间](../../identity-service/namespaces.md)：身份命名空间定义了可与单个人员相关的不同类型的身份信息，并且是每个身份字段的必需组件。
* [Real-time Customer Profile](../../profile/home.md)：利用身份图根据来自多个来源的汇总数据提供统一的用户配置文件，近乎实时更新。
* [体验数据模型(XDM)](../../xdm/home.md)：通过使用架构提供Platform数据的标准定义和结构。 所有Platform数据集都符合特定的XDM架构，该架构定义哪些字段是标识。
   * [标识字段](../../xdm/ui/fields/identity.md)：了解如何在XDM架构中定义标识字段。

## 创建新请求

要启动流程，请选择 **[!UICONTROL 创建请求]** 从工作区的主页中。

![图像显示 [!UICONTROL 创建请求] 正在选择按钮](../images/ui/record-delete/create-request-button.png)

此时将显示请求创建对话框。 默认情况下， **[!UICONTROL 删除消费者]** 选项已选中 **[!UICONTROL 请求的操作]** 部分。 保持选中此选项。

![此图像显示在创建对话框中选择的删除使用者选项](../images/ui/record-delete/consumer-action.png)

## 选择数据集

在 **[!UICONTROL 使用者详细信息]** 章节，下一步是确定要从单个数据集还是所有数据集中删除记录。

如果您选择 **[!UICONTROL 选择数据集]**，选择数据库图标(![数据库图标的图像](../images/ui/record-delete/database-icon.png))并出现一个对话框，允许您从列表中选择所需的数据集。

![显示数据集选择对话框的图像](../images/ui/record-delete/select-dataset.png)

如果要删除所有数据集的记录，请选择 **[!UICONTROL 所有数据集]**.

![图像显示 [!UICONTROL 所有数据集] 已选择选项](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
>选择 **[!UICONTROL 所有数据集]** 选项可能会导致删除操作花费更长时间，并且可能不会导致准确的记录删除。

## 提供身份 {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="主要标识"
>abstract="主要标识是一个用于将记录与 Experience Platform 中的消费者配置文件相关联的属性。数据集的主要标识字段由数据集所基于的架构定义。在此列中，您必须为记录的主要标识提供类型（或命名空间），例如 `email`（对于电子邮件地址）和 `ecid`（对于 Experience Cloud ID）。要了解更多信息，请参阅《数据卫生 UI 指南》。"

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="标识值"
>abstract="在此列中，您必须提供记录的主要标识的值，该值必须与左列中提供的标识类型相对应。如果主要标识类型是 `email`，则值应是记录的电子邮件地址。要了解更多信息，请参阅《数据卫生 UI 指南》。"

删除记录时，必须提供身份信息，以便系统能够确定哪些记录必须删除。 对于Platform中的任何数据集，记录会根据以下规则删除： **主要身份** 由数据集的架构定义的字段。

与Platform中的所有标识字段一样，主标识由两部分组成： **type** （有时称为身份命名空间）和 **值**. 身份类型提供有关字段如何标识记录的上下文（如电子邮件地址），该值表示该类型记录的特定身份(例如， `jdoe@example.com` 对于 `email` 标识类型)。 用作标识的常见字段包括帐户信息、设备ID和Cookie ID。

>[!TIP]
>
>如果您不知道特定数据集的主要标识，则可以在Platform UI中找到它。 在 **[!UICONTROL 数据集]** 在工作区中，从列表中选择有问题的数据集。 在数据集的详细信息页面上，将鼠标悬停在右边栏中数据集架构的名称上。 主标识与架构名称和描述一起显示。
>
>![该图像显示UI中高亮显示的数据集的主要身份](../images/ui/record-delete/dataset-primary-identity.png)

如果要从单个数据集删除记录，则提供的所有标识必须具有相同的类型，因为一个数据集只能有一个主标识。 如果要从所有数据集中删除，则可以包含多个标识类型，因为不同的数据集可能具有不同的主标识。

删除记录时，提供身份有两个选项：

* [上传JSON文件](#upload-json)
* [手动输入身份值](#manual-identity)

### 上传JSON文件 {#upload-json}

要上传JSON文件，您可以将该文件拖放到提供区域，或选择 **[!UICONTROL 选择文件]** 浏览并从本地目录中选择。

![该图像显示了在UI中上传JSON的方法](../images/ui/record-delete/upload-json.png)

JSON文件必须格式化为一组对象，每个对象表示一个标识。

```json
[
  {
    "namespaceCode": "email",
    "value": "jdoe@example.com"
  },
  {
    "namespaceCode": "email",
    "value": "san.gray@example.com"
  }
]
```

| 属性 | 描述 |
| --- | --- |
| `namespaceCode` | 身份类型。 |
| `value` | 类型表示的标识值。 |

上传文件后，您可以继续 [提交请求](#submit).

### 手动输入身份 {#manual-identity}

要手动输入身份，请选择 **[!UICONTROL 添加身份]**.

![图像显示 [!UICONTROL 添加身份] 正在选择按钮](../images/ui/record-delete/add-identity.png)

显示的控件允许您一次输入一个标识。 下 **[!UICONTROL 主要身份]**，使用下拉菜单选择身份类型。 下 **[!UICONTROL 标识值]**，为记录提供主要标识值。

![显示手动添加的标识字段的图像](../images/ui/record-delete/identity-added.png)

要添加更多身份，请选择加号图标(![加号图标的图像](../images/ui/record-delete/plus-icon.png))或选择 **[!UICONTROL 添加身份]**.

![显示如何向请求添加更多标识的图像](../images/ui/record-delete/more-identities.png)

## 提交请求(#submit)

完成向请求添加身份后，位于 **[!UICONTROL 请求设置]**，在选择之前提供请求的名称和可选描述 **[!UICONTROL 提交]**.

![图像显示 [!UICONTROL 提交] 正在选择按钮](../images/ui/record-delete/submit.png)

系统会要求您确认要删除其数据的标识列表。 选择 **[!UICONTROL 提交]** 以确认您的选择。

![显示确认对话框的图像](../images/ui/record-delete/confirm-request.png)

提交请求后，将创建一个工作单，该工作单将显示在 [!UICONTROL 消费者] 的选项卡 [!UICONTROL 数据卫生] 工作区。 从此处，您可以监控工作单在处理请求时的状态。

>[!NOTE]
>
>请参阅概述部分，了解 [时间轴和透明度](../home.md#record-delete-transparency) 以了解记录删除在执行后如何处理的详细信息。

## 后续步骤

本文档介绍了如何删除Experience PlatformUI中的记录。 有关如何在UI中执行其他数据卫生任务的信息，请参阅 [数据卫生UI概述](./overview.md).

要了解如何使用数据卫生API删除记录，请参阅 [工单终结点指南](../api/workorder.md).
