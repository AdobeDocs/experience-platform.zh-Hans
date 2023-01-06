---
keywords: Experience Platform；教程；功能管道；数据科学工作区；热门主题
title: 使用模型创作SDK创建特征管道
type: Tutorial
description: Adobe Experience Platform允许您构建和创建自定义功能管道，以通过Sensei机器学习框架运行时大规模执行功能工程。 本文档介绍了在功能管道中找到的各种类，并提供了一个分步教程，用于使用PySpark中的模型创作SDK创建自定义功能管道。
exl-id: c2c821d5-7bfb-4667-ace9-9566e6754f98
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1441'
ht-degree: 0%

---

# 使用模型创作SDK创建特征管道

>[!IMPORTANT]
>
> 功能管道当前仅通过API提供。

Adobe Experience Platform允许您构建和创建自定义功能管道，以通过Sensei机器学习框架运行时（以下简称“运行时”）大规模执行功能工程。

本文档介绍了在功能管道中找到的各种类，并提供了使用创建自定义功能管道的分步教程 [模型创作SDK](./sdk.md) 在PySpark里。

运行特征管线时，会执行以下工作流：

1. 方法会将数据集加载到管道。
2. 功能转换在数据集上完成并写回Adobe Experience Platform。
3. 所转换的数据被加载用于训练。
4. 特征管道将梯度提升回归器定义为所选模型。
5. 管道用于拟合训练数据并创建训练模型。
6. 模型会与评分数据集一起转换。
7. 然后，选择输出中的相关列并将其保存回 [!DNL Experience Platform] 关联数据。

## 快速入门

要在任何组织中运行方法，需要满足以下条件：
- 输入数据集。
- 数据集的架构。
- 已转换的架构和基于该架构的空数据集。
- 输出架构和基于该架构的空数据集。

