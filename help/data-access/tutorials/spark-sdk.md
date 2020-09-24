---
keywords: Experience Platform;home;popular topics;data access;spark sdk;data access api
solution: Experience Platform
title: 安全Spark数据访问SDK
topic: tutorial
type: Tutorial
description: Secure Spark Data Access SDK是一个软件开发工具包，可以读取和写入来自Adobe Experience Platform的数据集。
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---


# 安全 [!DNL Spark Data Access] SDK

Secure SDK [!DNL Spark] 是一 [!DNL Data Access] 个软件开发工具包，它支持读取和写入来自Adobe Experience Platform的数据集。

## 入门指南

您必须已完成身份 [验证](../../tutorials/authentication.md) 教程，才能访问这些值以调用安全 [!DNL Spark][!DNL Data Access] SDK:

- `{ACCESS_TOKEN}`
- `{API_KEY}`
- `{IMS_ORG}`

中的所有资源 [!DNL Experience Platform] 都与特定虚拟沙箱隔离。 使用 [!DNL Spark] SDK需要操作将在以下位置进行的沙箱的名称和ID:

- `{SANDBOX_NAME}`
- `{SANDBOX_ID}`

有关中沙箱的详细信 [!DNL Platform]息，请参阅 [沙箱概述文档](../../sandboxes/home.md)。

## 环境设置

SDK [!DNL Spark] 希望您在环境变量或数据源选项中提供凭据。

| Variable | 值 |
| -------- | ----- | 
| `SERVICE_TOKEN` | 您的服务授权令牌。 |
| `SERVICE_API_KEY` | 您的服务API密钥。 这通常与您的IMS客户端ID相同。 |
| `ORG_ID` | 您的 `{IMS_ORG}` ID值。 |
| `USER_TOKEN` | 您的 `{ACCESS_TOKEN}` 价值。 |

其他配置参数包括：

| Variable | 值 |
| -------- | ----- |
| `ENVIRONMENT_NAME` | 您尝试连接的环境。 它可以是“dev”、“stage”或“prod”。 |
| `SANDBOX_NAME` | 要连接的沙箱的名称。 |

或者，除了 `ENVIRONMENT_NAME`以外，您还可以在中设置以上任 `QSOption`何环境变量，如下例所示：

```scala
val df = spark.read
    .format("com.adobe.platform.query")
    .option(QSOption.userToken, userToken) // same as env var USER_TOKEN
    .option(QSOption.imsOrg, "69A7534C5808063C0A494234@AdobeOrg") // same as env var ORG_ID
    .option(QSOption.apiKey, "acp_foundation_queryService") // same as env var SERVICE_API_KEY
    .option("mode", "interactive")
    .option("query", "SELECT * FROM csv10000row_xcm_001 LIMIT 10")
    .load()
```

## 安装

使用 [!DNL Spark] SDK需要将性能优化添加到 `SparkSession`。 您可以使用以下方法之一应用它们：

将其直接应用于当前SparkSession:

```scala
import com.adobe.platform.query.QSOptimizations
QSOptimizations.apply(spark)
```

在创建SparkSession之前或创建时设置以下会议：

```scala
spark.sql.extensions = com.adobe.platform.query.QSSparkSessionExtensions
```

## 读取数据集

SDK [!DNL Spark] 支持两种阅读模式：交互式和批处理。

交互模式创建与的Java数据库连接(JDBC) [!DNL Query Service] 连接，并通过自动转换为的常规 `ResultSet` JDBC获取结果 `DataFrame`。 此模式的工作方式与内置方 [!DNL Spark] 法类似 `spark.read.jdbc()`。 此模式仅适用于小数据集，并且仅需要用户令牌进行身份验证。

批处理模 [!DNL Query Service]式使用的COPY命令在共享位置生成Parce结果集。 然后，可以进一步处理这些Parke文件。 此模式需要用户令牌和具有该范围的服务 `acp.foundation.catalog.credentials` 令牌。

在交互模式下读取数据集的示例如下所示：

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("ims-org", {IMS_ORG})
      .option("api-key", {SERVICE_API_KEY})
      .option("mode", "interactive")
      .option("dataset-id", {DATASET_ID})
      .option("sandbox-name", {SANDBOX_NAME})
      .load()
df.show()
```

同样，在批处理模式下读取数据集的示例如下所示：

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("service-token", {SERVICE_TOKEN})
      .option("ims-org", {IMS_ORG})
      .option("api-key", {SERVICE_API_KEY})
      .option("mode", "batch")
      .option("dataset-id", {DATASET_ID})
      .option("sandbox-name", {SANDBOX_NAME})
      .load()
df.show()
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

LIMIT子句允许用户限制从数据集接收的记录数。

使用函数的示 `limit()` 例如下所示：

```scala
df = df.limit(100)
```

## 写入数据集

SDK支 [!DNL Spark] 持编写数据集。 用户首先需要检索以前的数据集才能写入新数据集。

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", userToken)
      .option("ims-org", "{IMS_ORG}")
      .option("api-key", "{API_KEY}")
      .option("mode", "interactive")
      .option("dataset-id", "{DATASET_ID}")
      .load()

    df.write
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("service-token", {SERVICE_TOKEN})
      .option("ims-org", "{IMS_ORG_ID})
      .option("api-key", "{API_KEY}")
      .option("create-dataset", "{DATASET_ID}")
      .save()
```
