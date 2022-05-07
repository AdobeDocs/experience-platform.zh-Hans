---
title: 基于机器学习的查询服务机器人过滤
description: 本文档概述了如何使用查询服务和机器学习来确定机器人活动，并从真正的在线网站访客流量中过滤其操作。
source-git-commit: 7b223b4917e6bdb3f4a05238cbaf66261d80660e
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 5%

---

# 机器人过滤 [!DNL Query Service] 与机器学习

机器人活动可能会影响分析量度并损害数据完整性。 Adobe Experience Platform [!DNL Query Service] 可用于通过机器人过滤过程维护数据质量。

机器人过滤功能允许您通过广泛删除与网站进行非人类交互而导致的数据污染，从而保持数据质量。 此过程是通过SQL查询与机器学习相结合来实现的。

机器人活动可通过多种方式进行识别。 本文档中采用的方法重点介绍活动峰值，在本例中，用户在给定时间段内执行的操作数。 最初， SQL查询会任意设置一段时间内执行的操作数量的阈值，以便确定为机器人活动。 然后，使用机器学习模型动态地细化该阈值以提高这些比率的准确性。

本文档提供了SQL机器人过滤查询以及在环境中设置该过程所必需的机器学习模型的概述和详细示例。

## 快速入门

在此过程中，需要您培训机器学习模型，本文档假定您了解一个或多个机器学习环境的工作知识。

