---
keywords: Experience Platform;developer guide;SDK;Model authoring;Data Science Workspace;popular topics;testing
solution: Experience Platform
title: SDK开发人员指南
topic: Overview
description: 模型创作SDK使您能够开发可在Adobe Experience Platform数据科学工作区中使用的自定义机器学习方法和功能管道，在PySpark和Spark(Scala)中提供可实施的模板。
translation-type: tm+mt
source-git-commit: 2a528c705a7aa610f57047be39be1ce9886ce44c
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 1%

---


# SDK开发人员指南

模型创作SDK使您能够开发可在Data Science Workspace中使用的自定义机器学习方法和功 [!DNL Adobe Experience Platform] 能管道，在和中提供可实施 [!DNL PySpark] 的模板 [!DNL Spark (Scala)]。

此文档提供有关“模型创作SDK”中的各种类的信息。

## DataLoader {#dataloader}

DataLoader类封装与检索、过滤和返回原始输入数据相关的任何内容。 输入数据的示例包括用于培训、评分或功能工程的数据。 数据加载器扩展抽象类 `DataLoader` ，并且必须覆盖抽象方法 `load`。

**PySpark**

下表描述了PySpark Data Loader类的抽象方法：

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code class=" language-undefined">load(self, configProperties, spark)</code></p>
                <p>将平台数据作为Aplytics DataFrame加载并返回</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自引用</li>
                    <li><code class=" language-undefined">configProperties</code>:配置属性映射</li>
                    <li><code class=" language-undefined">spark</code>:Spark会话</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

下表描述了Data Loader类的抽 [!DNL Spark] 象方法：

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code class=" language-undefined">load(configProperties, sparkSession)</code></p>
                <p>将平台数据作为DataFrame加载和返回</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:配置属性映射</li>
                    <li><code class=" language-undefined">sparkSession</code>:Spark会话</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### 从数据集加载数 [!DNL Platform] 据 {#load-data-from-a-platform-dataset}

以下示例按 [!DNL Platform] ID检索数据并返回DataFrame，其中数据集ID(`datasetId`)是配置文件中定义的属性。

**PySpark**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    """
    Implementation of DataLoader which loads a DataFrame and prepares data
    """

    def load_dataset(config_properties, spark, task_id):

        PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"
        PLATFORM_SDK_PQS_INTERACTIVE = "interactive"

        # prepare variables
        service_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        dataset_id = str(config_properties.get(task_id))

        # validate variables
        for arg in ['service_token', 'user_token', 'org_id', 'dataset_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # load dataset through Spark session

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

        # return as DataFrame
        return pd
```

**Spark(Scala)**

```scala
// Spark

package com.adobe.platform.ml

import java.time.LocalDateTime

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.query.QSOption
import org.apache.spark.ml.feature.StringIndexer
import org.apache.spark.sql.expressions.Window
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.{StructType, TimestampType}
import org.apache.spark.sql.{DataFrame, SparkSession}
import org.apache.spark.sql.Column

/**
 * Implementation of DataLoader which loads a DataFrame and prepares data
 */
class MyDataLoader extends DataLoader {

    final val PLATFORM_SDK_PQS_PACKAGE: String = "com.adobe.platform.query"
    final val PLATFORM_SDK_PQS_INTERACTIVE: String = "interactive"
    final val PLATFORM_SDK_PQS_BATCH: String = "batch"

    /**
    *
    * @param configProperties - Configuration Properties map
    * @param sparkSession     - SparkSession
    * @return                 - DataFrame which is loaded for training
    */


  def load_dataset(configProperties: ConfigProperties, sparkSession: SparkSession, taskId: String): DataFrame = {

    require(configProperties != null)
    require(sparkSession != null)

    // Read the configs
    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

    val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, PLATFORM_SDK_PQS_INTERACTIVE)
      .option(QSOption.datasetId, dataSetId)
      .load()
    df.show()
    df
    }
}
```

## 数据保护程序 {#datasaver}

DataSaver类封装与存储输出数据相关的任何内容，包括来自评分或功能工程的输出数据。 数据保护程序扩展抽象 `DataSaver` 类，并且必须覆盖抽象方法 `save`。

**PySpark**

下表描述了数据保护程序类的 [!DNL PySpark] 抽象方法：

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code class=" language-undefined">save(self, configProperties, dataframe)</code></p>
                <p>将输出数据作为DataFrame接收并存储在平台数据集中</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自引用</li>
                    <li><code class=" language-undefined">configProperties</code>:配置属性映射</li>
                    <li><code class=" language-undefined">dataframe</code>:以DataFrame形式存储的数据</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark(Scala)**

下表描述了数据保护程序类的 [!DNL Spark] 抽象方法：

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code class=" language-undefined">save(configProperties, dataFrame)</code></p>
                <p>将输出数据作为DataFrame接收并存储在平台数据集中</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:配置属性映射</li>
                    <li><code class=" language-undefined">dataFrame</code>:以DataFrame形式存储的数据</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### 将数据保存到数 [!DNL Platform] 据集 {#save-data-to-a-platform-dataset}

要将数据存储到数据集 [!DNL Platform] 上，必须在配置文件中提供或定义属性：

- 要存储数 [!DNL Platform] 据的有效数据集ID
- 属于您的组织的租户ID

以下示例将数据(`prediction`)存储到数 [!DNL Platform] 据集上，其中数据集ID(`datasetId`)和租户ID()是配置文`tenantId`件中定义的属性。


**PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct
from .helper import *


class MyDataSaver(DataSaver):
    """
    Implementation of DataSaver which stores a DataFrame to a Platform dataset
    """

    def save(self, config_properties, prediction):

        # Spark context
        sparkContext = prediction._sc

        # preliminary checks
        if config_properties is None:
            raise ValueError("config_properties parameter is null")
        if prediction is None:
            raise ValueError("prediction parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")
        
        PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"

        # prepare variables
        scored_dataset_id = str(config_properties.get("scoringResultsDataSetId"))
        tenant_id = str(config_properties.get("tenant_id"))
        timestamp = "2019-01-01 00:00:00"

        service_token = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
       for arg in ['service_token', 'user_token', 'org_id', 'scored_dataset_id', 'api_key', 'tenant_id']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)
        
        scored_df = prediction.withColumn("date", col("date").cast(StringType()))
        scored_df = scored_df.withColumn(tenant_id, struct(col("date"), col("store"), col("prediction")))
        scored_df = scored_df.withColumn("timestamp", lit(timestamp).cast(TimestampType()))
        scored_df = scored_df.withColumn("_id", lit("empty"))
        scored_df = scored_df.withColumn("eventType", lit("empty")

        # store data into dataset

        query_options = get_query_options(sparkContext)

        scored_df.select(tenant_id, "_id", "eventType", "timestamp").write.format(PLATFORM_SDK_PQS_PACKAGE) \
            .option(query_options.userToken(), user_token) \
            .option(query_options.serviceToken(), service_token) \
            .option(query_options.imsOrg(), org_id) \
            .option(query_options.apiKey(), api_key) \
            .option(query_options.datasetId(), scored_dataset_id) \
            .save()
```

