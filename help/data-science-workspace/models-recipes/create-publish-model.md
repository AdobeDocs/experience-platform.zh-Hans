---
keywords: Experience Platform；机器学习模型；Data Science Workspace；热门主题；创建和发布模型
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

以下指南介绍了创建和发布机器学习模型所需的步骤。 每个部分都包含将要执行的操作的描述，以及一个指向UI和API文档的链接，以便执行所述步骤。

## 快速入门

在开始本教程之前，您必须满足以下先决条件：

- 访问 [!DNL Adobe Experience Platform]. 如果您无权访问中的组织 [!DNL Experience Platform]，请在继续之前与系统管理员联系。

- 所有数据科学工作区教程都使用Luma倾向模型。 为了遵循，您必须已创建 [Luma倾向模型架构和数据集](./create-luma-data.md).

### 浏览数据并了解架构

登录 [Adobe Experience Platform](https://platform.adobe.com/) 并选择 **[!UICONTROL 数据集]** 以列出所有现有数据集并选择要浏览的数据集。 在这种情况下，您应选择 **Luma Web数据** 数据集。

![选择Luma Web数据集](../images/models-recipes/model-walkthrough/luma-dataset.png)

随即会打开数据集活动页面，其中列出与数据集相关的信息。 您可以选择 **[!UICONTROL 预览数据集]** 右上角附近，用于检查样本记录。 您还可以查看选定数据集的架构。

![预览Luma Web数据](../images/models-recipes/model-walkthrough/preview-dataset.png)

在右边栏中选择架构链接。 此时会出现一个弹出窗口，选择下面的链接 **[!UICONTROL 架构名称]** 在新选项卡中打开架构。

![预览luma web数据架构](../images/models-recipes/model-walkthrough/preview-schema.png)

您可以使用提供的探索数据分析(EDA)笔记本进一步浏览数据。 此笔记本可用于帮助了解Luma数据中的模式、检查数据是否正常以及总结预测倾向模型的相关数据。 要了解有关探索性数据分析的更多信息，请访问 [EDA文档](../jupyterlab/eda-notebook.md).

## 创建Luma倾向方法 {#author-your-model}

的主要组件 [!DNL Data Science Workspace] 生命周期涉及创作方法和模型。 Luma倾向模型旨在预测客户是否有从Luma购买产品的高倾向。

要创建Luma倾向模型，请使用方法生成器模板。 配方是模型的基础，因为它们包含用于解决特定问题的机器学习算法和逻辑。 更重要的是，“方法”使您能够让整个组织的机器学习普及化，使其他用户无需编写任何代码即可访问用于不同用例的模型。

请遵循 [使用JupyterLab Notebooks创建模型](../jupyterlab/create-a-model.md) 本教程将创建在后续教程中使用的Luma倾向模型方法。

## 从外部源导入和打包方法(*可选*)

如果您希望导入并打包方法以用于Data Science Workspace，则必须将源文件打包到存档文件中。 请遵循 [将源文件打包到方法中](./package-source-files-recipe.md) 教程。 本教程向您展示了如何将源文件打包到方法中，这是将方法导入数据科学工作区的先决条件步骤。 完成本教程后，将在Azure容器注册表中为您提供Docker图像，以及相应的图像URL，即存档文件。

此存档文件可用于在数据科学工作区中创建方法，方法是使用遵循方法导入工作流 [UI工作流](./import-packaged-recipe-ui.md) 或 [API工作流](./import-packaged-recipe-api.md).

## 训练和评估模型 {#train-and-evaluate-your-model}

现在您的数据已准备好，方法已准备就绪，您能够进一步创建、训练和评估您的机器学习模型。 在使用方法生成器时，您应该先对模型进行培训、评分和评估，然后再将其打包到方法中。

数据科学工作区UI和API允许您将方法作为模型发布。 此外，还可进一步微调模型的特定方面，如添加、删除和更改超参数。

### 创建模型

要了解有关使用UI创建模型的更多信息，请访问培训并在数据科学工作区中评估模型 [用户界面教程](./train-evaluate-model-ui.md) 或 [api教程](./train-evaluate-model-api.md). 本教程提供了一个示例，说明如何创建、训练和更新超参数以微调模型。

>[!NOTE]
>
> 无法学习超参数，因此必须在运行训练之前分配超参数。 调整超参数可能会改变已训练模型的精度。 由于优化模型是一个迭代过程，可能需要多次训练才能获得满意的评价。

## 为模型评分 {#score-a-model}

创建和发布模型的下一步是使模型可操作化，以便从数据湖和实时客户档案为见解评分和使用。

数据科学工作区中的评分可通过将输入数据馈送到现有的已训练模型来实现。 评分结果将作为新批次存储在指定的输出数据集中以供查看。

要了解如何为模型评分，请访问模型评分 [用户界面教程](./score-model-ui.md) 或 [api教程](./score-model-api.md).

## 将已评分模型发布为服务

Data Science Workspace允许您将经过培训的模型发布为服务。 这使您组织内的用户无需创建自己的模型即可对数据进行评分。

要了解如何将模型发布为服务，请访问 [用户界面教程](./publish-model-service-ui.md) 或 [api教程](./publish-model-service-api.md).

### 安排服务的自动培训

将模型发布为服务后，即可为机器学习服务设置计划的评分和训练运行。 自动化培训和评分过程有助于通过及时了解数据中的模式来维护和改进服务的效率。 访问 [在数据科学工作区UI中计划模型](./schedule-models-ui.md) 教程。

>[!NOTE]
>
> 您只能通过UI计划用于自动训练和评分的模型。

## 后续步骤 {#next-steps}

Adobe Experience Platform [!DNL Data Science Workspace] 提供用于创建、评估和利用机器学习模型以生成数据预测和洞察的工具和资源。 将机器学习分析摄取到 [!DNL Profile] — 启用的数据集，则同样的数据也会被摄取为 [!DNL Profile] 记录，然后可以使用以下方式对其进行分段： [!DNL Adobe Experience Platform Segmentation Service].

在摄取用户档案和时间序列数据时，实时客户档案会通过称为流式客户细分的持续过程自动决定从区段包含或排除该数据，然后再将其与现有数据合并并更新合并视图。 因此，您可以即时执行计算并做出决策，以便在客户与您的品牌互动时为他们提供经过增强、个性化的体验。

访问教程，了解 [利用机器学习见解丰富Real-time Customer Profile](./enrich-profile.md) 详细了解如何利用机器学习见解。
