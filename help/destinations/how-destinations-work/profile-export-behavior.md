---
title: 配置文件导出行为
description: 了解在Experience Platform目标中支持的各种集成模式之间，配置文件导出行为如何变化。
exl-id: 2be62843-0644-41fa-a860-ccd65472562e
source-git-commit: e6545dfaf5c43ac854986cfdc4f5cb153a07405b
workflow-type: tm+mt
source-wordcount: '2924'
ht-degree: 0%

---

# 不同目标类型的配置文件导出行为

Experience Platform中有多种目标类型，如下图所示。 这些目标在触发目标导出以及导出中包括的内容方面略有不同，如下面的部分所述。

>[!IMPORTANT]
>
>本文档页面仅介绍图表底部高亮显示的连接的配置文件导出行为。

![目标类型图表](/help/destinations/assets/how-destinations-work/types-of-destinations-v4.png)

## 流式目标中的消息聚合

在深入了解每种目标类型的特定信息之前，了解以下各项的消息聚合概念很重要： *流目标*.

Experience Platform目标会以HTTPS调用的形式将数据导出到基于API的集成。 一旦其他上游服务通知目标服务由于批量摄取、流式摄取、批量分段、流式分段或身份图更改而更新了用户档案，数据将被导出并发送到流式目标。

用户档案在发送到目标API端点之前会聚合到HTTPS消息中。

获取 [facebook目标](/help/destinations/catalog/social/facebook.md) 带有 *[可配置聚合](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)* 例如，策略 — 数据以聚合方式发送，其中目标服务从配置文件服务获取上游的所有传入数据，并在将其调度到Facebook之前按以下方式之一聚合这些数据：

* 记录数（最多10,000）或
* 时间窗口间隔（300秒）

首次满足上述阈值的任何一个都会触发导出到Facebook的操作。 因此，在 [!DNL Facebook Custom Audiences] 在功能板中，您可能会看到以10,000条记录增量从Experience Platform中输入的受众。 您可能会每2-3分钟看到10,000条记录，因为处理和聚合数据的速度比300秒导出间隔快，而且发送速度也快，所以大约每2-3分钟就会处理一次所有记录。 如果没有足够的记录来构成10,000批，则当前记录数将按满足时间窗口阈值时的方式发送，因此您也可能会看到发送到Facebook的较小批。

作为另一个示例，请考虑 [HTTP API目标](/help/destinations/catalog/streaming/http-destination.md)，它具有 *[最大努力聚合](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)* 策略，使用 `maxUsersPerRequest: 10`. 这意味着，在触发对此目标的HTTP调用之前，最多将汇总10个配置文件，但Experience Platform会在目标服务收到来自上游服务的更新重新评估信息后立即尝试将配置文件调度到目标。

聚合策略是可配置的，目标开发人员可以决定如何配置聚合策略以最好地满足下游API端点的速率限制。 详细了解 [聚合策略](../destination-sdk/functionality/destination-configuration/aggregation-policy.md) 在Destination SDK文档中。

## 流配置文件导出（企业）目标 {#streaming-profile-destinations}

