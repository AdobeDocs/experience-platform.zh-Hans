---
title: 发布流
description: 了解在Adobe Experience Platform中创建库、测试内部版本以及批准将它们用于生产环境的流程。
exl-id: 4885f60b-6401-4ec7-aa1a-29c135087847
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 65%

---

# 发布流 {#publishing-flow}

>[!CONTEXTUALHELP]
>id="platform_tags_publishing_flow"
>title="发布流"
>abstract="了解发布流量所需的用户权限级别，包括开发、批准和发布权限。"

Adobe Experience Platform中的标记发布流是指创建库、测试内部版本以及批准将它们用于生产环境的过程。

您可以对库执行的操作取决于库的状态以及您具有的权限级别。此外，根据发布流中上游的内容，库的状态还影响到其中包含的资源（规则、数据元素以及扩展）。

以下部分介绍了与发布流相关的权限、库状态以及上游的详细信息。

## 权限 {#permissions}

有各种不同级别的用户权限，这些权限对发布流非常重要；具体而言，有 [!UICONTROL Develop]、[!UICONTROL Approve] 和 [!UICONTROL Publish] 资产权限：

* **[!UICONTROL Develop]**：包括创建库、构建用于开发和提交供审批的能力。
* **[!UICONTROL Approve]**：包括构建用于暂存以及审批暂存的内部版本的能力。
* **[!UICONTROL Publish]**：包括发布经过批准的库的能力。

这些权限不相互包含。对于执行整个工作流程的个人，必须向该人员授予给定资产内的所有三个权限。

有关管理标记权限的更多信息，请参阅[用户权限指南](../administration/user-permissions.md)。

## 库状态 {#state}

对于发布流，库可以处于四种基本状态：

