---
keywords: Experience Platform;preview schema data;Data Science Workspace;popular topics
solution: Experience Platform
title: 预览模式和数据集
topic: Tutorial
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34

---


# 预览模式和数据集

成功完成引导脚本后，请参 [阅创建零售销售模式和数据集教程](./create-retails-sales-dataset.md) 。 输出模式和数据集可在Experience Platform上查看。 要视图模式和数据集，请按照以下步骤操作：

1. 单击左 **[!UICONTROL Schemas]** 侧导航列中的链接，找到由引导脚本创建的输入模式。 模式的名称将与上一步中定义 `config.yaml` 的名称相对应。 视图模式详细信息，并通过单击它进行合成。

   ![](../images/models-recipes/access-data/schema_overview.png)

2. 单击左 **[!UICONTROL Datasets]** 侧导航列中的链接，然后打开通过单击列表名称创建的输入数据集。 数据集的名称将与上一步中定义 `config.yaml` 的内容相对应。

   ![](../images/models-recipes/access-data/dataset_overview.png)

3. 单击 **[!UICONTROL Preview Dataset]** 位于右上方预览数据集的子集。

   ![](../images/models-recipes/access-data/preview_dataset.png)

## 后续步骤

您现在已使用提供的引导脚本成功将零售销售范例数据引入Experience Platform。

要继续处理所摄取的数据：
- [使用Jupyter笔记本分析数据](../jupyterlab/analyze-your-data.md)
   - 在数据科学工作区中使用Jupyter笔记本，访问、探索、可视化和了解您的数据。
- [将源文件打包到菜谱中](./package-source-files-recipe.md)
   - 按照本教程学习如何通过将源文件打包到可导入的Recipe文件中，将您自己的模型引入数据科学工作区。