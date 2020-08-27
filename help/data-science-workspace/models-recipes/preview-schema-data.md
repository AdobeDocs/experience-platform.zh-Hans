---
keywords: Experience Platform;preview schema data;Data Science Workspace;popular topics
solution: Experience Platform
title: 预览模式和数据集
topic: Tutorial
description: 以下文档概述了预览Adobe Experience Platform上的模式和数据集。
translation-type: tm+mt
source-git-commit: 7615476c4b728b451638f51cfaa8e8f3b432d659
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---


# 预览模式和数据集

成功完成引导脚本后，请参 [阅创建零售销售模式和数据集教程](./create-retails-sales-dataset.md) 。 可以在上查看输出模式和数据集 [!DNL Experience Platform]。 要视图模式和数据集，请按照以下步骤操作：

1. 单击左 **[!UICONTROL 侧导航]** 列中的模式链接，并查找由引导脚本创建的输入模式。 模式的名称将与上一步中定义 `config.yaml` 的名称相对应。 视图模式详细信息，并通过单击它进行合成。

   ![](../images/models-recipes/access-data/schema_overview.png)

2. 单击左 **[!UICONTROL 侧导航列]** 中的“数据集”链接，然后打开通过单击列表名称创建的输入数据集。 数据集的名称将与上一步中定义 `config.yaml` 的内容相对应。

   ![](../images/models-recipes/access-data/dataset_overview.png)

3. 单 **[!UICONTROL 击右上方]** 的预览数据集预览数据集的子集。

   ![](../images/models-recipes/access-data/preview_dataset.png)

## 后续步骤

您现在已使用提供的引导脚本成功将零售 [!DNL Experience Platform] 销售示例数据引入。

要继续处理所摄取的数据：
- [使用Jupyter笔记本分析数据](../jupyterlab/analyze-your-data.md)
   - 使用Jupyter笔记本 [!DNL Data Science Workspace] 访问、探索、可视化和了解您的数据。
- [将源文件打包到菜谱中](./package-source-files-recipe.md)
   - 请按照本教程学习如何通过将源文件打包到可 [!DNL Data Science Workspace] 导入的Recipe文件中，将自己的Model引入其中。