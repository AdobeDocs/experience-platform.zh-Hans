---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;query service
solution: Experience Platform
title: Jupyter笔记本中的查询服务
topic: Tutorial
description: Adobe Experience Platform将查询服务作为标准功能集成到JupyterLab中，使您能够在数据科学工作区中使用结构化查询语言(SQL)。 本教程演示了用于浏览、转换和分析Adobe Analytics数据的常见用例的SQL查询示例。
translation-type: tm+mt
source-git-commit: 3876c33a2d20481f45bd12eda3921898e9e65654
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 1%

---


# Jupyter笔记本中的查询服务

[!DNL Adobe Experience Platform] 允许您通过集成到标准功能中来 [!DNL Data Science Workspace] 使用结 [!DNL Query Service] 构化 [!DNL JupyterLab] 查询语言(SQL)。

本教程演示了用于浏览、转换和分析数据的常见用例的SQL查询 [!DNL Adobe Analytics] 示例。

## 入门指南

在开始本教程之前，您必须具有以下先决条件：

- 访问 [!DNL Adobe Experience Platform]。 如果您无权访问中的IMS组织，请在继 [!DNL Experience Platform]续操作之前与系统管理员联系

- 数据 [!DNL Adobe Analytics] 集

- 对本教程中使用的下列主要概念的有效理解：
   - [[!DNL体验数据模型(XDM)和XDM系统]](../../xdm/home.md)
   - [[!DNL查询服务]](../../query-service/home.md)
   - [[!DNL查询服务SQL语法]](../../query-service/sql/overview.md)
   - [Adobe Analytics]

## 访问 [!DNL JupyterLab] 和 [!DNL Query Service] {#access-jupyterlab-and-query-service}

