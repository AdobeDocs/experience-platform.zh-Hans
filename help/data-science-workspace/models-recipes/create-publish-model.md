---
keywords: Experience Platform；机器学习模型；数据科学工作区；热门主题；创建和发布模型
solution: Experience Platform
title: 创建和发布机器学习模型
topic: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace提供了使用预建的产品Recommendations菜谱实现目标的方法。 按照本教程，了解如何访问和了解您的零售数据、创建和优化机器学习模型以及在数据科学工作区中生成洞察。
translation-type: tm+mt
source-git-commit: b5d42c6a38a50d39e1ca46e18623dde59c33833b
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 0%

---


# 创建和发布机器学习模型

![](../images/models-recipes/model-walkthrough/objective.png)

假装您拥有在线零售网站。 当您的客户在您的零售网站上购物时，您希望向他们展示个性化的产品推荐，以展示您的业务优惠的各种其他产品。 在您网站的整个存在过程中，您不断收集客户数据并希望以某种方式利用这些数据生成个性化的产品推荐。

[!DNL Adobe Experience Platform] [!DNL Data Science Workspace] 借助预建的产品Recommendations菜谱，提供实现 [您目标的方法](../pre-built-recipes/product-recommendations.md)。请阅读本教程，了解如何访问和了解您的零售数据、创建和优化机器学习模型以及在[!DNL Data Science Workspace]中生成洞察。

本教程介绍了[!DNL Data Science Workspace]的工作流程，并介绍了创建机器学习模型的以下步骤：

