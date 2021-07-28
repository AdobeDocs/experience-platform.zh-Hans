---
title: 发布流程
description: 了解在Adobe Experience Platform中创建库、测试内部版本并批准这些版本以用于生产的过程。
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 7%

---

# 发布流程

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，在产品文档中推出了一些术语更改。 有关术语更改的统一参考，请参阅以下[文档](../../term-updates.md)。

Adobe Experience Platform中的标记发布流程是指创建库、测试内部版本以及批准这些版本以用于生产环境的过程。

您可以对库执行的可用操作取决于库的状态和您拥有的权限级别。 此外，库的状态还会根据发布流程中的上游内容，影响库包含的资源（规则、数据元素和扩展）。

以下各节介绍了与发布流程相关的权限、库状态以及上游内容的详细信息。

## 权限 {#permissions}

对于发布流程而言，用户权限的级别有所不同；具体而言，[!UICONTROL Develop]、[!UICONTROL Approve]和[!UICONTROL Publish]资产权限：

* **[!UICONTROL 开发]**:包括创建库、构建以用于开发，以及提交以供审批的功能。
* **[!UICONTROL 批准]**:包括生成内部版本以用于暂存环境和批准暂存环境。
* **[!UICONTROL 发布]**:包括发布已批准库的功能。

这些权限不包含在内。 对于执行整个工作流程的个人，必须向该人员授予给定资产内的所有三个权限。

有关管理标记权限的更多信息，请参阅[用户权限指南](../administration/user-permissions.md) 。

## 库状态 {#state}

在发布流程中，库可以处于以下四个基本状态：

