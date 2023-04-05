---
title: 配置文件导出行为
description: 了解配置文件导出行为在Experience Platform目标中支持的不同集成模式之间有何不同。
source-git-commit: 4d1f9fa19bd35095e3ccbd8d83bcc33dcd4c45a8
workflow-type: tm+mt
source-wordcount: '2933'
ht-degree: 0%

---

# 不同目标类型的配置文件导出行为

Experience Platform中有几种目标类型，如下图所示。 这些目标在触发目标导出的因素以及出口中包含的内容方面的导出模式略有不同，如以下各节所述。

>[!IMPORTANT]
>
>本文档页面仅描述图表底部突出显示的连接的配置文件导出行为。

![目标图类型](/help/destinations/assets/how-destinations-work/types-of-destinations-v4.png)

## 微批量处理和聚合策略

在深入研究每个目标类型的特定信息之前，请务必了解 *流目标*.

Experience Platform目标将数据导出为基于API的集成，作为HTTPS调用。 当目标服务被其他上游服务通知，配置文件已因批量摄取、流式摄取、批量分段、流式划分或身份图更改而更新时，数据即会导出并发送到流目标。

在将用户档案调度到目标API端点之前，先将用户档案聚合到HTTPS消息中的过程，将调用 *微批量*.

获取 [Facebook目标](/help/destinations/catalog/social/facebook.md) 带有 *[可配置聚合](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation)* 例如，策略 — 数据以聚合方式发送，其中目标服务会从用户档案服务上游接收所有传入数据，并按以下任一方式将其聚合，然后再将其调度到Facebook:

* 记录数（最多10.000条）或
* 时间窗口间隔（30分钟）

以上任何一个阈值最先满足时，都会导出到Facebook。 所以，在 [!DNL Facebook Custom Audiences] 功能板中，您可能会看到来自Experience Platform的受众以10.000个记录增量进入。 您可能每10-15分钟会看到10,000条记录，因为处理和汇总数据的速度比导出间隔30分钟快，发送速度也快，因此在处理所有记录之前大约每10-15分钟会看到一条记录。 如果没有足够的记录来组成10.000批，则当满足时间窗口阈值时将按原样发送当前记录数，因此您也可能会看到发送到Facebook的较小批次。

