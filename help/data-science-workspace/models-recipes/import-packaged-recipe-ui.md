---
keywords: Experience Platform；导入打包的方法；数据科学Workspace；热门主题；方法；ui；创建引擎
solution: Experience Platform
title: 在数据科学Workspace UI中导入打包的方法
type: Tutorial
description: 本教程将深入分析如何使用提供的零售示例配置和导入打包的方法。 在本教程结束时，您将可以在Adobe Experience Platform数据科学Workspace中创建、培训和评估模型。
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1855'
ht-degree: 0%

---

# 在数据科学Workspace UI中导入打包的方法

>[!NOTE]
>
>数据科学Workspace不再可供购买。
>
>本文档面向之前有权访问数据科学Workspace的现有客户。

本教程将深入分析如何使用提供的零售示例配置和导入打包的方法。 在本教程结束时，您将准备好在Adobe Experience Platform [!DNL Data Science Workspace]中创建、训练和评估模型。

## 先决条件

本教程需要以Docker图像URL形式打包的方法。 有关详细信息，请参阅关于如何[将源文件](./package-source-files-recipe.md)打包到方法中的教程。

## UI工作流

将打包的方法导入到[!DNL Data Science Workspace]中需要特定的方法配置，这些配置编译为单个JavaScript对象表示法(JSON)文件，这种方法配置的编译称为配置文件。 具有特定配置集的打包方法称为方法实例。 一个方法可用于在[!DNL Data Science Workspace]中创建多个方法实例。

