---
title: 运行和操作概述
description: 使用运行和操作工具检查、排除和优化Experience Platform实施。 了解计划的批量激活，识别配置问题，并提高系统可靠性。
solution: Experience Platform
type: Documentation
role: Admin, User
exl-id: 7f44cdf3-4db1-47f9-bcde-401f6dcfc551
source-git-commit: 41abc542b11dcd9c295d29cdfad68720ad50129d
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 2%

---

# 运行和操作概述

当批处理作业失败或投放的数据不完整时，您需要快速了解导致问题的原因。 根本原因可能是数据可用性问题、计时错误、配置问题或系统容量限制。 如果没有明确的可见性，您可能要花几个小时调查多个系统，才能找到答案。

使用[!UICONTROL Run and Operate]工具，您可以：

* **检查您的数据操作**：获取所有工作流的作业执行状态和运行状况的完整视图。
* **更快地排除故障**：访问详细的诊断信息和执行历史记录，以快速识别根本原因并缩短解决问题的平均时间。
* **主动预防问题**：分析作业模式，在配置问题导致失败之前对其进行检测，并优化数据操作。

## 目标受众 {#target-audiences}

[!UICONTROL Run and Operate]工具旨在为整个组织内的多个受众提供服务：

* **数据和IT团队**：维护可靠数据管道并解决技术问题的系统管理员和数据工程师。
* **营销操作**：营销技术人员，他们负责检查到营销平台的数据交付并解决激活问题。
* **实施人员**：验证实施效率和可靠性以及解决技术问题的从业人员。

## 先决条件 {#prerequisites}

要访问“运行和操作”工具，您需要&#x200B;**[!UICONTROL View Job Schedules]**&#x200B;和&#x200B;**[!UICONTROL View Profile Management]** [访问控制权限](/help/access-control/home.md#permissions)。 请与系统管理员联系以确保您拥有适当的权限。

## 快速入门 {#getting-started}

要从Experience Platform UI访问运行和操作工具，请执行以下操作：

1. 登录到您的Experience Platform帐户，然后从左侧导航中选择&#x200B;**[!UICONTROL Run and Operate]**。
2. 选择符合检查或故障诊断需求的工具。

![显示“运行和操作”左侧导航的Experience Platform UI。](assets/overview/run-and-operate.png)

## 可用工具 {#available-tools}

以下工具可帮助您检查和优化数据操作。

### 作业计划 {#job-schedules}

>[!IMPORTANT]
>
>[!UICONTROL Job schedules]当前仅适用于以下Real-Time CDP作业：
>
> * 批量数据湖摄取
> * 批量配置文件摄取
> * 批次分段
> * 批量目标激活

通过[作业计划](job-schedules.md)，您可以按沙盒检查整个组织内所有计划的批处理操作，包括数据湖摄取、配置文件摄取、分段和目标激活。 查看作业执行状态、性能量度和执行历史记录，以识别模式并诊断影响可靠性的配置问题。

![Experience Platform UI显示“作业计划”屏幕。](assets/overview/job-schedules-interface.png)

作业计划提供三个调查级别：

* **[检查作业计划](job-schedules.md)**：在时间表中查看所有数据集及其计划的作业，以识别整个管道中的模式和计划冲突。
* **[识别反模式](job-schedules-anti-patterns.md)**：了解如何发现并解决常见的配置问题，例如计划重叠、密集批次栈叠和过度批次处理等会对性能造成影响的问题。
* **[查看作业详细信息](job-schedules-details.md)**：深入查看特定数据集和单个作业运行，以调查失败、检查时间并验证已处理的记录。

您还可以了解数据处理阶段之间的依赖关系，帮助您确保整个Experience Platform工作流中的可靠数据流。

### 健康检查 {#health-checks}

通过[运行状况检查](health-checks.md)，您可以主动检测架构和身份配置问题，以免它们影响您的业务操作。 目前，运行状况检查每天对架构和身份命名空间运行静态扫描，这会显示缺少的最佳实践、错误配置以及导致下游故障的模式。

运行状况检查当前评估五个基本领域：

* **[标识字段验证](health-checks.md#identity-field-validation)**：验证标识字段是否具有正确的长度和模式约束。
* **[身份图形链接规则](health-checks.md#identity-graph-linking-rules)**：确认已配置链接规则以防止配置文件折叠。
* **[人员和非人员标识配置](health-checks.md#people-non-people-identity)**：验证架构类中标识类型的使用方式是否正确。
* **[自定义身份命名空间描述](health-checks.md#namespace-missing-description)**：确保命名空间元数据完整。
* **[已弃用的标识命名空间](health-checks.md#deprecated-namespace)**：检测过时的命名空间以进行清理。

## 后续步骤 {#next-steps}

现在您已了解[!UICONTROL Run and Operate]工具的用途和功能，请探索以下资源以深化您的知识：

* 了解如何使用[运行状况检查](health-checks.md)检测架构和身份配置问题
* 了解如何[检查批处理摄取和激活的作业计划](job-schedules.md)
* 了解[批量摄取](../ingestion/batch-ingestion/overview.md)，以了解数据如何摄取到Experience Platform
* 了解如何为批处理目标[配置计划激活](../destinations/ui/activate-batch-profile-destinations.md)
* 探索[数据流监控](../dataflows/ui/monitor-destinations.md)以了解目标