* [[!UICONTROL 开发]](#development)
* [[!UICONTROL 已提交]](#submitted)
* [[!UICONTROL 已批准]](#approved)
* [[!UICONTROL 已发布]](#published)

这四个状态在数据收集UI的&#x200B;**[!UICONTROL 发布流程]**&#x200B;选项卡中以列表示。

![](./images/approval-workflow/flow-ui.png)

必须执行特定操作才能在这些状态之间移动库。下图概述了在状态之间移动库的每个操作：

![](./images/approval-workflow/library-state.png)

### [!UICONTROL 开发] {#development}

创建新库后，它们将以[!UICONTROL Development]状态开始。 当库位于[!UICONTROL Development]中时，必须对库进行任何更改。 开发和测试完成后，可以提交库以供审批。

下表概述了处于[!UICONTROL Development]状态的库的可用操作：

| 操作 | 描述 |
| --- | --- |
| [!UICONTROL 编辑] | 使用[!UICONTROL Edit Library]屏幕可在库中添加或删除组件。 |
| [!UICONTROL 构建到开发] | 为库创建内部版本。系统会编译该内部版本并将其部署到分配了库的环境。 如果尚未将库分配到环境，或包含已在上游中定义的更改，则此步骤会失败。 |
| [!UICONTROL Submit for Approval] | 从开发环境中取消分配库，并将库移动到[!UICONTROL Submitted]列，以供具有工作审批权限的用户使用。 必须成功生成库的最新版本，才能启用此选项。 |
| [!UICONTROL 提交并构建到暂存环境] | 此操作只能由同时具有开发和批准权限的用户执行。 此操作会从开发环境中取消分配库，将库移动到[!UICONTROL Submitted]状态，并将库构建到暂存环境。 必须成功生成库的最新版本，才能启用此选项。 |
| [!UICONTROL Approve for Publishing] | 此操作只能由同时具有开发和批准权限的用户执行。 此操作将从开发环境中取消分配库，并将其移动到[!UICONTROL Approved]状态 — 完全跳过暂存环境和[!UICONTROL Submitted]状态。 必须成功生成库的最新版本，才能启用此选项。 |
| [!UICONTROL 批准并发布到生产环境] | 此操作只能由具有开发、批准和发布权限的用户执行。 此操作将从开发环境中取消分配库，将其移动到[!UICONTROL Approved]状态，然后发布到生产环境。 生产内部版本完成后，库将变为[!UICONTROL Published]状态。 必须成功生成库的最新版本，才能启用此选项。 |
| [!UICONTROL 删除] | 从系统中删除库。 这不会从环境中删除内部版本。 |

### [!UICONTROL 已提交] {#submitted}

当库处于[!UICONTROL Submitted]状态时，具有批准权限的用户可以在暂存环境中测试该库。 测试完成后，库可以被批准或拒绝。 已拒绝的内部版本会返回到[!UICONTROL Development]，以便在重新启动发布流程之前可以进行其他更改。

下表概述了处于[!UICONTROL Submitted]状态的库的可用操作：

| 操作 | 描述 |
| --- | --- |
| [!UICONTROL Open] | 查看库的内容。不允许对[!UICONTROL Development]列外的库进行更改。 如果需要更改，则应拒绝库，以便在[!UICONTROL Development]中进行更改。 |
| [!UICONTROL Build for Staging] | 在暂存环境中构建库以进行部署。 |
| [!UICONTROL 批准发布] | 将库移动到[!UICONTROL Approved]列，以供具有工作权限的用户处理。 |
| [!UICONTROL 批准并发布到生产环境] | 此操作只能由同时具有批准和发布权限的用户执行。 此操作会从暂存环境中取消分配库，将其移动到[!UICONTROL Approved]状态，然后发布到生产环境。 生产内部版本完成后，库将变为[!UICONTROL Published]状态。 如果在暂存环境中没有成功的内部版本，则可以使用执行此操作。 |
| [!UICONTROL Reject] | 从暂存环境中取消分配库，并将库移回[!UICONTROL Development]列，以便进行进一步更改。 |

### [!UICONTROL 已批准] {#approved}

库获得批准后，具有发布权限的用户可以发布或拒绝库。 已拒绝的内部版本会返回到[!UICONTROL Development]，以便在发布流程重新开始之前可以进行进一步的更改。

下表概述了处于[!UICONTROL Approved]状态的库的可用操作：

| 操作 | 描述 |
| --- | --- |
| [!UICONTROL 打开] | 查看库的内容。不允许对[!UICONTROL Development]列外的库进行更改。 如果需要更改，则应拒绝库，以便在[!UICONTROL Development]中进行更改。 |
| [!UICONTROL Build and Publish to Production] | 从暂存环境中取消分配库，将库分配到生产环境并进行部署。<br><br>**重要信息**:选择此选项后，您的库将在生产环境中处于活动状态。在选择此选项之前，请确保库包含您需要的更改。 |
| [!UICONTROL 拒绝] | 从暂存环境中取消分配库，并将库移动到[!UICONTROL Development]列，以便进行进一步更改。 |

### [!UICONTROL 已发布] {#published}

[!UICONTROL Published]列显示已发布的库及其发布日期。 当前发布的库将在其旁边显示一个绿色圆点。 除非您对之前的库执行了重新发布，否则该库将始终为列顶部的库。

| 操作 | 描述 |
| --- | --- |
| [!UICONTROL 打开] | 查看库的内容。不允许对[!UICONTROL Development]列外的库进行更改。 如果要更改生产环境中的内容，必须创建一个新库并在整个发布过程中移动该库。 |
| [!UICONTROL 重新发布] | 此操作仅在最近发布的五个库上可用，并且仅当生产环境(A)配置了“存档”选项关闭，并且(b)在生成时使用[!UICONTROL 由Adobe管理]主机时才可用。 |
| [!UICONTROL 下载] | 此操作仅在最近发布的五个库上可用，并且仅当生产环境(A)在上配置了“存档”选项，并且(b)在生成时使用[!UICONTROL 由Adobe管理]主机时才可用。 |

## 上游 {#upstream}

发布第一个库后，当您通过发布流程移动较新的库时，了解上游库的角色将变得至关重要。

如果库当前位于[!UICONTROL Development]、[!UICONTROL Submitted]或[!UICONTROL Approved]阶段，则该库将继承任何上游库的规则、数据元素和扩展。 当每个库在发布流程中移动时，这些继承的资源将构成其“基线”。 基本上，您可以将每个新库仅视为对上游库所建立基线的一系列更改。 这可确保在发布新小版本时，不会意外覆盖先前库中的任何内容。

上游库中包含的内容取决于库的当前阶段。 例如，[!UICONTROL Approved]列中的库仅继承[!UICONTROL Published]库的资源，而[!UICONTROL Development]下的库继承所有其他列的资源。

![](./images/approval-workflow/upstream.png)

在数据收集UI中编辑库时，从上游继承的所有资源都显示在&#x200B;**[!UICONTROL Resources Upsream]**&#x200B;部分中。 要查看这些资源，请选择部分标题下方的展开选项卡。

![](./images/approval-workflow/upstream-collapse.png)

此部分将展开以显示从上游继承的单个资源。 您可以使用左边栏在[!UICONTROL Rules]、[!UICONTROL Data Elements]和[!UICONTROL Extensions]之间进行筛选，或使用搜索栏按名称查找特定资源。

![](./images/approval-workflow/upstream-resources.png)

## 后续步骤

本指南简要概述了Adobe Experience Platform中的库发布流程。 要了解有关如何发布库的更多信息，请参阅[发布概述](./overview.md)。
