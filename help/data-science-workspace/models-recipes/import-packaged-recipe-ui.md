---
keywords: Experience Platform；导入打包的配方；Data Science Workspace；热门主题；配方；ui；创建引擎
solution: Experience Platform
title: 在数据科学工作区UI中导入打包的处方
type: Tutorial
description: 本教程提供了有关如何使用提供的零售示例配置和导入打包方法的分析。 在本教程结束时，您将准备好在Adobe Experience Platform数据科学工作区中创建、培训和评估模型。
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1832'
ht-degree: 0%

---

# 在数据科学工作区UI中导入打包的处方

本教程提供了有关如何使用提供的零售示例配置和导入打包方法的分析。 在本教程结束时，您将准备好在Adobe Experience Platform中创建、培训和评估模型 [!DNL Data Science Workspace].

## 先决条件

本教程需要采用Docker图像URL形式的打包方法。 请参阅教程，了解如何 [将源文件打包到方法中](./package-source-files-recipe.md) 了解更多信息。

## UI工作流

将包装的配方导入 [!DNL Data Science Workspace] 需要特定的方法配置，编译为一个JavaScript对象表示法(JSON)文件，这种方法配置的编译称为配置文件。 具有特定配置集的包装配方称为配方实例。 一种方法可用于在中创建多个方法实例 [!DNL Data Science Workspace].

