---
title: 使用机器学习生成的预测模型确定倾向得分
description: 了解如何使用查询服务将您的预测模型应用到Platform数据。 本文档演示如何使用Platform数据预测客户每次访问时的购买倾向。
exl-id: 29587541-50dd-405c-bc18-17947b8a5942
source-git-commit: 40c27a52fdae2c7d38c5e244a6d1d6ae3f80f496
workflow-type: tm+mt
source-wordcount: '1295'
ht-degree: 0%

---

# 使用机器学习生成的预测模型确定倾向得分

使用查询服务，您可以利用在机器学习平台上构建的预测模型（如倾向得分）来分析Experience Platform数据。

本指南介绍如何使用查询服务将数据发送到机器学习平台，以便在计算笔记本中培训模型。 训练好的模型可以应用于使用SQL的数据，以预测客户每次访问的购买倾向。

## 快速入门

在此过程中，需要您培训机器学习模型，本文档假定您了解一个或多个机器学习环境的工作知识。

此示例使用 [!DNL Jupyter Notebook] 作为开发环境。 尽管有许多可用选项， [!DNL Jupyter Notebook] 推荐使用，因为它是一个计算要求较低的开源web应用程序。 它可以是 [从官方网站下载](https://jupyter.org/).

如果尚未执行此操作，请按照 [connect [!DNL Jupyter Notebook] 使用Adobe Experience Platform查询服务](../clients/jupyter-notebook.md) ，然后再继续阅读本指南。

此示例中使用的库包括：

```console
python=3.6.7
psycopg2
sklearn
pandas
matplotlib
numpy
tqdm
```

## 将Analytics表从Platform导入到 [!DNL Jupyter Notebook] {#import-analytics-tables}

要生成倾向得分模型，必须将存储在Platform中的分析数据的投影导入 [!DNL Jupyter Notebook]. 从 [!DNL Python] 3 [!DNL Jupyter Notebook] 以下命令连接到查询服务，会从Luma（一个虚构的服装商店）导入客户行为数据集。 由于Platform数据是使用Experience Data Model(XDM)格式存储的，因此必须生成一个符合架构结构的示例JSON对象。 有关如何 [生成示例JSON对象](../../xdm/ui/sample.md).

![的 [!DNL Jupyter Notebook] 高亮显示多个命令的仪表板。](../images/use-cases/jupyter-commands.png)

输出将显示一个表格化视图，其中显示Luma行为数据集(位于 [!DNL Jupyter Notebook] 功能板。

![Luma在 [!DNL Jupyter Notebook].](../images/use-cases/behavioural-dataset-results.png)

## 准备数据以进行机器学习 {#prepare-data-for-machine-learning}

必须识别目标列才能训练机器学习模型。 由于购买倾向是此用例的目标，因此， `analytic_action` 列作为Luma结果中的目标列。 值 `productPurchase` 是客户购买的指标。 的 `purchase_value` 和 `purchase_num` 列也会被删除，因为它们与产品购买操作直接相关。

用于执行这些操作的命令如下所示：

```python
#define the target label for prediction
df['target'] = (df['analytic_action'] == 'productPurchase').astype(int)
#remove columns that are dependent on the label
df.drop(['analytic_action','purchase_value'],axis=1,inplace=True)
```

接下来，必须将Luma数据集中的数据转换为相应的表示形式。 需要两个步骤：

1. 将表示数字的列转换为数字列。 为此，请在 `dataframe`.
1. 也将类别列转换为数值列。

```python
#convert columns that represent numbers
num_cols = ['purchase_num', 'value_cart', 'value_lifetime']
df[num_cols] = df[num_cols].apply(pd.to_numeric, errors='coerce')
```

一种名为 *热编码* 用于转换类别数据变量，以便与机器和深层学习算法结合使用。 这反过来会改进预测以及模型的分类准确性。 使用 `Sklearn` 库来表示单独列中的每个类别值。

```python
from sklearn.preprocessing import OneHotEncoder

#get the categorical columns
cat_columns = list(set(df.columns) - set(num_cols + ['target']))

#get the dataframe with categorical columns only
df_cat = df.loc[:,cat_columns]

#initialize sklearn's OneHotEncoder
enc = OneHotEncoder(handle_unknown='ignore')

#fit the data into the encoder
enc.fit(df_cat)

#define OneHotEncoder's columns names
ohc_columns = [[c+'='+c_ for c_ in cat] for c,cat in zip(cat_columns,enc.categories_)]
ohc_columns = [item for sublist in ohc_columns for item in sublist]

#finalize the data input to the ML models
X = pd.DataFrame( np.concatenate((enc.transform(df_cat).toarray(),df[num_cols]),axis=1),
                 columns =  ohc_columns + num_cols)

#define target column
y = df['target']
```

定义为 `X` 标记为表格，如下所示：

![X在 [!DNL Jupyter Notebook].](../images/use-cases/x-output-table.png)


现在，机器学习所需的数据已经可用，因此可以在 [!DNL Python]&#39;s `sklearn` 库。 [!DNL Logistics Regression] 用于训练倾向模型，并允许您查看测试数据的准确性。 在这种情况下，大约为85%。

的 [!DNL Logistic Regression] 算法和训练测试拆分方法用于评估机器学习算法的性能，在以下代码块中导入：

```python
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42)

clf = LogisticRegression(max_iter=2000, random_state=0).fit(X_train, y_train)

print("Test data accuracy: {}".format(clf.score(X_test, y_test)))
```

测试数据的准确度为0.8518518518518519。

通过使用物流回归，您可以直观地显示购买原因，并按降序排列功能以确定其排名重要性。 第一列表示导致购买行为的较高因果关系。 后一列表示不会导致购买行为的因素。

将结果可视化为两个条形图的代码如下所示：

```python
from matplotlib import pyplot as plt

#get feature importance as a sorted list of columns
feature_importance = np.argsort(-clf.coef_[0])
top_10_features_purchase_names = X.columns[feature_importance[:10]]
top_10_features_purchase_values = clf.coef_[0][feature_importance[:10]]
top_10_features_not_purchase_names = X.columns[feature_importance[-10:]]
top_10_features_not_purchase_values = clf.coef_[0][feature_importance[-10:]]

#plot the figures
fig, (ax1, ax2) = plt.subplots(1, 2,figsize=(10,5))

ax1.bar(np.arange(10),top_10_features_purchase_values)
ax1.set_xticks(np.arange(10))
ax1.set_xticklabels(top_10_features_purchase_names,rotation = 90)
ax1.set_ylim([np.min(clf.coef_[0])-0.1,np.max(clf.coef_[0])+0.1])
ax1.set_title("Top 10 features to define \n a propensity to purchase")

ax2.bar(np.arange(10),top_10_features_not_purchase_values, color='#E15750')
ax2.set_xticks(np.arange(10))
ax2.set_xticklabels(top_10_features_not_purchase_names,rotation = 90)
ax2.set_ylim([np.min(clf.coef_[0])-0.1,np.max(clf.coef_[0])+0.1])
ax2.set_title("Top 10 features to define \n a propensity to NOT purchase")

plt.show()
```

结果的垂直条形图可视化如下所示：

![前10项功能的可视化图表，这些功能定义了购买或不购买的倾向。](../images/use-cases/visualized-results.png)

可以从条形图中识别多个模式。 渠道的销售点(POS)和电话报销主题是决定购买行为的最重要因素。 而作为投诉和发票的呼叫主题对于定义不购买行为具有重要作用。 这些是可量化的可操作洞察，营销人员可以利用这些洞察来开展营销活动，以消除购买这些客户的倾向。

## 使用查询服务来应用培训的模型 {#use-query-service-to-apply-trained-model}

创建培训后的模型后，必须将其应用于保存在Experience Platform中的数据。 要实现此目的，必须将机器学习管道的逻辑转换为SQL。 此过渡的两个关键组件如下：

- 首先，SQL必须代替 [!DNL Logistics Regression] 模块获取预测标签的概率。 物流回归所建立的模型产生了回归模型 `y = wX + c`  权重 `w` 截距 `c` 是模型的输出。 SQL功能可用于乘以权值以获得概率。

- 其次，在工程实际中，在 [!DNL Python] SQL中还必须包含一个热编码。 例如，在原始数据库中，我们 `geo_county` 列来存储县，但该列将转换为 `geo_county=Bexar`, `geo_county=Dallas`, `geo_county=DeKalb`. 以下SQL语句执行相同的转换，其中 `w1`, `w2`和 `w3` 可以用从 [!DNL Python]:

```sql
SELECT  CASE WHEN geo_state = 'Bexar' THEN FLOAT(w1) ELSE 0 END AS f1,
        CASE WHEN geo_state = 'Dallas' THEN FLOAT(w2) ELSE 0 END AS f2,
        CASE WHEN geo_state = 'Bexar' THEN FLOAT(w3) ELSE 0 END AS f3,
```

对于数值功能，可以直接将列与权重相乘，如下面的SQL语句中所示。

```sql
SELECT FLOAT(purchase_num) * FLOAT(w4) AS f4,
```

在获得数值后，可将其移植到一个Sigmoid函数中，Logistics Regresion算法生成最终预测。 在下面的陈述中， `intercept` 是回归中截距的数。
        

```sql
SELECT CASE WHEN 1 / (1 + EXP(- (f1 + f2 + f3 + f4 + FLOAT(intercept)))) > 0.5 THEN 1 ELSE 0 END AS Prediction;
```
 
### 端到端示例

如果您有两列(`c1` 和 `c2`)，如果 `c1` 有两个类别， [!DNL Logistic Regression] 算法通过以下函数进行训练：
 

```python
y = 0.1 * "c1=category 1"+ 0.2 * "c1=category 2" +0.3 * c2+0.4
```
 
SQL中的等效函数如下所示：

```sql
SELECT
  CASE WHEN 1 / (1 + EXP(- (f1 + f2 + f3 + FLOAT(0.4)))) > 0.5 THEN 1 ELSE 0 END AS Prediction
FROM
  (
    SELECT
      CASE WHEN c1 = 'Cateogry 1' THEN FLOAT(0.1) ELSE 0 END AS f1,
      CASE WHEN c1 = 'Cateogry 2' THEN FLOAT(0.2) ELSE 0 END AS f2,
      FLOAT(c2) * FLOAT(0.3) AS f3
    FROM TABLE
  )
```
 
的 [!DNL Python] 自动翻译过程的代码如下所示：

```python
def generate_lr_inference_sql(ohc_columns, num_cols, clf, db):
    features_sql = []
    category_sql_text = "case when {col} = '{val}' then float({coef}) else 0 end as f{name}"
    numerical_sql_text = "float({col}) * float({coef}) as f{name}"
    for i, (column, coef) in enumerate(zip(ohc_columns+num_cols, clf.coef_[0])):
        if i < len(ohc_columns):
            col,val = column.split('=')
            val = val.replace("'","%''%")
            sql = category_sql_text.format(col=col,val=val,coef=coef,name=i+1)
        else:
            sql = numerical_sql_text.format(col=column,coef=coef,name=i+1)
        features_sql.append(sql)
    features_sum = '+'.join(['f{}'.format(i) for i in range(1,len(features_sql)+1)])
    final_sql = '''
    select case when 1/(1 + EXP(-({features} + float({intercept})))) > 0.5 then 1 else 0 end as Prediction
    from
        (select {cols}
        from {db})
    '''.format(features=features_sum,cols=",".join(features_sql),intercept=clf.intercept_[0],db=db)
    return final_sql
```

当使用SQL推断数据库时，输出如下：

```python
sql = generate_lr_inference_sql(ohc_columns, num_cols, clf, "fdu_luma_raw")
cur.execute(sql)    
samples = [r for r in cur]
colnames = [desc[0] for desc in cur.description]
pd.DataFrame(samples,columns=colnames)
```

表格化结果显示了购买每个客户会话的倾向 `0` 表示没有购买倾向和 `1` 即确认的购买倾向。

![使用SQL进行数据库推理的表格化结果。](../images/use-cases/inference-results.png)

## 处理采样数据：引导 {#working-on-sampled-data}

如果本地计算机存储模型培训数据的数据过大，则可以采取样本，而不是查询服务中的完整数据。 要了解从查询服务中采样需要多少数据，可以应用称为引导的技术。 在这方面，引导是指利用各种样本对模型进行多次训练，并检查模型精度在不同样本之间的方差。 为了调整上述倾向模型示例，首先将整个机器学习工作流封装到一个函数中。 代码如下：

```python
def end_to_end_pipeline(df):
    
    #define the target label for prediction
    df['target'] = (df['analytic_action'] == 'productPurchase').astype(int)
    #remove columns that are dependent on the label
    df.drop(['analytic_action','purchase_value'],axis=1,inplace=True)
    
    num_cols = ['purchase_num','value_cart','value_lifetime']
    df[num_cols] = df[num_cols].apply(pd.to_numeric, errors='coerce')
    
    #get the categorical columns
    cat_columns = list(set(df.columns) - set(num_cols + ['target']))

    #get the dataframe with categorical columns only
    df_cat = df.loc[:,cat_columns]

    #initialize sklearn's One Hot Encoder
    enc = OneHotEncoder(handle_unknown='ignore')

    #fit the data into the encoder
    enc.fit(df_cat)

    #define one hot encoder's columns names
    ohc_columns = [[c+'='+c_ for c_ in cat] for c,cat in zip(cat_columns,enc.categories_)]
    ohc_columns = [item for sublist in ohc_columns for item in sublist]

    #finalize the data input to the ML models
    X = pd.DataFrame( np.concatenate((enc.transform(df_cat).toarray(),df[num_cols]),axis=1),
                     columns =  ohc_columns + num_cols)

    #define target column
    y = df['target']
    
    X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42)

    clf = LogisticRegression(max_iter=2000,random_state=0).fit(X_train, y_train)

    return clf.score(X_test, y_test)
```

然后，此函数可在循环中运行多次，例如10次。 与上一代码的不同之处在于，现在不是从整个表中获取示例，而是只从行的示例中获取示例。 例如，下面的示例代码仅占用1000行。 可以存储每次迭代的准确度。

```python
from tqdm import tqdm

bootstrap_accuracy = []
for i in tqdm(range(100)):
    
    #sample data from QS
    cur.execute('''SELECT *
    FROM fdu_luma_raw
    ORDER BY random()
    LIMIT 1000
    ''')    
    samples = [r for r in cur]
    colnames = [desc[0] for desc in cur.description]
    df_samples = pd.DataFrame(samples,columns=colnames)
    df_samples.fillna(0,inplace=True)
    
    #train the propensity model with sampled data and output its accuracy
    bootstrap_accuracy.append(end_to_end_pipeline(df_samples))
    
bootstrap_accuracy = np.sort(bootstrap_accuracy)
```

然后，对引导模型的准确度进行排序。 之后，模型的第10和90分量的准确度在给定样本量的情况下，变为模型准确度的95%置信区间。

![用于显示倾向得分的置信区间的print命令。](../images/use-cases/confidence-interval.png)

上图说明，如果您只需花费1000行来培训模型，则精度可能会在84%到88%之间。 您可以调整 `LIMIT` 子句，以确保模型的性能。