* [[!UICONTROL Development]](#development)
* [[!UICONTROL Submitted]](#submitted)
* [[!UICONTROL Approved]](#approved)
* [[!UICONTROL Published]](#published)

这四个状态在 **[!UICONTROL Publishing Flow]** 选项卡中以不同的列表示。

![](./images/approval-workflow/flow-ui.png)

必须执行特定操作才能在这些状态之间移动库。下图概述了将库在不同状态之间移动的各种操作：

![](./images/approval-workflow/library-state.png)

### [!UICONTROL Development] {#development}

创建新库时，它们一开始处于 [!UICONTROL Development] 状态。对库的任何更改必须在库处于 [!UICONTROL Development] 状态时进行。开发和测试完成后，可以提交库进行审批。

下表概述了当库处于 [!UICONTROL Development] 状态时可用的操作：

| 操作 | 描述 |
| --- | --- |
| [!UICONTROL Edit] | 使用 [!UICONTROL Edit Library] 屏幕在库中添加或删除组件。 |
| [!UICONTROL Build to Development] | 为库创建内部版本。编译内部版本并将内部版本部署到库所分配到的环境。如果库尚未分配到某个环境，或者包含已在上游中定义的更改，此步骤将失败。 |
| [!UICONTROL Submit for Approval] | 从开发环境中取消分配库，然后将库移动到 [!UICONTROL Submitted] 列，以供具有审批权限的用户处理。库的最新内部版本必须成功，才能启用此选项。 |
| [!UICONTROL Submit & Build to Staging] | 这只能由同时具有开发和批准权限的用户执行。 此操作将从开发环境中取消分配库，将库移动到[!UICONTROL Submitted]状态，并将库构建到暂存环境。 库的最新内部版本必须成功，才能启用此选项。 |
| [!UICONTROL Approve for Publishing] | 这只能由同时具有开发和批准权限的用户执行。 此操作从开发环境中取消分配库并将其移动到[!UICONTROL Approved]状态 — 完全跳过暂存环境和[!UICONTROL Submitted]状态。 库的最新内部版本必须成功，才能启用此选项。 |
| [!UICONTROL Approve & Publish to Production] | 这只能由具有“开发”、“批准”和“发布”权限的用户执行。 此操作将从开发环境中取消分配库，将其移动到[!UICONTROL Approved]状态，然后发布到生产环境。 生产生成完成后，库将移至[!UICONTROL Published]状态。 库的最新内部版本必须成功，才能启用此选项。 |
| [!UICONTROL Delete] | 从系统中删除库。 这不会从环境中删除内部版本。 |

### [!UICONTROL Submitted] {#submitted}

当库处于 [!UICONTROL Submitted] 状态时，具有审批权限的用户可以在暂存环境中测试库。测试完成时，可以批准或拒绝库。被拒绝的内部版本将返回到 [!UICONTROL Development]，这样可以进行其他更改，然后再重新开始发布流。

下表概述了当库处于 [!UICONTROL Submitted] 状态时可用的操作：

| 操作 | 描述 |
| --- | --- |
| [!UICONTROL Open] | 查看库的内容。不允许对 [!UICONTROL Development] 列以外的库进行更改。如果需要进行更改，应该拒绝库，这样可以在 [!UICONTROL Development] 下进行更改。 |
| [!UICONTROL Build for Staging] | 在暂存环境中构建库以用于部署。 |
| [!UICONTROL Approve for Publishing] | 将库移动到 [!UICONTROL Approved] 列，以供具有发布权限的用户处理。 |
| [!UICONTROL Approve & Publish to Production] | 该操作只能由同时具有批准和发布权限的用户执行。 此操作从暂存环境中取消分配库，将其移动到[!UICONTROL Approved]状态，然后发布到生产环境。 生产生成完成后，库将移至[!UICONTROL Published]状态。 如果无法在暂存环境中成功构建，则可以使用我们的来执行此操作。 |
| [!UICONTROL Reject] | 从暂存环境中取消分配库，然后将库移动回 [!UICONTROL Development] 列，以供进一步更改。 |

### [!UICONTROL Approved] {#approved}

当库经过批准之后，具有发布权限的用户可以发布或拒绝该库。被拒绝的内部版本将返回到 [!UICONTROL Development]，这样可以进一步进行更改，然后重新开始发布流。

下表概述了当库处于 [!UICONTROL Approved] 状态时可用的操作：

| 操作 | 描述 |
| --- | --- |
| [!UICONTROL Open] | 查看库的内容。不允许对 [!UICONTROL Development] 列以外的库进行更改。如果需要进行更改，应该拒绝库，这样可以在 [!UICONTROL Development] 下进行更改。 |
| [!UICONTROL Build and Publish to Production] | 从暂存环境中取消分配库，将库分配到生产环境，然后部署库。<br><br>**重要提示**：选择此选项时，您的库将在生产环境中处于活动状态。在选择此选项之前，请确保库包含了您需要进行的更改。 |
| [!UICONTROL Reject] | 从暂存环境中取消分配库，然后将库移动到 [!UICONTROL Development] 列，以供进一步更改。 |

### [!UICONTROL Published] {#published}

[!UICONTROL Published]列显示已发布的库及其发布日期。 当前发布的库将在其旁边显示一个绿色圆点。 除非您对之前的库执行了重新发布，否则此发布始终是列顶部的库。

| 操作 | 描述 |
| --- | --- |
| [!UICONTROL Open] | 查看库的内容。不允许对 [!UICONTROL Development] 列以外的库进行更改。如果您希望更改生产环境中的库，则必须创建新库并让该库经过完整的发布流程。 |
| [!UICONTROL Republish] | 此操作仅适用于最近发布的五个库，并且仅在生产环境为(A)且关闭了“存档”选项，且(b)在生成时使用[!UICONTROL Managed by Adobe]主机时可用。 |
| [!UICONTROL Download] | 此操作仅适用于最近发布的五个库，并且仅当生产环境在(A)上配置了存档选项且(b)在生成时使用[!UICONTROL Managed by Adobe]主机时，才可用。 |

## 上游 {#upstream}

在您发布首个库之后，务必要了解上游的角色，因为您通过发布流来处理较新的库。

如果某个库当前处于 [!UICONTROL Development]、[!UICONTROL Submitted] 或 [!UICONTROL Approved] 阶段，该库将继承其上游的任何库的规则、数据元素和扩展。这些继承的资源构成了各个库在发布流中移动时的“基线”。本质上，您可以将各个新库简单地视为对上游所建立的基线的一系列更改。这确保在发布新迭代时，不会意外地覆盖以前库中的任何内容。

包括在上游中的内容取决于库的当前阶段。例如，[!UICONTROL Approved] 列中的库只能从 [!UICONTROL Published] 库继承资源，而 [!UICONTROL Development] 下的库可以从所有其他列中的库继承资源。

![](./images/approval-workflow/upstream.png)

在UI中编辑库时，从上游继承的所有资源都将显示在&#x200B;**[!UICONTROL Resources Upstream]**&#x200B;部分中。 要查看这些资源，请选择展开部分标题下的选项卡。

![](./images/approval-workflow/upstream-collapse.png)

该部分将会展开，显示从上游继承的各个资源。您可以使用左侧边栏在 [!UICONTROL Rules]、[!UICONTROL Data Elements] 和 [!UICONTROL Extensions] 之间筛选，或者使用搜索栏按名称查看特定资源。

![](./images/approval-workflow/upstream-resources.png)

## 后续步骤

本指南提供了Adobe Experience Platform中库发布流的总体概述。 如需了解如何发布库的详细信息，请参阅[发布概述](./overview.md)。
