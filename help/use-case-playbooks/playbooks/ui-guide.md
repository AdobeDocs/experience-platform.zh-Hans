---
solution: Experience Platform
title: 教战手册UI指南
description: 了解如何使用Experience PlatformUI查看和启用行动手册。
badgeBeta: label="Beta" type="Informative"
source-git-commit: 63ea852ca9f9a45d1c071fd1033cbd44cbb427c6
workflow-type: tm+mt
source-wordcount: '1307'
ht-degree: 1%

---


# （测试版）如何启用和重复使用剧本

>[!AVAILABILITY]
>
>此功能当前为测试版，并非对所有用户都可用。 文档和功能可能会发生变化。

要使用行动手册，请导航到 **[!UICONTROL 用例行动手册] > [!UICONTROL 行动手册]**. 浏览并使用页面上的各种搜索和筛选选项，选择并开始使用特定的行动手册。

## 搜索和过滤 {#search-and-filter}

使用页面上提供的搜索窗口和过滤器查找适合您用例的剧本。

例如，您可以根据营销漏斗中要定位的阶段（转化、参与或维系）筛选可以使用的行动手册。 您还可以按您所属的行业或您有权访问的产品权利(Adobe Journey Optimizer或Real-time CDP)筛选显示的行动手册。

![按营销漏斗、行业或产品过滤行动手册](/help/use-case-playbooks/assets/playbooks/ui-guide/filter-by-funnel-industry-product.gif)

您还可以使用搜索功能找到适合您的剧本。 请参阅下面的示例，了解如何查找可帮助您与可能放弃其购物车的用户互动的行动手册。

![与可能放弃购物车的用户接洽。](/help/use-case-playbooks/assets/playbooks/ui-guide/engage-abandoned-cart.gif)

或者，您可以按计划用于联系客户的渠道筛选可用的行动手册，如下所示：

![按渠道筛选](/help/use-case-playbooks/assets/playbooks/ui-guide/channel-select-filter.gif)

尝试使用过滤器和搜索选项，并为您找到合适的剧本。

## 查看行动手册并生成资源 {#view-playbook-generate-assets}

在确定剧本并创建其实例之前，您应该检查它以确保它符合您的需求。 为了帮助您更好地了解它们涵盖的用例，所有行动手册都包含以下部分。 当您准备好继续并生成资源时，请选择 **[!UICONTROL 创建实例]**.

### 思维导图 {#mindmap}

使用剧本中的思维导图部分了解剧本可以帮助您解决的工作流步骤。 从用例中定位的角色的角度可视化所有生成的对象如何帮助您实现用例的流程。

思维导图首先定义用户旅程中可访问的人员，并描述通过Adobe投放某些内容（如新消息或提醒）时，或者目标角色执行了某些操作后触发了下一个消息或事件，则会在每个步骤进行描述。

![强调行动手册思维导图。](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-mindmap.png)


### 概要 {#summary}

Inspect的“摘要”部分，了解从行动手册中创建实例后生成的资产。 为每个剧本生成的资产根据剧本启用的用例进行定制。 获取以下有关摘要部分中所有项目的更多信息。

