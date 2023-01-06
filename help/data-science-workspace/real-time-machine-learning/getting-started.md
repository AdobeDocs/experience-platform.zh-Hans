---
keywords: Experience Platform；开发人员指南；Data Science Workspace；热门主题；实时机器学习；
solution: Experience Platform
title: 实时机器学习入门
description: 以下文档概述了在Adobe Experience Platform中创建实时机器学习模型所需的步骤。
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# 实时机器学习(Alpha)入门

>[!IMPORTANT]
>
>尚未向所有用户提供实时机器学习功能。 此功能位于Alpha中，且仍在测试中。 本文档可能会更改。

要利用实时机器学习，您需要有权访问配置了Adobe Experience Platform和 [!DNL Data Science Workspace]. 此外，您还需要有一个完整的数据集，以用于培训和评分。

实时机器学习指南需要对Python 3进行有效的了解， [Jupyter笔记本](../jupyterlab/overview.md)、数据科学和机器学习。

**关键术语：**

- **DSL:** 域特定语言。
- **边缘：** 实时机器学习评分服务可以在离激活和应用程序更近的Edge群集上运行。
- **中心：** 当前的Alpha在开发Experience Edge Network时，正在Adobe Experience Platform集线器上运行实时机器学习评分服务。
- **节点：** 节点是图形的基本单位。 每个节点都执行特定任务，并且可以使用链接将它们链接在一起，以形成表示ML管道的图形。 节点执行的任务表示对输入数据的操作，如数据或模式的转换或机器学习推理。 节点将转换或推断的值输出到下一个节点。

## Adobe Experience Platform中的数据集

要开始使用实时机器学习，您必须有权访问数据集。 您可以选择使用外部数据集并将其上传到您的 [!DNL JupyterLab] 环境，或在Platform中创建新数据集（如果尚未创建）。

>[!NOTE]
>
>如果您已经有要使用的数据集，则可以跳到 [后续步骤](#next-steps).

### 使用外部数据集

了解有关使用外部数据集(例如，将数据上传到 [!DNL JupyterLab] 环境，请访问 [使用笔记本分析数据](../jupyterlab/analyze-your-data.md#external-data).

### 创建新数据集

要创建用于实时机器学习的新数据集，您需要为数据集提供一个数据架构。 接下来，您需要使用您创建的架构摄取数据。 请通过以下教程为 [!DNL Platform]:

- [在API中创建和填充数据集](../../catalog/datasets/create.md)
- [在UI中创建和填充数据集](../../ingestion/tutorials/ingest-batch-data.md)

## 后续步骤 {#next-steps}

准备好数据进行实时机器学习后，请首先按照 [实时机器学习笔记本用户指南](./rtml-authoring-notebook.md) 了解如何创建ONNX模型并将其上传到实时机器学习模型库。
