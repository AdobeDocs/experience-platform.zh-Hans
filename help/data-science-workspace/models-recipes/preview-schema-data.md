---
keywords: Experience Platform；预览架构数据；数据科学Workspace；热门主题
solution: Experience Platform
title: 预览零售架构和数据集
type: Tutorial
description: 以下文档概述了在Adobe Experience Platform上预览架构和数据集。
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 3%

---

# 预览零售架构和数据集

>[!NOTE]
>
>数据科学Workspace不再可供购买。
>
>本文档面向之前有权访问数据科学Workspace的现有客户。

成功完成[零售架构和数据集](./create-retails-sales-dataset.md)教程中的引导脚本后。 可以在[!DNL Experience Platform]上查看输出架构和数据集。 要查看架构和数据集，请执行以下步骤：

选择位于左侧导航栏中的&#x200B;**[!UICONTROL Schemas]**&#x200B;选项卡，并查找由引导脚本创建的输入架构。 架构的名称将对应于上一步中`config.yaml`定义的名称。 通过单击架构中的可查看架构详细信息和架构组成。

![](../images/models-recipes/access-data/schema.PNG)

选择位于左侧导航栏中的&#x200B;**[!UICONTROL Datasets]**&#x200B;选项卡，并打开通过选择数据集的名称创建的输入数据集。 数据集的名称对应于上一步中`config.yaml`定义的名称。

![](../images/models-recipes/access-data/dataset.PNG)

选择位于右上角的&#x200B;**[!UICONTROL Preview Dataset]**&#x200B;以预览数据集的子集。

![](../images/models-recipes/access-data/preview.PNG)

## 后续步骤

您现在已成功使用提供的引导脚本将零售业样本数据摄取到[!DNL Experience Platform]。

要继续使用摄取的数据，请执行以下操作：

- [使用 Jupyter Notebooks 分析数据](../jupyterlab/analyze-your-data.md)
   - 在[!DNL Data Science Workspace]中使用Jupyter Notebooks访问、浏览、可视化和了解您的数据。
- [将源文件打包到方法中](./package-source-files-recipe.md)
   - 按照本教程了解如何通过将源文件打包到可导入的方法文件中来将您自己的模型导入[!DNL Data Science Workspace]。
