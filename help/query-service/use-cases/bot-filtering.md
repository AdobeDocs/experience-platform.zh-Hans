---
title: 使用机器学习的查询服务中的机器人筛选
description: 本文档概述如何使用查询服务和机器学习确定机器人活动，并根据真正的在线网站访客流量过滤其操作。
exl-id: fc9dbc5c-874a-41a9-9b60-c926f3fd6e76
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 5%

---

# 使用机器学习在[!DNL Query Service]中过滤机器人

机器人活动可能会影响分析指标并破坏数据完整性。 Adobe Experience Platform [!DNL Query Service]可用于通过机器人过滤过程保持您的数据质量。

机器人过滤允许您通过广泛消除因与网站的非人为交互而造成的数据污染来保持数据质量。 此过程通过SQL查询和机器学习的组合来实现。

可以通过多种方式识别机器人活动。 本文档中采取的方法侧重于活动峰值，在此例中，是指用户在给定时间段内采取的操作数量。 最初，SQL查询会任意设置一段时间内采取的操作数阈值，以符合机器人活动的条件。 然后，使用机器学习模型动态地细化该阈值以提高这些比率的准确性。

本文档提供了在环境中设置进程所必需的SQL机器人过滤查询和机器学习模型的概述和详细示例。

## 快速入门

作为此过程的一部分，您需要培训机器学习模型，本文档假定您掌握一个或多个机器学习环境的工作知识。

此示例使用[!DNL Jupyter Notebook]作为开发环境。 虽然有许多可用选项，但建议使用[!DNL Jupyter Notebook]，因为它是开源Web应用程序，计算要求较低。 可从官方网站[&#128279;](https://jupyter.org/)下载。

## 使用[!DNL Query Service]定义机器人活动的阈值

用于提取数据以进行机器人检测的两个属性是：

* Experience Cloud访客ID （ECID，也称为MCID）：这个通用的永久性ID可以在所有Adobe解决方案中标识您的访客。
* 时间戳：当网站上发生活动时，以UTC格式提供时间和日期。

>[!NOTE]
>
>在对Experience Cloud访客ID的命名空间引用中仍然可以找到`mcid`的使用，如下例所示。

以下SQL语句提供了用于标识机器人活动的初始示例。 该语句假定，如果访客在一分钟内执行50次点击，则用户是机器人。

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

表达式筛选满足阈值但不处理其他间隔中流量激增的所有访客的ECID (`mcid`)。

## 使用机器学习改进机器人检测

初始SQL语句可以细化，成为机器学习的特征提取查询。 改进的查询应该可以在各种间隔产生更多特征，用于训练高准确率的机器学习模型。

此示例语句从单击计数为300和1800的1分钟扩展到60分钟，包括5分钟和30分钟周期。

示例语句收集各持续时间每个ECID (`mcid`)的最大点击次数。 初始语句已扩展为包括1分钟（60秒）、 5分钟（300秒）和1小时（1800秒）周期。

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

## 使用机器学习识别新的尖峰阈值

接下来，将生成的查询数据集导出为CSV格式，然后将其导入到[!DNL Jupyter Notebook]中。 在该环境中，您可以使用当前的机器学习库来训练机器学习模型。 有关[如何以CSV格式从 [!DNL Query Service] 导出数据的更多详细信息，请参阅故障排除指南](../troubleshooting-guide.md#export-csv)

最初建立的临时尖峰阈值不是数据驱动的，因此缺乏准确性。 机器学习模型可用来训练参数作为阈值。 因此，您可以通过删除不需要的功能来减少`GROUP BY`关键字的数量，从而提高查询效率。

此示例使用默认随[!DNL Jupyter Notebook]安装的Scikit-Learn机器学习库。 此外，还将导入“pandas”Python库以在此处使用。 以下命令已输入到[!DNL Jupyter Notebook]中。

```shell
import pandas as ps

df = pd_read.csv('data/bot.csv')
df = df[df['count_1-min'] > 1]
df['is_bot'] = 0
df.loc[df['count_1_min'] > 50,'is_bot'] = 1
df
```

接下来，必须在数据集上训练决策树分类器，并观察模型产生的逻辑。

“Matplotlib”库用于可视化以下示例中的决策树分类器。

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

此示例从[!DNL Jupyter Notebook]返回的值如下。

```text
Model Accuracy: 0.99935
```

![来自[!DNL Jupyter Notebook]机器学习模型的统计输出。](../images/use-cases/jupiter-notebook-output.png)

上述算例的计算结果准确率达到99%以上。

由于决策树分类器可以使用来自[!DNL Query Service]的数据定期使用计划的查询进行训练，因此可以通过高准确度地筛选机器人活动来确保数据完整性。 利用机器学习模型得到的参数，利用模型所创建的高精度参数更新原始查询。

此示例模型非常准确地确定，在5分钟内交互超过130次的任何访客都是机器人。 此信息现在可用于优化机器人筛选SQL查询。

## 后续步骤

通过阅读本文档，您可以更好地了解如何使用[!DNL Query Service]和机器学习来确定和过滤机器人活动。

显示[!DNL Query Service]对贵组织的战略业务洞察有益的其他文档是[放弃的浏览用例](./abandoned-browse.md)示例。
