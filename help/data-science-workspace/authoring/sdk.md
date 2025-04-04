---
keywords: Experience Platform；开发人员指南；SDK；模型创作；数据科学Workspace；热门主题；测试
solution: Experience Platform
title: 模型创作SDK
description: 模型创作SDK允许您开发自定义机器学习方法和功能管道，这些管道可以在Adobe Experience Platform数据科学Workspace中使用，从而在PySpark和Spark (Scala)中提供可实施的模板。
exl-id: c7577f93-a64f-49b7-a76d-71f21d619052
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 1%

---

# 模型创作SDK

>[!NOTE]
>
>数据科学Workspace不再可供购买。
>
>本文档面向之前有权访问数据科学Workspace的现有客户。

模型创作SDK允许您开发自定义机器学习方法和功能管道，这些管道可在[!DNL Adobe Experience Platform]数据科学Workspace中使用，从而在[!DNL PySpark]和[!DNL Spark (Scala)]中提供可实施的模板。

本文档提供了有关在模型创作SDK中找到的各种类的信息。

## 数据加载程序 {#dataloader}

DataLoader类封装与检索、筛选和返回原始输入数据相关的任何内容。 输入数据的示例包括用于训练、评分或功能工程的示例。 数据加载器扩展抽象类`DataLoader`，必须覆盖抽象方法`load`。

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
                <p><code>load(self, configProperties, spark)</code></p>
                <p>将Experience Platform数据作为Pandas DataFrame加载和返回</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>：自引用</li>
                    <li><code>configProperties</code>：配置属性映射</li>
                    <li><code>spark</code>： Spark会话</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

下表描述了[!DNL Spark] Data Loader类的抽象方法：

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
                <p><code>load(configProperties, sparkSession)</code></p>
                <p>将Experience Platform数据作为DataFrame加载和返回</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>：配置属性映射</li>
                    <li><code>sparkSession</code>： Spark会话</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### 从[!DNL Experience Platform]数据集加载数据 {#load-data-from-a-platform-dataset}

以下示例按ID检索[!DNL Experience Platform]数据并返回一个DataFrame，其中数据集ID (`datasetId`)是配置文件中定义的属性。

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

**Spark (Scala)**

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

## DataSaver {#datasaver}

DataSaver类封装与存储输出数据相关的任何内容，包括来自评分或功能工程的数据。 数据保存程序扩展抽象类`DataSaver`，必须覆盖抽象方法`save`。

**PySpark**

下表描述了[!DNL PySpark]数据保存程序类的抽象方法：

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
                <p><code>save(self, configProperties, dataframe)</code></p>
                <p>将输出数据作为DataFrame进行接收并将其存储在Experience Platform数据集中</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>：自引用</li>
                    <li><code>configProperties</code>：配置属性映射</li>
                    <li><code>dataframe</code>：要以DataFrame形式存储的数据</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

下表描述了[!DNL Spark]数据保存程序类的抽象方法：

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
                <p><code>save(configProperties, dataFrame)</code></p>
                <p>将输出数据作为DataFrame进行接收并将其存储在Experience Platform数据集中</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>：配置属性映射</li>
                    <li><code>dataFrame</code>：要以DataFrame形式存储的数据</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### 将数据保存到[!DNL Experience Platform]数据集 {#save-data-to-a-platform-dataset}

要将数据存储到[!DNL Experience Platform]数据集上，必须在配置文件中提供或定义属性：

- 数据将存储到的有效[!DNL Experience Platform]数据集ID
- 属于您组织的租户ID

以下示例将数据(`prediction`)存储到[!DNL Experience Platform]数据集上，其中数据集ID (`datasetId`)和租户ID (`tenantId`)是配置文件中定义的属性。


**PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct
from .helper import *


