---
keywords: Experience Platform；预览架构数据；Data Science Workspace；热门主题
solution: Experience Platform
title: 预览零售销售架构和数据集
type: Tutorial
description: 以下文档概述了在Adobe Experience Platform上预览架构和数据集。
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# 预览零售销售架构和数据集

成功完成从 [零售销售架构和数据集](./create-retails-sales-dataset.md) 教程。 可以在上查看输出架构和数据集 [!DNL Experience Platform]. 要查看架构和数据集，请执行以下步骤：

选择 **[!UICONTROL 模式]** 选项卡，并找到由引导脚本创建的输入模式。 架构的名称将与 `config.yaml` 中。 通过单击查看架构详细信息及其组成。

![](../images/models-recipes/access-data/schema.PNG)

选择 **[!UICONTROL 数据集]** 选项卡，然后打开通过选择数据集名称创建的输入数据集。 数据集的名称对应于 `config.yaml` 中。

![](../images/models-recipes/access-data/dataset.PNG)

选择 **[!UICONTROL 预览数据集]** 位于右上方，用于预览数据集的子集。

![](../images/models-recipes/access-data/preview.PNG)

## 后续步骤

您现在已成功将零售销售示例数据摄取到 [!DNL Experience Platform] 使用提供的引导脚本。

要继续使用摄取的数据，请执行以下操作：
- [使用Jupyter Notebooks分析数据](../jupyterlab/analyze-your-data.md)
   - 在 [!DNL Data Science Workspace] 以访问、探索、可视化和了解您的数据。
- [将源文件打包到方法中](./package-source-files-recipe.md)
   - 请阅读本教程，了解如何将您自己的模型引入 [!DNL Data Science Workspace] 将源文件打包到可导入的方法文件中。
