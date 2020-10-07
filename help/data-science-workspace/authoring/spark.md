---
keywords: Experience Platform;home;popular topics;data access;spark sdk;data access api;spark recipe;read spark;write spark
solution: Experience Platform
title: 使用Spark访问数据
topic: tutorial
type: Tutorial
description: 以下文档包含有关如何使用Spark访问数据以用于数据科学工作区的示例。
translation-type: tm+mt
source-git-commit: fcb4088ecac76d10b0cb69b04ad55167f5cdac3e
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---


# 使用Spark访问数据

以下文档包含有关如何使用Spark访问数据以用于数据科学工作区的示例。 有关使用JupyterLab笔记本访问数据的信息，请访 [问JupyterLab笔记本数据访问](../jupyterlab/access-notebook-data.md) 文档。

## 入门指南

使 [!DNL Spark] 用要求性能优化，需要将其添加到 `SparkSession`。 此外，您还可以设置 `configProperties` 以后对数据集进行读写。

```scala
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.query.QSOption
import org.apache.spark.sql.{DataFrame, SparkSession}

Class Helper {

 /**
   *
   * @param configProperties - Configuration Properties map
   * @param sparkSession     - SparkSession
   * @return                 - DataFrame which is loaded for training
   */

   def load_dataset(configProperties: ConfigProperties, sparkSession: SparkSession, taskId: String): DataFrame = {
            // Read the configs
            val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
            val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
            val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
            val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
            val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

   }
}
```

## 读取数据集

使用Spark时，您可以访问两种阅读模式：交互式和批处理。

交互模式创建与的Java数据库连接(JDBC) [!DNL Query Service] 连接，并通过自动转换为的常规 `ResultSet` JDBC获取结果 `DataFrame`。 此模式的工作方式与内置方 [!DNL Spark] 法类似 `spark.read.jdbc()`。 此模式仅适用于小数据集。 如果数据集超过500万行，建议您换用批处理模式。

批处理模 [!DNL Query Service]式使用的COPY命令在共享位置生成Parce结果集。 然后，可以进一步处理这些Parke文件。

在交互模式下读取数据集的示例如下所示：

```scala
  // Read the configs
    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

 val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, "interactive")
      .option(QSOption.datasetId, dataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .load()
    df.show()
    df
  }
```

同样，在批处理模式下读取数据集的示例如下所示：

```scala
val df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, "batch")
      .option(QSOption.datasetId, dataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .load()
    df.show()
    df
```

### 数据集中的SELECT列

```scala
df = df.select("column-a", "column-b").show()
```

### DISTINCT子句

DISTINCT子句允许您在行／列级别提取所有不同值，从响应中删除所有重复值。

使用函数的示 `distinct()` 例如下所示：

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### WHERE子句

SDK [!DNL Spark] 允许两种筛选方法：使用SQL表达式或通过筛选条件。

使用这些过滤函数的示例如下所示：

#### SQL表达式

```scala
df.where("age > 15")
```

#### 筛选条件

```scala
df.where("age" > 15 || "name" = "Steve")
```

### ORDER BY子句

ORDER BY子句允许按指定列按特定顺序（升序或降序）对接收结果进行排序。 在SDK [!DNL Spark] 中，这是使用函数完 `sort()` 成的。

使用函数的示 `sort()` 例如下所示：

```scala
df = df.sort($"column1", $"column2".desc)
```

### LIMIT子句

LIMIT子句允许您限制从数据集接收的记录数。

使用函数的示 `limit()` 例如下所示：

```scala
df = df.limit(100)
```

## 写入数据集

使用映 `configProperties` 射，您可以使用在Experience Platform中写入数据集 `QSOption`。

```scala
val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString 

    df.write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .save()
```


## 后续步骤

Adobe Experience Platform数据科学工作区提供Scala(Spark)菜谱样本，它使用上述代码样本来读取和写入数据。 如果您想进一步了解如何使用Spark访问数据，请查阅数据科学工 [作区缩放GitHub存储库](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala)。