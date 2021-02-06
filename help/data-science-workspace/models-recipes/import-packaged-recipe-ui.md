---
keywords: Experience Platform；导入打包菜谱；数据科学工作区；热门主题；菜谱；ui；创建引擎
solution: Experience Platform
title: 在数据科学工作区UI中导入打包菜谱
topic: tutorial
type: Tutorial
description: 本教程通过提供的零售销售示例提供有关如何配置和导入打包菜谱的分析。 在本教程结束时，您将准备好在Adobe Experience Platform数据科学工作区中创建、培训和评估模型。
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '1827'
ht-degree: 0%

---


# 在数据科学工作区UI中导入打包菜谱

本教程通过提供的零售销售示例提供有关如何配置和导入打包菜谱的分析。 在本教程的结尾，您将准备好在Adobe Experience Platform[!DNL Data Science Workspace]创建、培训和评估模型。

## 先决条件

本教程需要以Docker图像URL形式打包的菜谱。 有关详细信息，请参阅教程，了解如何将源文件打包到Recipe](./package-source-files-recipe.md)中。[

## UI工作流程

将打包的菜谱导入[!DNL Data Science Workspace]需要特定菜谱配置并编译为单个JavaScript对象表示法(JSON)文件，此菜谱配置编译称为配置文件。 具有特定配置集的打包菜谱称为菜谱实例。 一个菜谱可用于在[!DNL Data Science Workspace]中创建多个菜谱实例。

导入包菜谱的工作流包含以下步骤：
- [配置菜谱](#configure)
- [导入基于Docker的菜谱- Python](#python)
- [导入基于Docker的菜谱- R](#r)
- [导入基于Docker的菜谱- PySpark](#pyspark)
- [导入基于Docker的菜谱- Scala](#scala)

### 配置菜谱{#configure}

[!DNL Data Science Workspace]中的每个菜谱实例都附带一组配置，这些配置根据特定用例定制菜谱实例。 配置文件定义使用此菜谱实例创建的模型的默认培训和评分行为。

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
| `tenantId` | 字符串 | 此ID可确保您创建的资源命名正确且包含在IMS组织中。 [请按照以下](../../xdm/api/getting-started.md#know-your-tenant_id) 步骤查找您的租户ID。 |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 字符串 | 用于培训模型的输入模式。 在UI中导入时将此留空，在使用API导入时替换为培训架构ID。 |
| `evaluation.labelColumn` | 字符串 | 用于评估可视化的列标签。 |
| `evaluation.metrics` | 字符串 | 用于评估模型的评估指标的逗号分隔列表。 |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 字符串 | 用于对模型进行评分的输出模式。 在UI中导入时将此留空，在使用API导入时替换为评分SchemaID。 |

在本教程中，您可以保留“零售销售”菜谱的默认配置文件，该配置文件位于[!DNL Data Science Workspace]参考中。

### 导入基于Docker的菜谱- [!DNL Python] {#python}

开始，方法是导航并选择位于[!DNL Platform] UI左上角的&#x200B;**[!UICONTROL 工作流]**。 接下来，选择&#x200B;**导入菜谱**&#x200B;并单击&#x200B;**[!UICONTROL 启动]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

出现&#x200B;**导入菜谱**&#x200B;工作流的&#x200B;**配置**&#x200B;页。 输入菜谱的名称和说明，然后选择右上角的&#x200B;**[!UICONTROL 下一个]**。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在[将源文件打包到Recipe](./package-source-files-recipe.md)教程中，在使用Python源文件构建零售销售菜谱结束时提供了Docker URL。

在&#x200B;**选择源**&#x200B;页面上后，请在&#x200B;**[!UICONTROL 源URL]**&#x200B;字段中粘贴与使用[!DNL Python]源文件构建的打包菜谱对应的Docker URL。 然后，通过拖放导入提供的配置文件，或使用文件系统&#x200B;**Browser**。 可在`experience-platform-dsw-reference/recipes/python/retail/retail.config.json`找到提供的配置文件。 在&#x200B;**Runtime**&#x200B;下拉框中选择&#x200B;**[!UICONTROL Python]**，在&#x200B;**Type**&#x200B;下拉框中选择&#x200B;**[!UICONTROL Classification]**。 填写完所有内容后，单击右上角的&#x200B;**[!UICONTROL 下一个]**&#x200B;以继续&#x200B;**管理模式**。

>[!NOTE]
>
> 类型支持&#x200B;**[!UICONTROL 分类]**&#x200B;和&#x200B;**[!UICONTROL 回归]**。 如果您的型号不属于这些类型之一，请选择&#x200B;**[!UICONTROL Custom]**。

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

接下来，在&#x200B;**管理模式**&#x200B;部分下选择零售销售输入和输出模式，这些是使用[中提供的引导脚本创建的，创建零售销售模式和数据集](../models-recipes/create-retails-sales-dataset.md)教程。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在&#x200B;**功能管理**&#x200B;部分下，在模式查看器中单击租户标识以展开零售销售输入模式。 通过突出显示所需功能并在右侧的&#x200B;**[!UICONTROL 字段属性]**&#x200B;窗口中选择&#x200B;**[!UICONTROL 输入功能]**&#x200B;或&#x200B;**[!UICONTROL 目标功能]**，选择输入和输出功能。 为本教程的目的，将&#x200B;**[!UICONTROL weeklySales]**&#x200B;设置为&#x200B;**[!UICONTROL 目标功能]**，将其他设置为&#x200B;**[!UICONTROL 输入功能]**。 单击&#x200B;**[!UICONTROL 下一步]**&#x200B;查看新配置的菜谱。

根据需要审核菜谱、添加、修改或删除配置。 单击&#x200B;**[!UICONTROL 完成]**&#x200B;以创建菜谱。

![](../images/models-recipes/import-package-ui/recipe_review.png)

继续执行[后续步骤](#next-steps)，了解如何使用新创建的零售销售菜谱在[!DNL Data Science Workspace]中创建模型。

### 导入基于Docker的菜谱- R {#r}

开始，方法是导航并选择位于[!DNL Platform] UI左上角的&#x200B;**[!UICONTROL 工作流]**。 接下来，选择&#x200B;**导入菜谱**&#x200B;并单击&#x200B;**[!UICONTROL 启动]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

出现&#x200B;**导入菜谱**&#x200B;工作流的&#x200B;**配置**&#x200B;页。 输入菜谱的名称和说明，然后选择右上角的&#x200B;**[!UICONTROL 下一个]**。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在[将源文件打包到Recipe](./package-source-files-recipe.md)教程中，在构建使用R源文件的零售销售菜谱结束时提供了Docker URL。

在&#x200B;**选择源**&#x200B;页面上，将与使用R源文件构建的打包菜谱对应的Docker URL粘贴到&#x200B;**[!UICONTROL 源URL]**&#x200B;字段中。 然后，通过拖放导入提供的配置文件，或使用文件系统&#x200B;**Browser**。 可在`experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`找到提供的配置文件。 在&#x200B;**Runtime**&#x200B;下拉框中选择&#x200B;**[!UICONTROL R]**，在&#x200B;**Type**&#x200B;下拉框中选择&#x200B;**[!UICONTROL Classification]**。 填写完所有内容后，单击右上角的&#x200B;**[!UICONTROL 下一个]**&#x200B;以继续&#x200B;**管理模式**。

>[!NOTE]
>
> *排* 版支持 **** 分类和 **[!UICONTROL 回归]**。如果您的型号不属于这些类型之一，请选择&#x200B;**[!UICONTROL Custom]**。

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

接下来，在&#x200B;**管理模式**&#x200B;部分下选择零售销售输入和输出模式，这些是使用[中提供的引导脚本创建的，创建零售销售模式和数据集](../models-recipes/create-retails-sales-dataset.md)教程。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在&#x200B;*功能管理*&#x200B;部分下，在模式查看器中单击租户标识以展开零售销售输入模式。 通过突出显示所需功能并在右侧的&#x200B;**[!UICONTROL 字段属性]**&#x200B;窗口中选择&#x200B;**[!UICONTROL 输入功能]**&#x200B;或&#x200B;**[!UICONTROL 目标功能]**，选择输入和输出功能。 为本教程的目的，将&#x200B;**[!UICONTROL weeklySales]**&#x200B;设置为&#x200B;**[!UICONTROL 目标功能]**，将其他设置为&#x200B;**[!UICONTROL 输入功能]**。 单击&#x200B;**[!UICONTROL 下一步]**&#x200B;查看您的新配置菜谱。

根据需要审核菜谱、添加、修改或删除配置。 单击&#x200B;**完成**&#x200B;以创建菜谱。

![](../images/models-recipes/import-package-ui/recipe_review.png)

继续执行[后续步骤](#next-steps)，了解如何使用新创建的零售销售菜谱在[!DNL Data Science Workspace]中创建模型。

### 导入基于Docker的菜谱- PySpark {#pyspark}

开始，方法是导航并选择位于[!DNL Platform] UI左上角的&#x200B;**[!UICONTROL 工作流]**。 接下来，选择&#x200B;**导入菜谱**&#x200B;并单击&#x200B;**[!UICONTROL 启动]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

出现&#x200B;**导入菜谱**&#x200B;工作流的&#x200B;**配置**&#x200B;页。 输入菜谱的名称和说明，然后选择右上角的&#x200B;**[!UICONTROL 下一个]**&#x200B;以继续。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在[将源文件打包到Recipe](./package-source-files-recipe.md)教程中，在使用PySpark源文件构建零售销售菜谱结束时提供了Docker URL。

在&#x200B;**选择源**&#x200B;页面上，将与使用PySpark源文件构建的打包菜谱对应的Docker URL粘贴到&#x200B;**[!UICONTROL 源URL]**&#x200B;字段中。 然后，通过拖放导入提供的配置文件，或使用文件系统&#x200B;**Browser**。 可在`experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`找到提供的配置文件。 在&#x200B;**运行时**&#x200B;下拉框中选择&#x200B;**[!UICONTROL PySpark]**。 选择PySpark运行时后，默认的伪影会自动填充到&#x200B;**[!UICONTROL Docker]**。 接下来，在&#x200B;**类型**&#x200B;下拉框中选择&#x200B;**[!UICONTROL 分类]**。 填写完所有内容后，单击右上角的&#x200B;**[!UICONTROL 下一个]**&#x200B;以继续&#x200B;**管理模式**。

>[!NOTE]
>
> *排* 版支持 **** 分类和 **[!UICONTROL 回归]**。如果您的型号不属于这些类型之一，请选择&#x200B;**[!UICONTROL Custom]**。

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

接下来，在&#x200B;**管理模式**&#x200B;部分下选择零售销售输入和输出模式，这些是使用[中提供的引导脚本创建的，创建零售销售模式和数据集](../models-recipes/create-retails-sales-dataset.md)教程。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在&#x200B;**功能管理**&#x200B;部分下，在模式查看器中单击租户标识以展开零售销售输入模式。 通过突出显示所需功能并在右侧的&#x200B;**[!UICONTROL 字段属性]**&#x200B;窗口中选择&#x200B;**[!UICONTROL 输入功能]**&#x200B;或&#x200B;**[!UICONTROL 目标功能]**，选择输入和输出功能。 为本教程的目的，将&#x200B;**[!UICONTROL weeklySales]**&#x200B;设置为&#x200B;**[!UICONTROL 目标功能]**，将其他设置为&#x200B;**[!UICONTROL 输入功能]**。 单击&#x200B;**[!UICONTROL 下一步]**&#x200B;查看新配置的菜谱。

根据需要审核菜谱、添加、修改或删除配置。 单击&#x200B;**[!UICONTROL 完成]**&#x200B;以创建菜谱。

![](../images/models-recipes/import-package-ui/recipe_review.png)

继续执行[后续步骤](#next-steps)，了解如何使用新创建的零售销售菜谱在[!DNL Data Science Workspace]中创建模型。

### 导入基于Docker的菜谱- Scala {#scala}

开始，方法是导航并选择位于[!DNL Platform] UI左上角的&#x200B;**[!UICONTROL 工作流]**。 接下来，选择&#x200B;**导入菜谱**&#x200B;并单击&#x200B;**[!UICONTROL 启动]**。

![](../images/models-recipes/import-package-ui/launch-import.png)

出现&#x200B;**导入菜谱**&#x200B;工作流的&#x200B;**配置**&#x200B;页。 输入菜谱的名称和说明，然后选择右上角的&#x200B;**[!UICONTROL 下一个]**&#x200B;以继续。

![配置工作流](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> 在[将源文件打包到Recipe](./package-source-files-recipe.md)教程中，在使用Scala([!DNL Spark])源文件构建零售销售菜谱结束时提供了Docker URL。

在&#x200B;**选择源**&#x200B;页面上后，请在源URL字段中粘贴与使用Scala源文件构建的打包菜谱对应的Docker URL。 然后，通过拖放导入提供的配置文件，或使用文件系统浏览器。 可在`experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`找到提供的配置文件。 在&#x200B;**运行时**&#x200B;下拉框中选择&#x200B;**[!UICONTROL Spark]**。 选择[!DNL Spark]运行时后，默认的伪影会自动填充到&#x200B;**[!UICONTROL Docker]**。 接下来，从&#x200B;**类型**&#x200B;下拉菜单中选择&#x200B;**[!UICONTROL 回归]**。 填写完所有内容后，单击右上角的&#x200B;**[!UICONTROL 下一个]**&#x200B;以继续&#x200B;**管理模式**。

>[!NOTE]
>
> 类型支持&#x200B;**[!UICONTROL 分类]**&#x200B;和&#x200B;**[!UICONTROL 回归]**。 如果您的型号不属于这些类型之一，请选择&#x200B;**[!UICONTROL Custom]**。

![](../images/models-recipes/import-package-ui/scala-databricks.png)

接下来，在&#x200B;**管理模式**&#x200B;部分下选择零售销售输入和输出模式，这些是使用[中提供的引导脚本创建的，创建零售销售模式和数据集](../models-recipes/create-retails-sales-dataset.md)教程。

![](../images/models-recipes/import-package-ui/recipe_schema.png)

在&#x200B;**功能管理**&#x200B;部分下，在模式查看器中单击租户标识以展开零售销售输入模式。 通过突出显示所需功能并在右侧的&#x200B;**[!UICONTROL 字段属性]**&#x200B;窗口中选择&#x200B;**[!UICONTROL 输入功能]**&#x200B;或&#x200B;**[!UICONTROL 目标功能]**，选择输入和输出功能。 在本教程中，将“[!UICONTROL weeklySales]”设置为&#x200B;**[!UICONTROL 目标功能]**，将其他设置为&#x200B;**[!UICONTROL 输入功能]**。 单击&#x200B;**[!UICONTROL 下一步]**&#x200B;查看新配置的菜谱。

根据需要审核菜谱、添加、修改或删除配置。 单击&#x200B;**[!UICONTROL 完成]**&#x200B;以创建菜谱。

![](../images/models-recipes/import-package-ui/recipe_review.png)

继续执行[后续步骤](#next-steps)，了解如何使用新创建的零售销售菜谱在[!DNL Data Science Workspace]中创建模型。

## 后续步骤 {#next-steps}

本教程提供了有关配置菜谱并将其导入[!DNL Data Science Workspace]的见解。 您现在可以使用新创建的菜谱创建、培训和评估模型。

- [在UI中培训和评估模型](./train-evaluate-model-ui.md)
- [使用API培训和评估模型](./train-evaluate-model-api.md)