---
keywords: Experience Platform;预览模式数据；数据科学工作区；热门主题
solution: Experience Platform
title: 预览零售销售模式和数据集
topic: tutorial
type: Tutorial
description: 以下文档概述了在Adobe Experience Platform上预览模式和数据集。
translation-type: tm+mt
source-git-commit: 5129a75071af680bc54a7f60bb89ce32d3216d09
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 1%

---


# 预览零售销售模式和数据集

成功完成[零售销售模式和数据集](./create-retails-sales-dataset.md)教程中的引导脚本后。 可以在[!DNL Experience Platform]上查看输出模式和数据集。 要视图模式和数据集，请执行以下步骤：

选择位于左侧导航中的&#x200B;**[!UICONTROL 模式]**&#x200B;选项卡，并查找由引导脚本创建的输入模式。 模式的名称将与上一步中在`config.yaml`中定义的内容相对应。 视图模式详细信息，并通过单击它进行合成。

![](../images/models-recipes/access-data/schema.PNG)

选择左侧导航中的&#x200B;**[!UICONTROL Datasets]**&#x200B;选项卡，然后打开通过选择数据集名称创建的输入数据集。 数据集的名称与上一步`config.yaml`中定义的内容相对应。

![](../images/models-recipes/access-data/dataset.PNG)

选择位于右上角的&#x200B;**[!UICONTROL 预览数据集]**&#x200B;以预览数据集的子集。

![](../images/models-recipes/access-data/preview.PNG)

## 后续步骤

您现在已使用提供的引导脚本成功将零售销售示例数据引入[!DNL Experience Platform]。

要继续使用摄取的数据，请执行以下操作：
- [使用Jupyter笔记本分析数据](../jupyterlab/analyze-your-data.md)
   - 使用[!DNL Data Science Workspace]中的Jupyter Notebooks访问、浏览、可视化和了解您的数据。
- [将源文件打包到菜谱中](./package-source-files-recipe.md)
   - 请按照本教程学习如何通过将源文件打包到可导入的处方文件中，将您自己的模型引入[!DNL Data Science Workspace]中。