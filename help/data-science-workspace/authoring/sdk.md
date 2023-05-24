---
keywords: Experience Platform；開發人員指南；SDK；模型製作；Data Science Workspace；熱門主題；測試
solution: Experience Platform
title: 模型製作SDK
description: Model Authoring SDK可讓您開發可在Adobe Experience Platform Data Science Workspace中使用的自訂機器學習方法和功能管道，在PySpark和Spark (Scala)中提供可實施的範本。
exl-id: c7577f93-a64f-49b7-a76d-71f21d619052
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 1%

---

# 模型製作SDK

Model Authoring SDK可讓您開發自訂的機器學習方法和功能管道，這些方法可用於 [!DNL Adobe Experience Platform] Data Science Workspace，提供可實施的範本 [!DNL PySpark] 和 [!DNL Spark (Scala)].

本檔案提供Model Authoring SDK中各種類別的相關資訊。

## DataLoader {#dataloader}

DataLoader類別會封裝與擷取、篩選和傳回原始輸入資料相關的任何專案。 輸入資料的範例包括訓練、評分或功能工程方面的資料。 資料載入器會擴充抽象類別 `DataLoader` 和必須覆寫抽象方法 `load`.

**PySpark**

下表說明PySpark Data Loader類別的抽象方法：

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>load(self, configProperties, spark)</code></p>
                <p>以Pandas DataFrame載入並傳回Platform資料</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>：自我參照</li>
                    <li><code>configProperties</code>：設定屬性對應</li>
                    <li><code>spark</code>： Spark工作階段</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

下表說明的抽象方法 [!DNL Spark] 資料載入器類別：

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>load(configProperties, sparkSession)</code></p>
                <p>以DataFrame形式載入及傳回Platform資料</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>：設定屬性對應</li>
                    <li><code>sparkSession</code>： Spark工作階段</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### 從載入資料 [!DNL Platform] 資料集 {#load-data-from-a-platform-dataset}

下列範例會擷取 [!DNL Platform] 依ID分類資料並傳回DataFrame，其中資料集ID (`datasetId`)是設定檔案中定義的屬性。

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

DataSaver類別會封裝與儲存輸出資料相關的任何專案，包括來自評分或功能工程的資料。 資料儲存器會擴充抽象類別 `DataSaver` 和必須覆寫抽象方法 `save`.

**PySpark**

下表說明的抽象方法 [!DNL PySpark] 資料儲存器類別：

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>save(self, configProperties, dataframe)</code></p>
                <p>以DataFrame形式接收輸出資料，並將其儲存在Platform資料集中</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>：自我參照</li>
                    <li><code>configProperties</code>：設定屬性對應</li>
                    <li><code>dataframe</code>：要以DataFrame形式儲存的資料</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

下表說明的抽象方法 [!DNL Spark] 資料儲存器類別：

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>save(configProperties, dataFrame)</code></p>
                <p>以DataFrame形式接收輸出資料，並將其儲存在Platform資料集中</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>：設定屬性對應</li>
                    <li><code>dataFrame</code>：要以DataFrame形式儲存的資料</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### 將資料儲存至 [!DNL Platform] 資料集 {#save-data-to-a-platform-dataset}

為了將資料儲存至 [!DNL Platform] 資料集，必須在設定檔案中提供或定義屬性：

- 有效的 [!DNL Platform] 要儲存資料的資料集ID
- 屬於您組織的租使用者ID

以下範例會儲存資料(`prediction`)至 [!DNL Platform] 資料集，其中資料集ID (`datasetId`)和租使用者ID (`tenantId`)的屬性定義於設定檔案中。


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

## Datasettransformer {#datasettransformer}

DatasetTransformer類別會修改及轉換資料集的結構。 此 [!DNL Sensei Machine Learning Runtime] 不需定義此元件，且會根據您的需求實作。

關於功能管道，資料集轉換器可與功能管道工廠搭配使用，以便為功能工程準備資料。

**PySpark**

下表說明PySpark資料集轉換器類別的類別方法：

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>transform(self, configProperties, dataset)</code></p>
                <p>將資料集作為輸入，並輸出新的衍生資料集</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>：自我參照</li>
                    <li><code>configProperties</code>：設定屬性對應</li>
                    <li><code>dataset</code>：轉換的輸入資料集</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

