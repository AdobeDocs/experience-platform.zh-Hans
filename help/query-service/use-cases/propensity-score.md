---
title: 使用机器学习生成的预测模型确定倾向分数
description: 了解如何使用查询服务将您的预测模型应用于Experience Platform数据。 本文档演示了如何使用Experience Platform数据来预测客户每次访问的购买倾向。
exl-id: 29587541-50dd-405c-bc18-17947b8a5942
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 0%

---

# 使用机器学习生成的预测模型确定倾向分数

使用查询服务，您可以利用基于机器学习平台构建的预测模型（例如倾向分数）来分析Experience Platform数据。

本指南介绍如何使用查询服务将数据发送到机器学习平台，以便在计算笔记本中训练模型。 训练后的模型可应用于使用SQL的数据，以预测客户每次访问的购买倾向。

## 快速入门

作为此过程的一部分，您需要培训机器学习模型，本文档假定您掌握一个或多个机器学习环境的工作知识。

此示例使用[!DNL Jupyter Notebook]作为开发环境。 虽然有许多可用选项，但建议使用[!DNL Jupyter Notebook]，因为它是开源Web应用程序，计算要求较低。 可从官方网站](https://jupyter.org/)下载[。

如果您尚未这样做，请按照[连接 [!DNL Jupyter Notebook] Adobe Experience Platform查询服务](../clients/jupyter-notebook.md)的步骤，然后再继续阅读本指南。

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

## 将Experience Platform中的分析表导入[!DNL Jupyter Notebook] {#import-analytics-tables}

要生成倾向分数模型，必须将存储在Experience Platform中的分析数据的投影导入[!DNL Jupyter Notebook]。 从连接到查询服务的[!DNL Python] 3 [!DNL Jupyter Notebook]，以下命令从虚拟服装店Luma导入客户行为数据集。 由于Experience Platform数据是使用Experience Data Model (XDM)格式存储的，因此必须生成符合架构结构的示例JSON对象。 有关如何[生成示例JSON对象](../../xdm/ui/sample.md)的说明，请参阅文档。

![高亮显示具有多个命令的[!DNL Jupyter Notebook]仪表板。](../images/use-cases/jupyter-commands.png)

输出显示[!DNL Jupyter Notebook]仪表板中Luma行为数据集中所有列的列表化视图。

![Luma在[!DNL Jupyter Notebook].](../images/use-cases/behavioural-dataset-results.png)内导入的客户行为数据集的列表化输出

## 为机器学习准备数据 {#prepare-data-for-machine-learning}

必须标识目标列才能训练机器学习模型。 由于购买倾向是此用例的目标，因此从Luma结果中选择`analytic_action`列作为目标列。 值`productPurchase`是客户购买的指示器。 `purchase_value`和`purchase_num`列也将删除，因为它们与产品购买操作直接相关。

执行这些操作的命令如下：

```python
#define the target label for prediction
df['target'] = (df['analytic_action'] == 'productPurchase').astype(int)
#remove columns that are dependent on the label
df.drop(['analytic_action','purchase_value'],axis=1,inplace=True)
```

接下来，必须将Luma数据集中的数据转换为相应的表示形式。 需要执行两个步骤：

1. 将表示数字的列转换为数字列。 为此，请显式转换`dataframe`中的数据类型。
1. 还将分类列转换为数字列。

```python
#convert columns that represent numbers
num_cols = ['purchase_num', 'value_cart', 'value_lifetime']
df[num_cols] = df[num_cols].apply(pd.to_numeric, errors='coerce')
```

使用名为&#x200B;*一个热编码*&#x200B;的技术转换分类数据变量以用于机器和深度学习算法。 这反过来又改善了预测以及模型的分类准确性。 使用`Sklearn`库在单独的列中表示每个分类值。

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

定义为`X`的数据将列表化，如下所示：

![在[!DNL Jupyter Notebook].](../images/use-cases/x-output-table.png)内的X的列表化输出


现在，机器学习所需的数据可用，它可以适应[!DNL Python]的`sklearn`库中预配置的机器学习模型。 [!DNL Logistics Regression]用于训练倾向模型，并允许您查看测试数据的准确性。 在本例中，大约为85%。

用于估计机器学习算法性能的[!DNL Logistic Regression]算法和训练测试拆分方法导入到下面的代码块中：

```python
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42)

clf = LogisticRegression(max_iter=2000, random_state=0).fit(X_train, y_train)

print("Test data accuracy: {}".format(clf.score(X_test, y_test)))
```

试验数据精度为0.8518518518518519。

通过使用物流回归，您可以可视化购买原因，并按倾向重要性降序对确定倾向的特征进行排序。 第一列表示导致购买行为的较高因果关系。 后一列指明了不会导致购买行为的因素。

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

下面显示了结果的垂直条形图可视化图表：

![定义购买或不购买倾向的前10项功能的可视化图表。](../images/use-cases/visualized-results.png)

可以从条形图中发现几种模式。 渠道的销售点(POS)和作为报销的呼叫主题是决定购买行为的最重要因素。 而投诉和发票等呼叫主题是定义非购买行为的重要角色。 这些是可量化的、可操作的洞察，营销人员可以利用它们开展营销活动以解决购买这些客户的倾向。

## 使用查询服务应用训练后的模型 {#use-query-service-to-apply-trained-model}

创建经过训练的模型后，必须将其应用于Experience Platform中保存的数据。 为此，必须将机器学习管道的逻辑转换为SQL。 此过渡的两个主要组成部分如下：

- 首先，SQL必须取代[!DNL Logistics Regression]模块才能获得预测标签的概率。 物流回归创建的模型生成了回归模型`y = wX + c`，其中权重`w`和截距`c`是模型的输出。 SQL特征可用于将权重相乘以获得概率。

- 其次，在[!DNL Python]中用一种热编码实现的工程过程也必须合并到SQL中。 例如，在原始数据库中，我们有`geo_county`列用于存储县，但该列已转换为`geo_county=Bexar`、`geo_county=Dallas`、`geo_county=DeKalb`。 以下SQL语句执行相同的转换，其中`w1`、`w2`和`w3`可以用从[!DNL Python]中的模型学习到的权重替代：

```sql
SELECT  CASE WHEN geo_state = 'Bexar' THEN FLOAT(w1) ELSE 0 END AS f1,
        CASE WHEN geo_state = 'Dallas' THEN FLOAT(w2) ELSE 0 END AS f2,
        CASE WHEN geo_state = 'Bexar' THEN FLOAT(w3) ELSE 0 END AS f3,
```

对于数字功能，可以将列与权数直接相乘，如下面的SQL语句所示。

```sql
SELECT FLOAT(purchase_num) * FLOAT(w4) AS f4,
```

在获得数字之后，它们可以移植到sigmoid函数中，其中物流回归算法产生最终预测。 在下面的语句中，`intercept`是回归中的截距数。
        

```sql
SELECT CASE WHEN 1 / (1 + EXP(- (f1 + f2 + f3 + f4 + FLOAT(intercept)))) > 0.5 THEN 1 ELSE 0 END AS Prediction;
```
 
### 端到端示例

在您有两个列（`c1`和`c2`）的情况下，如果`c1`有两个类别，则[!DNL Logistic Regression]算法将使用以下函数进行训练：
 

```python
y = 0.1 * "c1=category 1"+ 0.2 * "c1=category 2" +0.3 * c2+0.4
```
 
SQL中的等效项如下：

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
 
用于自动化翻译过程的[!DNL Python]代码如下所示：

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

使用SQL推断数据库时，输出如下：

```python
sql = generate_lr_inference_sql(ohc_columns, num_cols, clf, "fdu_luma_raw")
cur.execute(sql)    
samples = [r for r in cur]
colnames = [desc[0] for desc in cur.description]
pd.DataFrame(samples,columns=colnames)
```

列表化的结果显示每个客户会话的购买倾向，其中`0`表示无购买倾向，`1`表示已确认的购买倾向。

![使用SQL的数据库推理的列表化结果。](../images/use-cases/inference-results.png)

## 处理采样数据：引导 {#working-on-sampled-data}

如果数据大小对于本地计算机来说太大而无法存储用于模型训练的数据，则可以从Query Service中获取样本而不是完整数据。 要了解需要多少数据才能从查询服务中采样，您可以应用称为引导的技术。 为此，自举法就是用不同样本对模型进行多次训练，检验不同样本之间模型精度的差异。 为了调整上述倾向性模型示例，首先，将整个机器学习工作流封装为一个函数。 代码如下：

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

然后，可以在循环中多次运行此函数，例如10次。 与上一个代码的区别在于，现在示例不是取自整个表，而只取自一行示例。 例如，下面的示例代码只需1000行。 可以存储每个迭代的精度。

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

然后，对引导模型的精度进行排序。 之后，模型准确度的第10个和第90个分位数会变成95%置信区间，即模型对于给定样本大小的准确度的置信区间。

![用于显示倾向分数的置信区间的打印命令。](../images/use-cases/confidence-interval.png)

上图表明，如果您只用1000行来培训模型，则准确度预计会下降约84%到88%。 您可以根据需要调整查询服务查询中的`LIMIT`子句，以确保模型的性能。
