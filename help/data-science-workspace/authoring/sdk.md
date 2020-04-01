---
keywords: Experience Platform;developer guide;SDK;Model authoring;Data Science Workspace;popular topics
solution: Experience Platform
title: SDK开发人员指南
topic: Overview
translation-type: tm+mt
source-git-commit: 13b6c08b1038d48cdff7147dfcd7b65ea2f95599

---


# SDK开发人员指南

模型创作SDK使您能够开发可在Adobe Experience Platform Data Science Workspace中使用的自定义机器学习方法和功能管道，在PySpark和Spark中提供可实施的模板。

本文档提供有关“模型创作SDK”中的各种类的信息：

- [DataLoader](#dataloader)
   - [从平台数据集加载数据](#load-data-from-a-platform-dataset)
- [DataSaver](#datasaver)
   - [将数据保存到平台数据集](#save-data-to-a-platform-dataset)
- [DatasetTransformer](#datasettransformer)
- [FeaturePipelineFactory](#featurepipelinefactory)
- [PipelineFactory](#pipelinefactory)
- [MLE值器](#mlevaluator)

## DataLoader

DataLoader类封装与检索、过滤和返回原始输入数据相关的任何内容。 输入数据的示例包括用于培训、评分或功能工程的数据。 数据加载程序扩展抽象类， `DataLoader` 并且必须覆盖抽象方法 `load`。

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
                <p>将平台数据作为Pactys DataFrame加载和返回</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自我参考</li>
                    <li><code class=" language-undefined">configProperties</code>:配置属性映射</li>
                    <li><code class=" language-undefined">spark</code>:Spark会话</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

下表描述了Spark Data Loader类的抽象方法：

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

### 从平台数据集加载数据

以下示例按ID检索平台数据并返回一个DataFrame，其中数据集ID(`datasetId`)是配置文件中定义的属性。

**PySpark**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    """
    Implementation of DataLoader which loads a DataFrame and prepares data
    """

    def load(self, configProperties, spark):
        """
        Load and return dataset

        :param configProperties:    Configuration properties
        :param spark:               Spark session
        :return:                    DataFrame
        """

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
        pd = spark.read.format("com.adobe.platform.dataset") \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('orgId', org_id) \
            .option('serviceApiKey', api_key) \
            .load(dataset_id)

        # return as DataFrame
        return pd
```

**Spark**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DataLoader
import org.apache.spark.sql.{DataFrame, SparkSession}

/**
 * Implementation of DataLoader which loads a DataFrame and prepares data
 */
class MyDataLoader extends DataLoader {

    /**
     * @param configProperties  - Configuration properties
     * @param sparkSession      - Spark session
     * @return                  - DataFrame
     */
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

## DataSaver

DataSaver类封装与存储输出数据相关的任何内容，包括来自评分或功能工程的输出数据。 数据保护程序扩展了抽象类， `DataSaver` 并且必须覆盖抽象方法 `save`。

**PySpark**

下表描述了PySpark Data Saver类的抽象方法：

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
                    <li><code class=" language-undefined">self</code>:自我参考</li>
                    <li><code class=" language-undefined">configProperties</code>:配置属性映射</li>
                    <li><code class=" language-undefined">dataframe</code>:以DataFrame形式存储的数据</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

下表介绍了Spark Data Saver类的抽象方法：

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
                <p><code class=" language-undefined">save(configProperties, sparkSession)</code></p>
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

### 将数据保存到平台数据集

要将数据存储到平台数据集上，必须在配置文件中提供或定义属性：

- 数据将存储到的有效平台数据集ID
- 属于您的组织的租户ID

以下示例将数据(`prediction`)存储到平台数据集上，其中数据集ID(`datasetId`)和租户ID(`tenantId`)是配置文件中定义的属性。


**PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType


class MyDataSaver(DataSaver):
    """
    Implementation of DataSaver which stores a DataFrame to a Platform dataset
    """

    def save(self, configProperties, prediction):
        """
        Store DataFrame to a Platform dataset

        :param configProperties:    Configuration properties
        :param prediction:          DataFrame to be stored to a Platform dataset
        """

        # Spark context
        sparkContext = prediction._sc

        # preliminary checks
        if configProperties is None:
            raise ValueError("configProperties parameter is null")
        if prediction is None:
            raise ValueError("prediction parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")

        # prepare variables
        timestamp = "2019-01-01 00:00:00"
        output_dataset_id = str(
            configProperties.get("datasetId"))
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

        # store data into dataset
        prediction.write.format("com.adobe.platform.dataset") \
            .option('orgId', org_id) \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('serviceApiKey', api_key) \
            .save(output_dataset_id)
```




**Spark**

```scala
// Spark

import com.adobe.platform.dataset.DataSetOptions
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

/**
 * Implementation of DataSaver which stores a DataFrame to a Platform dataset
 */
class ScoringDataSaver extends DataSaver {

    /**
     * @param configProperties  - Configuration properties
     * @param dataFrame         - DataFrame to be stored to a Platform dataset
     */
    override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

        // Spark session
        val sparkSession = dataFrame.sparkSession
        import sparkSession.implicits._

        // preliminary checks
        require(configProperties != null)
        require(dataFrame != null)

        // prepare variables
        val predictionColumn = configProperties.get(Constants.PREDICTION_COL)
            .getOrElse(Constants.DEFAULT_PREDICTION)
        val timestamp:String = "2019-01-01 00:00:00"
        val output_dataset_id: String = configProperties
            .get("datasetId").getOrElse("")
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

        // store data into dataset
        dataFrame.write.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .save(output_dataset_id)
    }
}
```

## DatasetTransformer

DatasetTransformer类修改和转换数据集的结构。 Sensei机器学习运行时不需要定义此组件，并根据您的要求实施。

关于特征管线，数据集转换器可以与特征管线工厂协同使用，以准备用于特征工程的数据。

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
                <p><i>摘要</i><br/><code class=" language-undefined">transform(self, configProperties, dataset)</code></p>
                <p>将数据集作为输入并输出新的派生数据集</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自我参考</li>
                    <li><code class=" language-undefined">configProperties</code>:配置属性映射</li>
                    <li><code class=" language-undefined">dataset</code>:转换的输入数据集</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

下表描述了Spark数据集转换器类的抽象方法：

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

## FeaturePipelineFactory

FeaturePipelineFactory类包含特征提取算法，并定义从开始到完成的特征管道的阶段。

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
                <p><i>摘要</i><br/><code class=" language-undefined">create_pipeline(self, configProperties)</code></p>
                <p>创建并返回包含一系列Spark Transporters的Spark管道</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自我参考</li>
                    <li><code class=" language-undefined">configProperties</code>:配置属性映射</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>摘要</i><br/><code class=" language-undefined">get_param_map(self, configProperties, sparkSession)</code></p>
                <p>从配置属性检索和返回参数映射</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自我参考</li>
                    <li><code class=" language-undefined">configProperties</code>:配置属性</li>
                    <li><code class=" language-undefined">sparkSession</code>:Spark会话</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

下表描述了Spark FeaturePipelineFactory的类方法：

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
                <p><i>摘要</i><br/><code class=" language-undefined">createPipeline(configProperties)</code></p>
                <p>创建并返回包含一系列变压器的管线</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:配置属性映射</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>摘要</i><br/><code class=" language-undefined">getParamMap(configProperties, sparkSession)</code></p>
                <p>从配置属性检索和返回参数映射</p>
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

## PipelineFactory

PipelineFactory类封装了模型培训和评分的方法和定义，其中培训逻辑和算法以Spark Pipeline的形式进行定义。

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
                <p><i>摘要</i><br/><code class=" language-undefined">apply(self, configProperties)</code></p>
                <p>创建并返回Spark Pipeline，其中包含用于模型培训和评分的逻辑和算法</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自我参考</li>
                    <li><code class=" language-undefined">configProperties</code>:配置属性</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>摘要</i><br/><code class=" language-undefined">train(self, configProperties, dataframe)</code></p>
                <p>返回包含训练模型的逻辑和算法的自定义管道。 如果使用Spark管道，则不需要此方法</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自我参考</li>
                    <li><code class=" language-undefined">configProperties</code>:配置属性</li>
                    <li><code class=" language-undefined">dataframe</code>:用于培训输入的功能数据集</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>摘要</i><br/><code class=" language-undefined">score(self, configProperties, dataframe, model)</code></p>
                <p>使用经过培训的模型进行评分并返回结果</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自我参考</li>
                    <li><code class=" language-undefined">configProperties</code>:配置属性</li>
                    <li><code class=" language-undefined">dataframe</code>:用于评分的输入数据集</li>
                    <li><code class=" language-undefined">model</code>:用于评分的训练模型</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>摘要</i><br/><code class=" language-undefined">get_param_map(self, configProperties, sparkSession)</code></p>
                <p>从配置属性检索和返回参数映射</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自我参考</li>
                    <li><code class=" language-undefined">configProperties</code>:配置属性</li>
                    <li><code class=" language-undefined">sparkSession</code>:Spark会话</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

下表描述了Spark PipelineFactory的类方法：

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
                <p><i>摘要</i><br/><code class=" language-undefined">apply(configProperties)</code></p>
                <p>创建并返回一个管道，其中包含用于模型培训和评分的逻辑和算法</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:配置属性</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>摘要</i><br/><code class=" language-undefined">getParamMap(configProperties, sparkSession)</code></p>
                <p>从配置属性检索和返回参数映射</p>
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

## MLE值器

MLEvaluator类提供了用于定义评估度量和确定培训和测试数据集的方法。

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
                <p><i>摘要</i><br/><code class=" language-undefined">split(self, configProperties, dataframe)</code></p>
                <p>将输入数据集拆分为培训和测试子集</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自我参考</li>
                    <li><code class=" language-undefined">configProperties</code>:配置属性</li>
                    <li><code class=" language-undefined">dataframe</code>:要拆分的输入数据集</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>摘要</i><br/><code class=" language-undefined">evaluate(self, dataframe, model, configProperties)</code></p>
                <p>评估经过培训的模型并返回评估结果</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>:自我参考</li>
                    <li><code class=" language-undefined">dataframe</code>:由培训和测试数据组成的DataFrame</li>
                    <li><code class=" language-undefined">model</code>:经过训练的模型</li>
                    <li><code class=" language-undefined">configProperties</code>:配置属性</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

下表描述了Spark MLvalueator的类方法：

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
                <p><i>摘要</i><br/><code class=" language-undefined">split(configProperties, data)</code></p>
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
                <p><i>摘要</i><br/><code class=" language-undefined">evaluate(configProperties, model, data)</code></p>
                <p>评估经过培训的模型并返回评估结果</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>:配置属性</li>
                    <li><code class=" language-undefined">model</code>:经过训练的模型</li>
                    <li><code class=" language-undefined">data</code>:由培训和测试数据组成的DataFrame</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>