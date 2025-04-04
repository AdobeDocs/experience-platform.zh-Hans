---
title: AI/ML数据管道扩充端到端工作流
description: 使用基于云的机器学习环境Notebooks创建训练和评分倾向模型，以预测Adobe Experience Platform数据的订阅转化。
hide: true
hidefromtoc: true
exl-id: 2853e7c7-cab8-4e1b-b73f-622c937fbbaf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

<!-- 
title: Cloud Machine Learning Environment Notebooks
Cloud machine learning environment notebooks
Old title: 
# AI/ML data pipeline enrichment end-to-end workflow
-->

# AI/ML数据管道扩充端到端工作流

使用Data Distiller通过Adobe Experience Platform中收集和整理的高价值客户体验数据丰富您的机器学习管道。

本文档提供一系列基于云的机器学习环境笔记本，这些笔记本演示了端到端的工作流程。 该工作流会使用您首选的机器学习工具来构建自定义数据模型，这些模型通过Experience Platform数据支持您的营销用例。

此工作流需要在您的机器学习环境中使用[!DNL Python]笔记本。 这些[!DNL Python]笔记本的入门说明包含在其各自的自述文件中。

在继续本指南之前，请按照[AI/ML功能管道概述](./overview.md)中概述的步骤，启用在此AI/ML功能管道用例中使用的示例Python笔记本。

## 云机器学习环境笔记本 {#cmle-notebooks}

根据用于实现工作流的服务，端到端的工作流可以分为三个广泛的阶段。

- Experience Platform数据的初步探索和准备依赖于Experience Platform服务。
- 模型训练和评分可在基于云的ML环境中利用工具。 ML平台的常见选择包括：Databricks ML、AWS Sagemaker、DataRobot等。
- 将分数重新摄取到Experience Platform以及基于这些分数的任何基于代码的受众创建和激活都将再次依赖于Experience Platform服务。

但是，所有这些阶段都可以在ML环境的一个或多个笔记本中执行，用户无需在Experience Platform及其基于云的ML工具之间切换上下文。

此端到端流程的典型步骤被分为一系列模块化笔记本，这些笔记本一起演示了涉及Experience Platform数据的典型机器学习项目所涉及的步骤。 这样可以更轻松地使用笔记本作为实施特定活动的参考，并从相关笔记本中选择和调整代码以实施实际用例。 在实践中，数据科学家可以准备一个笔记本，为其ML项目实施端到端管道。 或者，数据科学家可以简单地调整示例代码以查询Experience Platform数据，并在其ML环境中可用，然后再在其ML平台中使用基于UI的功能继续项目。

链接存储库中包含的示例笔记本如下所述。 每个笔记本的详细文档都随笔记本本身的代码散布。

<!-- Below is the meat - the how to (but without links or details) -->

### 生成合成数据 {#generate-synthetic-data}

此笔记本提供了用于在Experience Platform中生成合成配置文件数据集和体验事件的代码，这些数据集将用于说明CMLE工作流程。

### EDA和查询服务的功能 {#eda-and-featurization-with-query-service}

此笔记本包含有关使用Experience Platform查询服务的交互式查询对Experience Platform数据集进行探索性分析的示例。 下面是一些特征化查询示例，用于为示例倾向模型创建训练数据集。

### 导出培训数据 {#export-training-data}

此笔记本演示了将培训数据集导出到云存储，以供ML工具读取。

### 训练倾向性模型 {#train-a-propensity-model}

此笔记本演示了训练倾向性模型。 它假定Databricks ML作为您的ML环境，但它是通用编写的（即，无需大量使用Databricks特定的功能/API），以便它可以适应其他平台。

### 对倾向模型评分

此笔记本说明了如何对经过培训的倾向模型进行评分，以便为每个Experience Platform客户个人资料生成倾向分数数据集。

### 将分数摄取到AEP

此简短笔记本演示了摄取倾向分数数据集以丰富AEP中的客户用户档案。

### 从代码创建和激活受众

此笔记本说明了用户如何根据分数创建受众，以及如何通过Experience Platform应用程序从笔记本代码激活这些受众。
