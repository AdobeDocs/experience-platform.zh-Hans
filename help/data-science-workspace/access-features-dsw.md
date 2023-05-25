---
keywords: Experience Platform；主页；Data Science Workspace；热门主题；访问控制；沙盒；智能包；dsw功能；dsw访问；Adobe Experience Platform Intelligence；智能；aep intelligence包
solution: Experience Platform
title: 数据科学工作区访问和功能
description: 以下文档概述了Data Science Workspace的权限和功能访问权限。
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 2%

---

# 数据科学工作区访问和功能

以下文档概述了Data Science Workspace的权限和功能访问权限。

![DSW选项卡](./images/access/platform-tabs.png)

- **笔记本：** 提供交互式开发环境([JupyterLab](./jupyterlab/overview.md))，以在Experience Platform上探索、分析和建模您的数据。
- **模型：** 提供用于创建、发布和存储高级机器学习方法和模型的工具。 欲知更多信息，请访问 [创建和发布机器学习模型](./models-recipes/create-publish-model.md) 教程。
- **服务：** 包含Adobe提供的两种服务，例如 [AI/ML服务](../intelligent-services/home.md) 以及使用数据科学工作区创建的任何自定义服务。

为什么我只看到“服务”选项卡？

- 您的组织可能仅有权使用Adobe Real-time Customer Data Platform (Real-Time CDP)，其中包含客户人工智能/ML服务。

如果您看不到任何 **数据科学** 选项卡并希望利用Data Science Workspace功能，请联系您的公司管理员以检查您是否拥有Adobe Experience Platform Intelligence许可证。

## 数据科学工作区打包

可在Adobe Experience Platform Intelligence包和Advanced Intelligence Pack加载项中找到数据科学工作区功能

下表概述了使用和不使用高级智能包加载项时，数据科学工作区权利的一些主要差异：

>[!NOTE]
>
>您可以许可多个高级智能包加载项，增加的容量会添加到您的总体权利文件。 例如，如果您许可了2个Adobe Experience Platform Advanced Intelligence Pack加载项，则您有权同时使用20个笔记本用户。

| 数据科学工作区权利 | 仅限Adobe Experience Platform Intelligence包 | Adobe Experience Platform Intelligence plus Advanced Intelligence Pack附加组件 |
| --- | :---: | :---: |
| 支持的笔记本用户数量。 | 5个并发用户 | 第一个包将添加5个并发用户，而额外的购买操作将添加每个包10个并发用户。 |
| 允许集成的Jupyter Notebooks进行探索性数据分析和模型创作。 | X （支持R 、 Python和Scala库） | X（添加PySpark和Spark ML库） |
| 与查询服务的本机集成。 能够使用SQL在笔记本中浏览数据集并设置其形状。 | X | X |
| 访问用于预测分析的预建笔记本模板。 | X | X |
| 使用Jupyter Notebooks手动训练模型和为模型评分。 | X | X |
| 部署模型并使其可操作化，并能够安排培训和引用作业。 |  | X |
| 方法框架，用于轻松配置、评估、训练、评分和将模型发布到生产环境中。 |  | X |
| UI驱动的模型实验与评估。 |  | X |
| Tensorflow模型（GPU计算）的深度学习支持。 |  | X |
| 基于Spark的分布式计算，针对大型数据集（10MM +行）进行训练和评分。 |  | X |

## 访问控制

Experience Platform的访问控制是通过 [Adobe Admin Console](https://adminconsole.adobe.com). 此功能利用Admin Console中的产品配置文件，它将用户与权限和沙盒相关联。 请参阅 [访问控制概述](../access-control/home.md) 了解更多信息。

要使用数据科学工作区，必须启用“管理数据科学工作区”权限。 下表概述了启用或禁用此权限的影响：

| 权限 | 已启用 | 已禁用 |
|---|---|---|
| 管理数据科学工作区 | 提供对数据科学工作区中所有服务的访问权限。 | 已禁用对数据科学工作区中所有服务的API和UI访问。 禁用时，选择 **Notebooks**， **模型**、和 **服务** 页面被阻止。 <li>访问 **服务** 仍可通过Adobe Real-time Customer Data Platform (Real-Time CDP)使用。</li> |

## 沙盒支持

沙盒是单个Experience Platform实例中的虚拟分区。 每个Platform实例都支持多个生产沙盒和非生产沙盒，每个沙盒都维护自己的Platform资源库。 非生产沙盒允许您在不影响生产沙盒的情况下测试功能、运行实验以及进行自定义配置。 有关沙箱的详细信息，请参阅 [沙盒概述](../sandboxes/home.md).

目前，数据科学工作区具有以下沙盒限制：

- 计算资源在生产沙盒和非生产沙盒之间共享。

## 后续步骤

本文档概述了Data Science Workspace中可用的不同类型的访问和功能。

要了解有关数据科学工作区的更多信息（例如完整的日常工作流程），请从阅读 [数据科学工作区演练](./walkthrough.md) 文档。 欲知更多一般信息，请访问 [数据科学工作区概述](./home.md).