再举一个例子，请考虑 [HTTP API目标](/help/destinations/catalog/streaming/http-destination.md)，其中 *[最佳工作聚合](/help/destinations/destination-sdk/destination-configuration.md#best-effort-aggregation)* 策略， `maxUsersPerRequest: 10`. 这意味着在向此目标触发HTTP调用之前，最多将聚合10个用户档案，但是，当目标服务从上游服务收到更新的重新评估信息后，Experience Platform会尝试将用户档案调度到该目标。

聚合策略是可配置的，目标开发人员可以决定如何配置聚合策略以最好地满足下游API端点的速率限制。 有关更多信息 [聚合策略](/help/destinations/destination-sdk/destination-configuration.md#aggregation) (在Destination SDK文档中)。

## 流配置文件导出（企业）目标 {#streaming-profile-destinations}

>[!IMPORTANT]
>
> 企业目标仅可用于 [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 客户。

的 [企业目标](/help/destinations/destination-types.md#streaming-profile-export) Experience Platform中包括Amazon Kinesis、Azure事件中心和HTTP API。

Experience Platform会优化配置文件导出行为以导出到企业目标，以便仅在区段鉴别或其他重大事件之后对配置文件进行相关更新时，才将数据导出到API端点。 在以下情况下，用户档案会导出到您的目标：

* 用户档案更新由 [区段成员资格](/help/xdm/field-groups/profile/segmentation.md) ，用于映射到目标的至少一个区段。 例如，配置文件已符合映射到目标的其中一个区段的条件，或者已退出映射到目标的其中一个区段。
* 用户档案更新由 [身份映射](/help/xdm/field-groups/profile/identitymap.md). 例如，已符合映射到目标的某个区段资格条件的用户档案，已在身份映射属性中添加了新身份。
* 配置文件更新由至少一个映射到目标的属性的属性发生变化来确定。 例如，映射步骤中映射到目标的某个属性会添加到配置文件中。

在上述所有情况下，只会将发生相关更新的用户档案导出到您的目标。 例如，如果映射到目标流的区段有一百个成员，并且有五个新的配置文件符合该区段的资格条件，则导出到目标的过程将是递增的，并且仅包含五个新配置文件。

请注意，无论更改位于何处，都会导出配置文件的所有映射属性。 因此，在上例中，即使属性本身未发生更改，也会导出这五个新配置文件的所有映射属性。

### 决定数据导出的因素以及导出中包含的内容

对于为给定用户档案导出的数据，了解 *什么决定了导出到企业目标的数据* 和 *导出中包含哪些数据*.

| 决定目标导出的因素 | 目标导出中包含的内容 |
|---------|----------|
| <ul><li>映射的属性和区段可用作目标导出的提示。 这表示如果任何映射的区段更改状态(从 `null` to `realized` 或 `realized` to `exiting`)或任何映射的属性都会更新，则将开始导出目标。</li><li>由于身份当前无法映射到企业目标，因此给定配置文件中任何身份的更改也会决定目标导出。</li><li>属性的更改被定义为属性的任何更新，无论该更新是否与属性的值相同。 这意味着，即使值本身未发生更改，属性上的覆盖也会被视为更改。</li></ul> | <ul><li>的 `segmentMembership` 对象包括在激活数据流中映射的区段，在鉴别或区段退出事件后，配置文件的状态发生了更改。 请注意，如果配置文件符合条件的其他未映射区段属于同一区段，则这些区段可能属于目标导出的一部分 [合并策略](/help/profile/merge-policies/overview.md) 作为激活数据流中映射的区段。 </li><li>中的所有标识 `identityMap` 对象也包含在内(Experience Platform当前不支持企业目标中的身份映射)。</li><li>目标导出中只包含映射的属性。</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>在将用户档案激活到目标时，企业目标会流回填数据。 这意味着在将激活工作流配置到目标后首次导出数据时，将包含在区段映射到目标之前符合激活区段资格的用户档案。

>[!BEGINSHADEBOX]

例如，将此数据流视为HTTP目标，在该目标中，在数据流中选择了三个区段，并且有四个属性被映射到该目标。

![企业目标数据流](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

导出到目标的用户档案，可由符合或退出 *三个映射的区段*. 但是，在数据导出中， `segmentMembership` 对象，则可能会显示其他未映射的区段，如果该特定配置文件是其成员，并且这些区段与触发导出的区段共享相同的合并策略。 如果用户档案符合 **使用德罗林汽车的客户** 区段，但亦为 **观看了《回到未来》的电影** 和 **科幻迷** 区段，则另外两个区段也将显示在 `segmentMembership` 数据导出对象，即使这些对象未在数据流中映射，但前提是它们与 **使用德罗林汽车的客户** 区段。

从配置文件属性的角度来看，对上述四个映射属性所做的任何更改都将决定目标导出，并且配置文件上存在的四个映射属性中的任何一个将出现在数据导出中。

>[!ENDSHADEBOX]

>[!TIP]
>
> 您可以在 [AmazonKinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md#exported-data), [Azure事件中心](/help/destinations/catalog/cloud-storage/azure-event-hubs.md#exported-data)和 [HTTP API](/help/destinations/catalog/streaming/http-destination.md#exported-data) 目标文档页面。

## 基于流API的目标 {#streaming-api-based-destinations}

流目标(如Facebook、交易台和其他基于API的集成)的配置文件导出行为与上述企业目标的行为非常相似。

流目标的示例包括 [社交和广告类别](/help/destinations/destination-types.md#categories) 中。

Experience Platform会优化配置文件导出行为以将数据导出到您的流目标，以便仅在区段鉴别或其他重大事件之后对配置文件进行相关更新时，才将数据导出到基于流API的目标。 在以下情况下，用户档案会导出到您的目标：

* 用户档案更新由 [区段成员资格](/help/xdm/field-groups/profile/segmentation.md) ，用于映射到目标的至少一个区段。 例如，配置文件已符合映射到目标的其中一个区段的条件，或者已退出映射到目标的其中一个区段。
* 用户档案更新由 [身份映射](/help/xdm/field-groups/profile/identitymap.md) 标识命名空间，标记为为此目标实例导出。 例如，已符合映射到目标的某个区段资格条件的用户档案，已在身份映射属性中添加了新身份。
* 配置文件更新由至少一个映射到目标的属性的属性发生变化来确定。 例如，映射步骤中映射到目标的某个属性会添加到配置文件中。
* 配置了自动同意强制并选择禁用配置文件时，配置文件的同意更改。 自动执行同意会将受众退出事件发送到目标，以便该用户档案不会包含在目标的任何定位中。

在上述所有情况下，只会将发生相关更新的用户档案导出到您的目标。 例如，如果映射到目标流的区段有一百个成员，并且有五个新的配置文件符合该区段的资格条件，则导出到目标的过程将是递增的，并且仅包含五个新配置文件。

请注意，无论更改位于何处，都会导出配置文件的所有映射属性。 因此，在上例中，即使属性本身未发生更改，也会导出这五个新配置文件的所有映射属性。

### 决定数据导出的因素以及导出中包含的内容

关于为给定用户档案导出的数据，请务必了解以下两个不同的概念：哪些概念决定了要将数据导出到流API目标，哪些数据包含在导出中。

| 决定目标导出的因素 | 目标导出中包含的内容 |
|---------|----------|
| <ul><li>映射的属性和区段可用作目标导出的提示。 这表示如果任何映射的区段更改状态(从 `null` to `realized` 或 `realized` to `exiting`)或任何映射的属性都会更新，则将开始导出目标。</li><li>身份映射中的更改被定义为为 [身份图](/help/identity-service/ui/identity-graph-viewer.md) 的名称，用于映射以导出的身份命名空间。</li><li>属性的更改被定义为属性的任何更新，即映射到目标的属性的更新。</li></ul> | <ul><li>映射到目标且已更改的区段将包含在 `segmentMembership` 对象。 在某些情况下，可能会使用多个调用导出这些调用。 此外，在某些情况下，某些未更改的区段也可能包含在调用中。 无论如何，只会导出映射的区段。</li><li>命名空间中映射到 `identityMap` 对象。</li><li>目标导出中只包含映射的属性。</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>在将用户档案激活到目标时，流式API目标会流回填数据。 这意味着在将激活工作流配置到目标后首次导出数据时，将包含在区段映射到目标之前符合激活区段资格的用户档案。

>[!BEGINSHADEBOX]

例如，将此数据流视为在数据流中选择三个区段的流目标。

![流目标数据流](/help/destinations/assets/how-destinations-work/streaming-destination-example-dataflow.png)

导出到目标的配置文件取决于符合三个映射区段之一资格或退出该区段的配置文件。 如果某个用户档案符合 **使用德罗林汽车的客户** 区段，这将触发导出。 其他分段(**城市 — 达拉斯** 和 **基本活动网站**)，以防该区段具有以下可能的状态之一(`realized` 或 `exited`)。 未映射的区段(如 **科幻迷**)。

从配置文件属性的角度来看，对上述三个属性所做的任何更改都将决定目标导出。

>[!ENDSHADEBOX]

## 批量（基于文件）目标 {#file-based-destinations}

将用户档案导出到 [基于文件的目标](/help/destinations/destination-types.md#file-based) 在Experience Platform中，有三种类型的计划（如下所列）和两种文件导出选项（完整或增量文件）可供您使用。 所有这些设置都是在区段级别设置的，即使当多个区段映射到单个目标数据流时也是如此。

* 计划导出：配置目标、添加一个或多个区段、选择是要导出完整文件还是增量文件，然后选择设置的时间（每天一次）或每天几次应导出文件。 例如，下午5点导出时间意味着任何符合区段资格条件的用户档案都将在下午5点导出。
* 进行分段评估后：在运行每日区段评估作业后，会立即触发导出。 这意味着文件中导出的配置文件编号与区段的最新评估群体尽可能接近。
* 按需导出([立即导出文件](/help/destinations/ui/export-file-now.md)):根据最新的区段评估作业，完整文件将基于定期计划导出一次性导出。

在以上任何导出情况中，导出的文件包括符合导出条件的配置文件，以及您选择作为XDM属性进行导出的列。

>[!TIP]
>
>将流区段映射到批处理目标后，导出文件中的用户档案数量更有可能与区段中的用户数量更接近。 这是因为，最新区段评估更有可能接近导出时间。

### 增量文件导出 {#incremental-file-exports}

配置文件的所有更新并非使配置文件有资格包含在增量文件导出中。 例如，如果向配置文件添加属性或从配置文件中删除属性，则该属性在导出中不包含配置文件。 仅限 `segmentMembership` 属性已更改将包含在导出的文件中。 换言之，仅当用户档案成为区段的一部分或从区段中删除时，它才会包含在增量文件导出中。

同样，如果向 [身份图](/help/identity-service/ui/identity-graph-viewer.md)，则不表示将配置文件包含在新增量文件导出中的原因。

如果将新区段添加到目标映射，则不会影响另一个区段的资格和导出。 导出计划是针对每个区段单独配置的，并且每个区段的文件都会单独导出，即使已将区段添加到同一目标数据流中也是如此。

>[!BEGINSHADEBOX]

例如，在下图的导出设置中，如果区段正在导出增量文件更新，请注意以下情况，即配置文件是否包含在增量文件导出中：

![导出设置。](/help/destinations/assets/how-destinations-work/export-selection-batch-destination.png)

* 当配置文件符合或不符合区段的条件时，配置文件会包含在增量文件导出中。
* 用户档案是 *not* 将新电话号码添加到身份图时，包含在增量文件导出中。
* 用户档案是 *not* 当任何映射的XDM字段(如 `xdm: loyalty.points`, `xdm: loyalty.tier`, `xdm: personalEmail.address` 更新了用户档案。
* 只要 `segmentMembership.status` XDM字段已映射到目标激活工作流，退出区段的配置文件也会包含在导出的增量文件中，并且 `exited` 状态。

>[!ENDSHADEBOX]

### 决定数据导出的因素以及导出中包含的内容

根据上节中的信息，可将用户档案导出到基于文件的目标的行为概述如下：

**完整文件导出**

区段的完全活动群体会每天导出。

| 决定目标导出的因素 | 导出文件中包含的内容 |
|---------|----------|
| <ul><li>UI或API中设置的导出计划以及用户操作(选择 [立即导出文件](/help/destinations/ui/export-file-now.md) 或使用 [临时激活API](/help/destinations/api/ad-hoc-activation-api.md))确定目标导出的开始。</li></ul> | 在完整文件导出中，每个文件导出中都包含基于最新区段评估的区段的整个活动配置文件群体。 选择导出的每个XDM属性的最新值也作为列包含在每个文件中。 请注意，处于退出状态的用户档案未包含在文件导出中。 |

{style="table-layout:fixed"}

**增量文件导出**

在设置激活工作流后的第一个文件导出中，将导出区段的全部群体。 在后续导出中，仅导出已修改的用户档案。

| 决定目标导出的因素 | 导出文件中包含的内容 |
|---------|----------|
| <ul><li>UI或API中设置的导出计划可确定目标导出的开始。</li><li>配置文件的区段成员资格的任何更改（无论其是否符合区段的资格条件）均可使配置文件包含在增量导出中。 配置文件的属性或身份映射中的更改 *不* 确定要包含在增量导出中的配置文件。</li></ul> | <p>区段成员资格已更改的配置文件，以及选择导出的每个XDM属性的最新信息。</p><p>目标导出中包含已退出状态的用户档案(如果 `segmentMembership.status` 在映射步骤中选择XDM字段。</p> |

{style="table-layout:fixed"}

>[!TIP]
>
>请注意，配置文件的属性值或身份映射中的更改不会使配置文件有资格包含在增量文件导出中。

## 后续步骤 {#next-steps}

阅读本文档后，您现在知道在向流、企业和基于文件的目标的配置文件导出中应看到什么。

接下来，您可以阅读 [身份处理](/help/destinations/how-destinations-work/identity-handling.md) 激活工作流中。
