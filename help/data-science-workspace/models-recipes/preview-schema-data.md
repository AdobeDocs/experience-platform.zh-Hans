---
keywords: Experience Platform;预览模式数据；数据科学工作区；热门主题
solution: Experience Platform
title: 预览零售销售模式和数据集
topic: tutorial
type: Tutorial
description: 以下文档概述了预览Adobe Experience Platform上的模式和数据集。
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# 预览零售模式和数据集

成功完成[创建零售销售模式和数据集](./create-retails-sales-dataset.md)教程中的引导脚本后。 可在[!DNL Experience Platform]上查看输出模式和数据集。 要视图模式和数据集，请按照以下步骤操作：

1. 单击左侧导航列中的&#x200B;**[!UICONTROL 模式]**&#x200B;链接，找到由引导脚本创建的输入模式。 模式的名称将与上一步中在`config.yaml`中定义的内容相对应。 视图模式详细信息，并通过单击它进行合成。

   ![](../images/models-recipes/access-data/schema_overview.png)

2. 单击左侧导航列中的&#x200B;**[!UICONTROL Datasets]**&#x200B;链接，然后打开通过单击列表名称创建的输入数据集。 数据集的名称将与上一步中在`config.yaml`中定义的内容相对应。

   ![](../images/models-recipes/access-data/dataset_overview.png)

3. 单击右上方的&#x200B;**[!UICONTROL 预览数据集]**&#x200B;预览数据集的子集。

   ![](../images/models-recipes/access-data/preview_dataset.png)

## 后续步骤

您现在已使用提供的引导脚本成功将零售销售示例数据引入[!DNL Experience Platform]。

要继续处理所摄取的数据：
- [使用Jupyter笔记本分析数据](../jupyterlab/analyze-your-data.md)
   - 使用[!DNL Data Science Workspace]中的Jupyter Notebooks访问、浏览、可视化和了解您的数据。
- [将源文件打包到菜谱中](./package-source-files-recipe.md)
   - 请按照本教程学习如何通过将源文件打包到可导入的Recipe文件中，将您自己的Model引入[!DNL Data Science Workspace]中。