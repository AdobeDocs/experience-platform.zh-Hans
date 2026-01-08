---
title: 记录删除请求（UI工作流）
description: 了解如何在Adobe Experience Platform UI中删除记录。
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: 56ae47f511a7392286c4f85173dba30e93fc07d0
workflow-type: tm+mt
source-wordcount: '2520'
ht-degree: 4%

---

# 记录删除请求（UI工作流） {#record-delete}

使用[[!UICONTROL Data Lifecycle]工作区](./overview.md)根据记录的主要身份删除Adobe Experience Platform中的记录。 这些记录可以绑定到个人消费者或身份图中包含的任何其他实体。

>[!IMPORTANT]
>
>记录删除旨在用于数据清理、匿名数据删除或数据最小化。 它们&#x200B;**不是**&#x200B;用于数据主体权利请求（合规性），因为它与《通用数据保护条例》(GDPR)等隐私法规相关。 对于所有合规性用例，请改用[Adobe Experience Platform Privacy Service](../../privacy-service/home.md)。

## 先决条件 {#prerequisites}

删除记录需要深入了解标识字段在Experience Platform中的工作原理。 具体而言，您必须知道要删除其记录的实体的主身份命名空间和值，具体取决于从中删除这些记录的数据集（或数据集）。

有关Experience Platform中标识的更多信息，请参阅以下文档：

* [Adobe Experience Platform Identity服务](../../identity-service/home.md)：跨设备和系统桥接身份，根据数据集所遵循的XDM架构定义的身份字段将数据集链接在一起。
* [身份命名空间](../../identity-service/features/namespaces.md)：身份命名空间定义可以与单个人员相关的不同类型的身份信息，并且是每个身份字段的必需组件。
* [实时客户个人资料](../../profile/home.md)：使用标识图根据来自多个来源的汇总数据提供统一的使用者个人资料，这些数据近乎实时更新。
* [体验数据模型(XDM)](../../xdm/home.md)：通过使用架构为Experience Platform数据提供标准定义和结构。 所有Experience Platform数据集都符合特定的XDM架构，该架构定义哪些字段是身份。
* [标识字段](../../xdm/ui/fields/identity.md)：了解如何在XDM架构中定义标识字段。

>[!IMPORTANT]
>
>记录删除仅对数据集架构中定义的&#x200B;**主标识**&#x200B;字段起作用。 以下限制适用：
>
>* **未扫描辅助标识。**&#x200B;如果数据集包含多个标识字段，则仅使用主标识进行匹配。 无法根据非主标识定位或删除记录。
>* **跳过没有填充主标识的记录。**&#x200B;如果记录未填充主身份元数据，则无法将其删除。
>* **在身份配置之前摄取的数据不合格。**&#x200B;如果在数据摄取后将主标识字段添加到架构，则无法通过此工作流删除以前摄取的记录。

## 创建请求 {#create-request}

要开始此过程，请在Experience Platform UI的左侧导航中选择&#x200B;**[!UICONTROL Data Lifecycle]**。 出现[!UICONTROL Data lifecycle requests]工作区。 接下来，从工作区的主页中选择&#x200B;**[!UICONTROL Create request]**。

![已选择[!UICONTROL Data lifecycle requests]的[!UICONTROL Create request]工作区。](../images/ui/record-delete/create-request-button.png)

此时将显示请求创建工作流。 默认情况下，**[!UICONTROL Delete record]**&#x200B;部分下的&#x200B;**[!UICONTROL Requested Action]**&#x200B;选项处于选中状态。 保持选中此选项。