用于导入程序包方法的工作流包含以下步骤：
- [配置方法](#configure)
- [基于Docker的导入方法 — Python](#python)
- [导入基于Docker的方法 — R](#r)
- [导入基于Docker的方法 — PySpark](#pyspark)
- [基于Docker的导入方法 — Scala](#scala)

### 配置方法 {#configure}

中的每个方法实例 [!DNL Data Science Workspace] 随附一组配置，这些配置定制方法实例以适应特定用例。 配置文件定义使用此方法实例创建的模型的默认训练和评分行为。

>[!NOTE]
>
>配置文件特定于方法和大小写。

下面是一个示例配置文件，它显示零售方法默认的培训和评分行为。

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
| `learning_rate` | 数值 | 用于渐变乘法的标量。 |
| `n_estimators` | 数值 | 林中随机林分类器的树数。 |
| `max_depth` | 数值 | 随机林分类器中树的最大深度。 |
| `ACP_DSW_INPUT_FEATURES` | 字符串 | 逗号分隔的输入架构属性的列表。 |
| `ACP_DSW_TARGET_FEATURES` | 字符串 | 逗号分隔的输出架构属性的列表。 |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | 布尔值 | 确定输入和输出特征是否可修改 |
| `tenantId` | 字符串 | 此ID可确保正确命名您创建的资源，并将其包含在您的组织中。 [请按照此处的步骤操作](../../xdm/api/getting-started.md#know-your-tenant_id) 以查找您的租户ID。 |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 字符串 | 用于训练模型的输入架构。 在UI中导入时，请将此字段留空；使用API导入时，请将其替换为培训SchemaID。 |
| `evaluation.labelColumn` | 字符串 | 评估可视化图表的列标签。 |
| `evaluation.metrics` | 字符串 | 用于评估模型的评估指标列表（以逗号分隔）。 |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 字符串 | 用于对模型评分的输出架构。 在UI中导入时将此留空，在使用API导入时替换为评分SchemaID。 |

在本教程中，您可以将零售方法的默认配置文件保留在 [!DNL Data Science Workspace] 参考它们的方式。

### 导入基于Docker的方法 —  [!DNL Python] {#python}

首先，导航并选择 **[!UICONTROL 工作流]** 位于左侧的 [!DNL Platform] UI。 接下来，选择 **导入方法** 并选择 **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

此 **配置** 页面 **导入方法** 此时会显示工作流。 输入处方的名称和说明，然后选择 **[!UICONTROL 下一个]** 在右上角。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在 [将源文件打包到方法中](./package-source-files-recipe.md) 教程，在使用Python源文件构建零售方法结束时提供了Docker URL。

一旦您使用 **选择源** 页面，粘贴与使用构建的已打包方法对应的Docker URL [!DNL Python] 中的源文件 **[!UICONTROL 源URL]** 字段。 接下来，通过拖放方式导入提供的配置文件，或者使用文件系统 **浏览器**. 提供的配置文件位于 `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. 选择 **[!UICONTROL Python]** 在 **运行时** 下拉菜单和 **[!UICONTROL 分类]** 在 **类型** 下拉菜单。 填写完所有内容后，选择 **[!UICONTROL 下一个]** 以继续执行 **管理架构**.

>[!NOTE]
>
> 类型支持 **[!UICONTROL 分类]** 和 **[!UICONTROL 回归]**. 如果您的模型不属于这些类型之一，请选择 **[!UICONTROL 自定义]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

接下来，在部分下选择零售销售输入和输出架构 **管理架构**，它们是使用 [创建零售架构和数据集](../models-recipes/create-retails-sales-dataset.md) 教程。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在 **功能管理** 部分，在架构查看器中选择租户标识以展开零售销售输入架构。 通过突出显示所需特征，然后选择任一特征来选择输入和输出特征 **[!UICONTROL 输入功能]** 或 **[!UICONTROL 目标功能]** 右侧 **[!UICONTROL 字段属性]** 窗口。 在本教程中，将 **[!UICONTROL weeklySales]** 作为  **[!UICONTROL 目标功能]** 而其他所有东西都是 **[!UICONTROL 输入功能]**. 选择 **[!UICONTROL 下一个]** 查看您新配置的方法。

查看方法，根据需要添加、修改或删除配置。 选择 **[!UICONTROL 完成]** 创建方法。

![](../images/models-recipes/import-package-ui/recipe_review.png)

继续执行 [后续步骤](#next-steps) 以了解如何在中创建模型 [!DNL Data Science Workspace] 使用新创建的零售方法。

### 导入基于Docker的方法 — R {#r}

首先，导航并选择 **[!UICONTROL 工作流]** 位于左侧的 [!DNL Platform] UI。 接下来，选择 **导入方法** 并选择 **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

此 **配置** 页面 **导入方法** 此时会显示工作流。 输入处方的名称和说明，然后选择 **[!UICONTROL 下一个]** 在右上角。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在 [将源文件打包到方法中](./package-source-files-recipe.md) 教程，在使用R源文件构建零售方法结束时提供了Docker URL。

一旦您使用 **选择源** 页面，将对应于使用R源文件构建的打包方法的Docker URL粘贴到 **[!UICONTROL 源URL]** 字段。 接下来，通过拖放方式导入提供的配置文件，或者使用文件系统 **浏览器**. 提供的配置文件位于 `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. 选择 **[!UICONTROL R]** 在 **运行时** 下拉菜单和 **[!UICONTROL 分类]** 在 **类型** 下拉菜单。 填写完所有内容后，选择 **[!UICONTROL 下一个]** 以继续执行 **管理架构**.

>[!NOTE]
>
> *类型* 支持 **[!UICONTROL 分类]** 和 **[!UICONTROL 回归]**. 如果您的模型不属于这些类型之一，请选择 **[!UICONTROL 自定义]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

接下来，在部分下选择零售销售输入和输出架构 **管理架构**，它们是使用 [创建零售架构和数据集](../models-recipes/create-retails-sales-dataset.md) 教程。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在 *功能管理* 部分，在架构查看器中选择租户标识以展开零售销售输入架构。 通过突出显示所需特征，然后选择任一特征来选择输入和输出特征 **[!UICONTROL 输入功能]** 或 **[!UICONTROL 目标功能]** 右侧 **[!UICONTROL 字段属性]** 窗口。 在本教程中，将 **[!UICONTROL weeklySales]** 作为  **[!UICONTROL 目标功能]** 而其他所有东西都是 **[!UICONTROL 输入功能]**. 选择 **[!UICONTROL 下一个]** 查看您的新配置方法。

查看方法，根据需要添加、修改或删除配置。 选择 **完成** 创建方法。

![](../images/models-recipes/import-package-ui/recipe_review.png)

继续执行 [后续步骤](#next-steps) 以了解如何在中创建模型 [!DNL Data Science Workspace] 使用新创建的零售方法。

### 导入基于Docker的方法 — PySpark {#pyspark}

首先，导航并选择 **[!UICONTROL 工作流]** 位于左侧的 [!DNL Platform] UI。 接下来，选择 **导入方法** 并选择 **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

此 **配置** 页面 **导入方法** 此时会显示工作流。 输入处方的名称和说明，然后选择 **[!UICONTROL 下一个]** 以继续。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在 [将源文件打包到方法中](./package-source-files-recipe.md) 教程，在使用PySpark源文件构建零售方法结束时提供了Docker URL。

一旦您使用 **选择源** 页面，将对应于使用PySpark源文件构建的打包方法的Docker URL粘贴到 **[!UICONTROL 源URL]** 字段。 接下来，通过拖放方式导入提供的配置文件，或者使用文件系统 **浏览器**. 提供的配置文件位于 `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. 选择 **[!UICONTROL PySpark]** 在 **运行时** 下拉菜单。 选择PySpark运行时后，默认工件会自动填充到 **[!UICONTROL Docker]**. 接下来，选择 **[!UICONTROL 分类]** 在 **类型** 下拉菜单。 填写完所有内容后，选择 **[!UICONTROL 下一个]** 以继续执行 **管理架构**.

>[!NOTE]
>
> *类型* 支持 **[!UICONTROL 分类]** 和 **[!UICONTROL 回归]**. 如果您的模型不属于这些类型之一，请选择 **[!UICONTROL 自定义]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

接下来，使用以下方式选择零售销售输入和输出架构： **管理架构** 选择器中，架构是使用中提供的引导脚本创建的 [创建零售架构和数据集](../models-recipes/create-retails-sales-dataset.md) 教程。

![管理架构](../images/models-recipes/import-package-ui/manage-schemas.png)

在 **功能管理** 部分，在架构查看器中选择租户标识以展开零售销售输入架构。 通过突出显示所需特征，然后选择任一特征来选择输入和输出特征 **[!UICONTROL 输入功能]** 或 **[!UICONTROL 目标功能]** 右侧 **[!UICONTROL 字段属性]** 窗口。 在本教程中，将 **[!UICONTROL weeklySales]** 作为  **[!UICONTROL 目标功能]** 而其他所有东西都是 **[!UICONTROL 输入功能]**. 选择 **[!UICONTROL 下一个]** 查看您新配置的方法。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

查看方法，根据需要添加、修改或删除配置。 选择 **[!UICONTROL 完成]** 创建方法。

![](../images/models-recipes/import-package-ui/recipe_review.png)

继续执行 [后续步骤](#next-steps) 以了解如何在中创建模型 [!DNL Data Science Workspace] 使用新创建的零售方法。

### 基于Docker的导入方法 — Scala {#scala}

首先，导航并选择 **[!UICONTROL 工作流]** 位于左侧的 [!DNL Platform] UI。 接下来，选择 **导入方法** 并选择 **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

此 **配置** 页面 **导入方法** 此时会显示工作流。 输入处方的名称和说明，然后选择 **[!UICONTROL 下一个]** 以继续。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在 [将源文件打包到方法中](./package-source-files-recipe.md) 教程，在使用Scala ([!DNL Spark])。

一旦您使用 **选择源** 页面，将对应于使用Scala源文件构建的打包方法的Docker URL粘贴到源URL字段中。 接下来，通过拖放方式导入提供的配置文件，或者使用文件系统浏览器。 提供的配置文件位于 `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. 选择 **[!UICONTROL Spark]** 在 **运行时** 下拉菜单。 一旦 [!DNL Spark] 运行时处于选中状态，默认工件自动填充到 **[!UICONTROL Docker]**. 接下来，选择 **[!UICONTROL 回归]** 从 **类型** 下拉菜单。 填写完所有内容后，选择 **[!UICONTROL 下一个]** 以继续执行 **管理架构**.

>[!NOTE]
>
> 类型支持 **[!UICONTROL 分类]** 和 **[!UICONTROL 回归]**. 如果您的模型不属于这些类型之一，请选择 **[!UICONTROL 自定义]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

接下来，使用以下方式选择零售销售输入和输出架构： **管理架构** 选择器中，架构是使用中提供的引导脚本创建的 [创建零售架构和数据集](../models-recipes/create-retails-sales-dataset.md) 教程。

![管理架构](../images/models-recipes/import-package-ui/manage-schemas.png)

在 **功能管理** 部分，在架构查看器中选择租户标识以展开零售销售输入架构。 通过突出显示所需特征，然后选择任一特征来选择输入和输出特征 **[!UICONTROL 输入功能]** 或 **[!UICONTROL 目标功能]** 右侧 **[!UICONTROL 字段属性]** 窗口。 在本教程中，请设置&quot;[!UICONTROL weeklySales]”作为  **[!UICONTROL 目标功能]** 而其他所有东西都是 **[!UICONTROL 输入功能]**. 选择 **[!UICONTROL 下一个]** 查看您新配置的方法。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

查看方法，根据需要添加、修改或删除配置。 选择 **[!UICONTROL 完成]** 创建方法。

![](../images/models-recipes/import-package-ui/recipe_review.png)

继续执行 [后续步骤](#next-steps) 以了解如何在中创建模型 [!DNL Data Science Workspace] 使用新创建的零售方法。

## 后续步骤 {#next-steps}

本教程提供了有关配置方法并将其导入到的见解 [!DNL Data Science Workspace]. 您现在可以使用新创建的方法创建、训练和评估模型。

- [在UI中训练和评估模型](./train-evaluate-model-ui.md)
- [使用API训练和评估模型](./train-evaluate-model-api.md)
