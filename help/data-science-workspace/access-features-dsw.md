---
keywords: Experience Platform；主页；Data Science Workspace；热门主题；访问控制；沙盒；智能包；dsw功能；dsw访问；Adobe Experience Platform Intelligence；智能；aep智能包
solution: Experience Platform
title: 数据科学工作区访问和功能
topic-legacy: Access and features for data science workspace
description: 以下文档概述了Data Science Workspace的权限和对功能的访问权限。
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: 319cdb13c965010062aa9179b197d6f5b6a20287
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 2%

---

# 数据科学工作区访问和功能

以下文档概述了Data Science Workspace的权限和对功能的访问权限。

![DSW选项卡](./images/access/platform-tabs.png)

- **笔记本：** 提供交互式开发环境([JupyterLab](./jupyterlab/overview.md))，用于探索、分析和建模Experience Platform数据。
- **模型：** 提供用于创建、发布和存储高级机器学习方法和模型的工具。有关更多信息，请访问[创建并发布机器学习模型](./models-recipes/create-publish-model.md)教程。
- **服务：** 包含Adobe提供的服务(如AI/ML [服务)](../intelligent-services/home.md) 以及您使用Data Science Workspace创建的任何自定义服务。

为什么我只看到“服务”选项卡？

- 贵组织可能只有权使用实时客户数据平台(RTCDP)，该平台包括客户AI/ML服务。

如果您看不到任何&#x200B;**Data Science**&#x200B;选项卡，并希望利用Data Science Workspace功能，请与公司管理员联系，以检查您是否拥有Adobe Experience Platform Intelligence许可证。

## Data Science Workspace包装

Adobe Experience Platform Intelligence包和Advanced Intelligence Pack附加组件中提供了Data Science Workspace功能

下表概述了Data Science Workspace授权（无论是否具有高级智能包附加组件）的一些主要区别：

>[!NOTE]
>
>您可以授权多个高级智能包附加功能，并且增加的容量会添加到您的整体权利中。 例如，如果您授权使用2个Adobe Experience Platform Advanced Intelligence Pack地址，则您有权同时使用20个“笔记本”用户。

| 数据科学工作区权利 | 仅Adobe Experience Platform Intelligence Package | Adobe Experience Platform Intelligence与Advanced Intelligence Pack附加组件 |
| --- | :---: | :---: |
| 支持的笔记本用户数量。 | 5个并发用户 | 第一个包可添加5个并发用户，而其他购买则可为每个包添加10个并发用户。 |
| 允许集成Jupyter Notebooks进行探索性数据分析和模型创作。 | X（支持R、Python和Scala库） | X（添加PySpark和Spark ML库） |
| 与查询服务的本机集成。 能够在笔记本中使用SQL来浏览和塑造数据集。 | X | X |
| 访问用于预测分析的预建笔记本模板。 | X | X |
| 使用Jupyter Notebooks手动培训模型并对其进行评分。 | X | X |
| 部署和运行模型，并能够计划培训和引用作业。 |  | X |
| 方法框架，可轻松配置、评估、培训、评分并将模型发布到生产环境中。 |  | X |
| 用户界面驱动的模型实验和评估。 |  | X |
| 对Tensorflow模型（GPU计算）的深入学习支持。 |  | X |
| 基于Spark的分布式计算，用于针对大数据集（10MM+行）进行训练和评分。 |  | X |

## 访问控制

Experience Platform的访问控制通过[Adobe Admin Console](https://adminconsole.adobe.com)进行管理。 此功能可利用Admin Console中的产品配置文件，将用户与权限和沙箱相关联。 有关更多信息，请参阅[访问控制概述](../access-control/home.md)。

要使用数据科学工作区，必须启用“管理数据科学工作区”权限。 下表概述了启用或禁用此权限的效果：

| 权限 | 已启用 | 已禁用 |
|---|---|---|
| 管理数据科学工作区 | 提供对数据科学工作区中所有服务的访问权限。 | 禁用了对数据科学工作区中所有服务的API和UI访问。 禁用后，将阻止选择&#x200B;**Notebooks**、**Models**&#x200B;和&#x200B;**Services**&#x200B;页面。 <li>对&#x200B;**服务**&#x200B;的访问仍可通过实时客户数据平台(RTCDP)访问。</li> |

## 沙盒支持

沙箱是单个Experience Platform实例中的虚拟分区。 每个Platform实例都支持多个生产沙盒和非生产沙盒，每个沙盒都维护其自己的Platform资源库。 非生产沙箱允许您测试功能、运行实验和进行自定义配置，而不会影响生产沙箱。 有关沙箱的更多信息，请参阅[沙箱概述](../sandboxes/home.md)。

目前，数据科学工作区存在以下沙盒限制：

- 计算资源在生产沙盒和非生产沙盒之间共享。

## 后续步骤

本文档概述了数据科学工作区中可用的各种访问类型和功能。

要了解有关数据科学工作区的更多信息（如完整的日常工作流），请首先阅读[数据科学工作区演练](./walkthrough.md)文档。 有关更多常规信息，请访问[数据科学工作区概述](./home.md)。
