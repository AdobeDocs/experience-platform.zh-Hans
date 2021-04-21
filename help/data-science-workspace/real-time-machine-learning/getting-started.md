---
keywords: Experience Platform；开发人员指南；数据科学工作区；热门主题；实时机器学习；
solution: Experience Platform
title: 实时机器学习入门
topic-legacy: Getting started
description: 以下文档概述了在Adobe Experience Platform中创建实时机器学习模型所需的步骤。
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# 实时机器学习(Alpha)入门

>[!IMPORTANT]
>
>尚未向所有用户提供实时机器学习。 此功能位于alpha中，仍在测试中。 此文档可能会更改。

为了利用实时机器学习，您需要对随Adobe Experience Platform和[!DNL Data Science Workspace]提供的组织具有访问权限。 此外，您还需要具有完整的数据集才能用于培训和评分。

实时机器学习指南需要对Python 3、[Jupyter Notebooks](../jupyterlab/overview.md)、数据科学和机器学习进行有效的了解。

**主要条款：**

- **DSL：域** 特定语言。
- **Edge：实** 时机器学习评分服务可以在离您的激活和应用程序更近的Edge群集上运行。
- **集线器：** 当Experience Edge Network处于开发阶段时，当前alpha正在Adobe Experience Platform集线器上运行实时机器学习评分服务。
- **节点：** 节点是图形的基本单位。每个节点都执行特定任务，它们可以通过链接链接链接在一起，形成表示ML管线的图形。 由节点执行的任务表示对输入数据的操作，例如数据或模式的转换，或机器学习推理。 节点将变换或推断的值输出到下一个节点。

## Adobe Experience Platform中的数据集

要使用“实时机器学习”进行开始，您必须具有对数据集的访问权限。 您可以选择使用外部数据集并将其上传到[!DNL JupyterLab]环境，或在Platform中创建新数据集（如果尚未这样做）。

>[!NOTE]
>
>如果您已经有要使用的数据集，可以跳到[下一步](#next-steps)。

### 使用外部数据集

要了解有关使用外部数据集(如将数据上传到[!DNL JupyterLab]环境)的更多信息，请访问教程[中使用笔记本](../jupyterlab/analyze-your-data.md#external-data)分析数据。

### 创建新数据集

要创建用于实时机器学习的新数据集，您需要为数据集创建数据模式。 接下来，您需要使用您创建的模式收录数据。 使用以下教程为[!DNL Platform]创建和填充数据集：

- [在API中创建并填充数据集](../../catalog/datasets/create.md)
- [在UI中创建和填充数据集](../../ingestion/tutorials/ingest-batch-data.md)

## 后续步骤 {#next-steps}

在您准备好用于实时机器学习的数据后，请开始，方法是按照[实时机器学习笔记本用户指南](./rtml-authoring-notebook.md)，学习如何创建ONNX模型并将其上传到实时机器学习模型商店。
