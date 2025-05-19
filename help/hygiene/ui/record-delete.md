---
title: 删除记录
description: 了解如何在Adobe Experience Platform UI中删除记录。
badgeBeta: label="Beta 版" type="Informative"
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 8%

---

# 删除记录 {#record-delete}

使用[[!UICONTROL 数据生命周期]工作区](./overview.md)根据记录的主要标识删除Adobe Experience Platform中的记录。 这些记录可以绑定到个人消费者或身份图中包含的任何其他实体。

>[!IMPORTANT]
> 
>记录删除功能当前在Beta中，仅在&#x200B;**有限版本**&#x200B;中可用。 并非所有客户都可使用。 记录删除请求仅适用于受限版本中的组织。
> 
> 
>记录删除旨在用于数据清理、匿名数据删除或数据最小化。 它们&#x200B;**不是**&#x200B;用于数据主体权利请求（合规性），因为它与《通用数据保护条例》(GDPR)等隐私法规相关。 对于所有合规性用例，请改用[Adobe Experience Platform Privacy Service](../../privacy-service/home.md)。

## 先决条件 {#prerequisites}

删除记录需要深入了解标识字段在Experience Platform中的工作原理。 具体而言，您必须知道要删除其记录的实体的身份命名空间值，具体取决于从中删除这些记录的数据集（或数据集）。

有关Experience Platform中标识的更多信息，请参阅以下文档：

* [Adobe Experience Platform Identity服务](../../identity-service/home.md)：跨设备和系统桥接身份，根据数据集所遵循的XDM架构定义的身份字段将数据集链接在一起。
* [身份命名空间](../../identity-service/features/namespaces.md)：身份命名空间定义可以与单个人员相关的不同类型的身份信息，并且是每个身份字段的必需组件。
* [实时客户个人资料](../../profile/home.md)：使用标识图根据来自多个来源的汇总数据提供统一的使用者个人资料，这些数据近乎实时更新。
* [体验数据模型(XDM)](../../xdm/home.md)：通过使用架构为Experience Platform数据提供标准定义和结构。 所有Experience Platform数据集都符合特定的XDM架构，该架构定义哪些字段是身份。
* [标识字段](../../xdm/ui/fields/identity.md)：了解如何在XDM架构中定义标识字段。

## 创建请求 {#create-request}

要开始此过程，请在Experience Platform UI的左侧导航中选择&#x200B;**[!UICONTROL 数据生命周期]**。 出现[!UICONTROL 数据生命周期请求]工作区。 接下来，从工作区的主页中选择&#x200B;**[!UICONTROL 创建请求]**。

![已选择[!UICONTROL 创建请求]的[!UICONTROL 数据生命周期请求]工作区。](../images/ui/record-delete/create-request-button.png)

此时将显示请求创建工作流。 默认情况下，**[!UICONTROL 请求的操作]**&#x200B;部分下选择了&#x200B;**[!UICONTROL 删除记录]**&#x200B;选项。 保持选中此选项。

