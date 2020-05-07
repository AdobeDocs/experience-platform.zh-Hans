---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: 实时机器学习入门
topic: Getting started
translation-type: tm+mt
source-git-commit: c9e6eb41e51ad17ad11b9a669ca5e4cf6c899f8b
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---


# 实时机器学习入门

>[!IMPORTANT]
>尚未向所有用户提供实时机器学习。 此功能在alpha中，仍在测试中。 此文档可能会更改。

为了利用实时机器学习，您需要能够访问随Adobe Experience Platform和Data Science Workspace提供的组织。 此外，您需要在平台中拥有数据集。

实时机器学习指南需要对Python 3、Jupyter笔记本、数 [据科学](../jupyterlab/overview.md)和机器学习进行有效的理解。

## Adobe Experience Platform中的数据集

要使用实时机器学习进行开始，您必须在Experience Platform中拥有已填充的数据集。 您可以选择使用外部数据集并将其上传到JupyterLab环境，或者在Platform中创建新数据集（如果尚未这样做）。

>[!NOTE]
>如果您已经有要使用的数据集，可以跳过以下两个步骤。

### 使用外部数据集

要进一步了解如何使用外部数据集(如将数据上传到JupyterLab环境)，请访问有关使用笔记本 [分析数据的教程](../jupyterlab/analyze-your-data.md#external-data)。

### 创建新数据集

要创建用于实时机器学习的新数据集，您需要为数据集创建数据模式。 接下来，您需要使用您创建的模式来摄取数据。 使用以下教程创建和填充平台数据集：

- [在API中创建并填充数据集](../../catalog/datasets/create.md)
- [在UI中创建和填充数据集](../../ingestion/tutorials/ingest-batch-data.md)

## Git和Docker

如果您计划使用“数据科学工作场所”菜谱工作流来培训模型，则需要Git和Docker。

>[!NOTE]
>如果您计划使用Python笔记本培训模特，或者使用自己的ONNX模型，则无需下载Git和Docker。

- [Git安装指南](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Docker安装指南](https://docs.docker.com/get-docker/)

## 后续步骤

为实时机器学习准备好数据后，请开始 [，方法是](./training-ml-model.md) ，按照培训模型的教程学习如何创建ONNX模型并将其上传到实时机器学习模型商店。

