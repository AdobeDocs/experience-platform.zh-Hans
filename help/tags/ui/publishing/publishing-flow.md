---
title: 发布流程
description: 了解在Adobe Experience Platform中创建库、测试内部版本并批准这些版本以用于生产的过程。
exl-id: 4885f60b-6401-4ec7-aa1a-29c135087847
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '1490'
ht-degree: 36%

---

# 发布流

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

Adobe Experience Platform中的标记发布流程是指创建库、测试内部版本以及批准这些版本以用于生产环境的过程。

您可以对库执行的操作取决于库的状态以及您具有的权限级别。此外，根据发布流中上游的内容，库的状态还影响到其中包含的资源（规则、数据元素以及扩展）。

以下部分介绍了与发布流相关的权限、库状态以及上游的详细信息。

## 权限 {#permissions}

对于发布流程而言，用户权限的级别有所不同；具体而言， [!UICONTROL 开发], [!UICONTROL 批准]和 [!UICONTROL 发布] 资产权限：

* **[!UICONTROL 开发]**:包括创建库、构建以用于开发，以及提交以供审批的功能。
* **[!UICONTROL 批准]**:包括生成内部版本以用于暂存环境和批准暂存环境。
* **[!UICONTROL 发布]**:包括发布已批准库的功能。

这些权限不相互包含。对于执行整个工作流程的个人，必须向该人员授予给定资产内的所有三个权限。

请参阅 [用户权限指南](../administration/user-permissions.md) 有关管理标记权限的更多信息。

## 库状态 {#state}

对于发布流，库可以处于四种基本状态：

