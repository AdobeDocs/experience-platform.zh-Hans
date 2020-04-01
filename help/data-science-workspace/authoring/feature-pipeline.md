---
keywords: Experience Platform;Tutorial;Feature Pipeline;Data Science Workspace;popular topics
solution: Experience Platform
title: 创建特征管线
topic: Tutorial
translation-type: tm+mt
source-git-commit: b9b0578a43182650b3cfbd71f46bcb817b3b0cda

---


# 创建特征管线

Adobe Experience Platform允许您构建和创建自定义功能管道，通过Sensei机器学习框架运行时（以下简称“运行时”）大规模地执行功能工程。

本文档介绍在功能管道中找到的各种类，并提供了一个分步教程，用于使用PySpark和Spark中的“模型创作SDK [](./sdk.md) ”创建自定义功能管道。

本教程涵盖以下步骤：
- [实现功能管道类](#implement-your-feature-pipeline-classes)
   - [在配置文件中定义变量](#define-variables-in-the-configuration-json-file)
   - [使用DataLoader准备输入数据](#prepare-the-input-data-with-dataloader)
   - [使用DatasetTransformer转换数据集](#transform-a-dataset-with-datasettransformer)
   - [使用FeaturePipelineFactory设计数据功能](#engineer-data-features-with-featurepipelinefactory)
   - [使用DataSaver存储功能数据集](#store-your-feature-dataset-with-datasaver)
   - [在应用程序文件中指定实现的类名](#specify-your-implemented-class-names-in-the-application-file)
- [构建二进制伪像](#build-the-binary-artifact)
- [使用API创建功能管道引擎](#create-a-feature-pipeline-engine-using-the-api)

## 特征管线类

下表描述了构建特征管线时必须扩展的主要抽象类：

| 摘要类 | 描述 |
| -------------- | ----------- |
| DataLoader | DataLoader类提供用于检索输入数据的实现。 |
| DatasetTransformer | DatasetTransformer类提供用于转换输入数据集的实现。 您可以选择不提供DatasetTransformer类，而是在FeaturePipelineFactory类中实现您的功能工程逻辑。 |
| FeaturePipelineFactory | FeaturePipelineFactory类构建一个Spark Pipeline，它包含一系列Spark Transporters，用于执行功能工程。 您可以选择不提供FeaturePipelineFactory类，而是在DatasetTransformer类中实施您的功能工程逻辑。 |
| DataSaver | DataSaver类提供用于存储功能数据集的逻辑。 |

启动功能管道作业时，运行时将首先执行DataLoader以作为DataFrame加载输入数据，然后通过执行DatasetTransformer或FeaturePipelineFactory或两者来修改DataFrame。 最后，生成的特征数据集通过DataSaver进行存储。

以下流程图显示了Runtime的执行顺序：

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## 实现功能管道类

以下各节提供了有关为功能管道实现所需类的详细信息和示例。

### 在配置JSON文件中定义变量

配置JSON文件由键值对组成，供您指定以后在运行时定义的任何变量。 这些键值对可以定义诸如输入数据集位置、输出数据集ID、租户ID、列标题等属性。

以下示例演示了在配置文件中找到的键值对。 展开示例以查看详细信息：


**配置JSON示例**

```json
[
    {
        "name": "fp",
        "parameters": [
            {
                "key": "datasetId",
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



您可以通过定义为参数的任何类方法访 `configProperties` 问配置JSON。 例如：

**PySpark**

```python
input_dataset_id = str(configProperties.get("datasetId"))
```

**Spark**

```scala
val input_dataset_id: String = configProperties.get("datasetId")
```


### 使用DataLoader准备输入数据

DataLoader负责检索和过滤输入数据。 DataLoader的实现必须扩展抽象类 `DataLoader` 并覆盖抽象方法 `load`。

以下示例按ID检索平台数据集并将其返回为DataFrame，其中数据集ID(`datasetId`)是配置文件中定义的属性。 展开每个示例以查看详细信息：


**PySpark示例**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    def load(self, configProperties, spark):

        # preliminary checks
        if configProperties is None :
            raise ValueError("configProperties parameter is null")
        if spark is None:
            raise ValueError("spark parameter is null")

        # prepare variables
        dataset_id = str(
            configProperties.get("datasetId"))
        service_token = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
        for arg in ['dataset_id', 'service_token', 'user_token', 'org_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # load dataset through Spark session
        df = spark.read.format("com.adobe.platform.dataset") \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('orgId', org_id) \
            .option('serviceApiKey', api_key) \
            .load(dataset_id)

        # return as DataFrame
        return df
```




**Spark示例**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DataLoader
import org.apache.spark.sql.{DataFrame, SparkSession}

class MyDataLoader extends DataLoader {
    override def load(configProperties: ConfigProperties, sparkSession: SparkSession): DataFrame = {

        // preliminary checks
        require(configProperties != null)
        require(sparkSession != null)

        // prepare variables
        val dataSetId: String = configProperties
            .get("datasetId").getOrElse("")
        val serviceToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
        val userToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_TOKEN", "").toString
        val orgId: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
        val apiKey: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

        // validate variables
        List(dataSetId, serviceToken, userToken, orgId, apiKey).foreach(
            value => required(value != "")
        )

        // load dataset through Spark session
        var df = sparkSession.read.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .load(dataSetId)
        
        // return as DataFrame
        df
    }
}
```



### 使用DatasetTransformer转换数据集

DatasetTransformer提供用于转换输入DataFrame的逻辑并返回新派生的DataFrame。 可以实现此类以与FeaturePipelineFactory协同工作，作为唯一的特征工程组件工作，或者您可以选择不实现此类。

以下示例扩展了DatasetTransformer类。 展开每个示例以查看详细信息：


**PySpark示例**

```python
# PySpark

from sdk.dataset_transformer import DatasetTransformer

class MyDatasetTransformer(DatasetTransformer):

    def transform(self, configProperties, dataset):
        transformed = dataset

        '''
        Transformations
        '''

        # return new DataFrame
        return transformed
```




**Spark示例**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DatasetTransformer

class MyDatasetTransformer extends DatasetTransformer {

    override def transform(configProperties: ConfigProperties, dataset: Dataset[_]): Dataset[_] = {
        val transformed = dataset

        /*
        transformations
        */
        
        // return new DataFrame
        transformed
    }
}
```



### 使用FeaturePipelineFactory设计数据功能

FeaturePipelineFactory允许您通过Spark Pipeline定义一系列Spark Transporters并将其链接在一起，从而实现您的功能工程逻辑。 可以实现此类以与DatasetTransformer协同工作，作为唯一的特征工程组件，或者您可以选择不实现此类。

以下示例扩展了FeaturePipelieFactory类，并在Spark Pipeline中将一系列Spark变压器作为多个级实现。 展开每个示例以查看详细信息：


**PySpark示例**

```python
# PySpark

from pyspark.ml import Pipeline
from pyspark.ml.feature import HashingTF, Tokenizer
from sdk.feature_pipeline_factory import FeaturePipelineFactory

class MyFeaturePipelineFactory(FeaturePipelineFactory):

    def create_pipeline(self, configProperties):

        # Spark Transformers
        tokenizer = Tokenizer(inputCol="lower_text", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")

        # Chain together Spark Transformers as Spark Pipeline Stages
        pipeline = Pipeline(stages=[tokenizer, hashingTF])

        # return a Spark Pipeline
        return pipeline

    def get_param_map(self, configProperties, sparkSession):
        pass
```




**Spark示例**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.FeaturePipelineFactory
import org.apache.spark.ml.feature.{HashingTF, Tokenizer}
import org.apache.spark.ml.Pipeline
import org.apache.spark.ml.param.ParamMap
import org.apache.spark.sql.SparkSession

class MyFeaturePipelineFactory(uid:String) extends FeaturePipelineFactory(uid) {
    def this() = this("MyFeaturePipeline")

    override def createPipeline(configProperties: ConfigProperties): Pipeline = {
        
        // Spark Transformers
        val tokenizer = new Tokenizer()
            .setInputCol("lower_text")
            .setOutputCol("words")
        val hashingTF = new HashingTF()
            .setInputCol(tokenizer.getOutputCol())
            .setOutputCol("features")

        // Chain together Spark Transformers as Spark Pipeline Stages
        val pipeline = new Pipeline()
            .setStages(Array(tokenizer, hashingTF))
        
        // return a Spark Pipeline
        pipeline
    }

    override def getParamMap(configProperties: ConfigProperties, sparkSession: SparkSession): ParamMap = {
        val map = new ParamMap()
        map
    }
}
```



### 使用DataSaver存储功能数据集

DataSaver负责将生成的功能数据集存储到存储位置。 您对DataSaver的实现必须扩展抽象类 `DataSaver` 并覆盖抽象方法 `save`。

以下示例扩展了按ID将数据存储到平台数据集的DataSaver类，其中数据集ID(`featureDatasetId`)和租户ID(`tenantId`)是配置文件中定义的属性。 展开每个示例以查看详细信息：


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




**Spark示例**

```scala
// Spark

import com.adobe.platform.dataset.DataSetOptions
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

class MyDataSaver extends DataSaver {
    override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

        // Spark session
        val sparkSession = dataFrame.sparkSession

        // preliminary checks
        require(configProperties != null)
        require(dataFrame != null)

        // prepare variables
        val timestamp:String = "2019-01-01 00:00:00"
        val output_dataset_id: String = configProperties
            .get("featureDatasetId").getOrElse("")
        val tenant_id:String = configProperties
            .get("tenantId").getOrElse("")
        val serviceToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
        val userToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_TOKEN", "").toString
        val orgId: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
        val apiKey: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

        // validate variables
        List(output_dataset_id, tenant_id, serviceToken, userToken, orgId, apiKey).foreach(
            value => require(value != "")
        )

        // create and prepare DataFrame with valid columns
        import sparkSession.implicits._

        var output_df  = dataFrame.withColumn("date", $"date".cast("String"))
        output_df = output_df.withColumn("timestamp", lit(timestamp).cast(TimestampType))
        output_df = output_df.withColumn("_id", lit("empty"))
        output_df = output_df.withColumn("eventType", lit("empty"))

        // store data into dataset
        output_df.select(tenant_id, "_id", "eventType", "timestamp").write.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .save(output_dataset_id)
    }
}
```

### 在应用程序文件中指定实现的类名

既然已定义并实现了功能管道类，则必须在应用程序文件中指定类的名称。

以下示例指定实现的类名。 展开示例以查看详细信息：


**PySpark示例**

```yaml
# application.yaml

# Name of the implementation of DataLoader abstract class
feature.dataLoader: MyDataLoader

# Name of the implementation of DatasetTransformer abstract class
feature.dataset.transformer: MyDatasetTransformer

# Name of the implementation of FeaturePipelineFactory abstract class
feature.pipeline.class: MyFeaturePipelineFactory

# Name of the implementation of DataSaver abstract class
feature.dataSaver: MyDataSaver
```




**Spark示例**

```properties
# application.properties

# Name of the implementation of DataLoader abstract class
feature.pipeline.class=MyDataLoader

# Name of the implementation of DatasetTransformer abstract class
feature.dataset.transformer=MyDatasetTransformer

# Name of the implementation of FeaturePipelineFactory abstract class
feature.dataLoader=MyFeaturePipelineFactory

# Name of the implementation of DataSaver abstract class
feature.dataSaver=MyDataSaver
```



## 构建二进制伪像

现在，您的功能管道类已实现，您可以将其构建并编译为二进制对象，然后使用该对象通过API调用创建功能管道。

**PySpark**

要构建PySpark功能管道，请运行位于“模型创作SDK” `setup.py` 根目录中的Python脚本。

>[!NOTE] 构建PySpark功能管道要求您的计算机上安装Python 3。

```shell
python3 setup.py bdist_egg
```

成功构建特征管道将在目录 `.egg` 中生成一 `/dist` 个对象，该对象用于创建特征管道。

**Spark**

要构建Spark功能管道，请在“模型创作SDK”的根目录中运行以下控制台命令：

>[!NOTE] 要构建Spark功能管道，您必须在计算机上安装Scala和sbt。

```shell
mvn clean install
```

成功构建特征管道将在目录 `.jar` 中生成一 `/dist` 个对象，该对象用于创建特征管道。

## 使用API创建功能管道引擎

现在，您已经创作了功能管道并构建了二进制伪像，您可以 [使用Sensei机器学习API创建功能管道引擎](../api/engines.md#create-a-feature-pipeline-engine-using-binary-artifacts)。 成功创建特征管道引擎将提供引擎ID作为响应体的一部分，请确保在继续执行后续步骤之前保存此值。

## 后续步骤

[//]: # (Next steps section should refer to tutorials on how to score data using the Feature Pipeline Engine. Update this document once those tutorials are available)

通过阅读此文档，您使用模型创作SDK创作了功能管道，构建了二进制对象，并使用该对象通过API调用创建了功能管道引擎。 您现在可以使用新创 [建的引擎和开始大规模转换数据集和提取数据特征来创建功能管道模型](../api/mlinstances.md#create-an-mlinstance) 。