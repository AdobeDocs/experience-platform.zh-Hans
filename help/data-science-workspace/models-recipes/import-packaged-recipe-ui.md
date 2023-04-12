---
keywords: Experience Platform；导入打包的方法；Data Science Workspace；热门主题；方法；UI；创建引擎
solution: Experience Platform
title: 在数据科学工作区UI中导入打包的方法
type: Tutorial
description: 本教程提供了有关如何使用提供的零售销售示例配置和导入打包方法的分析。 在本教程结束时，您将准备好在Adobe Experience Platform数据科学工作区中创建、培训和评估模型。
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1832'
ht-degree: 0%

---

# 在Data Science Workspace UI中导入打包的方法

本教程提供了有关如何使用提供的零售销售示例配置和导入打包方法的分析。 在本教程结束时，您将准备好在Adobe Experience Platform中创建、培训和评估模型 [!DNL Data Science Workspace].

## 先决条件

本教程需要以Docker图像URL形式打包的方法。 请参阅有关如何 [将源文件打包到方法中](./package-source-files-recipe.md) 以了解更多信息。

## UI工作流程

将打包的方法导入 [!DNL Data Science Workspace] 需要特定的方法配置(编译为单个JavaScript对象表示法(JSON)文件)，此方法配置的编译称为配置文件。 具有一组特定配置的打包方法称为方法实例。 一个方法可用于在 [!DNL Data Science Workspace].

导入资源包方法的工作流包含以下步骤：
- [配置方法](#configure)
- [导入基于Docker的方法 — Python](#python)
- [导入基于Docker的方法 — R](#r)
- [导入基于Docker的方法 — PySpark](#pyspark)
- [导入基于Docker的方法 — Scala](#scala)

### 配置方法 {#configure}

中的每个方法实例 [!DNL Data Science Workspace] 随附一组配置，这些配置定制了方法实例以适合特定用例。 配置文件定义使用此方法实例创建的模型的默认培训和评分行为。

>[!NOTE]
>
>配置文件是特定于方法和案例的。

下面是一个示例配置文件，其中显示了零售销售方法的默认培训和评分行为。

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "learning_rate",
                "value": "0.1"  
            },
            {
                "key": "n_estimators",
                "value": "100"
            },
            {
                "key": "max_depth",
                "value": "3"
            },
            {
                "key": "ACP_DSW_INPUT_FEATURES",
                "value": "date,store,storeType,storeSize,temperature,regionalFuelPrice,markdown,cpi,unemployment,isHoliday"
            },
            {
                "key": "ACP_DSW_TARGET_FEATURES",
                "value": "weeklySales"
            },
            {
                "key": "ACP_DSW_FEATURE_UPDATE_SUPPORT",
                "value": false
            },
            {
                "key": "tenantId",
                "value": "_{TENANT_ID}"
            },
            {
                "key": "ACP_DSW_TRAINING_XDM_SCHEMA",
                "value": "{SEE BELOW FOR DETAILS}"
            },
            {
                "key": "evaluation.labelColumn",
                "value": "weeklySalesAhead"
            },
            {
                "key": "evaluation.metrics",
                "value": "MAPE,MAE,RMSE,MASE"
            }
        ]
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "tenantId",
                "value": "_{TENANT_ID}"
            },
            {
                "key":"ACP_DSW_SCORING_RESULTS_XDM_SCHEMA",
                "value":"{SEE BELOW FOR DETAILS}"
            }
        ]
    }
]
```

| 参数键 | 类型 | 描述 |
| ----- | ----- | ----- |
| `learning_rate` | 数值 | 梯度乘的标量。 |
| `n_estimators` | 数值 | 随机林分类器的林中树的数量。 |
| `max_depth` | 数值 | 随机林分类器中树的最大深度。 |
| `ACP_DSW_INPUT_FEATURES` | 字符串 | 以逗号分隔的输入架构属性列表。 |
| `ACP_DSW_TARGET_FEATURES` | 字符串 | 以逗号分隔的输出架构属性列表。 |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | 布尔值 | 确定输入和输出功能是否可修改 |
| `tenantId` | 字符串 | 此ID可确保您创建的资源命名正确并包含在您的组织内。 [按照此处的步骤操作](../../xdm/api/getting-started.md#know-your-tenant_id) 以查找租户ID。 |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 字符串 | 用于培训模型的输入模式。 在UI中导入时，将此参数留空，在使用API导入时，将替换为培训架构ID。 |
| `evaluation.labelColumn` | 字符串 | 用于评估可视化的列标签。 |
| `evaluation.metrics` | 字符串 | 用于评估模型的评估量度列表（以逗号分隔）。 |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 字符串 | 用于对模型进行评分的输出架构。 在UI中导入时，将此参数留空，在使用API导入时，将替换为评分模式ID。 |

在本教程中，您可以将零售销售方法的默认配置文件保留在 [!DNL Data Science Workspace] 引用它们的方式。

### 导入基于Docker的方法 —  [!DNL Python] {#python}

首先，导航并选择 **[!UICONTROL 工作流]** 位于 [!DNL Platform] UI。 接下来，选择 **导入方法** 选择 **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

的 **配置** 页面 **导入方法** 工作流。 输入处方的名称和说明，然后选择 **[!UICONTROL 下一个]** 中。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在 [将源文件打包到方法中](./package-source-files-recipe.md) 教程中，在使用Python源文件构建零售销售方法结束时提供了Docker URL。

一旦你在 **选择源** ，请粘贴与使用 [!DNL Python] 源文件(位于 **[!UICONTROL 源URL]** 字段。 接下来，通过拖放导入提供的配置文件，或使用文件系统 **浏览器**. 提供的配置文件可在 `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. 选择 **[!UICONTROL Python]** 在 **运行时** 下拉和 **[!UICONTROL 分类]** 在 **类型** 下拉。 填写完所有内容后，选择 **[!UICONTROL 下一个]** 中，以继续 **管理架构**.

