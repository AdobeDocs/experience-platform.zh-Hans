---
keywords: Experience Platform;Luma Web数据；Data Science Workspace；热门主题；配方；演示数据；Web演示数据；Luma数据
solution: Experience Platform
title: 创建Luma Web模式和数据集
type: Tutorial
description: 本教程将为您提供Luma演示倾向模型所需的先决条件和资产。
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---

# 创建Luma倾向模型架构和数据集

本教程将为您提供所有其他 [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] 教程。 完成后，您和IMS组织将可以使用以下架构和数据集。

**架构:**

- Luma Web数据模式
- 倾向模型评分结果模式

**数据集:**

- Luma Web数据集
- 倾向模型培训数据集
- 倾向模型评分数据集
- 倾向模型评分结果数据集

## 下载资产 {#assets}

以下教程使用自定义Luma购买倾向模型。 继续之前， [下载所需的资产](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip?lang=en) zip文件夹。 此文件夹包含：

- 购买倾向模型笔记本
- 用于将数据摄取到培训和评分数据集（Luma Web数据的子集）的笔记本
- 包含730,000个Luma用户的Web数据的演示JSON文件
- 可选的Python 3 EDA（探索性数据分析）笔记本，可用于帮助理解Web数据和模型。

>[!NOTE]
>
> 您可以为任何教程使用自己的架构和数据。 但是，资产中提供的演示模型不起作用，除非它提供了正确的配置文件和要求文件。 此演示倾向模型旨在用于处理Luma Web数据。

### 创建Luma Web数据模式并摄取数据

要创建模型，您必须在Platform中有一个数据集，该数据集用于对模型进行培训和评分。 以下视频教程(位于 [数据科学工作区课程](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2021.1.dsw) 指导您创建Luma架构并摄取购买倾向模型使用的数据。

>[!VIDEO](https://video.tv.adobe.com/v/333312)

### 创建培训、评分和评分结果数据集

要运行方法生成器笔记本或使用API来训练和评分模型，您需要指定用于培训/评分的数据集和架构。 以下视频教程将指导您设置培训、评分和评分结果数据集，以及Luma购买倾向模型中使用的评分结果架构。

>[!VIDEO](https://video.tv.adobe.com/v/333426)

## 后续步骤

通过阅读本教程，您已成功为Luma倾向模型创建了所需的架构和数据集。 现在，您可以继续阅读下一个教程，并使用 [方法生成器笔记本](../jupyterlab/create-a-model.md) 教程。

此外，您还可以使用提供的探索性数据分析(EDA)笔记本来浏览数据。 此笔记本可用于帮助了解Luma数据中的模式、检查数据健全性，并汇总用于预测倾向模型的相关数据。 要了解有关探索性数据分析的更多信息，请访问 [EDA文档](../jupyterlab/eda-notebook.md).