此示例使用 [!DNL Jupyter Notebook] 作为开发环境。 尽管有许多可用选项， [!DNL Jupyter Notebook] 推荐使用，因为它是一个计算要求较低的开源web应用程序。 它可以是 [从官方网站下载](https://jupyter.org/).

## 使用 [!DNL Query Service] 为机器人活动定义阈值

用于提取机器人检测数据的两个属性是：

* Marketing CloudID(MCID):这提供了一个通用的永久性ID，用于在所有Adobe解决方案中标识您的访客。
* 时间戳：网站上发生活动时，将以UTC格式提供日期和时间。

以下SQL语句提供了一个用于标识机器人活动的初始示例。 该语句假定，如果访客在一分钟内执行了50次点击，则用户是机器人。

```sql
SELECT * 
FROM   <YOUR_TABLE_NAME> 
WHERE  enduserids._experience.mcid NOT IN (SELECT enduserids._experience.mcid 
                                           FROM   <YOUR_TABLE_NAME> 
                                           GROUP  BY Unix_timestamp(timestamp) / 
                                                     60, 
                                                     enduserids._experience.mcid 
                                           HAVING Count(*) > 50);  
```

表达式会过滤所有符合阈值但未解决其他间隔流量峰值的访客的MCID。

## 利用机器学习改进机器人检测

可以对初始SQL语句进行细化，使其成为机器学习的特征提取查询。 改进的查询应该为各种间隔提供更多功能，以便训练具有较高准确度的机器学习模型。

示例语句从1分钟（最多60次点击）扩展为包含5分钟和30分钟时段（点击计数分别为300和1800）。

示例语句收集各个持续时间内每个MCID的最大点击次数。 初始语句已扩展为包括1分钟（60秒）、5分钟（300秒）和1小时（即1800秒）时段。

```sql
SELECT table_count_1_min.mcid AS id, 
       count_1_min, 
       count_5_mins, 
       count_30_mins 
FROM   ( ( (SELECT mcid, 
                 Max(count_1_min) AS count_1_min 
          FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                         Count(*)                       AS count_1_min 
                  FROM 
       <YOUR_TABLE_NAME> 
                  GROUP  BY Unix_timestamp(timestamp) / 60, 
                            enduserids._experience.mcid.id) 
          GROUP BY mcid) AS table_count_1_min 
           LEFT JOIN (SELECT mcid, 
                             Max(count_5_mins) AS count_5_mins 
                      FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                                     Count(*)                       AS 
                                     count_5_mins 
                              FROM 
           <YOUR_TABLE_NAME> 
                              GROUP  BY Unix_timestamp(timestamp) / 300, 
                                        enduserids._experience.mcid.id) 
                      GROUP  BY mcid) AS table_count_5_mins 
                  ON table_count_1_min.mcid = table_count_5_mins.mcid ) 
         LEFT JOIN (SELECT mcid, 
                           Max(count_30_mins) AS count_30_mins 
                    FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                                   Count(*)                       AS 
                                   count_30_mins 
                            FROM 
         <YOUR_TABLE_NAME> 
                            GROUP  BY Unix_timestamp(timestamp) / 1800, 
                                      enduserids._experience.mcid.id) 
                    GROUP  BY mcid) AS table_count_30_mins 
                ON table_count_1_min.mcid = table_count_30_mins.mcid ) 
```

此表达式的结果可能与下面提供的表类似。

| `id` | `count_1_min` | `count_5_min` | `count_30_min` |
|---|---|---|---|
| 4833075303848917832 | 1 | 1 | 1 |
| 1469109497068938520 | 1 | 1 | 1 |
| 5045682519445554093 | 1 | 1 | 1 |
| 7148203816406620066 | 3 | 3 | 3 |
| 1013065429311352386 | 1 | 1 | 1 |
| 3077475871984695013 | 7 | 7 | 7 |
| 4151486040344674930 | 2 | 2 | 2 |
| 6563366098591762751 | 6 | 6 | 6 |
| 2403566105776993627 | 4 | 4 | 4 |
| 5710530640819698543 | 1 | 1 | 1 |
| 3675089655839425960 | 1 | 1 | 1 |
| 9091930660723241307 | 1 | 1 | 1 |

## 使用机器学习确定新的尖峰阈值

接下来，将生成的查询数据集导出为CSV格式，然后将其导入 [!DNL Jupyter Notebook]. 从该环境中，您可以使用当前的机器学习库来培训机器学习模型。 有关 [如何从 [!DNL Query Service] 格式](../troubleshooting-guide.md#export-csv)

最初建立的临时尖峰阈值不是数据驱动的，因此缺乏准确性。 机器学习模型可用于训练参数作为阈值。 因此，您可以通过减少 `GROUP BY` 关键词。

此示例使用Scikit-Learn机器学习库，默认情况下，该库随 [!DNL Jupyter Notebook]. “熊猫”蟒蛇库也在这里进口使用。 以下命令将输入到 [!DNL Jupyter Notebook].

```shell
import pandas as ps

df = pd_read.csv('data/bot.csv')
df = df[df['count_1-min'] > 1]
df['is_bot'] = 0
df.loc[df['count_1_min'] > 50,'is_bot'] = 1
df
```

接下来，您必须在数据集上培训决策树分类器，并观察由模型生成的逻辑。

在以下示例中，“Matplotlib”库用于显示决策树分类器。

```shell
from sklearn.tree import DecisionTreeClassifier
from sklearn import tree
from matplotlib import pyplot as plt

X = df.iloc[:,:[1,3]]
y = df.iloc[:,-1]

clf = DecisionTreeClassifier(max_leaf_nodes=2, random_state=0)
clf.fit(X,y)

print("Model Accuracy: {:.5f}".format(clf.scre(X,y)))

tree.plot_tree(clf,feature_names=X.columns)
plt.show()
```

从 [!DNL Jupyter Notebook] 对于此示例，如下所示。

```text
Model Accuracy: 0.99935
```

![来自 [!DNL Jupyter Notebook] 机器学习模型。](../images/use-cases/jupiter-notebook-output.png)

以上示例所示模型的结果准确率超过99%。

由于决策树分类器可以使用来自 [!DNL Query Service] 在使用计划查询的常规频率下，您可以通过高准确度过滤机器人活动来确保数据完整性。 通过使用从机器学习模型派生的参数，可以使用由模型创建的高精度参数来更新原始查询。

该示例模型非常准确地确定，在五分钟内进行交互超过130次的任何访客都是机器人。 此信息现在可用于优化机器人过滤SQL查询。

## 后续步骤

通过阅读本文档，您可以更好地了解如何使用查询服务和机器学习来确定和筛选机器人活动。

其他文档，这些文档说明了 [!DNL Query Service] 放弃的浏览用例示例是贵组织的战略业务分析。