>[!IMPORTANT]
> 
>为了提高效率并降低数据集操作的成本，已迁移到Delta格式的组织可以从Identity Service、实时客户档案和数据湖中删除数据。 此类型的用户称为增量迁移。 已增量迁移的组织中的用户可以选择删除单个或所有数据集的记录。 来自未经历增量迁移的组织中的用户无法从单个数据集或所有数据集中有选择地删除记录，如下图所示。 在这种情况下，请继续指南的[提供标识](#provide-identities)部分。

![已选择并突出显示[!UICONTROL Delete record]选项的请求创建工作流。](../images/ui/record-delete/delete-record.png)

## 选择数据集 {#select-dataset}

下一步是确定要从单个数据集还是从所有数据集删除记录。 数据集选择选项可能不可用，具体取决于您组织的配置。 如果未看到此选项，请继续阅读指南的[提供标识](#provide-identities)部分。

在&#x200B;**[!UICONTROL Record Details]**&#x200B;部分中，选择一个单选按钮以选择特定数据集或所有数据集。

若要从特定数据集中删除，请选择&#x200B;**[!UICONTROL Select dataset]**，然后选择数据库图标（![数据库图标](/help/images/icons/database.png)）。 在显示的对话框中，选择一个数据集并选择要确认的&#x200B;**[!UICONTROL Done]**。

![包含选定数据集并突出显示[!UICONTROL Select dataset]的[!UICONTROL Done]对话框。](../images/ui/record-delete/select-dataset.png)

要从所有数据集中删除，请选择&#x200B;**[!UICONTROL All datasets]**。 此选项会增加操作的范围，并要求您为要定位的每个数据集提供主标识类型。

![已选择带有[!UICONTROL Select dataset]选项的[!UICONTROL All datasets]对话框。](../images/ui/record-delete/all-datasets.png)

>[!WARNING]
>
>选择&#x200B;**[!UICONTROL All datasets]**&#x200B;会将此操作扩展到组织中的所有数据集。 每个数据集可能使用不同的主标识类型。 您必须为每个数据集&#x200B;**提供**&#x200B;主标识类型以确保准确匹配。
>
>如果缺少任何标识类型，则在删除过程中可能会跳过某些记录。 这可能会降低处理速度，并导致&#x200B;**部分结果**。

Experience Platform中的每个数据集仅支持一种主要身份类型。

* 从&#x200B;**单个数据集**&#x200B;中删除时，请求中的所有标识都必须使用&#x200B;**相同类型**。
* 从&#x200B;**所有数据集**&#x200B;中删除时，您可以包含&#x200B;**多个标识类型**，因为不同的数据集可能依赖不同的主标识。”

## 提供身份标识 {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="主要身份标识命名空间"
>abstract="主身份命名空间是唯一将记录与Experience Platform中的消费者配置文件关联的属性。 数据集的主要身份标识字段由数据集所基于的架构定义。在此列中，您必须提供与数据集架构匹配的主要身份命名空间(例如，电子邮件地址为`email`，Experience Cloud ID为`ecid`)。 要了解详情，请参阅数据生命周期 UI 指南。"

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="主要身份标识值"
>abstract="在此列中，您必须提供记录的身份标识命名空间的值，该值必须与左列中提供的身份标识类型相对应。如果身份标识命名空间类型是 `email`，则值应是记录的电子邮件地址。要了解详情，请参阅数据生命周期 UI 指南。"

删除记录时，必须提供身份信息，以便系统能够确定要删除的记录。 对于Experience Platform中的任何数据集，会根据由数据集的架构定义的&#x200B;**主标识**&#x200B;字段删除记录。

>[!NOTE]
>
>虽然UI允许您选择身份命名空间，但在执行时只使用在数据集架构中配置的&#x200B;**主身份**。 确保您提供的身份值对应于数据集的主身份字段。

与Experience Platform中的所有标识字段一样，主标识由两部分组成：**type**（标识命名空间）和&#x200B;**value**。 标识类型提供有关字段如何标识记录的上下文（如电子邮件地址）。 该值表示该类型记录的特定标识（例如，`jdoe@example.com`标识类型的`email`）。 用作主标识的常见字段包括帐户信息、设备ID和Cookie ID。

>[!TIP]
>
>如果您不知道特定数据集的身份命名空间，则可以在Experience Platform UI中找到它。 在&#x200B;**[!UICONTROL Datasets]**&#x200B;工作区中，从列表中选择有问题的数据集。 在数据集的详细信息页面上，将鼠标悬停在右边栏中数据集架构的名称上。 身份命名空间与架构名称和描述一起显示。
>
>![已选定数据集的数据集仪表板，并从数据集详细信息面板中打开了架构对话框。 数据集的主ID已突出显示。](../images/ui/record-delete/dataset-primary-identity.png)

删除记录时，可通过两个选项提供身份：

* [上传JSON文件](#upload-json)
* [手动输入主要标识值](#manual-identity)

### 上传JSON文件 {#upload-json}

要上传JSON文件，您可以将该文件拖放到提供的区域，或选择&#x200B;**[!UICONTROL Choose files]**&#x200B;以浏览并从本地目录中选择。

![请求创建工作流中突出显示了用于上传JSON文件的选择文件和拖放界面。](../images/ui/record-delete/upload-json.png)

JSON文件必须采用对象数组的格式，每个对象表示目标数据集的主要标识值。

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
| `namespaceCode` | 目标数据集的主要身份命名空间。 |
| `value` | 类型表示的主要标识值。 |

上传文件后，您可以继续[提交请求](#submit)。

### 手动输入身份 {#manual-identity}

要手动输入身份，请选择&#x200B;**[!UICONTROL Add identity]**。

![突出显示了[!UICONTROL Add identity]选项的请求创建工作流。](../images/ui/record-delete/add-identity.png)

显示的控件允许您一次输入一个身份。 在&#x200B;**[!UICONTROL identity namespace]**&#x200B;下，使用下拉菜单选择身份类型。 在&#x200B;**[!UICONTROL Primary Identity Value]**&#x200B;下，提供记录的身份命名空间值。

![手动添加了具有标识字段的请求创建工作流。](../images/ui/record-delete/identity-added.png)

要添加更多标识，请选择加号图标(![A加号图标。](/help/images/icons/tree-expand-all.png))，或选择&#x200B;**[!UICONTROL Add identity]**。

![加号图标和添加身份图标突出显示的请求创建工作流。](../images/ui/record-delete/more-identities.png)

## 配额和处理时间线 {#quotas}

记录删除请求受每天和每月标识符提交限制的约束，具体取决于贵组织的许可证权利。 这些限制同时适用于基于UI和基于API的删除请求。

>[!NOTE]
>
>您每天最多可以提交&#x200B;**1,000,000个标识符**，但前提是剩余的每月配额允许这样做。 如果每月上限不到100万，则每日提交内容不能超过该上限。

### 按产品显示的每月提交权利 {#quota-limits}

下表概述了按产品和权利级别划分的标识符提交限制。 对于每个产品，每月上限是两个值中的较小值：固定标识符上限或与许可数据量绑定的基于百分比的阈值。

| 产品 | 权利描述 | 每月上限（以较小者为准） |
|----------|-------------------------|---------------------------------|
| Real-Time CDP或Adobe Journey Optimizer | 不带Privacy and Security Shield或Healthcare Shield附加组件 | 2,000,000个标识符或可寻址受众的5% |
| Real-Time CDP或Adobe Journey Optimizer | 带有Privacy and Security Shield或Healthcare Shield附加组件 | 15,000,000个标识符或10%的可寻址受众 |
| Customer Journey Analytics | 不带Privacy and Security Shield或Healthcare Shield附加组件 | 2,000,000个标识符或每百万CJA权利行有100个标识符 |
| Customer Journey Analytics | 带有Privacy and Security Shield或Healthcare Shield附加组件 | 15,000,000个标识符或每百万CJA权利行有200个标识符 |

>[!NOTE]
>
> 根据大多数组织的实际可寻址受众或CJA行授权，其每月限制较低。

配额在每个日历月的第一天重置。 未使用的配额&#x200B;**未**&#x200B;延期。

>[!NOTE]
>
>配额基于贵组织为&#x200B;**提交的标识符**&#x200B;授予的每月授权。 系统护栏不强制执行这些操作，但可以对其进行监控和审查。
>
>记录删除是&#x200B;**共享服务**。 您的每月上限反映了Real-Time CDP、Adobe Journey Optimizer、Customer Journey Analytics和任何适用的Shield加载项中的最高权限。

### 处理标识符提交的时间表 {#sla-processing-timelines}

提交后，记录删除请求将根据您的权利级别进行排队和处理。

| 产品和权利描述 | 队列持续时间 | 最长处理时间(SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| 不带Privacy and Security Shield或Healthcare Shield附加组件 | 长达15天 | 30 天 |
| 带有Privacy and Security Shield或Healthcare Shield附加组件 | 通常为24小时 | 15 天 |

如果贵组织需要更高的限制，请联系您的Adobe代表进行权利审查。

>[!TIP]
>
>要检查您当前的配额使用情况或权利层，请参阅[配额参考指南](../api/quota.md)。

## 提交请求 {#submit}

完成向请求添加身份后，在&#x200B;**[!UICONTROL Request settings]**&#x200B;下，为请求提供名称和可选描述，然后再选择&#x200B;**[!UICONTROL Submit]**。

>[!TIP]
>
>您通过UI每个请求最多可提交10,000个身份。 若要提交较大的卷（每个请求最多100,000个ID），请使用[API方法](../api/workorder.md#create)。

![请求设置的[!UICONTROL Name]和[!UICONTROL Description]字段突出显示[!UICONTROL Submit]。](../images/ui/record-delete/submit.png)

出现[!UICONTROL Confirm request]对话框指示标识删除后无法恢复。 选择&#x200B;**[!UICONTROL Submit]**&#x200B;以确认要删除其数据的标识列表。

![该[!UICONTROL Confirm request]对话框。](../images/ui/record-delete/confirm-request.png)

提交请求后，将创建一个工作单，该工作单将出现在[!UICONTROL Record]工作区的[!UICONTROL Data Lifecycle]选项卡上。 从此处，您可以监控工作单处理请求时的状态。

>[!NOTE]
>
>有关执行记录删除后如何处理这些删除的详细信息，请参阅[时间线和透明度](../home.md#record-delete-transparency)的概述部分。

![突出显示新请求的[!UICONTROL Record]工作区的[!UICONTROL Data Lifecycle]选项卡。](../images/ui/record-delete/request-log.png)

## 从基于关系架构的数据集中删除记录 {#relational-record-delete}

如果要从中删除的数据集基于关系架构，请查看以下注意事项，以确保正确删除记录，并且不会由于Experience Platform与源系统之间的不匹配而重新摄取记录。

### 记录删除行为

下表概述了记录删除在Experience Platform和源系统中的行为，具体取决于摄取方法和更改数据捕获配置。

| 长宽比 | 行为 |
|---------------------|--------------------------------------------------------------------------|
| 平台删除 | 记录将从Experience Platform数据集和数据湖中删除。 |
| Source维系 | 除非在源系统中显式删除记录，否则记录将保留在该系统中。 |
| 全面刷新影响 | 如果使用完全刷新，则除非从源中删除或排除，否则可能会重新摄取已删除的记录。 |
| 更改数据捕获行为 | 标记为`_change_request_type = 'd'`的记录将在引入期间删除。 可以重新引入未标记的记录。 |

要防止重新摄取，请在源系统和Experience Platform中应用相同的删除方法，方法是从两个系统中删除记录，或为要删除的记录包含`_change_request_type = 'd'`。

### 更改数据捕获和控制列

将源用于变更数据捕获的关系架构在区分删除与更新插入时可以使用`_change_request_type`控件列。 在摄取期间，使用`d`标记的记录将从数据集中删除，而使用`u`或未使用列标记的记录将被视为更新插入。 `_change_request_type`列仅在摄取时读取，并且未存储在目标架构中或映射到XDM字段。

>[!NOTE]
>
>通过数据生命周期UI删除记录不会影响源系统。 要从这两个位置删除数据，请同时在Experience Platform和源中删除该数据。

### 关系架构的其他删除方法

除了标准记录删除工作流之外，关系架构还支持用于特定用例的其他方法：

* **安全复制数据集方法**：复制生产数据集并将删除应用于副本，以进行受控测试或协调，然后再将更改应用于生产数据。
* **仅删除批次上传**：需要删除特定记录而不影响其他数据时，请上传仅包含目标保健删除操作的文件。

### 对保健操作的描述符支持 {#descriptor-support}

关系模式描述符为精确卫生操作提供基本元数据：

* **主键描述符**：唯一标识目标更新或删除的记录，确保正确的记录受到影响。
* **版本描述符**：确保按正确的时间顺序应用删除和更新，防止操作顺序混乱。
* **时间戳描述符（时间序列架构）**：将删除操作与事件发生时间而不是摄取时间保持一致。

>[!NOTE]
>
>卫生流程在数据集级别运行。 对于启用了用户档案的数据集，可能需要其他用户档案工作流来保持实时客户档案的一致性。

### 关系架构的计划保留

有关基于数据年龄而不是特定身份的自动卫生，请参阅[管理体验事件数据集保留(TTL)](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md)以了解数据湖中的计划行级保留。

>[!NOTE]
>
>只有使用时间序列行为的数据集才支持行级到期。

### 关系记录删除的最佳实践

要避免无意中再次摄取并维护跨系统的数据一致性，请遵循以下最佳实践：

* **协调删除**：使记录删除与变更数据捕获配置和源数据管理策略保持一致。
* **监视变更数据捕获流**：在Platform中删除记录后，监视数据流并确认源系统删除了相同的记录或将其与`_change_request_type = 'd'`包含在内。
* **清理源**：对于使用完全刷新摄取的源或不支持通过更改数据捕获进行删除的源，请直接从源系统中删除记录以避免重新摄取。

有关架构要求的详细信息，请参阅[关系架构描述符要求](../../xdm/schema/relational.md#relational-schemas)。

要了解变更数据捕获如何与源一起使用，请参阅[在源中启用变更数据捕获](../../sources/tutorials/api/change-data-capture.md#using-change-data-capture-with-relational-schemas)。

## 后续步骤

本文档介绍了如何在Experience Platform UI中删除记录。 有关如何在UI中执行其他数据生命周期管理任务的信息，请参阅[数据生命周期UI概述](./overview.md)。

要了解如何使用数据卫生API删除记录，请参阅[工作单终结点指南](../api/workorder.md)。