1. 在[ [!DNLExperience Platform]](https://platform.adobe.com)中，从左 **[!UICONTROL 侧导航]** 列导航到“笔记本”。 请稍等片刻，JupyterLab将加载。

   ![](../images/jupyterlab/query/jupyterlab-launcher.png)

   >[!NOTE]
   >
   >如果未自动显示新的启动器选项卡，请通过单击文件打开新的启动器选项卡， **[!UICONTROL 然后选]** 择新 **[!UICONTROL 建启动器]**。

2. 在“启动器”选项卡中， **[!UICONTROL 单击]** Python 3环境中的“空白”图标以打开空笔记本。

   ![](../images/jupyterlab/query/blank_notebook.png)

   >[!NOTE]
   >
   >Python 3目前是笔记本电脑中唯一受支持的查询服务环境。

3. 在左侧选择边栏上，单击“数 **[!UICONTROL 据]** ”图标，多次单 **[!UICONTROL 击“数据集]** ”目录以列表所有数据集。

   ![](../images/jupyterlab/query/dataset.png)

4. 查找要 [!DNL Adobe Analytics] 浏览的数据集并右键单击列表，单击“笔记本 **[!UICONTROL 中的查询数据]** ”，在空笔记本中生成SQL查询。

5. 单击包含该函数的第一个生成的单 `qs_connect()` 元格，并通过单击播放按钮来执行它。 此函数在笔记本实例和实例之间建立连接 [!DNL Query Service]。

   ![](../images/jupyterlab/query/execute.png)

6. 从第二个生 [!DNL Adobe Analytics] 成的SQL查询中复制数据集名称，它将是后面的值 `FROM`。

   ![](../images/jupyterlab/query/dataset_name.png)

7. 单击+按钮插入新的笔记本 **单元** 格。

   ![](../images/jupyterlab/query/insert_cell.gif)

8. 在新单元格中复制、粘贴和执行以下导入语句。 这些语句将用于可视化您的数据：

   ```python
   import plotly.plotly as py
   import plotly.graph_objs as go
   from plotly.offline import iplot
   ```

9. 然后，在新单元格中复制并粘贴以下变量。 根据需要修改其值，然后执行它们。

   ```python
   target_table = "your Adobe Analytics dataset name"
   target_year = "2019"
   target_month = "04"
   target_day = "01"
   ```

   - `target_table` :数据集的 [!DNL Adobe Analytics] 名称。
   - `target_year` :目标数据的特定年份。
   - `target_month` :目标的特定月份。
   - `target_day` :目标数据的特定日期。

   >[!NOTE]
   >
   >您可以随时更改这些值。 执行此操作时，请确保为要应用的更改执行变量单元格。

## 查询数据 {#query-your-data}

在单个笔记本单元格中输入以下SQL查询。 通过单击查询的单元格，然后单击播放按 **[!UICONTROL 钮]** 。 成功的查询结果或错误日志显示在执行的单元格下方。

当笔记本处于长期非活动状态时，笔记本与笔记本之间的连接可能 [!DNL Query Service] 断开。 在这种情况下，请 [!DNL JupyterLab] 单击右上 **[!UICONTROL 角的]** “Power（电源）”按钮。

![](../images/jupyterlab/query/restart_button.png)

笔记本内核将重置，但单元格将保留，重 **[!UICONTROL 新运行]** 所有单元格以继续您离开的位置。

### 每小时访客计数 {#hourly-visitor-count}

以下查询返回指定日期的小时访客计数：

#### 查询

```sql
%%read_sql hourly_visitor -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                               AS Day,
       Substring(timestamp, 12, 2)                               AS Hour, 
       Count(DISTINCT concat(enduserids._experience.aaid.id, 
                             _experience.analytics.session.num)) AS Visit_Count 
FROM   {target_table}
WHERE _acp_year = {target_year} 
      AND _acp_month = {target_month}  
      AND _acp_day = {target_day}
GROUP  BY Day, Hour
ORDER  BY Hour;
```

在上述查询中，子 `_acp_year` 句中 `WHERE` 的目标设置为值 `target_year`。 通过将变量包含在大括号()中，在SQL查询中`{}`包括变量。

查询的第一行包含可选变量 `hourly_visitor`。 查询结果将作为Pactys数据帧存储在此变量中。 将结果存储在查询帧中允许您稍后使用所需的包可视化结 [!DNL Python] 果。 在新单元格 [!DNL Python] 中执行以下代码以生成条形图：

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

以下查询返回指定日期的小时活动计数：

#### 查询 <!-- omit in toc -->

```sql
%%read_sql hourly_actions -d -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                        AS Day,
       Substring(timestamp, 12, 2)                        AS Hour, 
       Count(concat(enduserids._experience.aaid.id, 
                    _experience.analytics.session.num,
                    _experience.analytics.session.depth)) AS Count 
FROM   {target_table}
WHERE  _acp_year = {target_year} 
       AND _acp_month = {target_month}  
       AND _acp_day = {target_day}
GROUP  BY Day, Hour
ORDER  BY Hour;
```

执行上述查询会将结果存储 `hourly_actions` 为数据帧。 在新单元格中执行以下函数以预览结果：

```python
hourly_actions.head()
```

可以修改上述查询，以使用WHERE子句中的逻辑运算符返回指定日期范围的每小时 **操作** 计数：

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

执行修改后的查询会将结果存储 `hourly_actions_date_range` 为数据帧。 在新单元格中执行以下函数以预览结果：

```python
hourly_actions_date_rage.head()
```

### 每个事件会话的访客数 {#number-of-events-per-visitor-session}

以下查询返回指定日期的每个访客会话的事件数：

#### 查询 <!-- omit in toc -->

```sql
%%read_sql events_per_session -c QS_CONNECTION
SELECT concat(enduserids._experience.aaid.id, 
              '-#', 
              _experience.analytics.session.num) AS aaid_sess_key, 
       Count(timestamp)                          AS Count 
FROM   {target_table}
WHERE  _acp_year = {target_year} 
       AND _acp_month = {target_month}  
       AND _acp_day = {target_day}
GROUP BY aaid_sess_key
ORDER BY Count DESC;
```

执行以下代 [!DNL Python] 码以生成每次访问会话事件数的直方图：

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

### 特定日期的热门页面 {#popular-pages-for-a-given-day}

以下查询返回指定日期的十个最受欢迎的页面：

#### 查询 <!-- omit in toc -->

```sql
%%read_sql popular_pages -c QS_CONNECTION
SELECT web.webpagedetails.name                 AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP  BY web.webpagedetails.name 
ORDER  BY page_views DESC 
LIMIT  10;
```

### 给定日期的活动用户数 {#active-users-for-a-given-day}

以下查询返回指定日期的十个最活跃的用户：

#### 查询 <!-- omit in toc -->

```sql
%%read_sql active_users -c QS_CONNECTION
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp)               AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP  BY aaid
ORDER  BY Count DESC
LIMIT  10;
```

### 按用户活动划分的活跃城市 {#active-cities-by-user-activity}

以下查询返回在指定日期生成大多数用户活动的十个城市：

#### 查询 <!-- omit in toc -->

```sql
%%read_sql active_cities -c QS_CONNECTION
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp)                                                     AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP  BY state_city
ORDER  BY Count DESC
LIMIT  10;
```

## 后续步骤

本教程演示了在笔记本中使用的一些 [!DNL Query Service] 示例 [!DNL Jupyter] 用例。 请按照 [使用Jupyter Notebooks教程分析数据](./analyze-your-data.md) ，了解如何使用Data Access SDK执行类似操作。