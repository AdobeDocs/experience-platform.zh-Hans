---
keywords: Experience Platform；Luma Web数据；数据科学Workspace；热门主题；脚本；演示数据；演示Web数据；Luma数据
solution: Experience Platform
title: 创建Luma Web架构和数据集
type: Tutorial
description: 本教程向您提供Luma演示倾向模型所需的先决条件和资产。
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# 创建Luma倾向模型架构和数据集

>[!NOTE]
>
>数据科学Workspace不再可供购买。
>
>本文档面向之前有权访问数据科学Workspace的现有客户。

本教程提供了所有其他[!DNL Adobe Experience Platform] [!DNL Data Science Workspace]教程所需的先决条件和资源。 完成后，您和您的组织可以使用以下架构和数据集。

**架构：**

- Luma Web数据架构
- 倾向模型评分结果架构

**数据集：**

- Luma Web数据集
- 倾向模型训练数据集
- 倾向模型评分数据集
- 倾向模型评分结果数据集

## 下载资源 {#assets}

以下教程使用自定义Luma购买倾向模型。 在继续之前，[下载所需的资产](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip) zip文件夹。 此文件夹包含：

- 购买倾向模型笔记本
- 用于将数据摄取到训练和评分数据集（Luma Web数据的子集）的笔记本
- 包含730,000个Luma用户的Web数据的演示JSON文件
- 可选的Python 3 EDA（探索性数据分析）笔记本，可用于帮助了解Web数据和模型。

>[!NOTE]
>
> 您可以将自己的架构和数据用于任何教程。 但是，除非提供了正确的配置文件和要求文件，否则资产中提供的演示模型将无法正常工作。 此演示倾向模型旨在处理Luma Web数据。

### 创建Luma Web数据架构并摄取数据

为了创建模型，Experience Platform中必须具有一个用于训练和评分模型的数据集。 [数据科学Workspace课程](https://experienceleague.adobe.com/?lang=zh-hans&recommended=ExperiencePlatform-U-1-2021.1.dsw)中的以下视频教程将指导您完成创建Luma架构以及摄取购买倾向模型使用的数据的过程。

>[!VIDEO](https://video.tv.adobe.com/v/333312)

### 创建训练、评分和评分结果数据集

要运行方法生成器笔记本或使用API来训练和评分模型，您需要指定用于训练/评分的数据集和架构。 以下视频教程将指导您设置培训、评分和评分结果数据集，以及在Luma购买倾向模型中使用的评分结果架构。

>[!VIDEO](https://video.tv.adobe.com/v/333426)

## 后续步骤

通过阅读本教程，您已成功为Luma倾向模型创建所需的架构和数据集。 您现在已准备好继续下一教程，并使用[方法生成器笔记本](../jupyterlab/create-a-model.md)教程创建模型。

此外，您可以使用提供的探索数据分析(EDA)笔记本浏览数据。 此笔记本可用于帮助了解Luma数据中的模式、检查数据健康度并总结预测倾向模型的相关数据。 若要了解有关探索性数据分析的更多信息，请访问[EDA文档](../jupyterlab/eda-notebook.md)。
