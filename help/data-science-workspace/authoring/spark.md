---
keywords: Experience Platform；主页；热门主题；数据访问；Spark SDK；数据访问API;Spark方法；读取Spark；写入Spark
solution: Experience Platform
title: 在数据科学工作区中使用Spark访问数据
type: Tutorial
description: 以下文档包含如何使用Spark访问数据以在数据科学工作区中使用的示例。
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# 在数据科学工作区中使用Spark访问数据

以下文档包含如何使用Spark访问数据以在数据科学工作区中使用的示例。 有关使用JupyterLab笔记本访问数据的信息，请访问 [JupyterLab笔记本电脑数据访问](../jupyterlab/access-notebook-data.md) 文档。

## 快速入门

使用 [!DNL Spark] 需要优化需要添加到 `SparkSession`. 此外，您还可以设置 `configProperties` 以后读取和写入数据集。

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

使用Spark时，您可以使用两种阅读模式：交互式和批量处理。

交互模式会创建到的Java数据库连接(JDBC)连接 [!DNL Query Service] 并通过常规JDBC获取结果 `ResultSet` 自动翻译成 `DataFrame`. 此模式的工作方式与内置模式类似 [!DNL Spark] 方法 `spark.read.jdbc()`. 此模式仅适用于小数据集。 如果您的数据集超过500万行，则建议您交换到批处理模式。

批处理模式使用 [!DNL Query Service]用于在共享位置中生成Parquet结果集的COPY命令。 然后，可进一步处理这些Parquet文件。

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

同样，下面显示了在批量模式下读取数据集的示例：

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

DISTINCT子句允许您在行/列级别获取所有不同值，从响应中删除所有重复值。

使用的示例 `distinct()` 函数如下所示：

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### WHERE子句

的 [!DNL Spark] SDK允许使用两种方法进行筛选：使用SQL表达式或通过条件进行筛选。

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

ORDER BY子句允许接收的结果按指定的列按特定顺序（升序或降序）排序。 在 [!DNL Spark] SDK，这是使用 `sort()` 函数。

使用的示例 `sort()` 函数如下所示：

```scala
df = df.sort($"column1", $"column2".desc)
```

### LIMIT子句

LIMIT子句用于限制从数据集接收的记录数。

使用的示例 `limit()` 函数如下所示：

```scala
df = df.limit(100)
```

## 写入数据集

使用 `configProperties` 映射时，您可以使用 `QSOption`.

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

Adobe Experience Platform Data Science Workspace提供了Scala(Spark)方法示例，该示例使用上述代码示例来读取和写入数据。 如果您想进一步了解如何使用Spark访问数据，请查看 [数据科学工作区可缩放GitHub存储库](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala).
