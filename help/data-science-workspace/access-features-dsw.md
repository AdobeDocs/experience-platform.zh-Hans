---
keywords: Experience Platform；主页；数据科学Workspace；热门主题；访问控制；沙盒；智能包；dsw功能；dsw访问；Adobe Experience Platform Intelligence；智能；aep intelligence包
solution: Experience Platform
title: 数据科学Workspace访问和功能
description: 以下文档概述了Data Science Workspace的权限和功能访问权限。
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 1%

---

# 数据科学Workspace访问和功能

>[!NOTE]
>
>数据科学Workspace不再可供购买。
>
>本文档面向之前有权访问数据科学Workspace的现有客户。

以下文档概述了Data Science Workspace的权限和功能访问权限。

![DSW选项卡](./images/access/platform-tabs.png)

- **笔记本：**&#x200B;提供交互式开发环境([JupyterLab](./jupyterlab/overview.md))，用于在Experience Platform上探索、分析和建模您的数据。
- **模型：**&#x200B;提供用于创建、发布和存储高级机器学习配方和模型的工具。 有关详细信息，请访问[创建和发布机器学习模型](./models-recipes/create-publish-model.md)教程。
- **服务：**&#x200B;包含Adobe提供的服务（如[AI/ML服务](../intelligent-services/home.md)）以及使用Data Science Workspace创建的任何自定义服务。

为什么我只看到“服务”选项卡？

- 您的组织可能仅有权使用Adobe Real-Time Customer Data Platform (Real-Time CDP)，其中包括客户人工智能/ML服务。

如果您无法查看&#x200B;**数据科学**&#x200B;选项卡中的任何一个，但希望使用数据科学Workspace功能，请联系您的公司管理员以检查您是否拥有Adobe Experience Platform Intelligence许可证。

## 数据科学Workspace打包

可在Adobe Experience Platform Intelligence包和Advanced Intelligence Pack加载项中找到数据科学Workspace功能

下表概述了数据科学Workspace授权中与使用Advanced Intelligence Pack加载项的一些主要区别：

>[!NOTE]
>
>您可以许可多个Advanced Intelligence Pack加载项，增加的容量会添加到您的总体权利文件。 例如，如果您许可了2个Adobe Experience Platform Advanced Intelligence Pack加载项，则您共有20个并发笔记本用户。

| Data Science Workspace权利 | 仅限Adobe Experience Platform Intelligence包 | Adobe Experience Platform Intelligence以及Advanced Intelligence Pack附加组件 |
| --- | :---: | :---: |
| 支持的笔记本用户数。 | 5个并发用户 | 第一个包将添加5个并发用户，而额外的购买将添加每个包10个并发用户。 |
| 允许集成的Jupyter Notebooks进行探索性数据分析和模型创作。 | X （支持R 、 Python和Scala库） | X（添加PySpark和Spark ML库） |
| 与查询服务的本机集成。 能够使用SQL在笔记本中浏览和设置数据集。 | X | X |
| 访问用于预测分析的预建笔记本模板。 | X | X |
| 使用Jupyter Notebooks手动训练模型和为其评分。 | X | X |
| 部署模型并使其可操作化，能够安排培训和引用作业。 | | X |
| 方法框架，用于轻松配置、评估、训练、得分并将模型发布到生产环境中。 |  | X |
| UI驱动的模型实验与评估。 | | X |
| Tensorflow模型（GPU计算）的深度学习支持。 | | X |
| 基于Spark的分布式计算，针对大型数据集（10MM +行）进行训练和评分。 | | X |

## 访问控制

Experience Platform的访问控制通过[Adobe Admin Console](https://adminconsole.adobe.com)进行管理。 此功能利用Admin Console中的产品配置文件，它将用户与权限和沙盒关联起来。 有关详细信息，请参阅[访问控制概述](../access-control/home.md)。

要使用数据科学Workspace，必须启用“管理数据科学Workspace”权限。 下表概述了启用或禁用此权限的效果：

| 权限 | 已启用 | 已禁用 |
|---|---|---|
| 管理数据科学Workspace | 提供对数据科学Workspace中所有服务的访问权限。 | 已禁用对数据科学Workspace中所有服务的API和UI访问。 禁用时，禁止选择&#x200B;**Notebooks**、**Models**&#x200B;和&#x200B;**Services**&#x200B;页面。 <li>仍可以通过Adobe Real-Time Customer Data Platform (Real-Time CDP)访问&#x200B;**服务**。</li> |

## 沙盒支持

沙盒是Experience Platform单个实例中的虚拟分区。 每个Experience Platform实例都支持多个生产沙盒和非生产沙盒，每个沙盒都维护自己的Experience Platform资源库。 非生产沙盒允许您测试功能、运行实验并进行自定义配置，而不会影响您的生产沙盒。 有关沙箱的详细信息，请参阅[沙箱概述](../sandboxes/home.md)。

目前，数据科学Workspace具有以下沙盒限制：

- 计算资源在生产沙盒和非生产沙盒之间共享。

## 后续步骤

本文档概述了数据科学Workspace中可用的各种访问类型和功能。

要了解有关Data Science Workspace的更多信息（如完整的日常工作流程），请从阅读[Data Science Workspace演练](./walkthrough.md)文档开始。 有关更一般的信息，请访问[数据科学Workspace概述](./home.md)。
