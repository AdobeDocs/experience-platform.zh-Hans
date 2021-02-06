---
keywords: Experience Platform；开发人员指南；数据科学工作区；热门主题；实时机器学习；
solution: Experience Platform
title: 实时机器学习入门
topic: Getting started
description: 以下文档概述了在Adobe Experience Platform创建实时机器学习模型所需的步骤。
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---


# 实时机器学习(Alpha)入门

>[!IMPORTANT]
>
>尚未向所有用户提供实时机器学习。 此功能在alpha中，仍在测试中。 此文档可能会更改。

为了利用实时机器学习，您需要有权访问由Adobe Experience Platform和[!DNL Data Science Workspace]提供的组织。 此外，您还需要拥有完整的数据集才能用于培训和评分。

实时机器学习指南需要对Python 3、[Jupyter Notebooks](../jupyterlab/overview.md)、数据科学和机器学习进行有效的了解。

**主要条款：**

- **DSL：域** 特定语言。
- **Edge：实** 时机器学习评分服务可以在离激活和应用程序更近的Edge群集上运行。
- **集线器：** 当前的alpha正在Adobe Experience Platform集线器上运行实时机器学习评分服务，而Experience Edge Network正在开发中。
- **节点：** 节点是构成图形的基本单位。每个节点都执行特定任务，可以使用链接将它们链在一起，以形成表示ML管道的图。 由节点执行的任务表示对输入数据的操作，如数据的转换或模式，或机器学习推理。 节点将转换或推断的值输出到下一个节点。

## Adobe Experience Platform数据集

要使用实时机器学习进行开始，您必须有权访问数据集。 您可以选择使用外部数据集并将其上传到[!DNL JupyterLab]环境，或在Platform中创建新数据集（如果尚未这样做）。

>[!NOTE]
>
>如果您已经有要使用的数据集，可跳到[后续步骤](#next-steps)。

### 使用外部数据集

要进一步了解如何使用外部数据集(如将数据上传到[!DNL JupyterLab]环境)，请访问[上的教程，使用笔记本](../jupyterlab/analyze-your-data.md#external-data)分析数据。

### 创建新数据集

要创建用于实时机器学习的新数据集，您需要为数据集创建数据模式。 接下来，您需要使用您创建的模式来摄取数据。 使用以下教程为[!DNL Platform]创建和填充数据集：

- [在API中创建并填充数据集](../../catalog/datasets/create.md)
- [在UI中创建和填充数据集](../../ingestion/tutorials/ingest-batch-data.md)

## 后续步骤 {#next-steps}

为实时机器学习准备数据后，请开始，遵循[实时机器学习笔记本用户指南](./rtml-authoring-notebook.md)，了解如何创建ONNX模型并将其上传到实时机器学习模型商店。