**Spark(Scala)**

```scala
// Spark

package com.adobe.platform.ml

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import com.adobe.platform.query.QSOption
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

/**
 * Implementation of DataSaver which stores a DataFrame to a Platform dataset
 */

class ScoringDataSaver extends DataSaver {

  final val PLATFORM_SDK_PQS_PACKAGE: String = "com.adobe.platform.query"
  final val PLATFORM_SDK_PQS_BATCH: String = "batch"

  /**
    * Method that saves the scoring data into a dataframe
    * @param configProperties  - Configuration Properties map
    * @param dataFrame         - Dataframe with the scoring results
    */
    
  override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

    require(configProperties != null)
    require(dataFrame != null)

    val predictionColumn = configProperties.get(Constants.PREDICTION_COL).getOrElse(Constants.DEFAULT_PREDICTION)
    val sparkSession = dataFrame.sparkSession

    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val tenantId:String = configProperties.get("tenantId").getOrElse("")
    val timestamp:String = "2019-01-01 00:00:00"

    val scoringResultsDataSetId: String = configProperties.get("scoringResultsDataSetId").getOrElse("")
    import sparkSession.implicits._

    var df = dataFrame.withColumn("date", $"date".cast("String"))

    var scored_df  = df.withColumn(tenantId, struct(df("date"), df("store"), df(predictionColumn)))
    scored_df = scored_df.withColumn("timestamp", lit(timestamp).cast(TimestampType))
    scored_df = scored_df.withColumn("_id", lit("empty"))
    scored_df = scored_df.withColumn("eventType", lit("empty"))

    scored_df.select(tenantId, "_id", "eventType", "timestamp").write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .save()
    }
}
```

## DatasetTransformer {#datasettransformer}

DatasetTransformer类修改和转换数据集的结构。 该组 [!DNL Sensei Machine Learning Runtime] 件不需要定义，并且根据您的要求实施。

对于特征管线，数据集转换器可以与特征管线工厂协同使用，为特征工程准备数据。

**PySpark**

下表描述了PySpark数据集转换器类的类方法：

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>抽象</i><br/><code class=" language-undefined">transform(self, configProperties, dataset)</code></p>
                <p>将数据集作为输入并输出新的派生数据集</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自引用</li>
                    <li><code class=" language-undefined">configProperties</code>:配置属性映射</li>
                    <li><code class=" language-undefined">dataset</code>:转换的输入数据集</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark(Scala)**

下表描述了数据集转换器类 [!DNL Spark] 的抽象方法：

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code class=" language-undefined">transform(configProperties, dataset)</code></p>
                <p>将数据集作为输入并输出新的派生数据集</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:配置属性映射</li>
                    <li><code class=" language-undefined">dataset</code>:转换的输入数据集</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## 功能管道工厂 {#featurepipelinefactory}

FeaturePipelineFactory类包含功能提取算法，并定义从开始到完成的功能管道的各个阶段。

**PySpark**

