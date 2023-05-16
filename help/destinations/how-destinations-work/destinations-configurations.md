---
title: 目标中的可配置和常用导出设置
description: 了解目标中的哪些导出设置可以在目标级别进行配置，哪些是固定的且无法编辑的。
exl-id: 3f4706cb-6d51-4567-81f6-5b2bf167b576
source-git-commit: a0400ab255b3b6a7edb4dcfd5c33a0f9e18b5157
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 0%

---

# 目标中的可配置和常用导出设置

在考虑将导出行为导出到Experience Platform目标时，您需要考虑三个不同的级别，这三个级别是配置采取行动的。

* 在第一个级别，与配置文件导出行为和配置设置相关的某些设置在属于目标类型的所有目标中都是通用的。 这些设置是指触发目标导出的因素，以及导出中包含的因素，这些因素无法由目标开发人员或实时CDP用户编辑。
* 在第二个级别上，当使用Destination SDK创作目标时，目标开发人员可以在目标级别自定义某些设置。
* 在第三级，实时CDP用户可以在激活工作流中设置一些配置设置。

![显示目标的常见和可配置导出设置之间相互作用的图表](/help/destinations/assets/how-destinations-work/profile-export-behavior-diagram.png)

本页介绍或链接到上述三个级别上目标的所有常用和可配置导出设置。

## 目标类型中的常见导出设置 {#common-settings-across-destination-types}

目标导出行为在属于目标类型的目标中与 *触发目标导出的因素* 和 *目标导出中包含的内容*. 目标导出由目标服务从 [上游实时客户资料服务](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=en#adobe-experience-platform-%26-applications-detailed-architecture-diagram).

目标导出中包含的内容因目标类型而略有不同。 有关 [每个目标类型的常见导出行为模式](/help/destinations/how-destinations-work/profile-export-behavior.md). 目标开发人员或实时CDP用户无法编辑这些设置。

## 目标开发人员可自定义的导出设置 {#customizable-settings-by-destination-developers}

目标开发人员可以使用 [Destination SDK](/help/destinations/destination-sdk/overview.md) 创建自定义或产品化（私有或公共）目标。 Destination SDK为开发人员提供了极大的灵活性，可以根据其API端点和文件接收系统的下游功能配置目标。 根据下游功能，目标开发人员在使用Destination SDK配置目标时可使用以下配置选项：

* 确定哪些属性和标识可以从Experience Platform导出到目标。 还确定目标需要哪些身份才能成功导出数据。
* 设置聚合策略，该策略可确定在聚合要发送到API集成的HTTP消息时，Experience Platform应等待多长时间。 目标开发人员可以配置不同的聚合类型，以确定传出HTTP消息中应包含多少个配置文件，以及Experience Platform应等待多长时间直到调度HTTP消息。 查找有关 [聚合策略配置选项](../destination-sdk/functionality/destination-configuration/aggregation-policy.md) 目标开发人员可在Destination SDK文档中找到。
* 确定HTTP消息导出是否应包含符合区段资格的配置文件、从区段中删除的配置文件，或者是同时包含这两者。
* 确定用户在导出文件时应使用的文件名和文件格式配置。

## 用户可自定义的数据流级别的设置 {#settings-on-dataflow-level}

除了依赖于目标类型和目标开发人员配置的设置的不可编辑设置之外，用户还可以在激活工作流中配置某些导出设置。 这些设置与特定数据流到目标的导出计划、应在数据流中导出的属性和标识字段，或导出文件的文件格式选项相关。

连接到目标时用户可用的设置取决于目标开发人员如何配置目标以及它们为用户提供哪些设置。

例如， [流目标](/help/destinations/destination-types.md#streaming-destinations)，则目标开发人员可以配置其目标接受的标识，并且在 [激活工作流的映射步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)，如下所示：

![在激活工作流的映射步骤中，屏幕记录目标字段的标识选择。 ](/help/destinations/assets/how-destinations-work/identity-mapping-example.gif)

同样，对于 [基于文件的目标](/help/destinations/destination-types.md#file-based)，目标开发人员可以确定 [文件名附加选项](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) 他们希望提供到其目的地，或 [文件格式选项](/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md) 他们希望可用，并且用户只能从这些选项中进行选择，如下所示：

![连接到基于文件的目标时，屏幕记录文件格式选项。](/help/destinations/assets/how-destinations-work/file-formatting-options.gif)

![在激活工作流的计划步骤中，屏幕记录文件名附加选项。 ](/help/destinations/assets/how-destinations-work/filename-append-options.gif)

有关激活工作流中可用的不同选项和步骤的更多信息，请参阅：

* [激活受众数据以批量配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md)
* [将受众数据激活到企业目标](/help/destinations/ui/activate-streaming-profile-destinations.md)
* [将受众数据激活到流区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)
* [按需将文件导出到批处理目标](/help/destinations/ui/export-file-now.md)
* [（测试版）将数据集导出到云存储目标](/help/destinations/ui/export-datasets.md)

## 后续步骤 {#next-steps}

阅读本文档后，您现在知道目标的哪些导出设置在各个目标类型中是通用的，开发人员可以在单个目标级别配置这些设置，以及用户可以在激活工作流中编辑哪些设置。

接下来，您可以阅读有关 [每个目标类型的常见导出行为模式](/help/destinations/how-destinations-work/profile-export-behavior.md).

对于目标开发人员，您可以 [入门](/help/destinations/destination-sdk/getting-started.md) Destination SDK。 对于要激活数据的用户，您可以在 [目录](/help/destinations/catalog/overview.md).
