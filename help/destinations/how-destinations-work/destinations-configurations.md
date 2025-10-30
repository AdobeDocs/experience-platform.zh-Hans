---
title: 目标中的可配置和常用导出设置
description: 了解目标中的哪些导出设置可在目标级别配置，哪些是固定的，无法编辑。
exl-id: 3f4706cb-6d51-4567-81f6-5b2bf167b576
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# 目标中的可配置和常用导出设置

在考虑导出到Experience Platform目标的行为时，您需要考虑三个单独的级别来决定配置行为。

* 在第一个级别，与配置文件导出行为和配置设置相关的某些设置对于属于某个目标类型的所有目标都是通用的。 这些设置引用了触发目标导出的内容以及导出中包含的、目标开发人员或Real-Time CDP用户无法编辑的内容。
* 在第二级别，目标开发人员在使用Destination SDK创作目标时，可以在目标级别自定义某些设置。
* 在第三层，Real-Time CDP用户可以在激活工作流中设置配置设置。

![显示目标的常用导出设置与可配置导出设置之间交互作用的图表](/help/destinations/assets/how-destinations-work/profile-export-behavior-diagram.png)

本页介绍或链接到上面列出的三个级别上的目标的所有常用和可配置的导出设置。

## 各种目标类型通用的导出设置 {#common-settings-across-destination-types}

对于属于某个目标类型的目标，有关&#x200B;*触发目标导出的内容*&#x200B;以及&#x200B;*目标导出中包含的内容*，目标导出行为是一致的。 目标导出由目标服务从[上游实时客户档案服务](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html#adobe-experience-platform-%26-applications-detailed-architecture-diagram)收到的通知触发。

目标导出中包含的内容因目标类型而异。 详细了解每个目标类型[的](/help/destinations/how-destinations-work/profile-export-behavior.md)常见导出行为模式。 目标开发人员或Real-Time CDP用户无法编辑这些设置。

## 目标开发人员可自定义的导出设置 {#customizable-settings-by-destination-developers}

目标开发人员可以使用[Destination SDK](/help/destinations/destination-sdk/overview.md)创建自定义或生产（私有或公共）目标。 Destination SDK为开发人员提供了极大的灵活性，使他们能够根据其API端点和文件接收系统的下游功能配置目标。 基于下游功能，在使用Destination SDK配置目标时，目标开发人员具有以下可用配置选项：

* 确定可将哪些属性和身份从Experience Platform导出到目标。 还确定成功导出数据所需的目标身份。
* 设置聚合策略，该策略可确定Experience Platform在聚合要发送到API集成的HTTP消息时应等待的时长。 目标开发人员可以配置不同的聚合类型，以确定传出HTTP消息中应包含多少个配置文件，以及Experience Platform在调度HTTP消息之前应等待多长时间。 在Destination SDK文档中查找有关目标开发人员可用的[聚合策略配置选项](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)的详细信息。
* 确定HTTP消息导出应包含符合区段条件的用户档案、从区段中删除的用户档案，还是同时包含这两个用户档案。
* 确定在导出文件时用户应该可以使用哪些文件名和文件格式配置。

## 数据流级别上的设置可由用户自定义 {#settings-on-dataflow-level}

在取决于目标类型和目标开发人员配置的设置的不可编辑设置之外，用户可以在激活工作流中配置某些导出设置。 这些设置与特定数据流导出到目标的计划、应导出到数据流中的属性和标识字段，或导出文件的文件格式设置选项有关。

用户在连接到目标时可用的设置取决于目标开发人员配置目标的方式，以及他们为用户提供的设置。

例如，对于[流式目标](/help/destinations/destination-types.md#streaming-destinations)，目标开发人员可以配置其目标接受哪些标识，并且仅在激活工作流[的](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)映射步骤中向用户显示这些标识，如下所示：

![在激活工作流的映射步骤中录制目标字段的标识选择。](/help/destinations/assets/how-destinations-work/identity-mapping-example.gif)

同样，对于[基于文件的目标](/help/destinations/destination-types.md#file-based)，目标开发人员可以确定要为其目标提供可用的[文件名附加选项](/help/destinations/ui/activate-batch-profile-destinations.md#file-names)，或者要为其提供可用的[文件格式选项](/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md)，用户只能从这些选项中进行选择，如下所示：

![连接到基于文件的目标时，对文件格式选项进行屏幕录制。](/help/destinations/assets/how-destinations-work/file-formatting-options.gif)

![在激活工作流的计划步骤中录制文件名附加选项。](/help/destinations/assets/how-destinations-work/filename-append-options.gif)

详细了解激活工作流中可用的不同选项和步骤：

* [将受众数据激活到批量配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md)
* [将受众数据激活到企业目标](/help/destinations/ui/activate-streaming-profile-destinations.md)
* [将受众数据激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)
* [按需将文件导出到批处理目标](/help/destinations/ui/export-file-now.md)
* [将数据集导出到云存储目标](/help/destinations/ui/export-datasets.md)

## 后续步骤 {#next-steps}

阅读本文档后，您现在知道哪些目标的导出设置是目标类型中通用的，哪些可由开发人员在单个目标级别配置，以及哪些设置可由用户在激活工作流中编辑。

接下来，您可以阅读有关每个目标类型[的](/help/destinations/how-destinations-work/profile-export-behavior.md)常见导出行为模式的更多详细信息。

对于目标开发人员，您可以[开始使用Destination SDK](/help/destinations/destination-sdk/getting-started.md)。 对于希望激活数据的用户，您可以签出[目录](/help/destinations/catalog/overview.md)中的所有可用目标。
