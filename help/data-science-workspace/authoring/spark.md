---
keywords: Experience Platform；主页；热门主题；数据访问；spark sdk；数据访问api；spark方法；读取spark；写入spark
solution: Experience Platform
title: 在数据科学Workspace中使用Spark访问数据
type: Tutorial
description: 以下文档包含有关如何使用Spark访问数据以用于数据科学Workspace的示例。
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# 在数据科学Workspace中使用Spark访问数据

以下文档包含有关如何使用Spark访问数据以用于数据科学Workspace的示例。 有关使用JupyterLab笔记本访问数据的信息，请访问[JupyterLab笔记本数据访问](../jupyterlab/access-notebook-data.md)文档。

## 开始使用

使用[!DNL Spark]需要优化性能，这些优化需要添加到`SparkSession`中。 此外，您还可以设置`configProperties`以便以后读取和写入数据集。

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
            val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
            val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
            val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
            val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

   }
}
```

## 读取数据集

使用Spark时，您可以访问两种读取模式：交互模式和批处理模式。

交互模式创建到[!DNL Query Service]的Java数据库连接(JDBC)连接，并通过自动转换为`DataFrame`的常规JDBC `ResultSet`获取结果。 此模式的工作方式与内置[!DNL Spark]方法`spark.read.jdbc()`类似。 此模式仅适用于小型数据集。 如果您的数据集超过500万行，建议切换到批处理模式。

批处理模式使用[!DNL Query Service]的COPY命令在共享位置生成Parquet结果集。 然后可以进一步处理这些Parquet文件。

在交互模式下读取数据集的示例如下所示：

```scala
  // Read the configs
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

 val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
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

同样，下面显示了以批处理模式读取数据集的示例：

```scala
val df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, "batch")
      .option(QSOption.datasetId, dataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .load()
    df.show()
    df
```

### 从数据集中选择列

```scala
df = df.select("column-a", "column-b").show()
```

### DISTINCT子句

DISTINCT子句允许您在行/列级别获取所有不同的值，从响应中删除所有重复值。

下面显示了使用`distinct()`函数的示例：

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### WHERE子句

[!DNL Spark] SDK允许使用两种过滤方法：使用SQL表达式或通过条件过滤。

下面显示了使用这些筛选函数的示例：

#### SQL表达式

```scala
df.where("age > 15")
```

#### 过滤条件

```scala
df.where("age" > 15 || "name" = "Steve")
```

### ORDER BY子句

ORDER BY子句允许按指定列以特定顺序（升序或降序）对接收结果进行排序。 在[!DNL Spark] SDK中，可使用`sort()`函数完成此操作。

下面显示了使用`sort()`函数的示例：

```scala
df = df.sort($"column1", $"column2".desc)
```

### LIMIT子句

LIMIT子句允许您限制从数据集接收的记录数。

下面显示了使用`limit()`函数的示例：

```scala
df = df.limit(100)
```

## 写入数据集

使用您的`configProperties`映射，您可以使用`QSOption`写入Experience Platform中的数据集。

```scala
val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString 

    df.write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .save()
```


## 后续步骤

Adobe Experience Platform数据科学Workspace提供了一个Scala (Spark)方法示例，该示例使用上述代码示例读取和写入数据。 如果您想了解有关如何使用Spark访问您的数据的更多信息，请查看[数据科学Workspace Scala GitHub存储库](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala)。
