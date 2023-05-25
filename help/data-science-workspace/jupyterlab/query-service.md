---
keywords: Experience Platform；JupyterLab；笔记本；Data Science Workspace；热门主题；查询服务
solution: Experience Platform
title: Jupyter Notebook中的查询服务
type: Tutorial
description: Adobe Experience Platform允许您通过将查询服务作为标准功能集成到JupyterLab中，来使用Data Science Workspace中的结构化查询语言(SQL)。 本教程演示了用于探索、转换和分析Adobe Analytics数据的常见用例的示例SQL查询。
exl-id: c5ac7d11-a3bd-4ef8-a650-9f496a8bbaa7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 1%

---

# Jupyter Notebook中的查询服务

[!DNL Adobe Experience Platform] 允许您在中使用结构化查询语言(SQL) [!DNL Data Science Workspace] 通过集成 [!DNL Query Service] 到 [!DNL JupyterLab] 作为标准功能。

本教程演示了用于探索、转换和分析常用用例的示例SQL查询 [!DNL Adobe Analytics] 数据。

## 快速入门

在开始本教程之前，您必须满足以下先决条件：

- 访问 [!DNL Adobe Experience Platform]. 如果您无权访问中的组织 [!DNL Experience Platform]，请在继续之前与系统管理员联系

- An [!DNL Adobe Analytics] 数据集

- 对本教程中使用的以下关键概念有了实际了解：
   - [[!DNL Experience Data Model (XDM) and XDM System]](../../xdm/home.md)
   - [[!DNL Query Service]](../../query-service/home.md)
   - [[!DNL Query Service SQL Syntax]](../../query-service/sql/overview.md)
   - Adobe Analytics

## 访问 [!DNL JupyterLab] 和 [!DNL Query Service] {#access-jupyterlab-and-query-service}

1. In [[!DNL Experience Platform]](https://platform.adobe.com)，导航到 **[!UICONTROL Notebooks]** （从左侧导航列中）。 等待片刻以加载JupyterLab。

   ![](../images/jupyterlab/query/jupyterlab-launcher.png)

   >[!NOTE]
   >
   >如果未自动显示新的“启动器”选项卡，请单击以打开新的“启动器”选项卡 **[!UICONTROL 文件]** 然后选择 **[!UICONTROL 新建启动器]**.

2. 在“启动器”选项卡中，单击 **[!UICONTROL 空白]** 图标，打开空笔记本。

   ![](../images/jupyterlab/query/blank_notebook.png)

   >[!NOTE]
   >
   >Python 3是当前笔记本中查询服务唯一支持的环境。

3. 在左侧的选择边栏中，单击 **[!UICONTROL 数据]** 图标，然后双击 **[!UICONTROL 数据集]** 目录，列出所有数据集。

   ![](../images/jupyterlab/query/dataset.png)

4. 查找 [!DNL Adobe Analytics] 要浏览并右键单击列表的数据集，请单击 **[!UICONTROL 在笔记本中查询数据]** 以在空笔记本中生成SQL查询。

5. 单击第一个生成的包含函数的单元格 `qs_connect()` 并通过单击“播放”按钮来执行。 此函数创建笔记本实例与 [!DNL Query Service].

   ![](../images/jupyterlab/query/execute.png)

6. 向下复制 [!DNL Adobe Analytics] 数据集名称来自第二个生成的SQL查询，它将是之后的值 `FROM`.

   ![](../images/jupyterlab/query/dataset_name.png)

7. 通过单击 **+** 按钮。

   ![](../images/jupyterlab/query/insert_cell.gif)

8. 在新单元格中复制、粘贴和执行以下import语句。 这些语句将用于可视化您的数据：

   ```python
   import plotly.plotly as py
   import plotly.graph_objs as go
   from plotly.offline import iplot
   ```

9. 接下来，将以下变量复制并粘贴到新单元格中。 根据需要修改它们的值，然后执行它们。

   ```python
   target_table = "your Adobe Analytics dataset name"
   target_year = "2019"
   target_month = "04"
   target_day = "01"
   ```

   - `target_table`：您的名称 [!DNL Adobe Analytics] 数据集。
   - `target_year`：目标数据来自的特定年份。
   - `target_month`：目标来自的特定月份。
   - `target_day`：目标数据来自的特定日期。

   >[!NOTE]
   >
   >您可以随时更改这些值。 在执行此操作时，请确保执行变量单元格以应用更改。

## 查询您的数据 {#query-your-data}

在单个笔记本单元格中输入以下SQL查询。 选择查询的单元格，然后选择 **[!UICONTROL play]** 按钮。 成功的查询结果或错误日志显示在执行的单元格下方。

当笔记本长时间处于非活动状态时，笔记本和服务器之间的连接 [!DNL Query Service] 可能会中断。 在这种情况下，重新启动 [!DNL JupyterLab] 通过选择 **重新启动** 按钮 ![重新启动按钮](../images/jupyterlab/user-guide/restart_button.png) 位于电源按钮旁边的右上角。

笔记本内核将重置，但单元格将保留，重新运行所有单元格以继续运行之前停止的操作。

### 每小时访客计数 {#hourly-visitor-count}

以下查询返回指定日期的每小时访客计数：

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

在上述查询中，时间戳 `WHERE` 子句设置为的值 `target_year`. 通过将变量包含在大括号(`{}`)。

查询的第一行包含可选变量 `hourly_visitor`. 查询结果将作为Pandas数据流存储在此变量中。 将结果存储在数据流中允许您稍后使用所需的可视化查询结果 [!DNL Python] 包。 执行以下命令 [!DNL Python] 新单元格中用于生成条形图的代码：

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

### 每小时活动计数 {#hourly-activity-count}

以下查询返回指定日期的每小时操作计数：

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

执行上述查询会将结果存储在 `hourly_actions` 作为数据流。 在新单元格中执行以下函数以预览结果：

```python
hourly_actions.head()
```

可以修改上述查询，以使用中的逻辑运算符返回指定日期范围内的每小时操作计数 **位置** 子句：

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

执行修改后的查询会将结果存储在 `hourly_actions_date_range` 作为数据流。 在新单元格中执行以下函数以预览结果：

```python
hourly_actions_date_rage.head()
```

### 每个访客会话的事件数 {#number-of-events-per-visitor-session}

以下查询返回指定日期内每个访客会话的事件数：

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

执行以下命令 [!DNL Python] 用于为每个访问会话的事件数生成直方图的代码：

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

### 给定日期的热门页面 {#popular-pages-for-a-given-day}

以下查询返回指定日期的最受欢迎的10个页面：

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

### 给定日期的活动用户 {#active-users-for-a-given-day}

以下查询返回指定日期内最活跃的十个用户：

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

### 按用户活动列出的活跃城市 {#active-cities-by-user-activity}

以下查询返回在指定日期生成大多数用户活动的十个城市：

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

本教程演示了利用的一些示例用例 [!DNL Query Service] 在 [!DNL Jupyter] 笔记本。 请遵循 [使用Jupyter Notebooks分析数据](./analyze-your-data.md) 本教程将介绍如何使用Data Access SDK执行类似操作。
