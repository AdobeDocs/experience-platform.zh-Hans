---
keywords: Experience Platform；JupyterLab；筆記型電腦；Data Science Workspace；熱門主題；查詢服務
solution: Experience Platform
title: Jupyter Notebook中的查詢服務
type: Tutorial
description: Adobe Experience Platform可讓您透過將查詢服務整合到JupyterLab中作為標準功能，來在Data Science Workspace中使用結構化查詢語言(SQL)。 本教學課程示範常見使用案例的範例SQL查詢，以探索、轉換和分析Adobe Analytics資料。
exl-id: c5ac7d11-a3bd-4ef8-a650-9f496a8bbaa7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 1%

---

# Jupyter Notebook中的查詢服務

[!DNL Adobe Experience Platform] 可讓您使用結構化查詢語言(SQL)於 [!DNL Data Science Workspace] 透過整合 [!DNL Query Service] 到 [!DNL JupyterLab] 作為標準特徵。

本教學課程示範常見使用案例的範例SQL查詢，以探索、轉換和分析 [!DNL Adobe Analytics] 資料。

## 快速入门

開始進行本教學課程之前，您必須具備下列必要條件：

- 存取 [!DNL Adobe Experience Platform]. 如果您無權存取中的組織 [!DNL Experience Platform]，請在繼續之前聯絡您的系統管理員

- 一個 [!DNL Adobe Analytics] 資料集

- 深入瞭解本教學課程使用的下列重要概念：
   - [[!DNL Experience Data Model (XDM) and XDM System]](../../xdm/home.md)
   - [[!DNL Query Service]](../../query-service/home.md)
   - [[!DNL Query Service SQL Syntax]](../../query-service/sql/overview.md)
   - Adobe Analytics

## 存取 [!DNL JupyterLab] 和 [!DNL Query Service] {#access-jupyterlab-and-query-service}

1. 在 [[!DNL Experience Platform]](https://platform.adobe.com)，導覽至 **[!UICONTROL Notebooks]** 左側導覽欄中的。 等待JupyterLab載入。

   ![](../images/jupyterlab/query/jupyterlab-launcher.png)

   >[!NOTE]
   >
   >如果新的啟動器標籤未自動顯示，請按一下以開啟新的啟動器標籤 **[!UICONTROL 檔案]** 然後選取 **[!UICONTROL 新增啟動器]**.

2. 在「啟動器」標籤中，按一下 **[!UICONTROL 空白]** 圖示開啟Python 3環境中的空白筆記本。

   ![](../images/jupyterlab/query/blank_notebook.png)

   >[!NOTE]
   >
   >Python 3目前是Notebooks中唯一支援查詢服務的環境。

3. 在左側選取範圍邊欄中，按一下 **[!UICONTROL 資料]** 圖示並連按兩下 **[!UICONTROL 資料集]** 目錄，列出所有資料集。

   ![](../images/jupyterlab/query/dataset.png)

4. 尋找 [!DNL Adobe Analytics] 要探索的資料集並在清單上按一下右鍵，請按一下 **[!UICONTROL 在筆記本中查詢資料]** 以在空白筆記本中產生SQL查詢。

5. 按一下第一個產生且包含函式的儲存格 `qs_connect()` 並按一下播放按鈕來執行它。 此函式會在您的Notebook執行個體與 [!DNL Query Service].

   ![](../images/jupyterlab/query/execute.png)

6. 向下複製 [!DNL Adobe Analytics] 資料集名稱來自第二個產生的SQL查詢，將是之後的值 `FROM`.

   ![](../images/jupyterlab/query/dataset_name.png)

7. 按一下「 」，插入新的筆記本儲存格 **+** 按鈕。

   ![](../images/jupyterlab/query/insert_cell.gif)

8. 在新儲存格中複製、貼上及執行下列匯入陳述式。 這些陳述式將用於視覺化您的資料：

   ```python
   import plotly.plotly as py
   import plotly.graph_objs as go
   from plotly.offline import iplot
   ```

9. 接下來，複製下列變數，並將其貼到新的儲存格中。 視需要修改其值，然後執行它們。

   ```python
   target_table = "your Adobe Analytics dataset name"
   target_year = "2019"
   target_month = "04"
   target_day = "01"
   ```

   - `target_table`：您的名稱 [!DNL Adobe Analytics] 資料集。
   - `target_year`：目標資料來自的特定年份。
   - `target_month`：目標來自的特定月份。
   - `target_day`：目標資料來自的特定日期。

   >[!NOTE]
   >
   >您可以隨時變更這些值。 執行此操作時，請務必執行變數儲存格以套用變更。

## 查詢您的資料 {#query-your-data}

在個別筆記本儲存格中輸入下列SQL查詢。 在查詢的儲存格上選取，然後選取 **[!UICONTROL play]** 按鈕。 成功的查詢結果或錯誤記錄檔會顯示在執行的儲存格下方。

當筆記型電腦長時間處於非使用中狀態時，筆記型電腦與電腦之間的連線 [!DNL Query Service] 可能會中斷。 在這種情況下，請重新啟動 [!DNL JupyterLab] 藉由選取 **重新啟動** 按鈕 ![重新啟動按鈕](../images/jupyterlab/user-guide/restart_button.png) 位於電源按鈕旁的右上角。

筆記型電腦核心會重設，但儲存格仍會保留，請重新執行所有儲存格，以繼續處理您中斷的儲存格。

### 每小時訪客計數 {#hourly-visitor-count}

下列查詢會傳回指定日期的每小時訪客計數：

#### 查询

```sql
%%read_sql hourly_visitor -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                               AS Day,
       Substring(timestamp, 12, 2)                               AS Hour, 
       Count(DISTINCT concat(enduserids._experience.aaid.id, 
                             _experience.analytics.session.num)) AS Visit_Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

在上述查詢中， `WHERE` 子句設為下列專案的值 `target_year`. 將變數包含在大括弧(`{}`)。

查詢的第一行包含選擇性變數 `hourly_visitor`. 查詢結果將作為Pandas資料流儲存在此變數中。 將結果儲存在資料流中可讓您稍後使用所需的視覺化查詢結果 [!DNL Python] 封裝。 執行下列動作 [!DNL Python] 在新儲存格中產生橫條圖的程式碼：

```python
trace = go.Bar(
    x = hourly_visitor['Hour'],
    y = hourly_visitor['Visit_Count'],
    name = "Visitor Count"
)
layout = go.Layout(
    title = 'Visit Count by Hour of Day',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'Hour of Day'),
    yaxis = dict(title = 'Count')
)
fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