用于导入程序包方法的工作流包含以下步骤：
- [配置方法](#configure)
- [导入基于Docker的方法 — Python](#python)
- [导入基于Docker的方法 — R](#r)
- [导入基于Docker的方法 — PySpark](#pyspark)
- [导入基于Docker的方法 — Scala](#scala)

### 配置方法 {#configure}

[!DNL Data Science Workspace]中的每个方法实例都随附了一组配置，这些配置定制方法实例以适应特定用例。 配置文件定义使用此方法实例创建的模型的默认训练和评分行为。

>[!NOTE]
>
>配置文件因具体方法和大小写而异。

下面是一个示例配置文件，其中显示零售方法的默认培训和评分行为。

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
| `n_estimators` | 数值 | 林中随机林分类器的树的数量。 |
| `max_depth` | 数值 | 随机林分类器中树的最大深度。 |
| `ACP_DSW_INPUT_FEATURES` | 字符串 | 逗号分隔的输入架构属性列表。 |
| `ACP_DSW_TARGET_FEATURES` | 字符串 | 逗号分隔的输出架构属性列表。 |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | 布尔值 | 确定输入和输出特征是否可修改 |
| `tenantId` | 字符串 | 此ID可确保正确命名您创建的资源，并将其包含在您的组织中。 [按照此处](../../xdm/api/getting-started.md#know-your-tenant_id)的步骤查找您的租户ID。 |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 字符串 | 用于训练模型的输入架构。 在UI中导入时，请将此字段留空；使用API导入时，请替换为培训SchemaID。 |
| `evaluation.labelColumn` | 字符串 | 评估可视化图表的列标签。 |
| `evaluation.metrics` | 字符串 | 用于评估模型的评估指标列表（以逗号分隔）。 |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 字符串 | 用于对模型评分的输出架构。 在UI中导入时，将此留空；使用API导入时，将替换为评分SchemaID。 |

在本教程中，您可以在[!DNL Data Science Workspace]引用中保留零售方法的默认配置文件，方法如下所示。

### 导入基于Docker的方法 — [!DNL Python] {#python}

首先导航并选择位于[!DNL Experience Platform] UI左上角的&#x200B;**[!UICONTROL 工作流]**。 接下来，选择&#x200B;**导入方法**&#x200B;并选择&#x200B;**[!UICONTROL 启动]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

此时将显示&#x200B;**导入方法**&#x200B;工作流的&#x200B;**配置**&#x200B;页面。 输入方法的名称和说明，然后选择右上角的&#x200B;**[!UICONTROL 下一步]**。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在将[源文件打包到方法](./package-source-files-recipe.md)教程中，在使用Python源文件构建零售方法结束时提供了Docker URL。

进入&#x200B;**选择源**&#x200B;页面后，将对应于使用[!DNL Python]源文件构建的打包方法的Docker URL粘贴到&#x200B;**[!UICONTROL Source URL]**&#x200B;字段中。 接下来，通过拖放方式导入提供的配置文件，或者使用文件系统&#x200B;**浏览器**。 提供的配置文件可在`experience-platform-dsw-reference/recipes/python/retail/retail.config.json`找到。 在&#x200B;**运行时**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL Python]**，在&#x200B;**类型**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 分类]**。 填写完所有内容后，选择右上角的&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续执行&#x200B;**管理架构**。

>[!NOTE]
>
> 类型支持&#x200B;**[!UICONTROL 分类]**&#x200B;和&#x200B;**[!UICONTROL 回归]**。 如果您的模型不属于这些类型之一，请选择&#x200B;**[!UICONTROL 自定义]**。

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

接下来，在&#x200B;**管理架构**&#x200B;部分下选择零售销售输入和输出架构，这些架构是使用[创建零售销售架构和数据集](../models-recipes/create-retails-sales-dataset.md)教程中提供的引导脚本创建的。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在&#x200B;**功能管理**&#x200B;部分下，在架构查看器中选择租户标识以展开零售销售输入架构。 通过突出显示所需功能并在右侧&#x200B;**[!UICONTROL 字段属性]**&#x200B;窗口中选择&#x200B;**[!UICONTROL 输入功能]**&#x200B;或&#x200B;**[!UICONTROL 目标功能]**&#x200B;来选择输入和输出功能。 在本教程中，请将&#x200B;**[!UICONTROL weeklySales]**&#x200B;设置为&#x200B;**[!UICONTROL 目标功能]**，其他内容设置为&#x200B;**[!UICONTROL 输入功能]**。 选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以查看您新配置的方法。

查看方法，根据需要添加、修改或删除配置。 选择&#x200B;**[!UICONTROL 完成]**&#x200B;以创建方法。

![](../images/models-recipes/import-package-ui/recipe_review.png)

继续执行[后续步骤](#next-steps)，了解如何使用新创建的零售方法在[!DNL Data Science Workspace]中创建模型。

### 导入基于Docker的方法 — R {#r}

首先导航并选择位于[!DNL Experience Platform] UI左上角的&#x200B;**[!UICONTROL 工作流]**。 接下来，选择&#x200B;**导入方法**&#x200B;并选择&#x200B;**[!UICONTROL 启动]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

此时将显示&#x200B;**导入方法**&#x200B;工作流的&#x200B;**配置**&#x200B;页面。 输入方法的名称和说明，然后选择右上角的&#x200B;**[!UICONTROL 下一步]**。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在[将源文件打包到方法](./package-source-files-recipe.md)教程中，在使用R源文件构建零售方法结束时提供了Docker URL。

进入&#x200B;**选择源**&#x200B;页面后，将对应于使用&#x200B;**[!UICONTROL Source URL]**&#x200B;字段中的R源文件构建的打包方法的Docker URL粘贴到其中。 接下来，通过拖放方式导入提供的配置文件，或者使用文件系统&#x200B;**浏览器**。 提供的配置文件可在`experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`找到。 在&#x200B;**运行时**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL R]**，在&#x200B;**类型**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 分类]**。 填写完所有内容后，选择右上角的&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续执行&#x200B;**管理架构**。

>[!NOTE]
>
> *类型*&#x200B;支持&#x200B;**[!UICONTROL 分类]**&#x200B;和&#x200B;**[!UICONTROL 回归]**。 如果您的模型不属于这些类型之一，请选择&#x200B;**[!UICONTROL 自定义]**。

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

接下来，在&#x200B;**管理架构**&#x200B;部分下选择零售销售输入和输出架构，这些架构是使用[创建零售销售架构和数据集](../models-recipes/create-retails-sales-dataset.md)教程中提供的引导脚本创建的。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在&#x200B;*功能管理*&#x200B;部分下，在架构查看器中选择租户标识以展开零售销售输入架构。 通过突出显示所需功能并在右侧&#x200B;**[!UICONTROL 字段属性]**&#x200B;窗口中选择&#x200B;**[!UICONTROL 输入功能]**&#x200B;或&#x200B;**[!UICONTROL 目标功能]**&#x200B;来选择输入和输出功能。 在本教程中，请将&#x200B;**[!UICONTROL weeklySales]**&#x200B;设置为&#x200B;**[!UICONTROL 目标功能]**，其他内容设置为&#x200B;**[!UICONTROL 输入功能]**。 选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以查看您新配置的方法。

查看方法，根据需要添加、修改或删除配置。 选择&#x200B;**完成**&#x200B;以创建方法。

![](../images/models-recipes/import-package-ui/recipe_review.png)

继续执行[后续步骤](#next-steps)，了解如何使用新创建的零售方法在[!DNL Data Science Workspace]中创建模型。

### 导入基于Docker的方法 — PySpark {#pyspark}

首先导航并选择位于[!DNL Experience Platform] UI左上角的&#x200B;**[!UICONTROL 工作流]**。 接下来，选择&#x200B;**导入方法**&#x200B;并选择&#x200B;**[!UICONTROL 启动]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

此时将显示&#x200B;**导入方法**&#x200B;工作流的&#x200B;**配置**&#x200B;页面。 输入方法的名称和描述，然后选择右上角的&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在将[源文件打包到方法](./package-source-files-recipe.md)教程中，在使用PySpark源文件构建零售方法结束时提供了Docker URL。

进入&#x200B;**选择源**&#x200B;页面后，将对应于使用PySpark源文件构建的打包方法的Docker URL粘贴到&#x200B;**[!UICONTROL Source URL]**&#x200B;字段中。 接下来，通过拖放方式导入提供的配置文件，或者使用文件系统&#x200B;**浏览器**。 提供的配置文件可在`experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`找到。 在&#x200B;**运行时**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL PySpark]**。 选择PySpark运行时后，默认工件会自动填充到&#x200B;**[!UICONTROL Docker]**。 接下来，在&#x200B;**类型**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 分类]**。 填写完所有内容后，选择右上角的&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续执行&#x200B;**管理架构**。

>[!NOTE]
>
> *类型*&#x200B;支持&#x200B;**[!UICONTROL 分类]**&#x200B;和&#x200B;**[!UICONTROL 回归]**。 如果您的模型不属于这些类型之一，请选择&#x200B;**[!UICONTROL 自定义]**。

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

接下来，使用&#x200B;**管理架构**&#x200B;选择器选择零售销售输入和输出架构，架构是使用[创建零售销售架构和数据集](../models-recipes/create-retails-sales-dataset.md)教程中提供的引导脚本创建的。

![管理架构](../images/models-recipes/import-package-ui/manage-schemas.png)

在&#x200B;**功能管理**&#x200B;部分下，在架构查看器中选择租户标识以展开零售销售输入架构。 通过突出显示所需功能并在右侧&#x200B;**[!UICONTROL 字段属性]**&#x200B;窗口中选择&#x200B;**[!UICONTROL 输入功能]**&#x200B;或&#x200B;**[!UICONTROL 目标功能]**&#x200B;来选择输入和输出功能。 在本教程中，请将&#x200B;**[!UICONTROL weeklySales]**&#x200B;设置为&#x200B;**[!UICONTROL 目标功能]**，其他内容设置为&#x200B;**[!UICONTROL 输入功能]**。 选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以查看您新配置的方法。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

查看方法，根据需要添加、修改或删除配置。 选择&#x200B;**[!UICONTROL 完成]**&#x200B;以创建方法。

![](../images/models-recipes/import-package-ui/recipe_review.png)

继续执行[后续步骤](#next-steps)，了解如何使用新创建的零售方法在[!DNL Data Science Workspace]中创建模型。

### 导入基于Docker的方法 — Scala {#scala}

首先导航并选择位于[!DNL Experience Platform] UI左上角的&#x200B;**[!UICONTROL 工作流]**。 接下来，选择&#x200B;**导入方法**&#x200B;并选择&#x200B;**[!UICONTROL 启动]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

此时将显示&#x200B;**导入方法**&#x200B;工作流的&#x200B;**配置**&#x200B;页面。 输入方法的名称和描述，然后选择右上角的&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在将[源文件打包到方法](./package-source-files-recipe.md)教程中，在使用Scala ([!DNL Spark])源文件构建零售方法结束时提供了Docker URL。

进入&#x200B;**选择源**&#x200B;页面后，将对应于使用Scala源文件构建的打包方法的Docker URL粘贴到Source URL字段中。 接下来，通过拖放方式导入提供的配置文件，或者使用文件系统浏览器。 提供的配置文件可在`experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`找到。 在&#x200B;**运行时**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL Spark]**。 选择[!DNL Spark]运行时后，默认工件会自动填充到&#x200B;**[!UICONTROL Docker]**。 接下来，从&#x200B;**类型**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 回归]**。 填写完所有内容后，选择右上角的&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续执行&#x200B;**管理架构**。

>[!NOTE]
>
> 类型支持&#x200B;**[!UICONTROL 分类]**&#x200B;和&#x200B;**[!UICONTROL 回归]**。 如果您的模型不属于这些类型之一，请选择&#x200B;**[!UICONTROL 自定义]**。

![](../images/models-recipes/import-package-ui/scala-databricks.png)

接下来，使用&#x200B;**管理架构**&#x200B;选择器选择零售销售输入和输出架构，架构是使用[创建零售销售架构和数据集](../models-recipes/create-retails-sales-dataset.md)教程中提供的引导脚本创建的。

![管理架构](../images/models-recipes/import-package-ui/manage-schemas.png)

在&#x200B;**功能管理**&#x200B;部分下，在架构查看器中选择租户标识以展开零售销售输入架构。 通过突出显示所需功能并在右侧&#x200B;**[!UICONTROL 字段属性]**&#x200B;窗口中选择&#x200B;**[!UICONTROL 输入功能]**&#x200B;或&#x200B;**[!UICONTROL 目标功能]**&#x200B;来选择输入和输出功能。 在本教程中，请将“[!UICONTROL weeklySales]”设置为&#x200B;**[!UICONTROL 目标功能]**，其他内容设置为&#x200B;**[!UICONTROL 输入功能]**。 选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以查看您新配置的方法。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

查看方法，根据需要添加、修改或删除配置。 选择&#x200B;**[!UICONTROL 完成]**&#x200B;以创建方法。

![](../images/models-recipes/import-package-ui/recipe_review.png)

继续执行[后续步骤](#next-steps)，了解如何使用新创建的零售方法在[!DNL Data Science Workspace]中创建模型。

## 后续步骤 {#next-steps}

本教程提供了有关配置方法并将其导入到[!DNL Data Science Workspace]中的见解。 您现在可以使用新创建的方法创建、训练和评估模型。

- [在UI中训练和评估模型](./train-evaluate-model-ui.md)
- [使用API训练和评估模型](./train-evaluate-model-api.md)