* [[!UICONTROL 开发]](#development)
* [[!UICONTROL 已提交]](#submitted)
* [[!UICONTROL 已批准]](#approved)
* [[!UICONTROL 已发布]](#published)

这四个状态在 **[!UICONTROL 发布流程]** 选项卡。

![](./images/approval-workflow/flow-ui.png)

必须执行特定操作才能在这些状态之间移动库。下图概述了将库在不同状态之间移动的各种操作：

![](./images/approval-workflow/library-state.png)

### [!UICONTROL 开发] {#development}

创建新库后，它们将在 [!UICONTROL 开发] 状态。 当库位于 [!UICONTROL 开发]. 开发和测试完成后，可以提交库进行审批。

下表概述了 [!UICONTROL 开发] 状态：

| 操作 | 描述 |
| --- | --- |
| [!UICONTROL 编辑] | 使用 [!UICONTROL 编辑库] 屏幕，以在库中添加或删除组件。 |
| [!UICONTROL 构建到开发] | 为库创建内部版本。编译内部版本并将内部版本部署到库所分配到的环境。如果库尚未分配到某个环境，或者包含已在上游中定义的更改，此步骤将失败。 |
| [!UICONTROL Submit for Approval] | 从开发环境中取消分配库，并将库移动到 [!UICONTROL 已提交] 列。 必须成功生成库的最新版本，才能启用此选项。 |
| [!UICONTROL 提交并构建到暂存环境] | 此操作只能由同时具有开发和批准权限的用户执行。 此操作会从开发环境中取消分配库，并将库移动到 [!UICONTROL 已提交] 状态，并将库构建到暂存环境。 必须成功生成库的最新版本，才能启用此选项。 |
| [!UICONTROL Approve for Publishing] | 此操作只能由同时具有开发和批准权限的用户执行。 此操作会从开发环境中取消分配库，并将其移动到 [!UICONTROL 已批准] state — 跳过暂存环境和 [!UICONTROL 已提交] 完全属于州。 必须成功生成库的最新版本，才能启用此选项。 |
| [!UICONTROL 批准并发布到生产环境] | 此操作只能由具有开发、批准和发布权限的用户执行。 此操作会从开发环境中取消分配库，并将其移动到 [!UICONTROL 已批准] 状态，并发布到生产环境。 生产内部版本完成后，库将移至 [!UICONTROL 已发布] 状态。 必须成功生成库的最新版本，才能启用此选项。 |
| [!UICONTROL 删除] | 从系统中删除库。 这不会从环境中删除内部版本。 |

### [!UICONTROL 已提交] {#submitted}

当库位于 [!UICONTROL 已提交] 状态下，具有批准权限的用户可以在暂存环境中测试库。 测试完成时，可以批准或拒绝库。已拒绝的内部版本返回 [!UICONTROL 开发] 这样，在重新启动发布流程之前，便可以进行其他更改。

下表概述了 [!UICONTROL 已提交] 状态：

| 操作 | 描述 |
| --- | --- |
| [!UICONTROL Open] | 查看库的内容。在 [!UICONTROL 开发] 列。 如果需要更改，则应拒绝库，以便在 [!UICONTROL 开发]. |
| [!UICONTROL Build for Staging] | 在暂存环境中构建库以用于部署。 |
| [!UICONTROL 批准发布] | 将库移动到 [!UICONTROL 已批准] 列。 |
| [!UICONTROL 批准并发布到生产环境] | 此操作只能由同时具有批准和发布权限的用户执行。 此操作会从暂存环境中取消分配库，并将其移动到 [!UICONTROL 已批准] 状态，并发布到生产环境。 生产内部版本完成后，库将移至 [!UICONTROL 已发布] 状态。 如果在暂存环境中没有成功的内部版本，则可以使用执行此操作。 |
| [!UICONTROL Reject] | 从暂存环境中取消分配库，并将库移回 [!UICONTROL 开发] 列以进行进一步更改。 |

### [!UICONTROL 已批准] {#approved}

当库经过批准之后，具有发布权限的用户可以发布或拒绝该库。已拒绝的内部版本返回 [!UICONTROL 开发] 以便在发布流程重新开始之前进行进一步的更改。

下表概述了 [!UICONTROL 已批准] 状态：

| 操作 | 描述 |
| --- | --- |
| [!UICONTROL 打开] | 查看库的内容。在 [!UICONTROL 开发] 列。 如果需要更改，则应拒绝库，以便在 [!UICONTROL 开发]. |
| [!UICONTROL Build and Publish to Production] | 从暂存环境中取消分配库，将库分配到生产环境，然后部署库。<br><br>**重要提示**：选择此选项时，您的库将在生产环境中处于活动状态。在选择此选项之前，请确保库包含了您需要进行的更改。 |
| [!UICONTROL 拒绝] | 从暂存环境中取消分配库，并将库移动到 [!UICONTROL 开发] 列以进行进一步更改。 |

### [!UICONTROL 已发布] {#published}

的 [!UICONTROL 已发布] 列会显示已发布的库及其发布日期。 当前发布的库将在其旁边显示一个绿色圆点。 除非您对之前的库执行了重新发布，否则该库将始终为列顶部的库。

| 操作 | 描述 |
| --- | --- |
| [!UICONTROL 打开] | 查看库的内容。在 [!UICONTROL 开发] 列。 如果您希望更改生产环境中的库，则必须创建新库并让该库经过完整的发布流程。 |
| [!UICONTROL 重新发布] | 此操作仅在最近发布的五个库上可用，并且仅在以下情况下才可用：(A)生产环境配置了“存档”选项，(b)使用 [!UICONTROL 由Adobe] 在生成时托管。 |
| [!UICONTROL 下载] | 此操作仅在最近发布的五个库中可用，并且仅在(A)在上配置了“存档”选项并且(b)使用 [!UICONTROL 由Adobe] 在生成时托管。 |

## 上游 {#upstream}

在您发布首个库之后，务必要了解上游的角色，因为您通过发布流来处理较新的库。

如果库当前位于 [!UICONTROL 开发], [!UICONTROL 已提交]或 [!UICONTROL 已批准] 暂存，则该库将继承任何上游库的规则、数据元素和扩展。 这些继承的资源构成了各个库在发布流中移动时的“基线”。本质上，您可以将各个新库简单地视为对上游所建立的基线的一系列更改。这确保在发布新迭代时，不会意外地覆盖以前库中的任何内容。

包括在上游中的内容取决于库的当前阶段。例如， [!UICONTROL 已批准] 列仅继承来自的资源 [!UICONTROL 已发布] 库，而库位于 [!UICONTROL 开发] 继承所有其他列的资源。

![](./images/approval-workflow/upstream.png)

在UI中编辑库时，所有从上游继承的资源都显示在 **[!UICONTROL 上游资源]** 中。 要查看这些资源，请选择展开部分标题下的选项卡。

![](./images/approval-workflow/upstream-collapse.png)

该部分将会展开，显示从上游继承的各个资源。您可以使用左边栏在 [!UICONTROL 规则], [!UICONTROL 数据元素]和 [!UICONTROL 扩展]，或使用搜索栏按名称查找特定资源。

![](./images/approval-workflow/upstream-resources.png)

## 后续步骤

本指南简要概述了Adobe Experience Platform中的库发布流程。 如需了解如何发布库的详细信息，请参阅[发布概述](./overview.md)。