1. [准备数据](#prepare-your-data)
2. [创作模型](#author-your-model)
3. [培训和评估您的模型](#train-and-evaluate-your-model)
4. [操作模型](#operationalize-your-model)

## 入门指南

在开始本教程之前，您必须具备以下先决条件：

- 访问[!DNL Adobe Experience Platform]。 如果您无权访问[!DNL Experience Platform]中的IMS组织，请在继续操作之前与您的系统管理员联系。

- Enablement Assets。 请联系您的客户代表，为您提供以下项目。
   - Recommendations菜谱
   - Recommendations输入数据集
   - Recommendations输入模式
   - Recommendations输出数据集
   - Recommendations输出模式
   - Golden Data Set postValues
   - 黄金数据集模式

- 从[Adobe public [!DNL Git] repository](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources/Notebooks-Thurs)下载三个必需的[!DNL Jupyter Notebook]文件，这些文件将用于演示[!DNL Data Science Workspace]中的[!DNL JupyterLab]工作流。

了解本教程中使用的以下主要概念：
- [[!DNL Experience Data Model]](../../xdm/home.md):由Adobe领导的标准化工作，为客户体验管理定 [!DNL Profile] 义标准模式，如和ExperienceEvent。
- 数据集：实际数据的存储和管理结构。 [XDM模式](../../xdm/schema/field-dictionary.md)的物理实例化实例。
- 批：数据集由批量组成。 批是在一段时间内收集的一组数据，并作为单个单元一起处理。
- [!DNL JupyterLab]: [[!DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) 是一个面向Project的开放源代码、基于web的 [!DNL Jupyter] 界面，并紧密集成到 [!DNL Experience Platform]中

## 准备数据{#prepare-your-data}

要创建能够向客户推荐个性化产品的机器学习模型，必须分析您网站上先前的客户购买。 本节探讨如何通过[!DNL Adobe Analytics]将此数据引入[!DNL Platform]，以及如何将该数据转换为要由机器学习模型使用的特征数据集。

### 浏览数据并了解模式

登录到[Adobe Experience Platform](https://platform.adobe.com/)并选择&#x200B;**[!UICONTROL 数据集]**&#x200B;以列表所有现有数据集并选择要浏览的数据集。 在这种情况下，[!DNL Analytics]数据集&#x200B;**Golden Data Set postValues**。

![](../images/models-recipes/model-walkthrough/dataset-browse.png)

此时将打开数据集活动页，其中列出与您的数据集相关的信息。 您可以选择右上角附近的&#x200B;**[!UICONTROL 预览数据集]**&#x200B;来检查示例记录。 您还可以视图所选数据集的模式。 在右边栏中选择模式链接。 出现一个弹出窗口，选择&#x200B;**[!UICONTROL 模式名称]**&#x200B;下的链接将在新选项卡中打开模式。

![](../images/models-recipes/model-walkthrough/dataset-activity.png)


![](../images/models-recipes/model-walkthrough/schema-view.png)

其他数据集已预填充了批，以用于预览。 您可以重复上述步骤来视图这些数据集。

| 数据集名称 | 架构 | 描述 |
| ----- | ----- | ----- |
| Golden Data Set postValues | 黄金数据集模式 | [!DNL Analytics] 您网站中的源数据 |
| Recommendations输入数据集 | Recommendations输入模式 | 使用功能管道将[!DNL Analytics]数据转换为培训数据集。 此数据用于培训产品Recommendations机器学习模型。 `itemid` 与该 `userid` 客户购买的产品相对应。 |
| Recommendations输出数据集 | Recommendations输出模式 | 存储了评分结果的数据集，其中将包含每个客户推荐产品的列表。 |

## 创作模型{#author-your-model}

[!DNL Data Science Workspace]生命周期的第二个组件涉及创作方法和模型。 产品Recommendations菜谱旨在通过利用过去的购买数据和机器学习大规模生成产品推荐。

菜谱是模型的基础，因为它们包含机器学习算法和用于解决特定问题的逻辑。 更重要的是，秘诀使您能够在整个组织内实现机器学习的大众化，使其他用户无需编写任何代码即可访问针对不同使用案例的模型。

### 浏览产品Recommendations菜谱

在Experience Platform中，从左侧导航列导航到&#x200B;**[!UICONTROL Models]**，然后在顶部导航中选择&#x200B;**[!UICONTROL 方法]**&#x200B;以视图组织的可用方法列表。

![](../images/models-recipes/model-walkthrough/recipe-tab.png)

接下来，通过选择提供的&#x200B;**[!UICONTROL Recommendations菜谱]**&#x200B;名称，找到并打开它。 此时将显示“菜谱”概述页。

![](../images/models-recipes/model-walkthrough/Recipe-view.png)

然后，在右边栏中，选择&#x200B;**[!UICONTROL Recommendations输入模式]**&#x200B;以视图为菜谱加电的模式。 模式字段“[!UICONTROL itemId]”和“[!UICONTROL userId]”对应于该客户在特定时间([!UICONTROL timestamp])购买的产品([!UICONTROL interactionType])。 按照相同的步骤查看&#x200B;**[!UICONTROL Recommendations输出模式]**&#x200B;的字段。

![](../images/models-recipes/model-walkthrough/input-output.png)

您现在已查看了产品Recommendations方法所需的输入和输出模式。 请继续阅读下一节，了解如何创建、培训和评估产品Recommendations模型。

## 培训和评估您的型号{#train-and-evaluate-your-model}

现在您的数据已准备就绪，菜谱已准备就绪，您可以创建、培训和评估您的机器学习模型。

### 创建模型

“模型”是“处方”的实例，使您能够大规模地对数据进行培训和评分。

在Experience Platform中，从左侧导航列导航到&#x200B;**[!UICONTROL Models]**，然后在顶部导航中选择&#x200B;**[!UICONTROL 方法]**。 它显示组织的可用菜谱的列表。选择产品推荐菜谱。

![](../images/models-recipes/model-walkthrough/recipe-tab.png)

在菜谱页中，选择&#x200B;**[!UICONTROL 创建模型]**。

![创建模型](../images/models-recipes/model-walkthrough/create-model-recipe.png)

通过选择菜谱开始创建模型工作流。 选择&#x200B;**[!UICONTROL Recommendations菜谱]**，然后选择右上角的&#x200B;**[!UICONTROL 下一个]**。

![](../images/models-recipes/model-walkthrough/create-model.png)

然后，提供模型名称。 列出了模型的可用配置，其中包含模型默认培训和评分行为的设置。 查看配置并选择&#x200B;**[!UICONTROL 完成]**。

![](../images/models-recipes/model-walkthrough/configure-model.png)

您将通过新生成的培训运行重定向模型概述页面。 默认情况下，创建模型时会生成培训运行。

![](../images/models-recipes/model-walkthrough/model-overview.png)

您可以选择等待培训运行完成，或在下一节中继续创建新的培训运行。

### 使用自定超参数训练模型

在&#x200B;**模型概述**&#x200B;页面上，选择右上角附近的&#x200B;**[!UICONTROL 培训]**&#x200B;以创建新的培训运行。 选择创建模型时使用的相同输入数据集，然后选择&#x200B;**[!UICONTROL 下一步]**。

![](../images/models-recipes/model-walkthrough/select-train.png)

将显示&#x200B;**[!UICONTROL Configuration]**&#x200B;页。 您可以在此配置培训运行`num_recommendations`值，也称为超参数。 训练和优化模型将根据训练结果利用性能最佳的超参数。

无法学习超参数，因此必须在进行培训运行之前分配超参数。 调整超参数可能会改变训练模型的精度。 由于优化模型是一个迭代过程，因此在获得满意的评价之前可能需要多次训练运行。

>[!TIP]
>
>将`num_recommendations`设置为10。

![](../images/models-recipes/model-walkthrough/training-configuration.png)

模型评估图表上会显示其他数据点。 运行完成后，此图标最多可能需要几分钟才能显示。

![](../images/models-recipes/model-walkthrough/training-graphs.png)

### 评估模型

每次培训运行完成时，您都可以视图生成的评估量度，以确定模型的执行情况。

要查看每个已完成培训运行的评估量度（“精确度”和“召回率”），请选择培训运行。

![](../images/models-recipes/model-walkthrough/select-training-run.png)

您可以浏览为每个评估量度提供的信息。 这些指标越高，模型的表现就越好。

![](../images/models-recipes/model-walkthrough/metrics.png)

您可以在右侧边栏上查看用于每个培训运行的数据集、模式和配置参数。 导航回“模型”页，通过观察其评估量度来确定运行效果最佳的培训。

## 操作模型{#operationalize-your-model}

数据科学工作流程的最后一步是操作模型，以便从数据存储中得分和使用洞察。

### 评分和生成洞察

在“产品推荐模型概述”页面上，选择性能最佳的培训运行的名称，其召回率和准确度值最高。

![打得最好](../images/models-recipes/model-walkthrough/select-training-run.png)

然后，在培训运行详细信息页面的右上角，选择&#x200B;**[!UICONTROL 得分]**。

![选择分数](../images/models-recipes/model-walkthrough/select-score.png)

接下来，选择&#x200B;**[!UICONTROL Recommendations输入数据集]**&#x200B;作为评分输入数据集，该数据集与您创建模型并执行其培训运行时使用的数据集相同。 然后，选择&#x200B;**[!UICONTROL 下一步]**。

![](../images/models-recipes/model-walkthrough/score-input.png)

获得输入数据集后，选择&#x200B;**[!UICONTROL Recommendations输出数据集]**&#x200B;作为评分输出数据集。 评分结果作为批存储在此数据集中。

![](../images/models-recipes/model-walkthrough/score-output.png)

最后，查看评分配置。 这些参数包含您之前选择的输入和输出数据集以及相应的模式。 选择&#x200B;**[!UICONTROL 完成]**&#x200B;以开始计分运行。 运行可能需要几分钟才能完成。

![](../images/models-recipes/model-walkthrough/score-finish.png)

### 视图的洞察

评分运行成功完成后，您可以预览结果并视图生成的洞察。

在评分运行页面上，选择已完成的评分运行，然后选择右边栏上的&#x200B;**[!UICONTROL 预览评分结果数据集]**。

![](../images/models-recipes/model-walkthrough/preview-scores.png)

在预览表中，每行包含针对特定客户的产品推荐，分别标记为[!UICONTROL recommendations]和[!UICONTROL userId]。 由于在示例截屏中将[!UICONTROL num_recommendations]超参数设置为10，因此每行推荐最多可包含10个以数字符号(#)分隔的产品标识。

![](../images/models-recipes/model-walkthrough/preview_score_results.png)

## 后续步骤 {#next-steps}

本教程向您介绍了[!DNL Data Science Workspace]的工作流程，演示如何通过机器学习将未处理的原始数据转换为有用的信息。 要了解有关使用[!DNL Data Science Workspace]的详细信息，请继续阅读有关创建零售销售模式和数据集](./create-retails-sales-dataset.md)的下一个指南。[