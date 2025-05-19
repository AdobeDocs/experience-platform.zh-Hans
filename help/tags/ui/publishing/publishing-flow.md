---
title: 发布流
description: 了解在Adobe Experience Platform中创建库、测试内部版本以及批准将它们用于生产环境的流程。
exl-id: 4885f60b-6401-4ec7-aa1a-29c135087847
source-git-commit: 2d71eafb00098d958c8cff9350caa27bd3f0260d
workflow-type: tm+mt
source-wordcount: '1509'
ht-degree: 37%

---

# 发布流 {#publishing-flow}

>[!CONTEXTUALHELP]
>id="platform_tags_publishing_flow"
>title="发布流"
>abstract="了解发布流量所需的用户权限级别，包括开发、批准和发布权限。"

>[!NOTE]
>
>经过品牌重塑，Adobe Experience Platform Launch 已变为 Adobe Experience Platform 中的一套数据收集技术。因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

Adobe Experience Platform中的标记发布流是指创建库、测试内部版本以及批准将它们用于生产环境的过程。

您可以对库执行的操作取决于库的状态以及您具有的权限级别。此外，根据发布流中上游的内容，库的状态还影响到其中包含的资源（规则、数据元素以及扩展）。

以下部分介绍了与发布流相关的权限、库状态以及上游的详细信息。

## 权限 {#permissions}

有不同级别的用户权限，这些权限对发布流非常重要；具体而言，[!UICONTROL 开发]、[!UICONTROL 批准]和[!UICONTROL 发布]属性权限：

* **[!UICONTROL 开发]**：包括创建库、生成内部版本以用于开发环境，以及提交以进行审批的能力。
* **[!UICONTROL 批准]**：包括生成暂存内部版本以及批准暂存内部版本的功能。
* **[!UICONTROL 发布]**：包括发布已批准库的功能。

这些权限不相互包含。对于执行整个工作流程的个人，必须向该人员授予给定资产内的所有三个权限。

有关管理标记权限的更多信息，请参阅[用户权限指南](../administration/user-permissions.md)。

## 库状态 {#state}

对于发布流，库可以处于四种基本状态：