>[!IMPORTANT]
> 
>为了提高效率并降低数据集操作的成本，已迁移到Delta格式的组织可以从Identity Service、实时客户档案和数据湖中删除数据。 此类型的用户称为增量迁移。 已增量迁移的组织中的用户可以选择删除单个或所有数据集的记录。 来自未经历增量迁移的组织中的用户无法从单个数据集或所有数据集中有选择地删除记录，如下图所示。 在这种情况下，请继续指南的[提供标识](#provide-identities)部分。

![选择并突出显示[!UICONTROL 删除记录]选项的请求创建工作流。](../images/ui/record-delete/delete-record.png)

## 选择数据集 {#select-dataset}

下一步是确定要从单个数据集还是从所有数据集删除记录。 如果此选项不可用，请继续阅读指南的[提供标识](#provide-identities)部分。

在&#x200B;**[!UICONTROL 记录详细信息]**&#x200B;部分下，使用单选按钮在特定数据集和所有数据集之间进行选择。 如果选择&#x200B;**[!UICONTROL 选择数据集]**，请继续选择数据库图标（![数据库图标](/help/images/icons/database.png)）以打开一个提供可用数据集列表的对话框。 从列表中选择所需的数据集，然后选择&#x200B;**[!UICONTROL 完成]**。

![包含选定数据集并突出显示[!UICONTROL 完成]的[!UICONTROL 选择数据集]对话框。](../images/ui/record-delete/select-dataset.png)

如果要删除所有数据集的记录，请选择&#x200B;**[!UICONTROL 所有数据集]**。

![已选择[!UICONTROL 所有数据集]选项的[!UICONTROL 选择数据集]对话框。](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
>选择&#x200B;**[!UICONTROL 所有数据集]**&#x200B;选项可能会导致删除操作花费较长时间，并且可能不会导致准确的记录删除。

## 提供身份标识 {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="身份标识命名空间"
>abstract="身份标识命名空间是一个用于将记录与 Experience Platform 中的消费者轮廓相关联的属性。数据集的身份标识命名空间字段由数据集所基于的架构定义。在此列中，您必须为记录的身份标识命名空间提供类型（或命名空间），例如 `email`（对于电子邮件地址）和 `ecid`（对于 Experience Cloud ID）。要了解详情，请参阅数据生命周期 UI 指南。"

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="主要身份标识值"
>abstract="在此列中，您必须提供记录的身份标识命名空间的值，该值必须与左列中提供的身份标识类型相对应。如果身份标识命名空间类型是 `email`，则值应是记录的电子邮件地址。要了解详情，请参阅数据生命周期 UI 指南。"

删除记录时，必须提供身份信息，以便系统能够确定要删除的记录。 对于Experience Platform中的任何数据集，会根据由该数据集的架构定义的&#x200B;**身份命名空间**&#x200B;字段删除记录。

与Experience Platform中的所有身份字段一样，身份命名空间由两部分组成：**类型**（有时也称为身份命名空间）和&#x200B;**值**。 标识类型提供有关字段如何标识记录的上下文（如电子邮件地址）。 该值表示该类型记录的特定标识（例如，`email`标识类型的`jdoe@example.com`）。 用作标识的常见字段包括帐户信息、设备ID和Cookie ID。

>[!TIP]
>
>如果您不知道特定数据集的身份命名空间，则可以在Experience Platform UI中找到它。 在&#x200B;**[!UICONTROL 数据集]**&#x200B;工作区中，从列表中选择相关数据集。 在数据集的详细信息页面上，将鼠标悬停在右边栏中数据集架构的名称上。 身份命名空间与架构名称和描述一起显示。
>
>![已选定数据集的数据集仪表板，并从数据集详细信息面板中打开了架构对话框。 数据集的主ID已突出显示。](../images/ui/record-delete/dataset-primary-identity.png)

如果要从单个数据集中删除记录，则您提供的所有身份都必须具有相同的类型，因为一个数据集只能有一个身份命名空间。 如果您要从所有数据集进行删除，则可以包含多个标识类型，因为不同的数据集可能具有不同的主标识。

删除记录时，可通过两个选项提供身份：

* [上传JSON文件](#upload-json)
* [手动输入主要标识值](#manual-identity)

### 上传JSON文件 {#upload-json}

要上传JSON文件，可以将文件拖放到提供的区域，或选择&#x200B;**[!UICONTROL 选择文件]**&#x200B;以浏览并从本地目录中选择。

![请求创建工作流中突出显示了用于上传JSON文件的选择文件和拖放界面。](../images/ui/record-delete/upload-json.png)

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
| `value` | 类型表示的主要标识值。 |

上传文件后，您可以继续[提交请求](#submit)。

### 手动输入身份 {#manual-identity}

要手动输入身份，请选择&#x200B;**[!UICONTROL 添加身份]**。

![突出显示了[!UICONTROL 添加身份]选项的请求创建工作流。](../images/ui/record-delete/add-identity.png)

显示的控件允许您一次输入一个身份。 在&#x200B;**[!UICONTROL 身份命名空间]**&#x200B;下，使用下拉菜单选择身份类型。 在&#x200B;**[!UICONTROL 主标识值]**&#x200B;下，提供记录的标识命名空间值。

![手动添加了具有标识字段的请求创建工作流。](../images/ui/record-delete/identity-added.png)

要添加更多标识，请选择加号图标(![A加号图标。](/help/images/icons/tree-expand-all.png))，或选择&#x200B;**[!UICONTROL 添加标识]**。

![加号图标和添加身份图标突出显示的请求创建工作流。](../images/ui/record-delete/more-identities.png)

## 提交请求 {#submit}

完成向请求添加身份后，在&#x200B;**[!UICONTROL 请求设置]**&#x200B;下，在选择&#x200B;**[!UICONTROL 提交]**&#x200B;之前，提供请求的名称和可选描述。

>[!IMPORTANT]
> 
>对于每月可以提交的唯一身份记录删除总数，存在不同的限制。 这些限制基于您的许可协议。 如果组织购买了Adobe Real-Time Customer Data Platform或Adobe Journey Optimizer的所有版本，则每月最多可以提交100,000个身份记录删除。 已购买&#x200B;**Adobe Healthcare Shield**&#x200B;或&#x200B;**Adobe Privacy &amp; Security Shield**&#x200B;的组织每月最多可提交600,000个身份记录删除。<br>通过用户界面发出的单个记录删除请求允许您同时提交10,000个ID。 用于删除记录的[API方法](../api/workorder.md#create)允许一次提交100,000个ID。<br>最佳实践是，根据您的ID限制，为每个请求提交尽可能多的ID。 当您打算删除大量ID时，应避免提交小量ID，或每个记录删除请求只提交一个ID。

![请求设置的[!UICONTROL Name]和[!UICONTROL Description]字段已突出显示[!UICONTROL Submit]。](../images/ui/record-delete/submit.png)

出现[!UICONTROL 确认请求]对话框，指示标识一旦删除就无法恢复。 选择&#x200B;**[!UICONTROL 提交]**&#x200B;以确认要删除其数据的标识列表。

![[!UICONTROL 确认请求]对话框。](../images/ui/record-delete/confirm-request.png)

提交请求后，将创建一个工作单，该工作单将出现在[!UICONTROL 数据生命周期]工作区的[!UICONTROL 记录]选项卡上。 从此处，您可以监控工作单处理请求时的状态。

>[!NOTE]
>
>有关执行记录删除后如何处理这些删除的详细信息，请参阅[时间线和透明度](../home.md#record-delete-transparency)的概述部分。

![数据生命周期]工作区的[!UICONTROL 记录]选项卡，其中新请求突出显示。](../images/ui/record-delete/request-log.png)[!UICONTROL 

## 后续步骤

本文档介绍了如何在Experience Platform UI中删除记录。 有关如何在UI中执行其他数据生命周期管理任务的信息，请参阅[数据生命周期UI概述](./overview.md)。

要了解如何使用数据卫生API删除记录，请参阅[工作单终结点指南](../api/workorder.md)。