| 项目 | 描述 |
---------|----------|
| **[!UICONTROL 目标受众]** | 描述您希望通过此用例剧本接触到的角色。 |
| **[!UICONTROL 营销渠道]** | 描述用于访问剧本中目标角色的渠道。 |
| **[!UICONTROL 技术资产]** | 创建剧本实例后生成的技术资产列表。 生成的资源因剧本而异，具体取决于用例。 某些行动手册可能会生成架构、区段和历程。 其他人可能会生成目标。 请参阅 [了解生成的资源](#understand-assets) 部分，以了解有关如何使用和重用生成的资产的更多信息。 |

{style="table-layout:auto"}

![突出显示的Playbook摘要](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-summary.png)

### 实例 {#instances}

向下滚动到实例部分，获取您或您的团队成员已创建的本Playbook实例的概述。 您可以使用各种控件对显示的实例进行排序和过滤，例如，仅查看由您创建的实例。 您还可以看到有关每个实例的各种信息，如下所列。

| 项目 | 描述 |
|---------|----------|
| **[!UICONTROL 名称]** | 基于剧本的实例名称。 您可以自定义实例的名称和说明。 请阅读以下部分： [如何编辑实例元数据](#edit-instance-metadata) 了解更多信息。 |
| **[!UICONTROL 状态]** | 指示实例的状态。 A **[!UICONTROL 已提交]** 实例已可供使用。 |
| **[!UICONTROL 已创建]** | 指示实例的创建时间。 |
| **[!UICONTROL 创建者]** | 指示实例的创建者。 |
| **[!UICONTROL 上次修改时间]** | 指示上次修改实例的时间。 |

{style="table-layout:auto"}

![突出显示的行动手册实例。](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-instances.png)

## 启用剧本 {#enable-playbook}

当您准备好继续使用剧本并创建实例时，请选择 **[!UICONTROL 创建实例]** 以继续编写剧本并生成技术资产。

![创建剧本实例。](/help/use-case-playbooks/assets/playbooks/ui-guide/create-playbook-instance.png)

此操作会生成多个资源，供您用于实现行动手册中所述的用例。

![启用后生成的资产的剧本视图。](/help/use-case-playbooks/assets/playbooks/ui-guide/play-view.png)

### 使用配置控件编辑实例名称和说明 {#edit-instance-metadata}

根据剧本创建实例后，您可以对其进行个性化设置，以将其与从同一剧本创建的其他实例区分开来。 选择配置控件，如下所示。 编辑名称、说明和注释，然后选择 **[!UICONTROL 保存]** 等你完事了。

![编辑实例的名称和描述。](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-settings.gif)

### 了解生成的资源 {#understand-assets}

>[!IMPORTANT]
>
>不用担心！ 这是一个安全的实验空间，你无法破坏任何东西。 目前还没有与您创建的任何资产关联的数据。 您必须先摄取数据才能实现用例。

请务必了解，生成的资源因您启用的用例而异：

* 为不同类型的行动手册生成了不同的资产。 这些资源是专门为通过行动手册实现的用例创建的。 例如，行动手册生成架构、区段、历程和消息。 另一个行动手册生成架构、区段和将数据激活到的目标。
* 资产本身因行动手册而异。 例如，对于 **[!UICONTROL 向来宾发送生日消息]** 剧本，创建的受众具有规则 `birthday=today AND year=any`.

举例来说，对于 **[!UICONTROL 放弃的购物车：商品]** 行动手册，您可以看到已创建特定历程，其中包括为此用例创建的消息。

![根据用例剧本创建的历程。](/help/use-case-playbooks/assets/playbooks/ui-guide/journey-preview.png)

### 使用和编辑生成的资源 {#use-and-edit-assets}

在您探索创建行动手册实例后生成的资源时，您可以编辑创建的任何资源。

如果您或您团队中的某人创建了剧本的其他实例，则会保留编辑过的资产，并为剧本的新实例创建新资产。

上述行为适用于已创建的所有资产，但架构除外。 对于架构，在创建新的剧本实例时不会创建新架构，因此您将使用新创建的实例中剧本另一实例的已编辑架构。

>[!TIP]
>
>在开发沙盒中测试，并在准备就绪后移至生产环境。
>
>生成对象后，您可以通过添加数据继续在开发沙盒中测试。 您可以根据需要在开发沙盒中测试资产，并在准备就绪后在生产沙盒中复制资产逻辑（区段定义、历程、架构等）。

### 重用行动手册 {#reuse-playbooks}

通过创建同一行动手册的多个实例，您可以稍后实施相同的用例，而无需修改之前实施用例的详细信息。

### 与其他团队成员共享行动手册和生成的资产 {#share-playbook}

您可以与其他团队成员共享生成的实例和资产。 为此，请复制浏览器中的URL链接并与您的团队共享，以便他们大致了解生成的资源。

![用例剧本视图中突出显示的URL。](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## 后续步骤 {#next-steps}

通过阅读本UI指南，您现在知道如何解释行动手册的各个部分，以及如何使用在创建行动手册实例后生成的资产。 接下来，您可以浏览行动手册目录，找到适合您用例的正确行动手册，并在遇到任何错误时阅读故障排除指南。