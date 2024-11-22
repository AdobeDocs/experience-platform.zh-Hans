---
title: 模型
description: 使用Data Distiller SQL扩展为生命周期管理建模。 了解如何使用SQL创建、培训和管理高级统计模型（包括模型版本控制、评估和预测等关键流程），以从数据中获得切实可行的见解。
role: Developer
exl-id: c609a55a-dbfd-4632-8405-55e99d1e0bd8
source-git-commit: 6a61900b19543f110c47e30f4d321d0016b65262
workflow-type: tm+mt
source-wordcount: '1229'
ht-degree: 1%

---

# 模型

>[!AVAILABILITY]
>
>此功能适用于购买了Data Distiller附加产品的客户。 有关更多信息，请与您的 Adobe 代表联系。

查询服务现在支持构建和部署模型的核心流程。 您可以使用SQL来使用您的数据训练模型，评估其准确性，然后应用训练模型来为新数据做出预测。 然后，您可以使用该模型从过去的数据进行归纳，以针对真实世界场景做出明智的决策。

模型生命周期中生成可操作洞察的三个步骤包括：

1. **培训**：模型从提供的数据集中学习模式。 （创建或替换模型）
2. **测试/评估**：使用单独的数据集评估模型的性能。(`model_evaluate`)
3. **预测**：已训练的模型用于预测新的、不可见的数据。

使用添加到现有SQL语法中的模型SQL扩展，根据您的业务需求管理模型生命周期。 本文档介绍了创建或替换模型、训练、评估、必要时重新训练以及预测洞察所必需的SQL。

## 模型创建和训练 {#create-and-train}

了解如何使用SQL命令定义、配置和培训机器学习模型。 下面的SQL演示了如何创建模型、应用特征工程转换以及启动培训过程，以确保正确配置模型以供将来使用。 以下SQL命令详细介绍了用于模型创建和管理的其他选项：

- **创建模型**：在指定的数据集上创建和训练新模型。 如果已经存在同名模型，此命令将返回错误。
- **如果不存在则创建模型**：仅当指定数据集中不存在同名模型时，才创建和训练新模型。
- **创建或替换模型**：创建并训练模型，使用指定数据集上的相同名称替换现有模型的最新版本。

```sql
CREATE MODEL | CREATE MODEL IF NOT EXISTS | CREATE OR REPLACE MODEL}
model_alias
[TRANSFORM (select_list)]
[OPTIONS(model_option_list)]
[AS {select_query}]
 
model_option_list:
    MODEL_TYPE = { 'LINEAR_REG' |
                   'LOGISTIC_REG' |
                   'KMEANS' }
  [, MAX_ITER = int64_value ]
 [, LABEL = string_array ]
[, REG_PARAM = float64_value ]
```

**示例**

```sql
CREATE MODEL churn_model
TRANSFORM (vector_assembler(array(current_customers, previous_customers)) features) 
OPTIONS(MODEL_TYPE='linear_reg', LABEL='churn_rate') 
AS
SELECT *
FROM churn_with_rate
ORDER BY period;
```

为了帮助您了解模型创建和训练过程中的关键组件和配置，以下说明解释了上述SQL示例中每个元素的用途和功能。

- `<model_alias>`：模型别名是分配给模型的可重用名称，以后可以引用。 需要为您的模型提供一个名称。
- `transform`： transform子句用于在训练模型之前对数据集应用功能工程转换（例如，单热编码和字符串索引）。 `TRANSFORM`语句的最后一个子句应为具有列列表的`vector_assembler`，这些列将构成用于模型训练的功能，或者是`vector_assembler`的派生类型（如`max_abs_scaler(feature)`、`standard_scaler(feature)`等）。 仅将使用最后一个子句中提到的列进行训练；将排除所有其他列，即使它们包含在`SELECT`查询中。
- `label = <label-COLUMN>`：训练数据集中的标签列，它指定模型要预测的目标或结果。
- `training-dataset`：此语法选择用于训练模型的数据。
- `type = 'LogisticRegression'`：此语法指定要使用的机器学习算法的类型。 选项包括`LinearRegression`、`LogisticRegression`和`KMeans`。
- `options`：此关键字提供了一组灵活的键值对来配置模型。
   - `Key model_type`： `model_type = '<supported algorithm>'`：指定要使用的机器学习算法的类型。 支持的选项包括`LinearRegression`、`LogisticRegression`和`KMeans`。
   - `Key label`： `label = <label_COLUMN>`：定义训练数据集中的标签列，它指示模型要预测的目标或结果。

使用SQL引用用于训练的数据集。

## 更新模型 {#update}

了解如何通过应用新的特征工程转换并配置算法类型和标签列等选项来更新现有的机器学习模型。 每次更新都会创建一个模型的新版本，该版本从上一个版本开始递增。 这样可以确保对更改进行跟踪，并且该模型可在未来的评估或预测步骤中重复使用。

以下示例演示使用新的转换和选项更新模型：

