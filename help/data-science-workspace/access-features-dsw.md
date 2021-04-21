---
keywords: Experience Platform；主页；数据科学工作区；热门主题；访问控制；沙箱；智能包；dsw功能；dsw访问；Adobe Experience Platform智能；智能；aep智能包
solution: Experience Platform
title: 数据科学工作区访问和功能
topic-legacy: Access and features for data science workspace
description: 以下文档概述了Data Science Workspace权限和对功能的访问。
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 3%

---

# 数据科学工作区访问和功能

以下文档概述了Data Science Workspace权限和对功能的访问。

![DSW选项卡](./images/access/platform-tabs.png)

- **笔记本：** 提供交互式开发环境[(JupyterLab](./jupyterlab/overview.md))，用于探索、分析和建模Experience Platform数据。
- **模型：** 提供用于创建、发布和存储高级机器学习方法和模型的工具。有关详细信息，请访问[创建并发布机器学习模型](./models-recipes/create-publish-model.md)教程。
- **服务：** 包含Adobe提供的服务（如Intelligent Services）和 [您](../intelligent-services/home.md) 使用Data Science Workspace创建的任何自定义服务。

为什么我只看到“服务”选项卡？

- 您的组织只能获得包含智能服务客户人工智能的实时客户数据平台(RTCDP)。

如果您无法看到任何&#x200B;**Data Science**&#x200B;选项卡并希望利用Data Science Workspace功能，请与公司管理员联系，检查您是否有Adobe Experience Platform Intelligence许可证。

## Adobe Experience Platform Intelligence包加载项

下表概述了Adobe Experience Platform Intelligence程序包添加和不添加数据科学工作区的一些主要差异：

>[!NOTE]
>
>您可以授权多个智能包加载项，并且增加的容量会添加到您的整体授权中。 例如，如果您获得了2个Adobe Experience Platform Intelligence程序包的授权，则您总共有20个并发笔记本用户。

|  | [!DNL Data Science Workspace] | [!DNL Data Science Workspace] Intelligence包加载项 |
| --- | :---: | :---: |
| 支持的笔记本用户数。 | 5个并发用户 | 第一个包增加了5个并发用户，另外购买每个包增加了10个并发用户。 |
| 允许集成Jupyter笔记本进行探索性数据分析和模型创作(R、Python、Scala、PySpark) | X | X |
| 与查询服务本机集成。 能够使用笔记本中的SQL来浏览和塑造数据集。 | X | X |
| 访问预建的笔记本模板进行预测分析。 | X | X |
| 使用Jupyter Notebooks手动培训模型并为其打分。 | X | X |
| 部署和操作模型，并能够计划培训和参考作业。 |  | X |
| 菜谱框架，可轻松配置、评估、培训、评分并将模型发布到生产中。 |  | X |
| UI驱动的模型试验和评估。 |  | X |
| 对Tensorflow模型（GPU计算）的深入学习支持。 |  | X |
| 基于Spark的分布式计算，可针对大数据集（10MM +行）进行培训和评分。 |  | X |

## 访问控制

Experience Platform访问控制通过[Adobe Admin Console](https://adminconsole.adobe.com)进行管理。 此功能利用Admin Console中的产品用户档案，将用户与权限和沙箱关联起来。 有关详细信息，请参阅[访问控制概述](../access-control/home.md)。

要使用数据科学工作区，必须启用“管理数据科学工作区”权限。 下表概述了启用或禁用此权限的效果：

| 权限 | 已启用 | 已禁用 |
|---|---|---|
| 管理数据科学工作区 | 提供对数据科学工作区中所有服务的访问。 | 禁用了对Data Science Workspace中所有服务的API和UI访问。 禁用后，将阻止选择&#x200B;**Notebooks**、**Models**&#x200B;和&#x200B;**Services**&#x200B;页。 <li>对&#x200B;**服务**&#x200B;的访问仍可通过实时客户数据平台(RTCDP)访问。</li> |

## 沙箱支持

沙箱是单个Experience Platform实例中的虚拟分区。 每个平台实例都支持一个生产沙箱和多个非生产沙箱，每个沙箱都维护自己的平台资源库。 非生产沙箱允许您测试功能、运行实验和制作自定义配置，而不会影响您的生产沙箱。 有关沙箱的详细信息，请参阅[沙箱概述](../sandboxes/home.md)。

目前，Data Science Workspace具有以下沙箱限制：

- 计算资源跨生产沙箱和非生产沙箱共享。

## 后续步骤

本文档概述了数据科学工作区中提供的各种访问类型和功能。

要了解有关数据科学工作区的更多信息（如完整的日常工作流），请首先阅读[数据科学工作区演练](./walkthrough.md)文档。 有关更多一般信息，请访问[数据科学工作区概述](./home.md)。