>[!IMPORTANT]
>
> 企业目标仅适用于 [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 客户。

此 [企业目标](/help/destinations/destination-types.md#streaming-profile-export) Experience Platform包括Amazon Kinesis、Azure事件中心和HTTP API。

Experience Platform可优化将配置文件导出到企业目标的行为，以便仅在符合受众资格或其他重要事件后对配置文件进行了相关更新时将数据导出到API端点。 在以下情况下，会将配置文件导出到您的目标：

* 配置文件更新由中的更改决定 [受众会员资格](/help/xdm/field-groups/profile/segmentation.md) 至少一个映射到目标的受众。 例如，配置文件已符合映射到目标的其中一个受众的条件，或已退出映射到目标的其中一个受众。
* 用户档案更新由 [身份映射](/help/xdm/field-groups/profile/identitymap.md). 例如，对于已经符合映射到目标的其中一个受众资格的用户档案，在身份映射属性中添加了一个新身份。
* 配置文件更新由映射到目标的至少一个属性的更改确定。 例如，将映射步骤中映射到目标的某个属性添加到配置文件中。

在上述所有情况中，只会将已发生相关更新的用户档案导出到您的目标。 例如，如果映射到目标流的受众具有一百个成员，并且有五个新配置文件符合该区段的条件，则导出到目标的操作将以增量方式进行，并且只包括五个新配置文件。

请注意，所有映射的属性都会导出到配置文件，无论更改位于何处。 因此，在上面的示例中，将导出这五个新配置文件的所有映射属性，即使属性本身未发生更改也是如此。

### 决定数据导出的因素以及导出中包含的内容

对于为给定用户档案导出的数据，了解 *决定数据导出到企业目标的因素* 和 *哪些数据包含在导出中*.

| 决定目标导出的因素 | 目标导出中包含的内容 |
|---------|----------|
| <ul><li>映射的属性和受众会作为目标导出的提示。 这意味着，如果任何映射的受众更改状态(从 `null` 到 `realized` 或从 `realized` 到 `exiting`)或者更新任何映射的属性，则将会启动目标导出。</li><li>由于身份当前无法映射到企业目标，因此给定配置文件上任何身份的更改也将决定目标导出。</li><li>属性的更改被定义为属性上的任何更新，无论其是否为相同的值。 这意味着即使值本身未发生更改，也会将覆盖属性视为更改。</li></ul> | <ul><li>此 `segmentMembership` 对象包括在激活数据流中映射的受众，对于该受众，在资格或受众退出事件后，用户档案的状态已发生更改。 请注意，如果配置文件符合条件的其他未映射受众属于同一受众，则这些受众也可以作为目标导出的一部分 [合并策略](/help/profile/merge-policies/overview.md) 与激活数据流中映射的受众相同。 </li><li>中的所有标识 `identityMap` 对象也包含在内(Experience Platform当前不支持企业目标中的标识映射)。</li><li>目标导出中只包含映射的属性。</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>将用户档案激活到目标时，企业目标会流式传输回填数据。 这意味着在将激活工作流配置到目标之后，首次数据导出将包括符合激活受众条件的用户档案，然后该受众将映射到目标。

>[!BEGINSHADEBOX]

例如，考虑将此数据流映射到HTTP目标，其中在数据流中选择了三个受众，并且四个属性映射到目标。

![企业目标数据流](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

导出到目标的配置文件可由符合或退出其中一个配置文件来确定 *三个映射区段*. 但是，在数据导出中，将 `segmentMembership` 对象时，如果该特定配置文件是其他未映射受众的成员，并且这些受众与触发导出的受众共享相同的合并策略，则可能会显示其他未映射受众。 如果配置文件符合 **拥有DeLorean Cars的客户** 受众，但同时也是 **看了《回到未来》的电影** 和 **科幻迷们** 然后，其他这两个受众也将出现在中 `segmentMembership` 数据导出的对象，即使这些对象未在数据流中映射，只要它们与共享相同的合并策略 **拥有DeLorean Cars的客户** 区段。

从配置文件属性的角度来看，对上述四个映射属性所做的任何更改都将决定目标导出，并且配置文件中存在的四个映射属性中的任何一个都会出现在数据导出中。

>[!ENDSHADEBOX]

>[!TIP]
>
> 您可以在中查看导出到各种企业目标的数据的示例。 [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md#exported-data)， [Azure事件中心](/help/destinations/catalog/cloud-storage/azure-event-hubs.md#exported-data)、和 [HTTP API](/help/destinations/catalog/streaming/http-destination.md#exported-data) 目标文档页面。

## 基于API的流目标 {#streaming-api-based-destinations}

流式目标(如Facebook、Trade Desk和其他基于API的集成)的配置文件导出行为与上述企业目标的行为非常相似。

流目标的示例是属于 [社交和广告类别](/help/destinations/destination-types.md#categories) 在目录中。

Experience Platform会优化将配置文件导出到您的流目标的行为，以便仅在符合受众资格或其他重要事件后对配置文件进行了相关更新时，将数据导出到基于流API的目标。 在以下情况下，会将配置文件导出到您的目标：

* 配置文件更新由中的更改决定 [受众会员资格](/help/xdm/field-groups/profile/segmentation.md) 至少一个映射到目标的受众。 例如，配置文件已符合映射到目标的其中一个受众的条件，或已退出映射到目标的其中一个受众。
* 用户档案更新由 [身份映射](/help/xdm/field-groups/profile/identitymap.md) 对于标记为导出此目标实例的身份命名空间。 例如，对于已经符合映射到目标的其中一个受众资格的用户档案，在身份映射属性中添加了一个新身份。
* 配置文件更新由映射到目标的至少一个属性的更改确定。 例如，将映射步骤中映射到目标的某个属性添加到配置文件中。
* 在配置自动同意实施并且用户档案选择退出后，用户档案的同意会发生更改。 自动同意实施会将受众退出事件发送到目标，因此该配置文件不会包含在目标的任何定位中。

在上述所有情况中，只会将已发生相关更新的用户档案导出到您的目标。 例如，如果映射到目标流的受众具有一百个成员，并且有五个新配置文件符合该区段的条件，则导出到目标的操作将以增量方式进行，并且只包括五个新配置文件。

请注意，所有映射的属性都会导出到配置文件，无论更改位于何处。 因此，在上面的示例中，将导出这五个新配置文件的所有映射属性，即使属性本身未发生更改也是如此。

### 决定数据导出的因素以及导出中包含的内容

有关为给定用户档案导出的数据，请务必了解决定数据导出到流API目标的两个不同概念，以及导出中包含哪些数据。

| 决定目标导出的因素 | 目标导出中包含的内容 |
|---------|----------|
| <ul><li>映射的属性和受众会作为目标导出的提示。 这意味着，如果任何映射的受众更改状态(从 `null` 到 `realized` 或从 `realized` 到 `exiting`)或者更新任何映射的属性，则将会启动目标导出。</li><li>标识映射中的更改被定义为添加/删除的标识 [身份图](/help/identity-service/ui/identity-graph-viewer.md) ，用于映射为导出的身份命名空间。</li><li>对于映射到目标的属性，属性的更改被定义为属性上的任何更新。</li></ul> | <ul><li>映射到目标且已更改的受众将包含在 `segmentMembership` 对象。 在某些情况下，它们可能会使用多个调用导出。 此外，在某些情况下，某些未更改的受众也可能包含在调用中。 在任何情况下，仅导出映射的受众。</li><li>命名空间中映射到目标的所有身份 `identityMap` 对象也包含在内。</li><li>目标导出中只包含映射的属性。</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>将用户档案激活到目标时，流API目标会流式回填数据。 这意味着在将激活工作流配置到目标之后，首次数据导出将包括符合激活受众条件的用户档案，然后该受众将映射到目标。

>[!BEGINSHADEBOX]

例如，将此数据流考虑到一个在数据流中选择了三个受众的流目标。

![流式目标数据流](/help/destinations/assets/how-destinations-work/streaming-destination-example-dataflow.png)

导出到目标的配置文件可由符合或退出三个映射区段之一的配置文件来确定。 如果配置文件符合 **拥有DeLorean Cars的客户** 区段，这将触发导出。 其他受众(**城市 — 达拉斯** 和 **基本站点活动**)也可以导出，以防用户档案中的受众显示为可能状态之一(`realized` 或 `exited`)。 未映射的受众(如 **科幻迷们**)将不会导出。

从配置文件属性的角度来看，对上述三个映射属性所做的任何更改都将决定目标导出。

>[!ENDSHADEBOX]

## 批处理（基于文件）目标 {#file-based-destinations}

将用户档案导出到时 [基于文件的目标](/help/destinations/destination-types.md#file-based) 在Experience Platform中，有三种类型的计划（如下所列）和两种文件导出选项（完整或增量文件）可供您使用。 所有这些设置都是在受众级别上设置的，即使多个受众映射到单个目标数据流也是如此。

* 计划导出：配置一个目标，添加一个或多个区段，选择要导出完整文件或增量文件，并选择每天的设置时间或每天应导出文件的几次。 例如，下午5点的导出时间意味着下午5点将导出符合受众条件的配置文件。
* 区段评估后：在每日受众评估作业运行后立即触发导出。 这意味着文件中的导出用户档案编号尽可能接近区段的最新评估群体。
* 按需导出([立即导出文件](/help/destinations/ui/export-file-now.md))：基于最新的受众评估作业，在定期计划导出的基础上，一次性导出完整文件。

在上述任何导出情况下，导出的文件都包含符合导出条件的配置文件，以及您选择作为要导出的XDM属性的列。

>[!TIP]
>
>当流式受众映射到批处理目标时，导出文件中的配置文件数更有可能接近于区段中的用户数。 这是因为最新受众评估更接近导出时间的可能性更高。

### 增量文件导出 {#incremental-file-exports}

并非配置文件的所有更新都允许在增量文件导出中包含配置文件。 例如，如果在配置文件中添加或删除了属性，则导出中不包含该配置文件。 仅限符合以下条件的配置文件： `segmentMembership` 属性已更改将包含在导出的文件中。 换言之，仅当配置文件成为受众的一部分或从受众中删除时，它才会包含在增量文件导出中。

同样，如果将新身份（新电子邮件地址、电话号码、ECID等）添加到中的用户档案 [身份图](/help/identity-service/ui/identity-graph-viewer.md)，这并不意味着需要将该配置文件包含在新的增量文件导出中。

如果将新受众添加到目标映射，这不会影响其他区段的资格和导出。 每个受众单独配置导出计划，并且每个区段单独导出文件，即使已将受众添加到同一目标数据流也是如此。

>[!BEGINSHADEBOX]

例如，在下图所示的导出设置中（受众正在导出增量文件更新），请注意以下情况（其中配置文件是否包含在增量文件导出中）：

![导出具有多个选定属性的设置。](/help/destinations/assets/how-destinations-work/export-selection-batch-destination.png)

* 当配置文件符合或不符合区段的资格时，该配置文件会包含在增量文件导出中。
* 配置文件是 *非* 当向身份图中添加新电话号码时，包含在增量文件导出中。
* 配置文件是 *非* 当任何映射的XDM字段(如 `xdm: loyalty.points`， `xdm: loyalty.tier`， `xdm: personalEmail.address` 会在配置文件中更新。
* 每当 `segmentMembership.status` XDM字段在目标激活工作流中映射，退出受众的用户档案也包含在导出的增量文件中，带有 `exited` 状态。

>[!ENDSHADEBOX]

### 决定数据导出的因素以及导出中包含的内容

根据上一节中的信息，可以按照以下描述概括向基于文件的目标的配置文件导出行为：

**完整文件导出**

每天导出受众的全部活跃群体。

| 决定目标导出的因素 | 导出文件中包含的内容 |
|---------|----------|
| <ul><li>在UI或API中设置的导出计划以及用户操作(选择 [立即导出文件](/help/destinations/ui/export-file-now.md) 在UI中或使用 [临时激活API](/help/destinations/api/ad-hoc-activation-api.md))确定目标导出的开始时间。</li></ul> | 在完整文件导出中，每个文件导出都会包含区段的整个活动用户档案群体（基于最新的受众评估）。 每个为导出选择的XDM属性的最新值也作为列包含在每个文件中。 请注意，处于已退出状态的配置文件不会包含在文件导出中。 |

{style="table-layout:fixed"}

**增量文件导出**

在设置激活工作流后的第一个文件导出中，将导出受众的整个群体。 在后续导出中，仅导出修改后的用户档案。

| 决定目标导出的因素 | 导出文件中包含的内容 |
|---------|----------|
| <ul><li>在UI或API中设置的导出计划决定了目标导出的开始。</li><li>无论用户档案符合还是不符合区段的条件，对其受众成员资格所做的任何更改都会使用户档案符合包含在增量导出中的条件。 配置文件的属性或标识映射中的更改 *不要* 限定要包含在增量导出中的用户档案。</li></ul> | <p>受众成员资格发生更改的用户档案，以及每个选定用于导出的XDM属性的最新信息。</p><p>如果符合以下条件，则具有已退出状态的配置文件将包含在目标导出中 `segmentMembership.status` 在映射步骤中选择XDM字段。</p> |

{style="table-layout:fixed"}

>[!TIP]
>
>提醒一下，配置文件的属性值或标识映射中的更改不符合将配置文件包含在增量文件导出中的条件。

## 后续步骤 {#next-steps}

阅读本文档后，您现在了解了在向流式、企业和基于文件的目标导出配置文件时应看到的内容。

接下来，您可以阅读如何 [身份已处理](/help/destinations/how-destinations-work/identity-handling.md) 在激活工作流中。
