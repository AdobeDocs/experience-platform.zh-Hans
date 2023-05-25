---
keywords: Experience Platform；预览架构数据；Data Science Workspace；热门主题
solution: Experience Platform
title: 预览零售架构和数据集
type: Tutorial
description: 以下文档概述了在Adobe Experience Platform上预览架构和数据集。
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# 预览零售架构和数据集

成功完成bootstrap脚本后， [零售架构和数据集](./create-retails-sales-dataset.md) 教程。 可以在以下位置查看输出架构和数据集： [!DNL Experience Platform]. 要查看架构和数据集，请执行以下步骤：

选择 **[!UICONTROL 架构]** 选项卡，查找由引导脚本创建的输入架构。 架构的名称将对应于中定义的名称 `config.yaml` 上一步骤中的。 通过单击架构中的可查看架构详细信息及其组成。

![](../images/models-recipes/access-data/schema.PNG)

选择 **[!UICONTROL 数据集]** 选项卡，打开通过选择数据集的名称创建的输入数据集。 数据集的名称对应于中定义的名称 `config.yaml` 上一步骤中的。

![](../images/models-recipes/access-data/dataset.PNG)

选择 **[!UICONTROL 预览数据集]** 位于右上角，用于预览数据集的子集。

![](../images/models-recipes/access-data/preview.PNG)

## 后续步骤

您现在已成功将零售业示例数据摄取到 [!DNL Experience Platform] 使用提供的引导脚本。

要继续使用摄取的数据，请执行以下操作：
- [使用Jupyter Notebooks分析数据](../jupyterlab/analyze-your-data.md)
   - 在中使用Jupyter Notebooks [!DNL Data Science Workspace] 访问、浏览、可视化和了解您的数据。
- [将源文件打包到方法中](./package-source-files-recipe.md)
   - 按照本教程中的说明进行操作，了解如何将您自己的模型导入 [!DNL Data Science Workspace] 将源文件打包到可导入的配方文件中。
