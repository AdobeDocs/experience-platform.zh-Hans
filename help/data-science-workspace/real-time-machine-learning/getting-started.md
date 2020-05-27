---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: 实时机器学习入门
topic: Getting started
translation-type: tm+mt
source-git-commit: 626bb7a0856a663e235ecd2b19954f4617fe9b6f
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---


# 实时机器学习(Alpha)入门

>[!IMPORTANT]
>尚未向所有用户提供实时机器学习。 此功能在alpha中，仍在测试中。 此文档可能会更改。

为了利用实时机器学习，您需要能够访问随Adobe Experience Platform和Data Science Workspace提供的组织。 此外，您还需要拥有完整的数据集才能用于培训和评分。

实时机器学习指南需要对Python 3、Jupyter笔记本、数 [据科学](../jupyterlab/overview.md)和机器学习进行有效的理解。

**主要条款：**

- **DSL:** 域特定语言。
- **边缘：** 实时机器学习评分服务可以在离您的激活和应用程序更近的Edge群集上运行。
- **中心：** 当前的alpha正在Adobe Experience Platform Hub上运行实时机器学习评分服务，而Experience Edge Network正在开发中。
- **节点：** 节点是形成图形的基本单位。 每个节点都执行特定任务，可以使用链接将它们链在一起，以形成表示ML管道的图。 由节点执行的任务表示对输入数据的操作，如数据的转换或模式，或机器学习推理。 节点将转换或推断的值输出到下一个节点。

## Adobe Experience Platform中的数据集

要使用实时机器学习进行开始，您必须有权访问数据集。 您可以选择使用外部数据集并将其上传到JupyterLab环境，或者在Platform中创建新数据集（如果尚未这样做）。

>[!NOTE]
>如果您已经有要使用的数据集，可以跳到“下 [一步”](#next-steps)。

### 使用外部数据集

要进一步了解如何使用外部数据集(如将数据上传到JupyterLab环境)，请访问有关使用笔记本 [分析数据的教程](../jupyterlab/analyze-your-data.md#external-data)。

### 创建新数据集

要创建用于实时机器学习的新数据集，您需要为数据集创建数据模式。 接下来，您需要使用您创建的模式来摄取数据。 使用以下教程创建和填充平台数据集：

- [在API中创建并填充数据集](../../catalog/datasets/create.md)
- [在UI中创建和填充数据集](../../ingestion/tutorials/ingest-batch-data.md)

## 后续步骤 {#next-steps}

在您为实时机器学习准备好数据后，开始 [可遵循实时机器学习笔记本用户指南](./rtml-authoring-notebook.md) ，学习如何创建ONNX模型并将其上传到实时机器学习模型商店。

