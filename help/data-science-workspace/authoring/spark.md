---
keywords: Experience Platform；首頁；熱門主題；資料存取；spark sdk；資料存取api；spark配方；讀取spark；寫入spark
solution: Experience Platform
title: 在資料科學工作區中使用Spark存取資料
type: Tutorial
description: 以下檔案包含如何使用Spark存取資料以用於資料科學工作區的範例。
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# 在資料科學工作區中使用Spark存取資料

以下檔案包含如何使用Spark存取資料以用於資料科學工作區的範例。 如需使用JupyterLab筆記型電腦存取資料的詳細資訊，請造訪 [JupyterLab Notebooks資料存取](../jupyterlab/access-notebook-data.md) 說明檔案。

## 快速入门

使用 [!DNL Spark] 需要效能最佳化，這些需要新增至 `SparkSession`. 此外，您也可以設定 `configProperties` 以稍後讀取及寫入資料集。

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

## 讀取資料集

使用Spark時，您可以存取兩種讀取模式：互動式和批次。

互動模式會建立Java Database Connectivity (JDBC)連線至 [!DNL Query Service] 和會透過一般JDBC取得結果 `ResultSet` 會自動轉譯為 `DataFrame`. 此模式的運作方式與內建類似 [!DNL Spark] 方法 `spark.read.jdbc()`. 此模式僅適用於小型資料集。 如果您的資料集超過500萬列，建議您切換至批次模式。

批次模式使用 [!DNL Query Service]在共用位置產生Parquet結果集的COPY指令。 然後可以進一步處理這些Parquet檔案。

在互動模式下讀取資料集的範例如下所示：

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

同樣地，在批次模式下讀取資料集的範例如下所示：

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

### 從資料集中選取欄

```scala
df = df.select("column-a", "column-b").show()
```

### DISTINCT子句

DISTINCT子句可讓您擷取列/欄層級的所有相異值，從回應中移除所有重複值。

使用 `distinct()` 函式如下所示：

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### WHERE子句

此 [!DNL Spark] SDK允許兩種篩選方法：使用SQL運算式或透過條件篩選。

以下提供使用這些篩選函式的範例：

#### SQL運算式

```scala
df.where("age > 15")
```

#### 篩選條件

```scala
df.where("age" > 15 || "name" = "Steve")
```

### ORDER BY子句

ORDER BY子句允許接收的結果以特定順序（升序或降序）依指定資料行排序。 在 [!DNL Spark] SDK可透過使用 `sort()` 函式。

使用 `sort()` 函式如下所示：

```scala
df = df.sort($"column1", $"column2".desc)
```

### LIMIT子句

LIMIT子句可讓您限制從資料集接收的記錄數。

使用 `limit()` 函式如下所示：

```scala
df = df.limit(100)
```

## 寫入資料集

使用您的 `configProperties` 對應，您可以使用將資料寫入Experience Platform的資料集 `QSOption`.

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

Adobe Experience Platform Data Science Workspace提供Scala (Spark)配方範例，此範例使用上述程式碼範例來讀取和寫入資料。 如果您想進一步瞭解如何使用Spark存取您的資料，請檢閱 [資料科學工作區Scala GitHub存放庫](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala).