class MyDataSaver(DataSaver):
    """
    Implementation of DataSaver which stores a DataFrame to an Experience Platform dataset
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

**Spark (Scala)**

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
 * Implementation of DataSaver which stores a DataFrame to an Experience Platform dataset
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

DatasetTransformer类可修改和转换数据集的结构。 [!DNL Sensei Machine Learning Runtime]不需要定义此组件，而是根据您的要求实施。

关于特征管道，数据集转换器可以与特征管道工厂协同使用，为特征工程准备数据。

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
                <p><i>摘要</i><br/><code>transform(self, configProperties, dataset)</code></p>
                <p>以数据集为输入，输出新的派生数据集</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>：自引用</li>
                    <li><code>configProperties</code>：配置属性映射</li>
                    <li><code>dataset</code>：要转换的输入数据集</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

下表描述了[!DNL Spark]数据集转换器类的抽象方法：

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
                <p><code>transform(configProperties, dataset)</code></p>
                <p>以数据集为输入，输出新的派生数据集</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>：配置属性映射</li>
                    <li><code>dataset</code>：要转换的输入数据集</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## 功能管道工厂 {#featurepipelinefactory}

FeaturePipelineFactory类包含特征提取算法，并定义特征管道从开始到结束的阶段。

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
                <p><i>摘要</i><br/><code>create_pipeline(self, configProperties)</code></p>
                <p>创建并返回包含一系列Spark转换器的Spark管线</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>：自引用</li>
                    <li><code>configProperties</code>：配置属性映射</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>摘要</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>从配置属性检索并返回参数映射</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>：自引用</li>
                    <li><code>configProperties</code>：配置属性</li>
                    <li><code>sparkSession</code>： Spark会话</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

下表描述了[!DNL Spark] FeaturePipelineFactory的类方法：

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
                <p><i>摘要</i><br/><code>createPipeline(configProperties)</code></p>
                <p>创建和返回包含一系列转换器的管道</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>：配置属性映射</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>摘要</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>从配置属性检索并返回参数映射</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>：配置属性</li>
                    <li><code>sparkSession</code>： Spark会话</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## 管道工厂 {#pipelinefactory}

PipelineFactory类封装用于模型训练和评分的方法和定义，其中训练逻辑和算法以[!DNL Spark]管道的形式定义。

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
                <p><i>摘要</i><br/><code>apply(self, configProperties)</code></p>
                <p>创建并返回Spark管道，其中包含模型训练和评分的逻辑和算法</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>：自引用</li>
                    <li><code>configProperties</code>：配置属性</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>摘要</i><br/><code>train(self, configProperties, dataframe)</code></p>
                <p>返回包含用于训练模型的逻辑和算法的自定义管道。 如果使用Spark管线，则不需要使用此方法</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>：自引用</li>
                    <li><code>configProperties</code>：配置属性</li>
                    <li><code>dataframe</code>：用于训练输入的功能数据集</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>摘要</i><br/><code>score(self, configProperties, dataframe, model)</code></p>
                <p>使用经过训练的模型对评分并返回结果</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>：自引用</li>
                    <li><code>configProperties</code>：配置属性</li>
                    <li><code>dataframe</code>：用于评分的输入数据集</li>
                    <li><code>model</code>：用于评分的经过训练的模型</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>摘要</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>从配置属性检索并返回参数映射</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>：自引用</li>
                    <li><code>configProperties</code>：配置属性</li>
                    <li><code>sparkSession</code>： Spark会话</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

下表描述了[!DNL Spark] PipelineFactory的类方法：

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
                <p><i>摘要</i><br/><code>apply(configProperties)</code></p>
                <p>创建并返回包含模型训练和评分的逻辑和算法的管道</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>：配置属性</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>摘要</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>从配置属性检索并返回参数映射</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>：配置属性</li>
                    <li><code>sparkSession</code>： Spark会话</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## MLEvaluator {#mlevaluator}

MLEvaluator类提供了用于定义评估指标以及确定训练和测试数据集的方法。

**PySpark**

下表描述了PySpark MLEvaluator的类方法：

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
                <p><i>摘要</i><br/><code>split(self, configProperties, dataframe)</code></p>
                <p>将输入数据集拆分为训练和测试子集</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>：自引用</li>
                    <li><code>configProperties</code>：配置属性</li>
                    <li><code>dataframe</code>：要拆分的输入数据集</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>摘要</i><br/><code>evaluate(self, dataframe, model, configProperties)</code></p>
                <p>评估经过训练的模型并返回评估结果</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>：自引用</li>
                    <li><code>dataframe</code>：由训练和测试数据组成的DataFrame</li>
                    <li><code>model</code>：经过训练的模型</li>
                    <li><code>configProperties</code>：配置属性</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

下表描述了[!DNL Spark] MLEvaluator的类方法：

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
                <p><i>摘要</i><br/><code>split(configProperties, data)</code></p>
                <p>将输入数据集拆分为训练和测试子集</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>：配置属性</li>
                    <li><code>data</code>：要拆分的输入数据集</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>摘要</i><br/><code>evaluate(configProperties, model, data)</code></p>
                <p>评估经过训练的模型并返回评估结果</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>：配置属性</li>
                    <li><code>model</code>：经过训练的模型</li>
                    <li><code>data</code>：由训练和测试数据组成的DataFrame</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>