### 每小時活動計數 {#hourly-activity-count}

下列查詢會傳回指定日期的每小時動作計數：

#### 查询 <!-- omit in toc -->

```sql
%%read_sql hourly_actions -d -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                        AS Day,
       Substring(timestamp, 12, 2)                        AS Hour, 
       Count(concat(enduserids._experience.aaid.id, 
                    _experience.analytics.session.num,
                    _experience.analytics.session.depth)) AS Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

執行上述查詢會將結果儲存在 `hourly_actions` 作為資料流。 在新儲存格中執行以下函式以預覽結果：

```python
hourly_actions.head()
```

您可以修改上述查詢，以使用中的邏輯運運算元傳回指定日期範圍的每小時動作計數 **位置** 子句：

#### 查询 <!-- omit in toc -->

```sql
%%read_sql hourly_actions_date_range -d -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                        AS Day,
       Substring(timestamp, 12, 2)                        AS Hour, 
       Count(concat(enduserids._experience.aaid.id, 
                    _experience.analytics.session.num,
                    _experience.analytics.session.depth)) AS Count 
FROM   {target_table}
WHERE  timestamp >= TO_TIMESTAMP('2019-06-01 00', 'YYYY-MM-DD HH')
       AND timestamp <= TO_TIMESTAMP('2019-06-02 23', 'YYYY-MM-DD HH')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

執行修改的查詢會將結果儲存在 `hourly_actions_date_range` 作為資料流。 在新儲存格中執行以下函式以預覽結果：

```python
hourly_actions_date_rage.head()
```

### 每個訪客工作階段的事件數 {#number-of-events-per-visitor-session}

以下查詢會傳回指定日期內每個訪客工作階段的事件數：

#### 查询 <!-- omit in toc -->

```sql
%%read_sql events_per_session -c QS_CONNECTION
SELECT concat(enduserids._experience.aaid.id, 
              '-#', 
              _experience.analytics.session.num) AS aaid_sess_key, 
       Count(timestamp)                          AS Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP BY aaid_sess_key
ORDER BY Count DESC;
```

執行下列動作 [!DNL Python] 產生每次造訪工作階段事件數長條圖的程式碼：

```python
data = [go.Histogram(x = events_per_session['Count'])]

layout = go.Layout(
    title = 'Histogram of Number of Events per Visit Session',
    xaxis = dict(title = 'Number of Events'),
    yaxis = dict(title = 'Count')
)

fig = go.Figure(data = data, layout = layout)
iplot(fig)
```

### 指定日期的熱門頁面 {#popular-pages-for-a-given-day}

下列查詢會傳回指定日期前十個最受歡迎的頁面：

#### 查询 <!-- omit in toc -->

```sql
%%read_sql popular_pages -c QS_CONNECTION
SELECT web.webpagedetails.name                 AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY web.webpagedetails.name 
ORDER  BY page_views DESC 
LIMIT  10;
```

### 指定日的作用中使用者 {#active-users-for-a-given-day}

以下查詢會傳回指定日期最活躍的十位使用者：

#### 查询 <!-- omit in toc -->

```sql
%%read_sql active_users -c QS_CONNECTION
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp)               AS Count
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY aaid
ORDER  BY Count DESC
LIMIT  10;
```

### 依使用者活動列出的活躍城市 {#active-cities-by-user-activity}

下列查詢會傳回在指定日期產生大部分使用者活動的十個城市：

#### 查询 <!-- omit in toc -->

```sql
%%read_sql active_cities -c QS_CONNECTION
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp)                                                     AS Count
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY state_city
ORDER  BY Count DESC
LIMIT  10;
```

## 后续步骤

本教學課程示範利用的一些範例使用案例 [!DNL Query Service] 在 [!DNL Jupyter] 筆記本。 請遵循 [使用Jupyter Notebooks分析您的資料](./analyze-your-data.md) 教學課程，以瞭解如何使用Data Access SDK執行類似操作。
