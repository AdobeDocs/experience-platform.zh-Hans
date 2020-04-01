---
keywords: Experience Platform;preview schema data;Data Science Workspace;popular topics
solution: Experience Platform
title: 预览模式和数据集
topic: Tutorial
translation-type: tm+mt
source-git-commit: 11eb1859f3e4b059765709e750f18b61509a2f93

---


# 预览模式和数据集

成功完成引导脚本后，请参阅创 [建零售模式和数据集教程](./create-retails-sales-dataset.md) 。 输出模式和数据集可在Experience Platform上查看。 要视图模式和数据集，请执行以下步骤：

1. 单击左 **侧导航列中的模式** ，然后找到由引导脚本创建的输入模式。 模式的名称将与上一步中定义的 `config.yaml` 名称相对应。 视图模式详细信息及其组成，只需单击它。

   ![](../images/models-recipes/access-data/schema_overview.png)

2. 单击位 **于左侧导航列的Datasets** （数据集）链接，然后打开通过单击列表名称创建的输入数据集。 数据集的名称将与上一步中定义的 `config.yaml` 名称相对应。

   ![](../images/models-recipes/access-data/dataset_overview.png)

3. 单击 **预览位于右上方的数据集** ，以预览数据集的子集。

   ![](../images/models-recipes/access-data/preview_dataset.png)

## 后续步骤

您现在已使用提供的引导脚本成功地将零售销售范例数据引入Experience Platform。

要继续使用摄取的数据，请执行以下操作：
- [使用Jupyter笔记本分析数据](../jupyterlab/analyze-your-data.md)
   - 使用Data Science Workspace中的Jupyter笔记本电脑访问、探索、可视化和了解您的数据。
- [将源文件打包到菜谱中](./package-source-files-recipe.md)
   - 按照本教程学习如何通过将源文件打包到可导入的Recipe文件中，将您自己的模型引入数据科学工作区。