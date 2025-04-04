---
keywords: Experience Platform；开发人员指南；数据科学Workspace；热门主题；实时机器学习；
solution: Experience Platform
title: Real-time Machine Learning入门
description: 以下文档概述了在Adobe Experience Platform中创建实时机器学习模型所需的步骤。
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# Real-time Machine Learning (Alpha)入门

>[!NOTE]
>
>数据科学Workspace不再可供购买。
>
>本文档面向之前有权访问数据科学Workspace的现有客户。

>[!IMPORTANT]
>
>实时机器学习尚未对所有用户可用。 此功能处于Alpha状态，仍在测试中。 此文档可能会发生更改。

为了利用实时机器学习，您需要具有配置了Adobe Experience Platform和[!DNL Data Science Workspace]的组织的访问权限。 此外，您需要具有完整的数据集才能用于训练和评分。

实时机器学习指南需要对Python 3、[Jupyter Notebooks](../jupyterlab/overview.md)、数据科学和机器学习有一定的了解。

**关键术语：**

- **DSL：**&#x200B;域特定语言。
- **Edge：**&#x200B;可以在Edge群集上运行更靠近您的激活和应用程序的Real-time Machine Learning评分服务。
- **中心：**&#x200B;当前Alpha正在Adobe Experience Platform中心上运行Real-time Machine Learning评分服务，而Edge Network正在开发中。
- **节点：**&#x200B;节点是构成图形的基本单位。 每个节点执行特定的任务，并且它们可以使用链接链接链接在一起，以形成表示ML管道的图形。 节点执行的任务表示对输入数据的操作，例如数据或模式的转换或机器学习推断。 该节点将转换或推断的值输出到下一个节点。

## Adobe Experience Platform中的数据集

要开始使用实时机器学习，您必须有权访问数据集。 您可以选择使用外部数据集并将其上传到您的[!DNL JupyterLab]环境，或者在Experience Platform中创建新数据集（如果尚未这样做）。

>[!NOTE]
>
>如果您已经拥有要使用的数据集，则可以跳至[后续步骤](#next-steps)。

### 使用外部数据集

要了解有关使用外部数据集（如将数据上载到[!DNL JupyterLab]环境）的更多信息，请访问有关[使用笔记本分析数据](../jupyterlab/analyze-your-data.md#external-data)的教程。

### 创建新数据集

要创建新数据集以用于实时机器学习，您需要数据集的数据架构。 接下来，您需要使用您创建的架构摄取数据。 使用以下教程创建和填充[!DNL Experience Platform]的数据集：

- [在API中创建并填充数据集](../../catalog/datasets/create.md)
- [在UI中创建和填充数据集](../../ingestion/tutorials/ingest-batch-data.md)

## 后续步骤 {#next-steps}

准备好数据以进行实时机器学习后，请按照[实时机器学习笔记本用户指南](./rtml-authoring-notebook.md)开始学习如何创建ONNX模型并将其上载到实时机器学习模型存储。
