---
title: 配置文件导出行为
description: 了解Experience Platform目标支持的不同集成模式之间的配置文件导出行为差异。
exl-id: 2be62843-0644-41fa-a860-ccd65472562e
source-git-commit: c54fa206b673868ca3d0ccfa5b0936b83cfd3ed4
workflow-type: tm+mt
source-wordcount: '2933'
ht-degree: 0%

---

# 不同目标类型的配置文件导出行为

Experience Platform中有多种目标类型，如下图所示。 在触发目标导出和导出中包含的内容方面，这些目标的导出模式稍有不同，如下节进一步所述。

>[!IMPORTANT]
>
>本文档页面仅介绍图表底部突出显示的连接的配置文件导出行为。

![目标类型图表](/help/destinations/assets/how-destinations-work/types-of-destinations-v4.png)

## 微批次处理和聚合策略

在深入了解每种目标类型的特定信息之前，请务必了解以下内容的微批量处理和聚合策略的概念： *流式目标*.

Experience Platform目标将数据导出到基于API的集成，作为HTTPS调用。 一旦目标服务被其他上游服务通知配置文件因批量摄取、流式摄取、批量分段、流式分段或身份图更改而更新，数据导出并发送到流式目标。

在配置文件被分派到目标API端点之前，配置文件被聚合到HTTPS消息中的过程称为 *微批处理*.

获取 [facebook目标](/help/destinations/catalog/social/facebook.md) 带有 *[可配置聚合](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)* 例如，策略 — 数据以聚合方式发送，其中，目标服务在上游获取来自配置文件服务的所有传入数据，并在将数据调度到Facebook之前按以下方式之一聚合这些数据：

* 记录数（最多10,000条）或
* 时间窗口间隔（30分钟）

首次满足上述阈值的任何一个都会触发导出到Facebook。 因此，在 [!DNL Facebook Custom Audiences] 仪表板，您可能会看到以10,000笔记录增量从Experience Platform中进入的受众。 您可能会每10-15分钟看到10,000条记录，因为处理和聚合数据的速度比30分钟的导出间隔要快，而且发送速度也快，所以大约每10-15分钟就会处理一次所有记录。 如果没有足够的记录来组成10,000批次，则当前记录数将按在达到时间窗口阈值时的情况发送，因此您也可能会看到发送到Facebook的较小批次。

作为另一个示例，请考虑 [HTTP API目标](/help/destinations/catalog/streaming/http-destination.md)，它具有 *[尽力而为聚合](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)* 策略，使用 `maxUsersPerRequest: 10`. 这意味着，在触发对此目标的HTTP调用之前，最多将汇总10个配置文件，但是Experience Platform会在目标服务收到来自上游服务的更新重新评估信息后立即尝试将配置文件调度到目标。

聚合策略是可配置的，目标开发人员可以决定如何配置聚合策略以最好地满足下游API端点的速率限制。 详细了解 [聚合策略](../destination-sdk/functionality/destination-configuration/aggregation-policy.md) 在Destination SDK文档中。

## 流配置文件导出（企业）目标 {#streaming-profile-destinations}

