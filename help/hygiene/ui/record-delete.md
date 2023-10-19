---
title: 删除记录
description: 了解如何在Adobe Experience Platform UI中删除记录。
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: 6e97b3a6b3830cf88802a8dd89944b6ce8791f02
workflow-type: tm+mt
source-wordcount: '1564'
ht-degree: 8%

---

# [!BADGE 测试版]{type=Informational}删除记录 {#record-delete}

使用 [[!UICONTROL 数据生命周期] 工作区](./overview.md) 根据记录的主要身份删除Adobe Experience Platform中的记录。 这些记录可以绑定到个人消费者或身份图中包含的任何其他实体。

>[!IMPORTANT]
> 
>记录删除功能当前为测试版，仅在 **限量发行**. 并非所有客户都可使用。 记录删除请求仅适用于受限版本中的组织。
> 
> 
>记录删除旨在用于数据清理、匿名数据删除或数据最小化。 他们是 **非** 用于数据主体权利请求（符合），与通用数据保护条例(GDPR)等隐私法规相关。 对于所有合规性用例，使用 [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) 而是。

## 先决条件 {#prerequisites}

删除记录需要深入了解身份字段在Experience Platform中的工作原理。 具体而言，您必须知道要删除其记录的实体的主要标识值，具体取决于从中删除这些记录的数据集（或数据集）。

有关Platform中标识的更多信息，请参阅以下文档：

* [Adobe Experience Platform Identity服务](../../identity-service/home.md)：跨设备和系统桥接身份，根据数据集符合的XDM架构定义的身份字段将数据集链接在一起。
* [身份命名空间](../../identity-service/namespaces.md)：身份命名空间定义可以与单个人员相关的不同类型的身份信息，是每个身份字段的必需组件。
* [Real-time Customer Profile](../../profile/home.md)：使用身份图根据来自多个来源的聚合数据提供统一的使用者配置文件，并近乎实时更新。
* [体验数据模型(XDM)](../../xdm/home.md)：通过使用架构提供Platform数据的标准定义和结构。 所有Platform数据集都符合特定的XDM架构，该架构定义哪些字段是身份。
* [身份字段](../../xdm/ui/fields/identity.md)：了解如何在XDM架构中定义标识字段。

## 创建请求 {#create-request}

要启动流程，请选择 **[!UICONTROL 数据生命周期]** （在Platform UI的左侧导航中）。 此 [!UICONTROL 数据生命周期请求] 工作区即会出现。 接下来，选择 **[!UICONTROL 创建请求]** 从工作区的主页开始。

![此 [!UICONTROL 数据生命周期请求] 工作区，使用 [!UICONTROL 创建请求] 已选定。](../images/ui/record-delete/create-request-button.png)

此时将显示请求创建工作流。 默认情况下， **[!UICONTROL 删除记录]** 选项，则该选项将在 **[!UICONTROL 请求的操作]** 部分。 保持选中此选项。