下表說明的抽象方法 [!DNL Spark] 資料集轉換器類別：

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>transform(configProperties, dataset)</code></p>
                <p>將資料集作為輸入，並輸出新的衍生資料集</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>：設定屬性對應</li>
                    <li><code>dataset</code>：轉換的輸入資料集</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## FeaturePipelineFactor {#featurepipelinefactory}

FeaturePipelineFactory類別包含功能擷取演演算法，並定義功能管道從開始到結束的階段。

**PySpark**

下表說明PySpark FeaturePipelineFactory的類別方法：

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>create_pipeline(self, configProperties)</code></p>
                <p>建立並傳回包含一系列Spark轉換器的Spark配管</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>：自我參照</li>
                    <li><code>configProperties</code>：設定屬性對應</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>從設定屬性擷取並傳回引數對應</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>：自我參照</li>
                    <li><code>configProperties</code>：設定屬性</li>
                    <li><code>sparkSession</code>： Spark工作階段</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

下表說明的類別方法 [!DNL Spark] FeaturePipelineFactory：

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>createPipeline(configProperties)</code></p>
                <p>建立並傳回包含一系列轉換器的管道</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>：設定屬性對應</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>從設定屬性擷取並傳回引數對應</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>：設定屬性</li>
                    <li><code>sparkSession</code>： Spark工作階段</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## Pipelinefactory {#pipelinefactory}

PipelineFactory類別封裝模型訓練和評分的方法和定義，其中訓練邏輯和演演算法的定義形式為 [!DNL Spark] 管道。

**PySpark**

下表說明PySpark PipelineFactory的類別方法：

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>apply(self, configProperties)</code></p>
                <p>建立並傳回Spark管道，其中包含模型訓練和評分的邏輯和演演算法</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>：自我參照</li>
                    <li><code>configProperties</code>：設定屬性</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>train(self, configProperties, dataframe)</code></p>
                <p>傳回包含用來訓練模型的邏輯和演演算法的自訂管道。 如果使用Spark配管，則不需要此方法</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>：自我參照</li>
                    <li><code>configProperties</code>：設定屬性</li>
                    <li><code>dataframe</code>：用於訓練輸入的功能資料集</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>score(self, configProperties, dataframe, model)</code></p>
                <p>使用經過訓練的模型分數並傳回結果</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>：自我參照</li>
                    <li><code>configProperties</code>：設定屬性</li>
                    <li><code>dataframe</code>：輸入資料集以進行評分</li>
                    <li><code>model</code>：用於評分的訓練模型</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>從設定屬性擷取並傳回引數對應</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>：自我參照</li>
                    <li><code>configProperties</code>：設定屬性</li>
                    <li><code>sparkSession</code>： Spark工作階段</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

下表說明的類別方法 [!DNL Spark] PipelineFactory：

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>apply(configProperties)</code></p>
                <p>建立並傳回包含模型訓練和評分的邏輯和演演算法的管道</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>：設定屬性</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>從設定屬性擷取並傳回引數對應</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>：設定屬性</li>
                    <li><code>sparkSession</code>： Spark工作階段</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## MLEvaluator {#mlevaluator}

MLEvaluator類別提供定義評估量度以及決定訓練和測試資料集的方法。

**PySpark**

下表說明PySpark MLEvaluator的類別方法：

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>split(self, configProperties, dataframe)</code></p>
                <p>將輸入資料集分割為訓練和測試子集</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>：自我參照</li>
                    <li><code>configProperties</code>：設定屬性</li>
                    <li><code>dataframe</code>：要分割的輸入資料集</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>evaluate(self, dataframe, model, configProperties)</code></p>
                <p>評估經過訓練的模型並傳回評估結果</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>：自我參照</li>
                    <li><code>dataframe</code>：由訓練和測試資料組成的DataFrame</li>
                    <li><code>model</code>：訓練有素的模型</li>
                    <li><code>configProperties</code>：設定屬性</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

下表說明的類別方法 [!DNL Spark] MLEvaluator：

<table>
    <thead>
        <tr>
            <th>方法和說明</th>
            <th>参数</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>split(configProperties, data)</code></p>
                <p>將輸入資料集分割為訓練和測試子集</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>：設定屬性</li>
                    <li><code>data</code>：要分割的輸入資料集</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>抽象</i><br/><code>evaluate(configProperties, model, data)</code></p>
                <p>評估經過訓練的模型並傳回評估結果</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>：設定屬性</li>
                    <li><code>model</code>：訓練有素的模型</li>
                    <li><code>data</code>：由訓練和測試資料組成的DataFrame</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>