```sql
UPDATE MODEL <model_alias> TRANSFORM (vector_assembler(array(current_customers, previous_customers)) features)  OPTIONS(MODEL_TYPE='logistic_reg', LABEL='churn_rate')  AS SELECT * FROM churn_with_rate ORDER BY period;
```

**示例**

为了帮助您了解版本控制过程，请考虑以下命令：

```sql
UPDATE MODEL model_vdqbrja OPTIONS(MODEL_TYPE='logistic_reg', LABEL='Survived') AS SELECT * FROM titanic_e2e_dnd;
```

执行此命令后，模型具有新版本，如下表所示：

| 已更新模型ID | 已更新模型 | 新版本 |
|--------------------------------------------|---------------|-------------|
| a8f6a254-8f28-42ec-8b26-94edeb4698e8 | model_vdqbrja | 2 |

以下注释说明了模型更新工作流中的关键组件和选项。

- `UPDATE model <model_alias>`：更新命令处理版本控制并创建一个从上一个版本增加的新模型版本。
- `version`：仅在更新期间使用的可选关键字，用于明确指定应创建新版本。 如果省略，系统会自动递增版本。


## 评估模型 {#evaluate-model}

为了确保可靠的结果，请在使用`model_evaluate`关键字将模型部署到预测之前，评估模型的准确性和有效性。 以下SQL语句指定测试数据集、特定列和模型版本，以通过评估模型性能来测试模型。

```sql
SELECT *
FROM   model_evaluate(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   test -dataset)
```

`model_evaluate`函数将`model-alias`作为第一个参数，将灵活的`SELECT`语句作为第二个参数。 查询服务首先执行`SELECT`语句并将结果映射到`model_evaluate`Adobe定义函数(ADF)。 系统要求`SELECT`语句结果中的列名和数据类型与训练步骤中使用的列名和数据类型匹配。 这些列名和数据类型被视为测试数据和标签数据进行评估。

>[!IMPORTANT]
>
>评估(`model_evaluate`)和预测(`model_predict`)时，将使用训练时执行的转换。

## 预测 {#predict}

接下来，使用`model_predict`关键字将指定的模型和版本应用于数据集，并为选定的列生成预测。 下面的SQL演示了此过程，说明了如何使用模型的别名和版本预测结果。

```sql
SELECT *
FROM   model_predict(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   dataset)
```

`model_predict`接受模型别名作为第一个参数，使用灵活的`SELECT`语句作为第二个参数。 查询服务首先执行`SELECT`语句并将结果映射到`model_predict` ADF。 系统希望`SELECT`语句结果中的列名和数据类型与训练步骤中的列名和数据类型匹配。 然后，此数据用于评分和生成预测。

>[!IMPORTANT]
>
>评估(`model_evaluate`)和预测(`model_predict`)时，将使用训练时执行的转换。

## 评估和管理模型

使用`SHOW MODELS`命令列出您创建的所有可用模型。 使用它可以查看已训练可用于评估或预测的模型。 查询时，将从模型存储库中获取信息，该信息会在模型创建过程中更新。 返回的详细信息包括：模型ID、模型名称、版本、源数据集、算法详细信息、选项/参数、创建/更新时间以及创建模型的用户。

```sql
SHOW MODELS;
```

结果会显示在类似于下面的表格中：

| model-id | model-name | 版本 | source-dataset | 类型 | options | 转换 | 字段 | 已创建 | 已更新 | 创建者 |
|--------------------|---------------|---------|------------------|-----------------------|------------------------------|---------------------------------------------------------------------------|----------------------|---------------------|---------------------|------------|
| `model-84362-mdunj` | `SalesModel` | 1.0 | `sales_data_2023` | `LogisticRegression` | `{"label": "label-field"}` | `one_hot_encoder(name)`、`ohe_name`、`string_indexer(gender)`、`genderSI` | \[&quot;name&quot;， &quot;gender&quot;\] | 2024-08-14 10:30 AM | 2024-08-14 11:00 AM | `JohnSnow@adobe.com` |

## 清理和维护您的模型

使用`DROP MODELS`命令删除从模型注册表创建的模型。 您可以使用它来删除过时、未使用或不需要的模型。 这样可释放资源，并确保仅维护相关模型。 您还可以包含可选的模型名称，以提高特殊性。 这仅会删除具有所提供模型版本的模型。

```sql
DROP MODEL IF EXISTS modelName
DROP MODEL IF EXISTS modelName modelVersion ;
```

## 后续步骤

阅读本文档后，您现在了解了使用Data Distiller创建、训练和管理可信模型所需的基本SQL语法。 接下来，浏览[实施高级统计模型文档](./implement-models/implement-models.md)，了解各种可用的可信模型以及如何在SQL工作流中有效实施它们。 如果您尚未这样做，请确保查阅[功能工程](./feature-engineering.md)文档，以确保您的数据已做好模型训练的最佳准备。
