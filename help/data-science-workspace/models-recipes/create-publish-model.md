---
keywords: Experience Platform；机器学习模型；数据科学工作区；热门主题；创建和发布模型
solution: Experience Platform
title: 创建和发布机器学习模型
type: Tutorial
description: 以下指南介绍了创建和发布机器学习模型所需的步骤。
exl-id: f71e5a17-9952-411e-8e6a-aab46bc4c006
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---


# 创建和发布机器学习模型

以下指南介绍了创建和发布机器学习模型所需的步骤。 每个部分都包含您要执行的操作的描述，以及指向UI和API文档的链接，以执行所述步骤。

## 快速入门

在启动本教程之前，您必须满足以下先决条件：

- 访问 [!DNL Adobe Experience Platform]. 如果您在 [!DNL Experience Platform]，请在继续操作之前与系统管理员联系。

- 所有数据科学工作区教程都使用Luma倾向模型。 为了跟进，您必须已创建 [Luma倾向性模型模式和数据集](./create-luma-data.md).

### 探索数据并了解模式

登录到 [Adobe Experience Platform](https://platform.adobe.com/) 选择 **[!UICONTROL 数据集]** 列出所有现有数据集，并选择要浏览的数据集。 在这种情况下，您应选择 **Luma Web数据** 数据集。

![选择Luma Web数据集](../images/models-recipes/model-walkthrough/luma-dataset.png)

此时会打开数据集活动页面，其中列出了与您的数据集相关的信息。 您可以选择 **[!UICONTROL 预览数据集]** 在右上方附近以检查示例记录。 您还可以查看选定数据集的架构。

![预览Luma Web数据](../images/models-recipes/model-walkthrough/preview-dataset.png)

选择右边栏中的架构链接。 出现一个弹出窗口，选择下方的链接 **[!UICONTROL 架构名称]** 在新选项卡中打开架构。

![预览luma web数据模式](../images/models-recipes/model-walkthrough/preview-schema.png)

您可以使用提供的探索性数据分析(EDA)笔记本进一步探索数据。 此笔记本可用于帮助了解Luma数据中的模式、检查数据健全性，以及汇总用于预测倾向模型的相关数据。 要了解有关探索性数据分析的更多信息，请访问 [EDA文档](../jupyterlab/eda-notebook.md).

## 创建Luma倾向方法 {#author-your-model}

的主要组件 [!DNL Data Science Workspace] 生命周期涉及创作方法和模型。 Luma倾向模型旨在生成关于客户是否具有从Luma购买产品的高倾向的预测。

要创建Luma倾向模型，请使用方法生成器模板。 配方是模型的基础，因为它们包含机器学习算法和用于解决特定问题的逻辑。 更重要的是，各种方法使您能够在整个组织内实现机器学习的大众化，使其他用户能够在不编写任何代码的情况下访问不同用例的模型。

关注 [使用JupyterLab Notebooks创建模型](../jupyterlab/create-a-model.md) 教程创建在后续教程中使用的Luma倾向模型方法。

## 从外部源导入和打包方法(*可选*)

如果要导入并打包一个方法以在Data Science Workspace中使用，则必须将源文件打包到存档文件中。 关注 [将源文件打包到方法中](./package-source-files-recipe.md) 教程。 本教程将向您展示如何将源文件打包到方法中，这是将方法导入数据科学工作区的先决条件步骤。 教程完成后，您将在Azure容器注册表中获得Docker图像，以及相应的图像URL，换言之，即存档文件。

此存档文件可用于在数据科学工作区中通过使用 [UI工作流程](./import-packaged-recipe-ui.md) 或 [API工作流](./import-packaged-recipe-api.md).

## 训练和评估模型 {#train-and-evaluate-your-model}

现在，您的数据已准备就绪并且方法已准备就绪，您便能够进一步创建、培训和评估机器学习模型。 在使用方法生成器时，您应该已经对模型进行了培训、评分和评估，然后才能将其打包到方法中。

通过数据科学工作区UI和API，您可以将方法作为模型发布。 此外，您还可以进一步微调模型的特定方面，如添加、删除和更改超参数。

### 创建模型

要了解有关使用UI创建模型的更多信息，请访问培训并评估数据科学工作区中的模型 [UI教程](./train-evaluate-model-ui.md) 或 [API教程](./train-evaluate-model-api.md). 本教程提供了有关如何创建、训练和更新超参数以优化模型的示例。

>[!NOTE]
>
> 无法学习超参数，因此必须在培训运行之前分配超参数。 调整超参数可能会改变训练模型的准确度。 由于优化模型是一个迭代过程，因此可能需要多次训练运行才能获得满意的评价。

## 为模型打分 {#score-a-model}

创建和发布模型的下一步是操作您的模型，以便对数据湖和实时客户资料中的分析进行评分和使用分析。

在数据科学工作区中，通过将输入数据输入到现有的训练模型中即可获得评分。 然后，将评分结果存储并作为新批次在指定的输出数据集中查看。

要了解如何对模型进行评分，请访问模型的得分 [UI教程](./score-model-ui.md) 或 [API教程](./score-model-api.md).

## 将打分的模型作为服务发布

数据科学工作区允许您将培训的模型作为服务发布。 这样，组织内的用户便可以对数据进行评分，而无需自行创建模型。

要了解如何将模型作为服务发布，请访问 [UI教程](./publish-model-service-ui.md) 或 [API教程](./publish-model-service-api.md).

### 为服务安排自动培训

将模型作为服务发布后，您可以为机器学习服务设置计划评分和培训运行。 自动化培训和评分流程有助于通过跟踪数据中的模式，随时保持和提高服务的效率。 访问 [在Data Science Workspace UI中计划模型](./schedule-models-ui.md) 教程。

>[!NOTE]
>
> 您只能从UI计划一个模型，以便进行自动培训和评分。

## 后续步骤 {#next-steps}

Adobe Experience Platform [!DNL Data Science Workspace] 提供用于创建、评估和利用机器学习模型生成数据预测和分析的工具和资源。 将机器学习分析引入 [!DNL Profile]启用的数据集，该数据也被摄取为 [!DNL Profile] 随后可使用 [!DNL Adobe Experience Platform Segmentation Service].

在摄取配置文件和时间系列数据时，实时客户配置文件会自动决定通过称为流分段的持续过程，将数据与现有数据合并并更新并集视图，从区段中包含或排除该数据。 因此，您可以即时执行计算并做出决策，在客户与您的品牌进行交互时为客户提供增强的个性化体验。

请访问 [利用机器学习洞察扩充实时客户档案](./enrich-profile.md) 以进一步了解如何利用机器学习分析。