>[!NOTE]
>
> 类型支持 **[!UICONTROL 分类]** 和 **[!UICONTROL 回归]**. 如果模型不属于这些类型之一，请选择 **[!UICONTROL 自定义]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

接下来，在部分下选择零售销售输入和输出架构 **管理架构**，则是使用 [创建零售销售架构和数据集](../models-recipes/create-retails-sales-dataset.md) 教程。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在 **功能管理** 部分，在架构查看器中选择租户标识以展开零售销售输入架构。 通过突出显示所需特征并选择任一特征来选择输入和输出特征 **[!UICONTROL 输入功能]** 或 **[!UICONTROL Target功能]** 在右侧 **[!UICONTROL 字段属性]** 窗口。 在本教程中，请将 **[!UICONTROL weeklySales]** 作为  **[!UICONTROL Target功能]** 其他一切 **[!UICONTROL 输入功能]**. 选择 **[!UICONTROL 下一个]** 来查看新配置的方法。

根据需要查看方法、添加、修改或删除配置。 选择 **[!UICONTROL 完成]** 创建方法。

![](../images/models-recipes/import-package-ui/recipe_review.png)

转到 [后续步骤](#next-steps) 了解如何在 [!DNL Data Science Workspace] 使用新创建的零售销售方法。

### 导入基于Docker的方法 — R {#r}

首先，导航并选择 **[!UICONTROL 工作流]** 位于 [!DNL Platform] UI。 接下来，选择 **导入方法** 选择 **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

的 **配置** 页面 **导入方法** 工作流。 输入处方的名称和说明，然后选择 **[!UICONTROL 下一个]** 中。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在 [将源文件打包到方法中](./package-source-files-recipe.md) 教程中，在使用R源文件构建零售销售方法结束时提供了Docker URL。

一旦你在 **选择源** ，请在 **[!UICONTROL 源URL]** 字段。 接下来，通过拖放导入提供的配置文件，或使用文件系统 **浏览器**. 提供的配置文件可在 `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. 选择 **[!UICONTROL R]** 在 **运行时** 下拉和 **[!UICONTROL 分类]** 在 **类型** 下拉。 填写完所有内容后，选择 **[!UICONTROL 下一个]** 中，以继续 **管理架构**.

>[!NOTE]
>
> *类型* 支持 **[!UICONTROL 分类]** 和 **[!UICONTROL 回归]**. 如果模型不属于这些类型之一，请选择 **[!UICONTROL 自定义]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

接下来，在部分下选择零售销售输入和输出架构 **管理架构**，则是使用 [创建零售销售架构和数据集](../models-recipes/create-retails-sales-dataset.md) 教程。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在 *功能管理* 部分，在架构查看器中选择租户标识以展开零售销售输入架构。 通过突出显示所需特征并选择任一特征来选择输入和输出特征 **[!UICONTROL 输入功能]** 或 **[!UICONTROL Target功能]** 在右侧 **[!UICONTROL 字段属性]** 窗口。 在本教程中，请将 **[!UICONTROL weeklySales]** 作为  **[!UICONTROL Target功能]** 其他一切 **[!UICONTROL 输入功能]**. 选择 **[!UICONTROL 下一个]** 以查看新的“配置”方法。

根据需要查看方法、添加、修改或删除配置。 选择 **完成** 创建方法。

![](../images/models-recipes/import-package-ui/recipe_review.png)

转到 [后续步骤](#next-steps) 了解如何在 [!DNL Data Science Workspace] 使用新创建的零售销售方法。

### 导入基于Docker的方法 — PySpark {#pyspark}

首先，导航并选择 **[!UICONTROL 工作流]** 位于 [!DNL Platform] UI。 接下来，选择 **导入方法** 选择 **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

的 **配置** 页面 **导入方法** 工作流。 输入处方的名称和说明，然后选择 **[!UICONTROL 下一个]** 的问题。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在 [将源文件打包到方法中](./package-source-files-recipe.md) 教程中，在使用PySpark源文件构建零售销售方法结束时提供了Docker URL。

一旦你在 **选择源** ，请将与使用PySpark源文件构建的打包方法对应的Docker URL粘贴到 **[!UICONTROL 源URL]** 字段。 接下来，通过拖放导入提供的配置文件，或使用文件系统 **浏览器**. 提供的配置文件可在 `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. 选择 **[!UICONTROL PySpark]** 在 **运行时** 下拉。 选择PySpark运行时后，默认对象会自动填充到 **[!UICONTROL Docker]**. 接下来，选择 **[!UICONTROL 分类]** 在 **类型** 下拉。 填写完所有内容后，选择 **[!UICONTROL 下一个]** 中，以继续 **管理架构**.

>[!NOTE]
>
> *类型* 支持 **[!UICONTROL 分类]** 和 **[!UICONTROL 回归]**. 如果模型不属于这些类型之一，请选择 **[!UICONTROL 自定义]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

接下来，使用 **管理架构** 选择器中，使用提供的引导脚本创建了架构，该脚本位于 [创建零售销售架构和数据集](../models-recipes/create-retails-sales-dataset.md) 教程。

![管理模式](../images/models-recipes/import-package-ui/manage-schemas.png)

在 **功能管理** 部分，在架构查看器中选择租户标识以展开零售销售输入架构。 通过突出显示所需特征并选择任一特征来选择输入和输出特征 **[!UICONTROL 输入功能]** 或 **[!UICONTROL Target功能]** 在右侧 **[!UICONTROL 字段属性]** 窗口。 在本教程中，请将 **[!UICONTROL weeklySales]** 作为  **[!UICONTROL Target功能]** 其他一切 **[!UICONTROL 输入功能]**. 选择 **[!UICONTROL 下一个]** 来查看新配置的方法。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

根据需要查看方法、添加、修改或删除配置。 选择 **[!UICONTROL 完成]** 创建方法。

![](../images/models-recipes/import-package-ui/recipe_review.png)

转到 [后续步骤](#next-steps) 了解如何在 [!DNL Data Science Workspace] 使用新创建的零售销售方法。

### 导入基于Docker的方法 — Scala {#scala}

首先，导航并选择 **[!UICONTROL 工作流]** 位于 [!DNL Platform] UI。 接下来，选择 **导入方法** 选择 **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

的 **配置** 页面 **导入方法** 工作流。 输入处方的名称和说明，然后选择 **[!UICONTROL 下一个]** 的问题。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在 [将源文件打包到方法中](./package-source-files-recipe.md) 教程中，在使用Scala([!DNL Spark])源文件。

一旦你在 **选择源** ，请在“源URL”字段中粘贴与使用Scala源文件构建的打包方法对应的Docker URL。 接下来，通过拖放操作导入提供的配置文件，或使用文件系统浏览器。 提供的配置文件可在 `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. 选择 **[!UICONTROL 火花]** 在 **运行时** 下拉。 一旦 [!DNL Spark] 运行时被选中，默认对象会自动填充到 **[!UICONTROL Docker]**. 接下来，选择 **[!UICONTROL 回归]** 从 **类型** 下拉。 填写完所有内容后，选择 **[!UICONTROL 下一个]** 中，以继续 **管理架构**.

>[!NOTE]
>
> 类型支持 **[!UICONTROL 分类]** 和 **[!UICONTROL 回归]**. 如果模型不属于这些类型之一，请选择 **[!UICONTROL 自定义]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

接下来，使用 **管理架构** 选择器中，使用提供的引导脚本创建了架构，该脚本位于 [创建零售销售架构和数据集](../models-recipes/create-retails-sales-dataset.md) 教程。

![管理模式](../images/models-recipes/import-package-ui/manage-schemas.png)

在 **功能管理** 部分，在架构查看器中选择租户标识以展开零售销售输入架构。 通过突出显示所需特征并选择任一特征来选择输入和输出特征 **[!UICONTROL 输入功能]** 或 **[!UICONTROL Target功能]** 在右侧 **[!UICONTROL 字段属性]** 窗口。 在本教程中，请将“[!UICONTROL weeklySales]”作为  **[!UICONTROL Target功能]** 其他一切 **[!UICONTROL 输入功能]**. 选择 **[!UICONTROL 下一个]** 来查看新配置的方法。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

根据需要查看方法、添加、修改或删除配置。 选择 **[!UICONTROL 完成]** 创建方法。

![](../images/models-recipes/import-package-ui/recipe_review.png)

转到 [后续步骤](#next-steps) 了解如何在 [!DNL Data Science Workspace] 使用新创建的零售销售方法。

## 后续步骤 {#next-steps}

本教程对如何配置方法并将其导入提供了分析 [!DNL Data Science Workspace]. 您现在可以使用新创建的方法创建、训练和评估模型。

- [在UI中培训和评估模型](./train-evaluate-model-ui.md)
- [使用API培训和评估模型](./train-evaluate-model-api.md)
