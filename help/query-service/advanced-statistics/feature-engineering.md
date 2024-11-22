---
title: 功能工程SQL扩展
description: 了解Data Distiller功能工程SQL扩展，用于预处理数据以实现高级统计建模。 它涵盖了可用的特征提取、转换和选择技术。
role: Developer
exl-id: 622c8ef3-9651-46b3-ad22-021a93190149
source-git-commit: e7bc30c153f67c59e9c04e8c8df60394f48871d0
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 0%

---

# 功能工程SQL扩展

>[!AVAILABILITY]
>
>此功能适用于购买了Data Distiller附加产品的客户。 有关更多信息，请与您的 Adobe 代表联系。

为了满足您的功能工程需求，请使用SQL Transformer扩展来简化和自动化数据预处理。 使用此扩展构建特征并使用不同的特征工程技术无缝试验，包括将其与模型相关联。 专为分布式计算而设计，您可以通过并行和可伸缩的方式在大型数据集上执行功能工程，显着减少使用Data Distiller功能工程SQL扩展进行数据预处理所需的时间。

## 技术概述 {#technique-overview}

特征工程功能包括特征提取、特征转换和特征选择。 每个区域都包含特定的功能，这些功能旨在提取、转换、聚焦并改进数据预处理。

### 特征提取 {#feature-extraction}

从数据中提取相关信息（尤其是文本数据），并将其转换为支持的模型可使用或转换和派生数据集的数字格式。 使用以下函数执行特征提取：

- **[文本转换器](./feature-transformation.md#textual-transformations)**：将文本数据转换为数字功能。
- **[计数矢量器](./feature-transformation.md#countvectorizer)**：将文本文档集合转换为令牌计数的矢量。
- **[N-gram](./feature-transformation.md#ngram)**：从文本数据生成n-gram序列。
- **[停止单词移除程序](./feature-transformation.md#stopwordsremover)**：筛选出没有重要意义的常用单词。
- **[TF-IDF](./feature-transformation.md#tf-idf)**：度量文档中单词相对于语料库的重要性。
- **[Tokenizer](./feature-transformation.md#tokenizer)**：将文本划分为单独的术语（单词）。
- **[Word2Vec](./feature-transformation.md#word2vec)**：将单词映射到固定大小的矢量并创建单词嵌入。

### 特征转换 {#feature-transformation}

除了提取特征之外，还可以使用下列常规转换器为高级统计模型和派生数据集准备特征。 应用缩放、标准化或编码以确保您的功能具有相同的缩放比例并具有相似的分布情况。

#### 常规转换器

以下是处理各种数据类型的工具列表，以增强您的数据预处理工作流。

- **[数值输入器](./feature-transformation.md#numeric-imputer)**：使用指定的值（如平均值或中间值）填充数值列中缺少的值。
- **[字符串输入器](./feature-transformation.md#string-imputer)**：将缺少的字符串值替换为指定的值，如列中最常见的字符串。
- **[矢量组合器](./feature-transformation.md#vector-assembler)**：将多个列组合为一个矢量列，以便为机器学习模型准备数据。
- **[布尔型输入器](./feature-transformation.md#boolean-imputer)**：使用指定的值（如`true`或`false`）填充缺少的布尔值。

#### 数值转换器

应用这些技术有效地处理和缩放数值数据以提高模型性能。

- **[二进制化器](./feature-transformation.md#binarizer)**：根据阈值将连续功能转换为二进制值。
- **[分段器](./feature-transformation.md#bucketizer)**：将连续功能映射到离散分段。
- **[最小 — 最大缩放器](./feature-transformation.md#minmaxscaler)**：将功能重新缩放到指定的范围，通常为[0,1]。
- **[最大Abs缩放器](./feature-transformation.md#maxabsscaler)**：将特征重新缩放到范围[-1、1]，而不更改稀疏度。
- **[规范化器](./feature-transformation.md#normalizer)**：规范化向量以具有单位规范。
- **[Quantile离散化](./feature-transformation.md#quantilediscretizer)**：通过将连续特征转换为分类特征，将其转换为分位数。
- **[标准缩放器](./feature-transformation.md#standardscaler)**：将特征标准化为具有单位标准差和/或平均数零。

#### 分类转换器

使用这些转换器将分类数据转换并编码为适合机器学习模型的格式。

- **[字符串索引器](./feature-transformation.md#stringindexer)**：将类别字符串数据转换为数字索引。
- **[一个Hot Encoder](./feature-transformation.md#onehotencoder)**：将分类数据映射到二进制矢量。

### 特征选择 {#feature-selection}

接下来，重点从原始集中选择最重要特征的子集。 此过程有助于减少数据的维数，使模型更易于处理并改进整体模型性能。

<!-- Commented out as it 
## Supported machine learning algorithms {#supported-ml-algorithms}

Once you have preprocessed your data, use the feature engineering SQL extension to prepare your data for the following machine learning algorithms:

### Classification and regression {#classification-regression}

Use logical regression to predict categorical outcomes and linear regression to predict continuous values.

- **Logical Regression**: Use this for binary classification tasks.
- **Linear Regression**: Apply this algorithm for predicting continuous values.

### Clustering {#clustering}

Use a clustering algorithm to group data points into distinct clusters based on their similarities.

- **[`K-Means`](./feature-transformation.md#kmeans)**: Use `K-Means` for unsupervised learning tasks to partition data into a specified number of clusters, with each data point assigned to the cluster with the nearest mean. -->

## 实施OPTIONS子句 {#options-clause}

定义模型时，请使用`OPTIONS`子句指定算法及其参数。 首先设置`type`参数以指示您所使用的算法，如`K-Means`。 然后，将`OPTIONS`子句中的相关参数定义为键值对以微调模型。 如果选择不自定义某些参数，系统将应用默认设置。 请参阅相关文档以了解每个参数的函数和默认值。

### 后续步骤

学习本文档中概述的功能工程技术后，请转至[模型](./models.md)文档。 它引导您使用所设计功能来创建、培训和管理可信模型。 生成模型后，请转到[实施高级统计模型文档。](./implement-models/implement-models.md)的问题。本文档作为概览，链接到不同建模技术（包括聚类、分类和回归）的深入指南。 通过阅读这些文档，您可以了解如何在SQL工作流中配置和实施各种可信模型，并优化模型以进行高级数据分析。