>[!IMPORTANT]
> 
>作为提高效率和降低数据集操作成本的持续更改的一部分，已迁移到增量格式的组织可以从Identity Service、实时客户档案和数据湖中删除数据。 此类型的用户称为增量迁移。 已增量迁移的组织中的用户可以选择删除单个或所有数据集的记录。 来自尚未进行增量迁移的组织中的用户不能选择从单个或所有数据集中删除记录，如下图所示。 在这种情况下，请继续执行 [提供身份](#provide-identities) 部分。

![使用创建请求的工作流 [!UICONTROL 删除记录] 选项已选中并突出显示。](../images/ui/record-delete/delete-record.png)

## 选择数据集 {#select-dataset}

下一步是确定要从单个数据集还是从所有数据集删除记录。 如果您无法使用此选项，请继续 [提供身份](#provide-identities) 部分。

在 **[!UICONTROL 记录详细信息]** 部分，使用单选按钮在特定数据集和所有数据集之间进行选择。 如果您选择 **[!UICONTROL 选择数据集]**，继续选择数据库图标(![数据库图标](../images/ui/record-delete/database-icon.png))以打开一个对话框，其中提供了可用数据集的列表。 从列表中选择所需的数据集，然后 **[!UICONTROL 完成]**.

![此 [!UICONTROL 选择数据集] 对话框中选择了一个数据集并 [!UICONTROL 完成] 突出显示。](../images/ui/record-delete/select-dataset.png)

如果要删除所有数据集的记录，请选择 **[!UICONTROL 所有数据集]**.

![此 [!UICONTROL 选择数据集] 与 [!UICONTROL 所有数据集] 已选中选项。](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
>选择 **[!UICONTROL 所有数据集]** 选项可能会导致删除操作花费较长时间，并且可能不会导致准确的记录删除。

## 提供身份 {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="主要标识"
>abstract="主要标识是一个用于将记录与 Experience Platform 中的消费者配置文件相关联的属性。数据集的主要标识字段由数据集所基于的架构定义。在此列中，您必须为记录的主要标识提供类型（或命名空间），例如 `email`（对于电子邮件地址）和 `ecid`（对于 Experience Cloud ID）。要了解详情，请参阅《数据生命周期 UI 指南》。"

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="标识值"
>abstract="在此列中，您必须提供记录的主要标识的值，该值必须与左列中提供的标识类型相对应。如果主要标识类型是 `email`，则值应是记录的电子邮件地址。要了解详情，请参阅《数据生命周期 UI 指南》。"

删除记录时，必须提供身份信息，以便系统能够确定要删除的记录。 对于Platform中的任何数据集，记录都将会根据 **主要身份** 由数据集的架构定义的字段。

与Platform中的所有标识字段一样，主标识由两部分组成： **type** （有时称为身份命名空间）和 **值**. 身份类型提供有关字段如何标识记录的上下文（如电子邮件地址），该值表示该类型的特定记录身份(例如， `jdoe@example.com` 对于 `email` 标识类型)。 用作标识的常见字段包括帐户信息、设备ID和Cookie ID。

>[!TIP]
>
>如果您不知道特定数据集的主要身份，则可以在Platform UI中找到它。 在 **[!UICONTROL 数据集]** 在工作区中，从列表中选择有问题的数据集。 在数据集的详细信息页面上，将鼠标悬停在右边栏中数据集架构的名称上。 主标识与架构名称和描述一起显示。
>
>![已选定数据集的“数据集”功能板，并从数据集详细信息面板中打开了架构对话框。 数据集的主ID会突出显示。](../images/ui/record-delete/dataset-primary-identity.png)

如果要从单个数据集删除记录，则您提供的所有标识必须具有相同的类型，因为一个数据集只能有一个主标识。 如果您要从所有数据集进行删除，则可以包含多个标识类型，因为不同的数据集可能具有不同的主标识。

删除记录时，可通过两个选项提供身份：

* [上传JSON文件](#upload-json)
* [手动输入身份值](#manual-identity)

### 上传JSON文件 {#upload-json}

要上传JSON文件，您可以将该文件拖放到提供的区域，或选择 **[!UICONTROL 选择文件]** 浏览并从本地目录中选择。

![突出显示具有用于上传JSON文件的选择文件和拖放界面的请求创建工作流。](../images/ui/record-delete/upload-json.png)

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

![使用创建请求的工作流 [!UICONTROL 添加身份] 选项突出显示。](../images/ui/record-delete/add-identity.png)

显示的控件允许您一次输入一个身份。 下 **[!UICONTROL 主要身份]**，使用下拉菜单选择身份类型。 下 **[!UICONTROL 标识值]**，提供记录的主要标识值。

![手动添加了带有标识字段的请求创建工作流。](../images/ui/record-delete/identity-added.png)

要添加更多身份，请选择加号图标(![加号图标。](../images/ui/record-delete/plus-icon.png))，或选择 **[!UICONTROL 添加身份]**.

![加号图标和添加身份图标突出显示的请求创建工作流。](../images/ui/record-delete/more-identities.png)

## 提交请求 {#submit}

完成向请求添加标识后，在 **[!UICONTROL 请求设置]**，在选择之前提供请求的名称和可选描述 **[!UICONTROL 提交]**.

>[!IMPORTANT]
> 
>对于每月可以提交的唯一身份记录删除总数，存在不同的限制。 这些限制基于您的许可协议。 如果组织购买了Adobe Real-time Customer Data Platform和Adobe Journey Optimizer的所有版本，则每月最多可以提交100,000个身份记录删除。 已购买的组织 **AdobeHealth Shield** 或 **Adobe隐私和安全防护板** 每月最多可提交600,000个身份记录删除。<br>通过UI发出单个记录删除请求允许您同时提交10,000个ID。 此 [用于删除记录的API方法](../api/workorder.md#create) 允许一次提交100,000个ID。<br>最佳实践是，根据您的ID限制，为每个请求提交尽可能多的ID。 当您打算删除大量ID时，应避免提交小量ID，或每个记录删除请求只提交一个ID。

![请求设置的 [!UICONTROL 名称] 和 [!UICONTROL 描述] 字段 [!UICONTROL 提交] 突出显示。](../images/ui/record-delete/submit.png)

A [!UICONTROL 确认请求] 对话框显示，指示标识删除后无法恢复。 选择 **[!UICONTROL 提交]** 确认要删除其数据的标识列表。

![此 [!UICONTROL 确认请求] 对话框。](../images/ui/record-delete/confirm-request.png)

提交请求后，系统将创建一个工作单，该工作单将显示在 [!UICONTROL 记录] 选项卡 [!UICONTROL 数据生命周期] 工作区。 从此处，您可以监控工作单处理请求时的状态。

>[!NOTE]
>
>请参阅概述部分，了解有关 [时间线和透明度](../home.md#record-delete-transparency) 以了解记录删除执行后如何处理这些删除的详细信息。

![此 [!UICONTROL 记录] 选项卡 [!UICONTROL 数据生命周期] 工作区中突出显示了新请求。](../images/ui/record-delete/request-log.png)

## 后续步骤

本文档介绍了如何删除Experience PlatformUI中的记录。 有关如何在UI中执行其他数据生命周期管理任务的信息，请参阅 [数据生命周期UI概述](./overview.md).

要了解如何使用数据卫生API删除记录，请参阅 [工单终结点指南](../api/workorder.md).