>[!IMPORTANT]
>
> 企业目标仅适用于 [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 客户。

此 [企业目标](/help/destinations/destination-types.md#streaming-profile-export) Experience Platform中包括Amazon Kinesis、Azure事件中心和HTTP API。

Experience Platform会优化将配置文件导出到企业目标的行为，以便仅在符合区段资格或其他重要事件后对配置文件进行了相关更新时，将数据导出到API端点。 在以下情况下，会将配置文件导出到您的目标：

* 配置文件更新由中的更改决定 [区段成员资格](/help/xdm/field-groups/profile/segmentation.md) 至少一个区段映射到目标。 例如，配置文件已符合映射到目标的其中一个区段的条件，或已退出映射到目标的其中一个区段。
* 配置文件更新由 [身份映射](/help/xdm/field-groups/profile/identitymap.md). 例如，已经符合映射到目标的其中一个区段资格的配置文件，已在标识映射属性中添加了一个新标识。
* 配置文件更新由映射到目标的至少一个属性的更改确定。 例如，会将映射步骤中映射到目标的某个属性添加到配置文件中。

在上述所有情况下，只会将已发生相关更新的用户档案导出到您的目标。 例如，如果映射到目标流的区段具有一百个成员，并且有五个新用户档案符合该区段的条件，则导出到目标的操作将以增量方式进行，并且只包含五个新用户档案。

请注意，无论更改发生在何处，都将为配置文件导出所有映射的属性。 因此，在上面的示例中，将导出这五个新配置文件的所有映射属性，即使属性本身未发生更改也是如此。

### 决定数据导出的因素以及导出中包含的内容

对于为给定用户档案导出的数据，了解以下两个不同的概念很重要： *决定数据导出到企业目标的因素* 和 *哪些数据包含在导出中*.

| 决定目标导出的因素 | 目标导出中包含的内容 |
|---------|----------|
| <ul><li>映射的属性和区段会作为目标导出的提示。 这意味着，如果任何映射的区段更改了状态(从 `null` 到 `realized` 或从 `realized` 到 `exiting`)或者更新任何映射的属性，则启动目标导出。</li><li>由于身份当前无法映射到企业目标，因此给定配置文件上任何身份的更改也会决定目标导出。</li><li>属性的更改被定义为属性上的任何更新，无论它是不是同一个值。 这意味着即使值本身未发生更改，对属性的覆盖也会被视为更改。</li></ul> | <ul><li>此 `segmentMembership` 对象包括激活数据流中映射的区段，在发生资格或区段退出事件后，用户档案的状态已发生更改。 请注意，配置文件符合条件的其他未映射区段也可以作为目标导出的一部分（如果这些区段属于同一个） [合并策略](/help/profile/merge-policies/overview.md) 区段在激活数据流中映射时相同。 </li><li>中的所有标识 `identityMap` 对象也包括在内(Experience Platform当前不支持企业目标中的身份映射)。</li><li>目标导出中仅包含映射的属性。</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>将用户档案激活到目标时，企业目标会流式传输回填数据。 这意味着在将激活工作流映射到目标之前，向目标配置后的首次数据导出将包括符合激活区段资格的用户档案。

>[!BEGINSHADEBOX]

例如，考虑将此数据流映射到HTTP目标，其中在数据流中选择了三个区段，并且四个属性映射到目标。

![企业目标数据流](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

导出到目标的配置文件可由符合或退出其中一个配置文件的配置文件来确定 *三个映射区段*. 但是，在数据导出中，在 `segmentMembership` 对象时，如果该特定配置文件是其他未映射区段的成员，并且这些区段与触发导出的区段共享相同的合并策略，则可能会显示其他未映射区段。 如果配置文件符合 **使用德洛雷亚汽车的客户** 区段，但同时也是 **看了《回到未来》的电影** 和 **科幻迷们** 区段，则其他这两个区段也将显示在 `segmentMembership` 数据导出对象，即使这些对象未在数据流中映射，只要它们与共享相同的合并策略 **使用德洛雷亚汽车的客户** 区段。

从配置文件属性的角度来看，对上述四个映射属性所做的任何更改都将决定目标导出，并且配置文件上存在的四个映射属性中的任何一个都将出现在数据导出中。

>[!ENDSHADEBOX]

>[!TIP]
>
> 您可以在中查看导出到各种企业目标的示例数据 [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md#exported-data)， [Azure事件中心](/help/destinations/catalog/cloud-storage/azure-event-hubs.md#exported-data)、和 [HTTP API](/help/destinations/catalog/streaming/http-destination.md#exported-data) 目标文档页面。

## 基于流API的目标 {#streaming-api-based-destinations}

流目标(如Facebook、Trade Desk和其他基于API的集成)的配置文件导出行为与上面所述的企业目标行为非常相似。

流目标示例是属于以下类别的目标： [社交和广告类别](/help/destinations/destination-types.md#categories) 在目录中。

Experience Platform会优化将配置文件导出到流目标的行为，以便仅在符合区段资格或其他重要事件后发生配置文件的相关更新时，将数据导出到基于流API的目标。 在以下情况下，会将配置文件导出到您的目标：

* 配置文件更新由中的更改决定 [区段成员资格](/help/xdm/field-groups/profile/segmentation.md) 至少一个区段映射到目标。 例如，配置文件已符合映射到目标的其中一个区段的条件，或已退出映射到目标的其中一个区段。
* 配置文件更新由 [身份映射](/help/xdm/field-groups/profile/identitymap.md) 对于已标记为导出此目标实例的身份命名空间。 例如，已经符合映射到目标的其中一个区段资格的配置文件，已在标识映射属性中添加了一个新标识。
* 配置文件更新由映射到目标的至少一个属性的更改确定。 例如，会将映射步骤中映射到目标的某个属性添加到配置文件中。
* 配置自动同意实施且用户档案选择退出后，用户档案的同意发生更改。 自动同意实施会将受众退出事件发送到目标，以便该配置文件不会包含在目标的任何定位中。

在上述所有情况下，只会将已发生相关更新的用户档案导出到您的目标。 例如，如果映射到目标流的区段具有一百个成员，并且有五个新用户档案符合该区段的条件，则导出到目标的操作将以增量方式进行，并且只包含五个新用户档案。

请注意，无论更改发生在何处，都将为配置文件导出所有映射的属性。 因此，在上面的示例中，将导出这五个新配置文件的所有映射属性，即使属性本身未发生更改也是如此。

### 决定数据导出的因素以及导出中包含的内容

对于为给定用户档案导出的数据，请务必了解决定数据导出到流API目标的两个不同概念，以及导出中包含哪些数据。

| 决定目标导出的因素 | 目标导出中包含的内容 |
|---------|----------|
| <ul><li>映射的属性和区段会作为目标导出的提示。 这意味着，如果任何映射的区段更改了状态(从 `null` 到 `realized` 或从 `realized` 到 `exiting`)或者更新任何映射的属性，则启动目标导出。</li><li>标识映射中的更改被定义为为添加/删除的标识 [身份图](/help/identity-service/ui/identity-graph-viewer.md) ，用于为导出而映射的身份命名空间。</li><li>对于映射到目标的属性，属性的更改被定义为属性上的任何更新。</li></ul> | <ul><li>映射到目标且已更改的区段将包含在 `segmentMembership` 对象。 在某些情况下，它们可能会使用多个调用导出。 此外，在某些情况下，某些未更改的区段可能也会包含在调用中。 在任何情况下，都将仅导出映射的区段。</li><li>命名空间中映射到目标的所有身份 `identityMap` 对象也包含在内。</li><li>目标导出中仅包含映射的属性。</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>将用户档案激活到目标时，流API目标会流式回填数据。 这意味着在将激活工作流映射到目标之前，向目标配置后的首次数据导出将包括符合激活区段资格的用户档案。

>[!BEGINSHADEBOX]

例如，将此数据流考虑到一个在数据流中选择了三个区段的流目标。

![流式传输目标数据流](/help/destinations/assets/how-destinations-work/streaming-destination-example-dataflow.png)

导出到目标的配置文件可由符合或退出三个映射区段之一的配置文件确定。 如果配置文件符合 **使用德洛雷亚汽车的客户** 区段，这将触发导出。 其他区段(**城市 — 达拉斯** 和 **基本站点活动**)也可以导出，以防用户档案中该区段显示为可能状态之一(`realized` 或 `exited`)。 未映射的区段(如 **科幻迷们**)将不会导出。

从配置文件属性的角度来看，对上面映射的三个属性所做的任何更改都将决定目标导出。

>[!ENDSHADEBOX]

## 批处理（基于文件）目标 {#file-based-destinations}

将用户档案导出到时 [基于文件的目标](/help/destinations/destination-types.md#file-based) 在Experience Platform中，有三种类型的计划（如下所列）和两种文件导出选项（完整文件或增量文件）可供您使用。 所有这些设置都是在区段级别上设置的，即使有多个区段映射到单个目标数据流也是如此。

* 计划导出：配置一个目标，添加一个或多个区段，选择是否要导出完整文件或增量文件，并选择每天设置一次导出文件的时间，或每天设置几次导出文件的时间。 例如，下午5点的导出时间意味着下午5点将导出符合区段条件的配置文件。
* 区段评估后：导出在每日区段评估作业运行后立即触发。 这意味着文件中的导出用户档案编号尽可能接近区段的最新评估群体。
* 按需导出([立即导出文件](/help/destinations/ui/export-file-now.md))：基于最新的区段评估作业，在定期计划的导出基础上一次性导出完整文件。

在上述任何导出情况下，导出的文件都包含符合导出条件的配置文件，以及您选择作为要导出的XDM属性的列。

>[!TIP]
>
>当流区段映射到批处理目标时，导出的文件中的配置文件数更有可能更接近区段中的用户数。 这是因为最新的区段评估更有可能在更接近导出时间的地方运行。

### 增量文件导出 {#incremental-file-exports}

并非所有配置文件更新都符合将配置文件包含在增量文件导出中的条件。 例如，如果在配置文件中添加或删除了属性，则导出中不包括该配置文件。 仅限符合以下条件的配置文件： `segmentMembership` 属性已更改将包含在导出的文件中。 换言之，仅当配置文件成为区段的一部分或从区段中移除时，它才会包含在增量文件导出中。

同样，如果将新身份（新电子邮件地址、电话号码、ECID等）添加到中的用户档案 [身份图](/help/identity-service/ui/identity-graph-viewer.md)，这并不意味着需要将该配置文件包含在新的增量文件导出中。

如果向目标映射中添加了新区段，则不会影响其他区段的资格和导出。 导出计划是按区段单独配置的，文件是按每个区段单独导出的，即使区段已添加到同一目标数据流中也是如此。

>[!BEGINSHADEBOX]

例如，在下图所示的导出设置中，如果区段正在导出增量文件更新，请注意以下情况，其中配置文件是否包含在增量文件导出中：

![导出具有多个选定属性的设置。](/help/destinations/assets/how-destinations-work/export-selection-batch-destination.png)

* 当配置文件符合或不符合区段资格时，它将被包含在增量文件导出中。
* 配置文件是 *非* 在向身份图中添加新电话号码时包含在增量文件导出中。
* 配置文件是 *非* 当任何映射的XDM字段(如 `xdm: loyalty.points`， `xdm: loyalty.tier`， `xdm: personalEmail.address` 更新了配置文件。
* 每当 `segmentMembership.status` XDM字段在目标激活工作流中进行映射，退出区段的用户档案也包含在导出的增量文件中，带有 `exited` 状态。

>[!ENDSHADEBOX]

### 决定数据导出的因素以及导出中包含的内容

根据上一节中的信息，可以按照以下所述摘要用户档案导出到基于文件的目标的行为：

**完整文件导出**

每天导出区段的完整活动群体。

| 决定目标导出的因素 | 导出文件中包含的内容 |
|---------|----------|
| <ul><li>在UI或API中设置的导出计划以及用户操作(选择 [立即导出文件](/help/destinations/ui/export-file-now.md) 在UI中或使用 [临时激活API](/help/destinations/api/ad-hoc-activation-api.md))确定目标导出的开始时间。</li></ul> | 在完整文件导出中，根据最新的区段评估，区段的整个活动用户档案人口将包含在每个文件导出中。 每个为导出选择的XDM属性的最新值也作为列包含在每个文件中。 请注意，处于退出状态的配置文件不包括在文件导出中。 |

{style="table-layout:fixed"}

**增量文件导出**

在设置激活工作流后的第一个文件导出中，将导出区段的整个群体。 在后续的导出中，只导出修改后的用户档案。

| 决定目标导出的因素 | 导出文件中包含的内容 |
|---------|----------|
| <ul><li>UI或API中设置的导出计划决定了目标导出的开始。</li><li>无论用户档案是否符合区段的条件，对其区段成员资格所做的任何更改都会使用户档案符合包含在增量导出中的条件。 配置文件的属性或标识映射中的更改 *不要* 限定要包含在增量导出中的用户档案。</li></ul> | <p>区段成员资格已更改的用户档案，以及每个选定导出的XDM属性的最新信息。</p><p>如果符合以下条件，则具有退出状态的配置文件将包含在目标导出中： `segmentMembership.status` 在映射步骤中选择XDM字段。</p> |

{style="table-layout:fixed"}

>[!TIP]
>
>提醒一下，配置文件的属性值或标识映射中的更改不符合将配置文件包含在增量文件导出中的条件。

## 后续步骤 {#next-steps}

在阅读本文档后，您现在了解了向流、企业和基于文件的目标的配置文件导出中会看到哪些内容。

接下来，您可以阅读有关如何 [身份已处理](/help/destinations/how-destinations-work/identity-handling.md) 在激活工作流中。
