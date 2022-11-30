---
title: 删除记录
description: 了解如何在Adobe Experience Platform UI中删除记录。
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: 70a2abcc4d6e27a89e77d68e7757e4876eaa4fc0
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 0%

---

# 删除记录

的 [[!UICONTROL 数据卫生] 工作区](./overview.md) 在Adobe Experience Platform UI中，您可以删除参与Identity服务和实时客户资料的记录。 这些记录可以绑定到单个用户或包含在身份图中的任何其他实体。

>[!IMPORTANT]
>
>记录删除请求仅适用于已购买的组织 **Adobe医疗保健盾**.
>
>
>记录删除用于数据清理、删除匿名数据或数据最小化。 是 **not** 用于与《通用数据保护条例》(GDPR)等隐私法规相关的数据主体权利请求（合规）。 对于所有法规遵从性用例，请使用 [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) 中。

## 先决条件

删除记录需要对身份字段在Experience Platform中的工作方式有一定的了解。 具体而言，您必须了解要删除其记录的实体的主要标识值，具体取决于您从中删除这些记录的数据集（或数据集）。

有关Platform中身份的更多信息，请参阅以下文档：

* [Adobe Experience Platform Identity Service](../../identity-service/home.md):跨设备和系统构建身份桥梁，根据数据集符合的XDM架构定义的身份字段，将数据集链接在一起。
   * [身份命名空间](../../identity-service/namespaces.md):身份命名空间定义可与单个人员关联的不同身份信息类型，这些信息是每个身份字段的必需组件。
* [实时客户资料](../../profile/home.md):利用身份图以基于来自多个来源的汇总数据提供统一的消费者用户档案，这些数据近乎实时地更新。
* [体验数据模型(XDM)](../../xdm/home.md):通过使用架构为平台数据提供标准定义和结构。 所有Platform数据集都符合特定的XDM架构，并且该架构定义哪些字段是标识。
   * [标识字段](../../xdm/ui/fields/identity.md):了解如何在XDM架构中定义标识字段。

## 创建新请求

要启动该流程，请选择 **[!UICONTROL 创建请求]** 的页面。

![显示 [!UICONTROL 创建请求] 按钮](../images/ui/record-delete/create-request-button.png)

将出现请求创建对话框。 默认情况下， **[!UICONTROL 删除使用者]** 选项 **[!UICONTROL 请求的操作]** 中。 保持选中此选项。

![显示在创建对话框中选择的删除使用者选项的图像](../images/ui/record-delete/consumer-action.png)

## 选择数据集

在 **[!UICONTROL 消费者详细信息]** 部分，下一步是确定要从单个数据集还是所有数据集中删除记录。

如果您选择 **[!UICONTROL 选择数据集]**，选择数据库图标(![数据库图标的图像](../images/ui/record-delete/database-icon.png))，此时会出现一个对话框，允许您从列表中选择所需的数据集。

![显示数据集选择对话框的图像](../images/ui/record-delete/select-dataset.png)

如果要从所有数据集中删除记录，请选择 **[!UICONTROL 所有数据集]**.

![显示 [!UICONTROL 所有数据集] 已选择](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
>选择 **[!UICONTROL 所有数据集]** 选项可能会导致删除操作花费较长的时间，并且可能不会导致准确删除记录。

## 提供身份 {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="主标识"
>abstract="主标识是将记录与Experience Platform中消费者的配置文件关联的属性。 数据集的主标识字段由数据集所基于的架构定义。 在此列中，必须为记录的主标识提供类型（或命名空间），例如 `email` (电子邮件地址和 `ecid` Experience CloudID。 要了解更多信息，请参阅数据卫生UI指南。"

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="标识值"
>abstract="在此列中，必须为记录的主标识提供值，该值必须与左列中提供的标识类型相对应。 如果主标识类型为 `email`，值应为记录的电子邮件地址。 要了解更多信息，请参阅数据卫生UI指南。"

删除记录时，必须提供身份信息，以便系统能够确定必须删除哪些记录。 对于Platform中的任何数据集，将根据 **主标识** 字段。

与Platform中的所有标识字段一样，主标识由两个部分组成：a **type** （有时称为身份命名空间）和 **值**. 标识类型提供有关字段如何标识记录（如电子邮件地址）的上下文，并且值表示该类型记录的特定标识(例如， `jdoe@example.com` 对于 `email` 标识类型)。 用作标识的常用字段包括帐户信息、设备ID和Cookie ID。

>[!TIP]
>
>如果您不知道特定数据集的主标识，则可以在Platform UI中找到该数据集。 在 **[!UICONTROL 数据集]** 工作区中，从列表中选择相关数据集。 在数据集的详细信息页面上，将鼠标悬停在右边栏中数据集架构的名称上。 主标识与架构名称和描述一起显示。
>
>![在UI中突出显示的数据集的主标识的图像](../images/ui/record-delete/dataset-primary-identity.png)

如果从单个数据集中删除记录，则您提供的所有标识都必须具有相同的类型，因为数据集只能有一个主标识。 如果从所有数据集中删除，则可以包含多个身份类型，因为不同的数据集可能具有不同的主身份。

在删除记录时，有两个选项可提供身份：

* [上传JSON文件](#upload-json)
* [手动输入标识值](#manual-identity)

### 上传JSON文件 {#upload-json}

要上传JSON文件，您可以将文件拖放到提供区域，或选择 **[!UICONTROL 选择文件]** 从本地目录中浏览并选择。

![显示在UI中上传JSON方法的图像](../images/ui/record-delete/upload-json.png)

JSON文件必须格式化为对象数组，每个对象表示一个标识。

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
| `value` | 由类型表示的身份值。 |

上传文件后，您可以继续 [提交请求](#submit).

### 手动输入标识 {#manual-identity}

要手动输入标识，请选择 **[!UICONTROL 添加标识]**.

![显示 [!UICONTROL 添加标识] 按钮](../images/ui/record-delete/add-identity.png)

此时会显示允许您一次输入一个标识的控件。 在 **[!UICONTROL 主标识]**，请使用下拉菜单选择身份类型。 在 **[!UICONTROL 标识值]**，为记录提供主标识值。

![显示手动添加的身份字段的图像](../images/ui/record-delete/identity-added.png)

要添加更多标识，请选择加号图标(![加号图标的图像](../images/ui/record-delete/plus-icon.png))，或选择 **[!UICONTROL 添加标识]**.

![显示如何向请求添加更多标识的图像](../images/ui/record-delete/more-identities.png)

## 提交请求(#submit)

完成向请求添加身份后，请在 **[!UICONTROL 请求设置]**，在选择 **[!UICONTROL 提交]**.

![显示 [!UICONTROL 提交] 按钮](../images/ui/record-delete/submit.png)

系统将要求您确认要删除其数据的身份列表。 选择 **[!UICONTROL 提交]** 以确认您的选择。

![显示确认对话框的图像](../images/ui/record-delete/confirm-request.png)

提交请求后，将创建工作单，并在 [!UICONTROL 消费者] 选项卡 [!UICONTROL 数据卫生] 工作区。 在此处，您可以在处理请求时监控工作单的状态。

>[!NOTE]
>
>请参阅 [时间表和透明度](../home.md#record-delete-transparency) 有关执行记录删除后如何处理记录删除的详细信息。

## 后续步骤

本文档介绍了如何删除Experience PlatformUI中的记录。 有关如何在UI中执行其他数据卫生任务的信息，请参阅 [数据卫生UI概述](./overview.md).

要了解如何使用数据卫生API删除记录，请参阅 [《工作单终端指南》](../api/workorder.md).
