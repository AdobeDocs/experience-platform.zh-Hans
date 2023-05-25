---
keywords: Experience Platform；Luma Web数据；数据科学工作区；热门主题；脚本；演示数据；演示Web数据；Luma数据
solution: Experience Platform
title: 创建Luma Web架构和数据集
type: Tutorial
description: 本教程向您提供Luma演示倾向模型所需的先决条件和资产。
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# 创建Luma倾向模型架构和数据集

本教程向您提供所有其他教程所需的先决条件和资源 [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] 教程。 完成后，您和您的组织将可以使用以下架构和数据集。

**架构:**

- Luma Web数据架构
- 倾向模型评分结果模式

**数据集:**

- Luma Web数据集
- 倾向模型训练数据集
- 倾向模型评分数据集
- 倾向模型评分结果数据集

## 下载资产 {#assets}

以下教程使用自定义Luma购买倾向模型。 在继续操作之前， [下载所需的资产](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip?lang=en) zip文件夹。 此文件夹包含：

- 购买倾向模型笔记本
- 用于将数据摄取到训练和评分数据集（Luma Web数据的子集）的笔记本
- 包含730,000个Luma用户的Web数据的演示JSON文件
- 可选的Python 3 EDA（探索性数据分析）笔记本，可用于帮助了解Web数据和模型。

>[!NOTE]
>
> 您可以将自己的架构和数据用于任何教程。 但是，除非提供正确的配置文件和要求文件，否则资产中提供的演示模型不起作用。 此演示倾向模型旨在处理Luma Web数据。

### 创建Luma Web数据架构并摄取数据

要创建模型，您必须在Platform中有一个数据集，用于训练和评分您的模型。 以下视频教程来自 [数据科学工作区课程](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2021.1.dsw) 引导您逐步创建Luma架构和摄取购买倾向模型使用的数据。

>[!VIDEO](https://video.tv.adobe.com/v/333312)

### 创建训练、评分和评分结果数据集

要运行方法生成器笔记本或使用API来训练和评分模型，您需要指定用于训练/评分的数据集和架构。 以下视频教程将指导您设置训练、评分和评分结果数据集，以及在Luma购买倾向模型中使用的评分结果架构。

>[!VIDEO](https://video.tv.adobe.com/v/333426)

## 后续步骤

通过阅读本教程，您已成功为Luma倾向模型创建所需的架构和数据集。 现在，您已准备好继续下一教程并使用创建模型 [配方生成器笔记本](../jupyterlab/create-a-model.md) 教程。

此外，您可以使用提供的探索数据分析(EDA)笔记本来探索数据。 此笔记本可用于帮助了解Luma数据中的模式、检查数据是否正常以及总结预测倾向模型的相关数据。 要了解有关探索性数据分析的更多信息，请访问 [EDA文档](../jupyterlab/eda-notebook.md).