上述所有数据集都需要上传到 [!DNL Platform] UI。 要设置此设置，请使用提供的Adobe [引导脚本](https://github.com/adobe/experience-platform-dsw-reference/tree/master/bootstrap).

## 特征管道类

下表描述了构建特征管线时必须扩展的主要抽象类：

| 抽象类 | 描述 |
| -------------- | ----------- |
| DataLoader | DataLoader类提供用于检索输入数据的实现。 |
| DatasetTransformer | DatasetTransformer类提供用于转换输入数据集的实施。 您可以选择不提供DatasetTransformer类，而是在FeaturePipelineFactory类中实施功能工程逻辑。 |
| 功能管道工厂 | FeaturePipelineFactory类构建由一系列Spark Transporters组成的Spark管线，以执行特征工程。 您可以选择不提供FeaturePipelineFactory类，而是在DatasetTransformer类中实施功能工程逻辑。 |
| 数据保护程序 | DataSaver类提供存储功能数据集的逻辑。 |

启动功能管道作业后，运行时首先执行DataLoader以将输入数据作为DataFrame加载，然后通过执行DatasetTransformer、FeaturePipelineFactory或两者之一来修改DataFrame。 最后，生成的功能数据集通过DataSaver进行存储。

以下流程图显示运行时的执行顺序：

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## 实施功能管道类 {#implement-your-feature-pipeline-classes}

以下各节提供了有关为功能管道实施所需类的详细信息和示例。

### 在配置JSON文件中定义变量 {#define-variables-in-the-configuration-json-file}

配置JSON文件由键值对组成，可用于指定以后在运行时定义的任何变量。 这些键值对可以定义属性，如输入数据集位置、输出数据集ID、租户ID、列标题等。

以下示例演示了在配置文件中找到的键值对：

**配置JSON示例**

```json
[
    {
        "name": "fp",
        "parameters": [
            {
                "key": "dataset_id",
                "value": "000"
            },
            {
                "key": "featureDatasetId",
                "value": "111"
            },
            {
                "key": "tenantId",
                "value": "_tenantid"
            }
        ]
    }
]
```

您可以通过定义 `config_properties` 作为参数。 例如：

**PySpark**

```python
dataset_id = str(config_properties.get(dataset_id))
```

请参阅 [pipeline.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/feature_pipeline_recipes/pyspark/pipeline.json) 数据科学工作区提供的文件，以了解更详细的配置示例。

### 使用DataLoader准备输入数据 {#prepare-the-input-data-with-dataloader}

DataLoader负责检索和过滤输入数据。 DataLoader的实现必须扩展抽象类 `DataLoader` 并覆盖抽象方法 `load`.

以下示例检索 [!DNL Platform] 数据集（按ID），并将其作为DataFrame返回，其中数据集ID(`dataset_id`)是配置文件中定义的属性。

**PySpark示例**

```python
# PySpark

from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct
import logging

class MyDataLoader(DataLoader):
    def load_dataset(config_properties, spark, tenant_id, dataset_id):
    PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"
    PLATFORM_SDK_PQS_INTERACTIVE = "interactive"

    service_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
    user_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
    org_id = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
    api_key = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

    dataset_id = str(config_properties.get(dataset_id))

    for arg in ['service_token', 'user_token', 'org_id', 'dataset_id', 'api_key']:
        if eval(arg) == 'None':
            raise ValueError("%s is empty" % arg)

    query_options = get_query_options(spark.sparkContext)

    pd = spark.read.format(PLATFORM_SDK_PQS_PACKAGE) \
        .option(query_options.userToken(), user_token) \
        .option(query_options.serviceToken(), service_token) \
        .option(query_options.imsOrg(), org_id) \
        .option(query_options.apiKey(), api_key) \
        .option(query_options.mode(), PLATFORM_SDK_PQS_INTERACTIVE) \
        .option(query_options.datasetId(), dataset_id) \
        .load()
    pd.show()

    # Get the distinct values of the dataframe
    pd = pd.distinct()

    # Flatten the data
    if tenant_id in pd.columns:
        pd = pd.select(col(tenant_id + ".*"))

    return pd
```

### 使用DatasetTransformer转换数据集 {#transform-a-dataset-with-datasettransformer}

DatasetTransformer提供了转换输入DataFrame的逻辑，并返回新的派生DataFrame。 可以实施此类以与FeaturePipelineFactory协同工作、作为唯一的特征工程组件工作，或者选择不实施此类。

以下示例扩展了DatasetTransformer类：

**PySpark示例**

```python
# PySpark

from sdk.dataset_transformer import DatasetTransformer
from pyspark.ml.feature import StringIndexer
from pyspark.sql.types import IntegerType
from pyspark.sql.functions import unix_timestamp, from_unixtime, to_date, lit, lag, udf, date_format, lower, col, split, explode
from pyspark.sql import Window
from .helper import setupLogger

class MyDatasetTransformer(DatasetTransformer):
    logger = setupLogger(__name__)

    def transform(self, config_properties, dataset):
        tenant_id = str(config_properties.get("tenantId"))

        # Flatten the data
        if tenant_id in dataset.columns:
            self.logger.info("Flatten the data before transformation")
            dataset = dataset.select(col(tenant_id + ".*"))
            dataset.show()

        # Convert isHoliday boolean value to Int
        # Rename the column to holiday and drop isHoliday
        pd = dataset.withColumn("holiday", col("isHoliday").cast(IntegerType())).drop("isHoliday")
        pd.show()

        # Get the week and year from date
        pd = pd.withColumn("week", date_format(to_date("date", "MM/dd/yy"), "w").cast(IntegerType()))
        pd = pd.withColumn("year", date_format(to_date("date", "MM/dd/yy"), "Y").cast(IntegerType()))

        # Convert the date to TimestampType
        pd = pd.withColumn("date", to_date(unix_timestamp(pd["date"], "MM/dd/yy").cast("timestamp")))

        # Convert categorical data
        indexer = StringIndexer(inputCol="storeType", outputCol="storeTypeIndex")
        pd = indexer.fit(pd).transform(pd)

        # Get the WeeklySalesAhead and WeeklySalesLag column values
        window = Window.orderBy("date").partitionBy("store")
        pd = pd.withColumn("weeklySalesLag", lag("weeklySales", 1).over(window)).na.drop(subset=["weeklySalesLag"])
        pd = pd.withColumn("weeklySalesAhead", lag("weeklySales", -1).over(window)).na.drop(subset=["weeklySalesAhead"])
        pd = pd.withColumn("weeklySalesScaled", lag("weeklySalesAhead", -1).over(window)).na.drop(subset=["weeklySalesScaled"])
        pd = pd.withColumn("weeklySalesDiff", (pd['weeklySales'] - pd['weeklySalesLag'])/pd['weeklySalesLag'])

        pd = pd.na.drop()
        self.logger.debug("Transformed dataset count is %s " % pd.count())

        # return transformed dataframe
        return pd
```

### 使用FeaturePipelineFactory进行数据功能工程 {#engineer-data-features-with-featurepipelinefactory}

FeaturePipelineFactory允许您通过Spark管道定义一系列Spark Transporters并将其链接在一起，从而实施您的功能工程逻辑。 可以实施此类，以与DatasetTransformer协作、作为唯一的特征工程组件工作，或选择不实施此类。

以下示例扩展了FeaturePipelineFactory类：

**PySpark示例**

```python
# PySpark

from pyspark.ml import Pipeline
from pyspark.ml.regression import GBTRegressor
from pyspark.ml.feature import VectorAssembler

import numpy as np

from sdk.pipeline_factory import PipelineFactory

class MyFeaturePipelineFactory(FeaturePipelineFactory):

    def apply(self, config_properties):
        if config_properties is None:
            raise ValueError("config_properties parameter is null")

        tenant_id = str(config_properties.get("tenantId"))
        input_features = str(config_properties.get("ACP_DSW_INPUT_FEATURES"))

        if input_features is None:
            raise ValueError("input_features parameter is null")
        if input_features.startswith(tenant_id):
            input_features = input_features.replace(tenant_id + ".", "")

        learning_rate = float(config_properties.get("learning_rate"))
        n_estimators = int(config_properties.get("n_estimators"))
        max_depth = int(config_properties.get("max_depth"))

        feature_list = list(input_features.split(","))
        feature_list.remove("date")
        feature_list.remove("storeType")

        cols = np.array(feature_list)

        # Gradient-boosted tree estimator
        gbt = GBTRegressor(featuresCol='features', labelCol='weeklySalesAhead', predictionCol='prediction',
                       maxDepth=max_depth, maxBins=n_estimators, stepSize=learning_rate)

        # Assemble the fields to a vector
        assembler = VectorAssembler(inputCols=cols, outputCol="features")

        # Construct the pipeline
        pipeline = Pipeline(stages=[assembler, gbt])

        return pipeline

    def train(self, config_properties, dataframe):
        pass

    def score(self, config_properties, dataframe, model):
        pass

    def getParamMap(self, config_properties, sparkSession):
        return None
```

### 使用DataSaver存储您的功能数据集 {#store-your-feature-dataset-with-datasaver}

DataSaver负责将生成的功能数据集存储到存储位置。 您对DataSaver的实施必须扩展抽象类 `DataSaver` 并覆盖抽象方法 `save`.

以下示例将存储数据的DataSaver类扩展到 [!DNL Platform] 按ID划分的数据集，其中数据集ID(`featureDatasetId`)和租户ID(`tenantId`)是配置中定义的属性。

**PySpark示例**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct


class MyDataSaver(DataSaver):
    def save(self, configProperties, data_feature):

        # Spark context
        sparkContext = data_features._sc

        # preliminary checks
        if configProperties is None:
            raise ValueError("configProperties parameter is null")
        if data_features is None:
            raise ValueError("data_features parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")

        # prepare variables
        timestamp = "2019-01-01 00:00:00"
        output_dataset_id = str(
            configProperties.get("featureDatasetId"))
        tenant_id = str(
            configProperties.get("tenantId"))
        service_token = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
        for arg in ['output_dataset_id', 'tenant_id', 'service_token', 'user_token', 'org_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # create and prepare DataFrame with valid columns
        output_df = data_features.withColumn("date", col("date").cast(StringType()))
        output_df = output_df.withColumn(tenant_id, struct(col("date"), col("store"), col("features")))
        output_df = output_df.withColumn("timestamp", lit(timestamp).cast(TimestampType()))
        output_df = output_df.withColumn("_id", lit("empty"))
        output_df = output_df.withColumn("eventType", lit("empty"))

        # store data into dataset
        output_df.select(tenant_id, "_id", "eventType", "timestamp") \
            .write.format("com.adobe.platform.dataset") \
            .option('orgId', org_id) \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('serviceApiKey', api_key) \
            .save(output_dataset_id)
```


### 在应用程序文件中指定实现的类名 {#specify-your-implemented-class-names-in-the-application-file}

现在，定义并实现了您的功能管道类，您必须在应用程序YAML文件中指定类的名称。

以下示例指定了实现的类名称：

**PySpark示例**

```yaml
#Name of the class which contains implementation to get the input data.
feature.dataLoader: InputDataLoaderForFeaturePipeline

#Name of the class which contains implementation to get the transformed data.
feature.dataset.transformer: MyDatasetTransformer

#Name of the class which contains implementation to save the transformed data.
feature.dataSaver: DatasetSaverForTransformedData

#Name of the class which contains implementation to get the training data
training.dataLoader: TrainingDataLoader

#Name of the class which contains pipeline. It should implement PipelineFactory.scala
pipeline.class: TrainPipeline

#Name of the class which contains implementation for evaluation metrics.
evaluator: Evaluator
evaluateModel: True

#Name of the class which contains implementation to get the scoring data.
scoring.dataLoader: ScoringDataLoader

#Name of the class which contains implementation to save the scoring data.
scoring.dataSaver: MyDatasetSaver
```

## 使用API创建功能管道引擎 {#create-feature-pipeline-engine-api}

现在，您已创作功能管道，接下来需要创建一个Docker图像，以调用 [!DNL Sensei Machine Learning] API。 要调用功能管道端点，您需要Docker图像URL。

>[!TIP]
>
>如果您没有Docker URL，请访问 [将源文件打包到方法中](../models-recipes/package-source-files-recipe.md) 有关创建Docker主机URL的分步说明教程。

或者，您还可以选择使用以下Postman集合来帮助完成功能管道API工作流：

https://www.postman.com/collections/c5fc0d1d5805a5ddd41a

### 创建特征管道引擎 {#create-engine-api}

获得Docker图像位置后，您可以 [创建特征管道引擎](../api/engines.md#feature-pipeline-docker) 使用 [!DNL Sensei Machine Learning] API(通过执行POST) `/engines`. 成功创建功能管道引擎为您提供引擎唯一标识符(`id`)。 在继续操作之前，请确保保存此值。

### 创建MLInstance {#create-mlinstance}

使用新创建的 `engineID`，您需要 [创建MLIstance](../api/mlinstances.md#create-an-mlinstance) 通过向 `/mlInstance` 端点。 成功的响应会返回一个有效负载，其中包含新创建的MLInstance的详细信息，包括其唯一标识符(`id`)用于下一个API调用。

### 创建实验 {#create-experiment}

接下来，您需要 [创建实验](../api/experiments.md#create-an-experiment). 要创建实验，您需要具有MLIstance唯一标识符(`id`)，并向发出POST请求 `/experiment` 端点。 成功的响应会返回一个有效负载，其中包含新创建实验的详细信息，包括其唯一标识符(`id`)用于下一个API调用。

### 指定“实验”运行功能管道任务 {#specify-feature-pipeline-task}

创建实验后，必须将实验的模式更改为 `featurePipeline`. 要更改模式，请额外POST [`experiments/{EXPERIMENT_ID}/runs`](../api/experiments.md#experiment-training-scoring) 与 `EXPERIMENT_ID` 在尸体上 `{ "mode":"featurePipeline"}` 指定特征管线实验运行。

完成后，向发送GET请求 `/experiments/{EXPERIMENT_ID}` to [检索实验状态](../api/experiments.md#retrieve-specific) 并等待实验状态更新完成。

### 指定“实验”运行培训任务 {#training}

接下来，您需要 [指定培训运行任务](../api/experiments.md#experiment-training-scoring). POST `experiments/{EXPERIMENT_ID}/runs` 在主体中，将模式设置为 `train` 并发送包含培训参数的任务数组。 成功的响应会返回包含所请求实验详细信息的有效负载。

完成后，向发送GET请求 `/experiments/{EXPERIMENT_ID}` to [检索实验状态](../api/experiments.md#retrieve-specific) 并等待实验状态更新完成。

### 指定“实验”运行评分任务 {#scoring}

>[!NOTE]
>
> 要完成此步骤，您需要至少将一个成功的培训运行与您的实验相关联。

成功运行培训后，您需要 [指定评分运行任务](../api/experiments.md#experiment-training-scoring). POST `experiments/{EXPERIMENT_ID}/runs` 在身体里 `mode` 属性。 这将开始您的评分实验运行。

完成后，向发送GET请求 `/experiments/{EXPERIMENT_ID}` to [检索实验状态](../api/experiments.md#retrieve-specific) 并等待实验状态更新完成。

评分完成后，您的功能管道应可以正常运行。

## 后续步骤 {#next-steps}

[//]: # (Next steps section should refer to tutorials on how to score data using the feature pipeline Engine. Update this document once those tutorials are available)

通过阅读本文档，您已使用“模型创作SDK”创作了一个功能管道，创建了Docker图像，并使用Docker图像URL通过 [!DNL Sensei Machine Learning] API。 现在，您可以继续使用转换数据集和提取大规模数据功能 [[!DNL Sensei Machine Learning API]](../api/getting-started.md).
