---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: 导入打包的菜谱(UI)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '1760'
ht-degree: 0%

---


# 导入打包的菜谱(UI)

本教程通过提供的零售销售示例提供有关如何配置和导入打包菜谱的分析。 在本教程的结尾，您将准备好在Adobe Experience Platform创建、培训和评估模型 [!DNL Data Science Workspace]。

## 先决条件

本教程需要以Docker图像URL形式打包的菜谱。 有关详细信息，请参 [阅有关如何将源文件打包到](./package-source-files-recipe.md) “菜谱”的教程。

## UI工作流程

将打包的菜谱导 [!DNL Data Science Workspace] 入需要特定菜谱配置，并编译为单个JavaScript对象表示法(JSON)文件，此菜谱配置编译称为配 **置文件**。 具有特定配置集的打包菜谱称为菜 **谱实例**。 一个菜谱可用于在中创建多个菜谱实例 [!DNL Data Science Workspace]。

导入包菜谱的工作流包含以下步骤：
- [配置菜谱](#configure)
- [导入基于Docker的菜谱- Python](#python)
- [导入基于Docker的菜谱- R](#r)
- [导入基于Docker的菜谱- PySpark](#pyspark)
- [导入基于Docker的菜谱- Scala](#scala)

### 配置菜谱 {#configure}

中的每个菜谱 [!DNL Data Science Workspace] 实例都附带一组配置，这些配置根据特定用例定制菜谱实例。 配置文件定义使用此菜谱实例创建的模型的默认培训和评分行为。

>[!NOTE]
>
>配置文件是特定于菜谱和大小写的。

以下是显示零售销售菜谱的默认培训和评分行为的示例配置文件。

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
| `learning_rate` | 数值 | 渐变乘法的标量。 |
| `n_estimators` | 数值 | 随机森林分类器的林中树数。 |
| `max_depth` | 数值 | 随机森林分类器中树的最大深度。 |
| `ACP_DSW_INPUT_FEATURES` | 字符串 | 列表以逗号分隔的输入模式属性。 |
| `ACP_DSW_TARGET_FEATURES` | 字符串 | 列表以逗号分隔的输出模式属性。 |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | 布尔值 | 确定输入和输出功能是否可修改 |
| `tenantId` | 字符串 | 此ID可确保您创建的资源命名正确且包含在IMS组织中。 [按照此处的步骤](../../xdm/api/getting-started.md#know-your-tenant_id) ，查找您的租户ID。 |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 字符串 | 用于培训模型的输入模式。 在UI中导入时将此留空，在使用API导入时替换为培训架构ID。 |
| `evaluation.labelColumn` | 字符串 | 用于评估可视化的列标签。 |
| `evaluation.metrics` | 字符串 | 用于评估模型的评估指标的逗号分隔列表。 |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 字符串 | 用于对模型进行评分的输出模式。 在UI中导入时将此留空，在使用API导入时替换为评分SchemaID。 |

在本教程中，您可以保留“零售销售”菜谱的默认配置文件(在“参考” [!DNL Data Science Workspace] 中)，方式为：

### 导入基于Docker的菜谱- [!DNL Python] {#python}

开始，方 **[!UICONTROL 法]** 是导航并选择UI左上角的 [!DNL Platform] 工作流。 然后，选择“ *导入菜谱* ”并单 **[!UICONTROL 击启动]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

此时 *将显示* “导入菜 *谱”工作流* 的“配置”页。 输入菜谱的名称和说明，然后 **[!UICONTROL 选择]** 右上角的下一步。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在将源 [文件打包到菜谱教程中](./package-source-files-recipe.md) ，在使用Python源文件构建零售销售菜谱结束时提供了一个Docker URL。

在“选择源”页 *面上* ，将与使用源URL字段中的源文件生成的打包菜谱 [!DNL Python] 对应的Docker **[!UICONTROL URL粘贴]** 。 然后，通过拖放导入提供的配置文件，或使用文件系统浏 **览器**。 可在上找到提供的配置文件 `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`。 在“ **[!UICONTROL 运行时]** ”下拉 *框中选* 择Python **[!UICONTROL ，在“类]** 型 *”下拉框中选* 择“分类”。 填写完所有内容后，单 **[!UICONTROL 击]** 右上角的“下一步”，继续 *管理模式*。

>[!NOTE]
>
> *类型* 支持 **[!UICONTROL 分类]** 和 **[!UICONTROL 回归]**。 如果模型不属于这些类型之一，请选择“自定 **[!UICONTROL 义”]**。

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

接下来，在“管理模式”部分下选择“零售销售”输 *入和输出模式*，这些是使用创建零售销售模式和数据集教程中 [提供的引导脚本创建的](../models-recipes/create-retails-sales-dataset.md) 。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在“功 *能管理* ”部分下，在模式查看器中单击租户标识以展开“零售销售”输入模式。 通过突出显示所需的功能并在右侧的“字段属性”窗口中选 **[!UICONTROL 择“输入功]****[!UICONTROL 能”或“]** 目标功能 **[!UICONTROL ”，选]** 择输入和输出功能。 在本教程中，请将 **[!UICONTROL weekly]** Sales设置为 **[!UICONTROL 目标功能]** ，将其他 **[!UICONTROL 设置为输]**&#x200B;入功能。 单击 **[!UICONTROL 下一]** 步以查看您新配置的菜谱。

根据需要审核菜谱、添加、修改或删除配置。 单击 **[!UICONTROL 完成]** ，以创建菜谱。

![](../images/models-recipes/import-package-ui/recipe_review.png)

继续执行 [后续步骤](#next-steps) ，了解如何使用新创建的零售 [!DNL Data Science Workspace] 销售菜谱创建模型。

### 导入基于Docker的菜谱- R {#r}

开始，方 **[!UICONTROL 法]** 是导航并选择UI左上角的 [!DNL Platform] 工作流。 然后，选择“ *导入菜谱* ”并单 **[!UICONTROL 击启动]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

此时 *将显示* “导入菜 *谱”工作流* 的“配置”页。 输入菜谱的名称和说明，然后 **[!UICONTROL 选择]** 右上角的下一步。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在将源 [文件打包到菜谱教程中](./package-source-files-recipe.md) ，在构建使用R源文件的零售销售菜谱结束时提供了Docker URL。

在“选择源”页 *面上* ，请在“源URL”字段中粘贴与使用R源文件构建的打包菜谱对应的 **[!UICONTROL Docker URL]** 。 然后，通过拖放导入提供的配置文件，或使用文件系统浏 **览器**。 可在上找到提供的配置文件 `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`。 在“ **[!UICONTROL 运行时]** ”下拉 *框中选* 择R，在“类 **[!UICONTROL 型”下]** 拉框中选 ** 择“分类”。 填写完所有内容后，单 **[!UICONTROL 击]** 右上角的“下一步”，继续 *管理模式*。

>[!NOTE]
>
> *类型* 支持 **[!UICONTROL 分类]** 和 **[!UICONTROL 回归]**。 如果模型不属于这些类型之一，请选择“自定 **[!UICONTROL 义”]**。

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

接下来，在“管理模式”部分下选择“零售销售”输 *入和输出模式*，这些是使用创建零售销售模式和数据集教程中 [提供的引导脚本创建的](../models-recipes/create-retails-sales-dataset.md) 。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在“功 *能管理* ”部分下，在模式查看器中单击租户标识以展开“零售销售”输入模式。 通过突出显示所需的功能并在右侧的“字段属性”窗口中选 **[!UICONTROL 择“输入功]****[!UICONTROL 能”或“]** 目标功能 **[!UICONTROL ”，选]** 择输入和输出功能。 在本教程中，请将 **[!UICONTROL weekly]** Sales设置为 **[!UICONTROL 目标功能]** ，将其他 **[!UICONTROL 设置为输]**&#x200B;入功能。 单击 **[!UICONTROL 下一]** 步以查看您的新配置菜谱。

根据需要审核菜谱、添加、修改或删除配置。 单击 **完成** ，以创建菜谱。

![](../images/models-recipes/import-package-ui/recipe_review.png)

继续执行 [后续步骤](#next-steps) ，了解如何使用新创建的零售 [!DNL Data Science Workspace] 销售菜谱创建模型。

### 导入基于Docker的菜谱- PySpark {#pyspark}

开始，方 **[!UICONTROL 法]** 是导航并选择UI左上角的 [!DNL Platform] 工作流。 然后，选择“ *导入菜谱* ”并单 **[!UICONTROL 击启动]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

此时 *将显示* “导入菜 *谱”工作流* 的“配置”页。 输入菜谱的名称和说明，然后 **[!UICONTROL 选择]** 右上角的下一步以继续。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在将源 [文件打包到菜谱教程中](./package-source-files-recipe.md) ，在使用PySpark源文件构建零售销售菜谱结束时提供了一个Docker URL。

在“选择源”页 *面上* ，请在“源URL”字段中粘贴与使用PySpark源文件构建的打包菜谱对应的 **[!UICONTROL Docker URL]** 。 然后，通过拖放导入提供的配置文件，或使用文件系统浏 **览器**。 可在上找到提供的配置文件 `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`。 在“ **[!UICONTROL 运行时]** ”下拉 *框中选* 择PySpark。 选择PySpark运行时后，默认工件会自动填充 **[!UICONTROL 到Docker]**。 接下来，在 **[!UICONTROL 类型]** 下拉 *框中选* 择分类。 填写完所有内容后，单 **[!UICONTROL 击]** 右上角的“下一步”，继续 *管理模式*。

>[!NOTE]
>
> *类型* 支持 **[!UICONTROL 分类]** 和 **[!UICONTROL 回归]**。 如果模型不属于这些类型之一，请选择“自定 **[!UICONTROL 义”]**。

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

接下来，在“管理模式”部分下选择“零售销售”输 *入和输出模式*，这些是使用创建零售销售模式和数据集教程中 [提供的引导脚本创建的](../models-recipes/create-retails-sales-dataset.md) 。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在“功 *能管理* ”部分下，在模式查看器中单击租户标识以展开“零售销售”输入模式。 通过突出显示所需的功能并在右侧的“字段属性”窗口中选 **[!UICONTROL 择“输入功]****[!UICONTROL 能”或“]** 目标功能 **[!UICONTROL ”，选]** 择输入和输出功能。 在本教程中，请将 **[!UICONTROL weekly]** Sales设置为 **[!UICONTROL 目标功能]** ，将其他 **[!UICONTROL 设置为输]**&#x200B;入功能。 单击 **[!UICONTROL 下一]** 步以查看您新配置的菜谱。

根据需要审核菜谱、添加、修改或删除配置。 单击 **[!UICONTROL 完成]** ，以创建菜谱。

![](../images/models-recipes/import-package-ui/recipe_review.png)

继续执行 [后续步骤](#next-steps) ，了解如何使用新创建的零售 [!DNL Data Science Workspace] 销售菜谱创建模型。

### 导入基于Docker的菜谱- Scala {#scala}

开始，方 **[!UICONTROL 法]** 是导航并选择UI左上角的 [!DNL Platform] 工作流。 然后，选择“ *导入菜谱* ”并单 **[!UICONTROL 击启动]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

此时 *将显示* “导入菜 *谱”工作流* 的“配置”页。 输入菜谱的名称和说明，然后 **[!UICONTROL 选择]** 右上角的下一步以继续。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在将源 [文件打包到菜谱教程中](./package-source-files-recipe.md) ，在使用Scala()源文件构建零售销售菜谱结束时提供了一个Docker[!DNL Spark]URL。

在“选择源”页 *面上* ，粘贴与使用“源URL”字段中的“缩放源文件”生成的打包菜谱对应的 *Docker URL* 。 然后，通过拖放导入提供的配置文件，或使用文件系统浏 **览器**。 可在上找到提供的配置文件 `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`。 在“ **[!UICONTROL 运行时]** ”下拉 *框中选* 择“Spark”。 选择运 [!DNL Spark] 行时后，默认对象会自动填充到 **[!UICONTROL Docker]**。 然后，从“ **[!UICONTROL 类型]** ”下 *拉框中* 选择“回归”。 填写完所有内容后，单 **[!UICONTROL 击]** 右上角的“下一步”，继续 *管理模式*。

>[!NOTE]
>
> *类型* 支持 **[!UICONTROL 分类]** 和 **[!UICONTROL 回归]**。 如果模型不属于这些类型之一，请选择“自定 **[!UICONTROL 义”]**。

![](../images/models-recipes/import-package-ui/scala-databricks.png)

接下来，在“管理模式”部分下选择“零售销售”输 *入和输出模式*，这些是使用创建零售销售模式和数据集教程中 [提供的引导脚本创建的](../models-recipes/create-retails-sales-dataset.md) 。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在“功 *能管理* ”部分下，在模式查看器中单击租户标识以展开“零售销售”输入模式。 通过突出显示所需的功能并在右侧的“字段属性”窗口中选 **[!UICONTROL 择“输入功]****[!UICONTROL 能”或“]** 目标功能 **[!UICONTROL ”，选]** 择输入和输出功能。 在本教程中，请将 **[!UICONTROL weekly]** Sales设置为 **[!UICONTROL 目标功能]** ，将其他 **[!UICONTROL 设置为输]**&#x200B;入功能。 单击 **[!UICONTROL 下一]** 步以查看您新配置的菜谱。

根据需要审核菜谱、添加、修改或删除配置。 单击 **[!UICONTROL 完成]** ，以创建菜谱。

![](../images/models-recipes/import-package-ui/recipe_review.png)

继续执行 [后续步骤](#next-steps) ，了解如何使用新创建的零售 [!DNL Data Science Workspace] 销售菜谱创建模型。

## 后续步骤 {#next-steps}

本教程提供了有关配置菜谱并将其导入的见解 [!DNL Data Science Workspace]。 您现在可以使用新创建的菜谱创建、培训和评估模型。

- [在UI中培训和评估模型](./train-evaluate-model-ui.md)
- [使用API培训和评估模型](./train-evaluate-model-api.md)