* [[!UICONTROL 开发]](#development)
* [[!UICONTROL 已提交]](#submitted)
* [[!UICONTROL 已批准]](#approved)
* [[!UICONTROL 已发布]](#published)

这四种状态在&#x200B;**[!UICONTROL 发布流]**&#x200B;选项卡中表示为列。

![](./images/approval-workflow/flow-ui.png)

必须执行特定操作才能在这些状态之间移动库。下图概述了将库在不同状态之间移动的各种操作：

![](./images/approval-workflow/library-state.png)

### [!UICONTROL 开发] {#development}

创建新库时，它们开始处于[!UICONTROL 开发]状态。 当库处于[!UICONTROL 开发]中时，必须对库进行任何更改。 开发和测试完成后，可以提交库进行审批。

下表概述了处于[!UICONTROL 开发]状态的库可用的操作：

| 操作 | 描述 |
| --- | --- |
| [!UICONTROL 编辑] | 使用[!UICONTROL Edit Library]屏幕在库中添加或删除组件。 |
| [!UICONTROL 生成到开发] | 为库创建内部版本。编译内部版本并将内部版本部署到库所分配到的环境。如果库尚未分配到某个环境，或者包含已在上游中定义的更改，此步骤将失败。 |
| [!UICONTROL Submit for Approval] | 从开发环境中取消分配库，并将库移动到[!UICONTROL Submitted]列，以供具有审批权限的用户处理。 库的最新内部版本必须成功，才能启用此选项。 |
| [!UICONTROL 提交并生成到暂存环境] | 这只能由同时具有开发和批准权限的用户执行。 此操作从开发环境中取消分配库，将库移动到[!UICONTROL 已提交]状态，并将库生成到暂存环境。 库的最新内部版本必须成功，才能启用此选项。 |
| [!UICONTROL Approve for Publishing] | 这只能由同时具有开发和批准权限的用户执行。 此操作从开发环境中取消分配库，并将其移动到[!UICONTROL 已批准]状态 — 完全跳过暂存环境和[!UICONTROL 已提交]状态。 库的最新内部版本必须成功，才能启用此选项。 |
| [!UICONTROL 批准并发布到生产环境] | 这只能由具有“开发”、“批准”和“发布”权限的用户执行。 此操作从开发环境中取消分配库，将其移动到[!UICONTROL 已批准]状态，然后发布到生产环境。 生产生成完成后，库将移至[!UICONTROL 已发布]状态。 库的最新内部版本必须成功，才能启用此选项。 |
| [!UICONTROL 删除] | 从系统中删除库。 这不会从环境中删除内部版本。 |

### [!UICONTROL 已提交] {#submitted}

当库处于[!UICONTROL 已提交]状态时，具有审批权限的用户可以在暂存环境中测试库。 测试完成时，可以批准或拒绝库。被拒绝的内部版本将返回到[!UICONTROL 开发]，以便在重新启动发布流之前进行其他更改。

下表概述了处于[!UICONTROL 已提交]状态的库可用的操作：

| 操作 | 描述 |
| --- | --- |
| [!UICONTROL 打开] | 查看库的内容。不允许对[!UICONTROL Development]列以外的库进行更改。 如果需要更改，则应拒绝库，以便在[!UICONTROL 开发]中进行更改。 |
| [!UICONTROL Build for Staging] | 在暂存环境中构建库以用于部署。 |
| [!UICONTROL Approve for Publishing] | 将库移动到[!UICONTROL 已批准]列，以供具有发布权限的用户处理。 |
| [!UICONTROL 批准并发布到生产环境] | 该操作只能由同时具有批准和发布权限的用户执行。 此操作从暂存环境中取消分配库，将其移动到[!UICONTROL 已批准]状态，然后发布到生产环境。 生产生成完成后，库将移至[!UICONTROL 已发布]状态。 如果无法在暂存环境中成功构建，则可以使用我们的来执行此操作。 |
| [!UICONTROL 拒绝] | 从暂存环境中取消分配库，然后将库移回[!UICONTROL 开发]列以进行进一步更改。 |

### [!UICONTROL 已批准] {#approved}

当库经过批准之后，具有发布权限的用户可以发布或拒绝该库。被拒绝的内部版本将返回到[!UICONTROL 开发]，以便在发布流再次开始之前进行进一步的更改。

下表概述了处于[!UICONTROL 已批准]状态的库可用的操作：

| 操作 | 描述 |
| --- | --- |
| [!UICONTROL 打开] | 查看库的内容。不允许对[!UICONTROL Development]列以外的库进行更改。 如果需要更改，则应拒绝库，以便在[!UICONTROL 开发]中进行更改。 |
| [!UICONTROL 生成并发布到生产环境] | 从暂存环境中取消分配库，将库分配到生产环境，然后部署库。<br><br>**重要提示**：选择此选项时，您的库将在生产环境中处于活动状态。在选择此选项之前，请确保库包含了您需要进行的更改。 |
| [!UICONTROL 拒绝] | 从暂存环境中取消分配库，并将库移动到[!UICONTROL 开发]列，以供进一步更改。 |

### [!UICONTROL 已发布] {#published}

[!UICONTROL Published]列显示已发布的库及其发布日期。 当前发布的库将在其旁边显示一个绿色圆点。 除非您对之前的库执行了重新发布，否则此发布始终是列顶部的库。

| 操作 | 描述 |
| --- | --- |
| [!UICONTROL 打开] | 查看库的内容。不允许对[!UICONTROL Development]列以外的库进行更改。 如果您希望更改生产环境中的库，则必须创建新库并让该库经过完整的发布流程。 |
| [!UICONTROL 重新发布] | 此操作仅适用于最近发布的五个库，并且仅适用于以下情况：(A)生产环境配置为关闭存档选项，且(b)在生成期间使用[!UICONTROL Managed by Adobe]主机。 |
| [!UICONTROL 下载] | 此操作仅适用于最近发布的五个库，并且仅当生产环境在(A)上配置了存档选项且(b)在生成时使用[!UICONTROL Managed by Adobe]主机时，才可用。 |

## 上游 {#upstream}

在您发布首个库之后，务必要了解上游的角色，因为您通过发布流来处理较新的库。

如果某个库当前处于[!UICONTROL 开发]、[!UICONTROL 已提交]或[!UICONTROL 已批准]阶段，则该库将继承其上游的任何库的规则、数据元素和扩展。 这些继承的资源构成了各个库在发布流中移动时的“基线”。本质上，您可以将各个新库简单地视为对上游所建立的基线的一系列更改。这确保在发布新迭代时，不会意外地覆盖以前库中的任何内容。

包括在上游中的内容取决于库的当前阶段。例如，[!UICONTROL Approved]列中的库仅继承来自[!UICONTROL Published]库的资源，而[!UICONTROL Development]下的库则继承所有其他列的资源。

![](./images/approval-workflow/upstream.png)

在UI中编辑库时，从上游继承的所有资源都将显示在&#x200B;**[!UICONTROL 资源上游]**&#x200B;部分中。 要查看这些资源，请选择展开部分标题下的选项卡。

![](./images/approval-workflow/upstream-collapse.png)

该部分将会展开，显示从上游继承的各个资源。您可以使用左边栏在[!UICONTROL 规则]、[!UICONTROL 数据元素]和[!UICONTROL 扩展]之间筛选，或使用搜索栏按名称查找特定资源。

![](./images/approval-workflow/upstream-resources.png)

## 后续步骤

本指南提供了Adobe Experience Platform中库发布流的总体概述。 如需了解如何发布库的详细信息，请参阅[发布概述](./overview.md)。
