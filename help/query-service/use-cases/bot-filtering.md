---
title: 使用機器學習的查詢服務中的機器人篩選
description: 本檔案概述如何使用查詢服務和機器學習來判斷機器人活動，並從正版線上網站訪客流量中篩選其動作。
exl-id: fc9dbc5c-874a-41a9-9b60-c926f3fd6e76
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 5%

---

# 中的機器人篩選 [!DNL Query Service] 使用機器學習

機器人活動可能會影響分析量度，並損害資料完整性。 Adobe Experience Platform [!DNL Query Service] 可用來透過機器人篩選程式來維持資料品質。

機器人篩選可讓您廣泛移除因與網站的非人為互動而造成的資料汙染，進而維持資料品質。 此程式是透過SQL查詢和機器學習的組合來達成。

識別機器人活動有多種方式。 本檔案採取的方法著重於活動尖峰，在此例中是使用者在指定時段內採取的動作次數。 最初，SQL查詢會任意設定一段時間內採取的動作數上限，以符合機器人活動的資格。 然後使用機器學習模型動態地調整此臨界值，以改善這些比率的準確性。

本檔案提供SQL機器人篩選查詢的概覽和詳細範例，以及您在環境中設定程式所需的機器學習模型。

## 快速入门

此程式的一部分需要您訓練機器學習模型，本檔案假設您具備一個或多個機器學習環境的工作知識。

此範例使用 [!DNL Jupyter Notebook] 作為開發環境。 雖然有許多可用選項， [!DNL Jupyter Notebook] 建議使用，因為這是開放原始碼Web應用程式，運算需求低。 它可以 [從官方網站下載](https://jupyter.org/).

## 使用 [!DNL Query Service] 若要定義機器人活動的臨界值

用於擷取資料以進行機器人偵測的兩個屬性為：

* Experience Cloud訪客ID （ECID，也稱為MCID）：這可提供永久性的通用ID，可識別所有Adobe解決方案中的訪客。
* 時間戳記：這會提供網站上發生活動時的時間和日期（UTC格式）。

>[!NOTE]
>
>使用 `mcid` 仍可在指向Experience Cloud訪客ID的名稱空間參考中找到，如下例所示。

下列SQL陳述式提供識別機器人活動的初始範例。 陳述式假設如果訪客在一分鐘內執行50次點選，則使用者為機器人。

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

運算式會篩選ECID (`mcid`)符合臨界值，但未處理其他間隔中流量尖峰的所有訪客。

## 透過機器學習改善機器人偵測

初始SQL陳述式可以細化，成為機器學習的功能擷取查詢。 改良的查詢應該會在各種間隔產生更多功能，以訓練高準確率的機器學習模型。

此範例陳述式會從1分鐘展開為最多60次點按，以包含5分鐘和30分鐘週期，分別點按計數為300和1800。

範例陳述式會收集每個ECID的最大點按次數(`mcid`)。 初始陳述式已展開為包含1分鐘（60秒）、5分鐘（300秒）和1小時（即1800秒）句點。

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

此運算式的結果看起來可能類似於下面提供的表格。

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

## 使用機器學習識別新的尖峰臨界值

接下來，將產生的查詢資料集匯出為CSV格式，然後將其匯入 [!DNL Jupyter Notebook]. 從該環境中，您可以使用目前的機器學習程式庫來訓練機器學習模型。 請參閱疑難排解指南，瞭解更多關於 [如何從匯出資料 [!DNL Query Service] CSV格式](../troubleshooting-guide.md#export-csv)

最初建立的臨時尖峰臨界值不是資料導向的，因此缺乏準確性。 機器學習模型可用來訓練引數做為臨界值。 因此，您可以透過減少查詢數量來提高查詢效率 `GROUP BY` 移除不需要的功能，以取得關鍵字。

此範例使用Scikit-Learn機器學習程式庫，此程式庫預設會透過安裝 [!DNL Jupyter Notebook]. 也會匯入「熊貓」Python資料庫供您在此使用。 下列指令輸入到 [!DNL Jupyter Notebook].

```shell
import pandas as ps

df = pd_read.csv('data/bot.csv')
df = df[df['count_1-min'] > 1]
df['is_bot'] = 0
df.loc[df['count_1_min'] > 50,'is_bot'] = 1
df
```

接下來，您必須在資料集上訓練決策樹分類器，並觀察從模型產生的邏輯。

「Matplotlib」資料庫用於在以下範例中視覺化決策樹分類器。

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

傳回的值來自 [!DNL Jupyter Notebook] 此範例如下。

```text
Model Accuracy: 0.99935
```

![的統計輸出 [!DNL Jupyter Notebook] 機器學習模型。](../images/use-cases/jupiter-notebook-output.png)

上述範例中顯示的模型結果精確度超過99%。

由於決策樹分類器可使用來自以下位置的資料進行訓練 [!DNL Query Service] 您可以使用排定的查詢定期進行篩選，以高精度篩選機器人活動，確保資料完整性。 透過使用衍生自機器學習模型的引數，可以使用模型建立的高度精確的引數來更新原始查詢。

此範例模型經高度精確判斷後，認為任何在5分鐘內互動超過130次的訪客都是機器人。 此資訊現在可用於縮小機器人篩選SQL查詢的範圍。

## 后续步骤

閱讀本檔案可讓您更瞭解如何使用 [!DNL Query Service] 和機器學習來決定和篩選機器人活動。

其他說明下列專案優點的檔案： [!DNL Query Service] 對貴組織的策略性業務見解如下 [捨棄的瀏覽使用案例](./abandoned-browse.md) 範例。