下表描述了PySpark FeaturePipelineFactory的类方法：

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>抽象</i><br/><code class=" language-undefined">create_pipeline(self, configProperties)</code></p>
                <p>创建并返回包含一系列Spark Transformers的Spark Pipeline</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自引用</li>
                    <li><code class=" language-undefined">configProperties</code>:配置属性映射</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code class=" language-undefined">get_param_map(self, configProperties, sparkSession)</code></p>
                <p>从配置属性检索并返回参数映射</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自引用</li>
                    <li><code class=" language-undefined">configProperties</code>:配置属性</li>
                    <li><code class=" language-undefined">sparkSession</code>:Spark会话</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark(Scala)**

下表描述了FeaturePipelineFactory的类方 [!DNL Spark] 法：

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>抽象</i><br/><code class=" language-undefined">createPipeline(configProperties)</code></p>
                <p>创建并返回包含一系列变压器的管道</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:配置属性映射</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code class=" language-undefined">getParamMap(configProperties, sparkSession)</code></p>
                <p>从配置属性检索并返回参数映射</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:配置属性</li>
                    <li><code class=" language-undefined">sparkSession</code>:Spark会话</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## PipelineFactory {#pipelinefactory}

PipelineFactory类封装了模型培训和评分的方法和定义，其中培训逻辑和算法以管道的形式进 [!DNL Spark] 行定义。

**PySpark**

下表描述了PySpark PipelineFactory的类方法：

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>抽象</i><br/><code class=" language-undefined">apply(self, configProperties)</code></p>
                <p>创建并返回一个Spark Pipeline，其中包含用于模型培训和评分的逻辑和算法</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自引用</li>
                    <li><code class=" language-undefined">configProperties</code>:配置属性</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code class=" language-undefined">train(self, configProperties, dataframe)</code></p>
                <p>返回包含训练模型的逻辑和算法的自定义管道。 如果使用Spark管道，则不需要此方法</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自引用</li>
                    <li><code class=" language-undefined">configProperties</code>:配置属性</li>
                    <li><code class=" language-undefined">dataframe</code>:用于培训输入的特征数据集</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code class=" language-undefined">score(self, configProperties, dataframe, model)</code></p>
                <p>使用训练好的模型进行评分并返回结果</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自引用</li>
                    <li><code class=" language-undefined">configProperties</code>:配置属性</li>
                    <li><code class=" language-undefined">dataframe</code>:用于评分的输入数据集</li>
                    <li><code class=" language-undefined">model</code>:用于评分的训练模型</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code class=" language-undefined">get_param_map(self, configProperties, sparkSession)</code></p>
                <p>从配置属性检索并返回参数映射</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自引用</li>
                    <li><code class=" language-undefined">configProperties</code>:配置属性</li>
                    <li><code class=" language-undefined">sparkSession</code>:Spark会话</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark(Scala)**

下表描述了PipelineFactory的类方 [!DNL Spark] 法：

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>抽象</i><br/><code class=" language-undefined">apply(configProperties)</code></p>
                <p>创建并返回包含模型培训和评分的逻辑和算法的管道</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:配置属性</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code class=" language-undefined">getParamMap(configProperties, sparkSession)</code></p>
                <p>从配置属性检索并返回参数映射</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:配置属性</li>
                    <li><code class=" language-undefined">sparkSession</code>:Spark会话</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## MLEvaluator {#mlevaluator}

MLEvaluator类提供了定义评估度量以及确定培训和测试数据集的方法。

**PySpark**

下表描述了PySpark MLvalueator的类方法：

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>抽象</i><br/><code class=" language-undefined">split(self, configProperties, dataframe)</code></p>
                <p>将输入数据集拆分为培训和测试子集</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自引用</li>
                    <li><code class=" language-undefined">configProperties</code>:配置属性</li>
                    <li><code class=" language-undefined">dataframe</code>:要拆分的输入数据集</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code class=" language-undefined">evaluate(self, dataframe, model, configProperties)</code></p>
                <p>评估经过培训的模型并返回评估结果</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自引用</li>
                    <li><code class=" language-undefined">dataframe</code>:由培训和测试数据组成的数据框架</li>
                    <li><code class=" language-undefined">model</code>:一个训练有素的模特</li>
                    <li><code class=" language-undefined">configProperties</code>:配置属性</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark(Scala)**

下表描述了MLEvaluator的类方 [!DNL Spark] 法：

<table>
    <thead>
        <tr>
            <th>方法和描述</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>抽象</i><br/><code class=" language-undefined">split(configProperties, data)</code></p>
                <p>将输入数据集拆分为培训和测试子集</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:配置属性</li>
                    <li><code class=" language-undefined">data</code>:要拆分的输入数据集</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code class=" language-undefined">evaluate(configProperties, model, data)</code></p>
                <p>评估经过培训的模型并返回评估结果</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:配置属性</li>
                    <li><code class=" language-undefined">model</code>:一个训练有素的模特</li>
                    <li><code class=" language-undefined">data</code>:由培训和测试数据组成的数据框架</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>