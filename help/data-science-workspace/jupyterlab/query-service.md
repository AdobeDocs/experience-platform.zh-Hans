---
keywords: 体验平台;朱皮特实验室;笔记本;数据科学工作区;热门话题;查询服务
solution: Experience Platform
title: Jupyter 笔记本中的查询服务
type: Tutorial
description: 通过将Query Service作为标准功能集成到JupyterLab中，Adobe Experience Platform允许您在数据科学Workspace中使用结构化查询语言(SQL)。 本教程演示了用于探索、转换和分析Adobe Analytics数据的常见用例的示例SQL查询。
exl-id: c5ac7d11-a3bd-4ef8-a650-9f496a8bbaa7
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 0%

---

# Jupyter 笔记本中的查询服务

>[!NOTE]
>
>不再可供购买数据科学工作区。
>
>本文档适用于先前有权访问数据科学工作区的现有客户。

[!DNL Adobe Experience Platform]允许您通过作为[!DNL Query Service][!DNL JupyterLab]标准功能集成到中使用结构化查询语言 （SQL[!DNL Data Science Workspace]）。

本教程演示了常见用例的示例 SQL 查询，以探索、转换和分析 [!DNL Adobe Analytics] 数据。

## 快速入门

在开始本教程之前，您必须具备以下先决条件：

- 访问[!DNL Adobe Experience Platform]。 如果您在[!DNL Experience Platform]中无权访问某个组织，请在继续操作之前与系统管理员联系

- [!DNL Adobe Analytics]数据集

- 了解本教程中使用的以下关键概念：
   - [[!DNL Experience Data Model (XDM) and XDM System]](../../xdm/home.md)
   - [[!DNL Query Service]](../../query-service/home.md)
   - [[!DNL Query Service SQL Syntax]](../../query-service/sql/overview.md)
   - Adobe Analytics

## 访问[!DNL JupyterLab]和[!DNL Query Service] {#access-jupyterlab-and-query-service}

1. 在[[!DNL Experience Platform]](https://platform.adobe.com)中，从左侧导航列导航到&#x200B;**[!UICONTROL Notebooks]**。 等待片刻以加载JupyterLab。

   ![](../images/jupyterlab/query/jupyterlab-launcher.png)

   >[!NOTE]
   >
   >如果未自动显示新的“启动器”选项卡，请单击&#x200B;**[!UICONTROL 文件]**&#x200B;打开新的“启动器”选项卡，然后选择&#x200B;**[!UICONTROL 新建启动器]**。

2. 在“启动器”选项卡中，单击Python 3环境中的&#x200B;**[!UICONTROL 空白]**&#x200B;图标以打开空笔记本。

   ![](../images/jupyterlab/query/blank_notebook.png)

   >[!NOTE]
   >
   >Python 3是目前唯一支持笔记本查询服务的环境。

3. 在左侧选择边栏上，单击 **[!UICONTROL 数据]** 图标，然后双击 **[!UICONTROL 数据集]** 目录以列出所有数据集。

   ![](../images/jupyterlab/query/dataset.png)

4. 找到要浏览的[!DNL Adobe Analytics]数据集并右键单击列表，单击“在笔记本&#x200B;**中查询数据”**&#x200B;以在空笔记本中生成 SQL 查询。

5. 单击包含函数 `qs_connect()` 的第一个生成的单元格，并通过单击播放按钮执行它。 此函数创建笔记本实例与[!DNL Query Service]之间的连接。

   ![](../images/jupyterlab/query/execute.png)

6. 从第二次生成的SQL查询中向下复制[!DNL Adobe Analytics]数据集名称，它将是`FROM`之后的值。

   ![](../images/jupyterlab/query/dataset_name.png)

7. 通过单击&#x200B;**+**&#x200B;按钮插入新的笔记本单元格。

   ![](../images/jupyterlab/query/insert_cell.gif)

8. 在新单元格中复制、粘贴并执行以下导入语句。 这些语句将用于可视化您的数据：

   ```python
   import plotly.plotly as py
   import plotly.graph_objs as go
   from plotly.offline import iplot
   ```

9. 接下来，将以下变量复制并粘贴到新单元格中。 根据需要修改其值，然后执行它们。

   ```python
   target_table = "your Adobe Analytics dataset name"
   target_year = "2019"
   target_month = "04"
   target_day = "01"
   ```

   - `target_table`：数据集 [!DNL Adobe Analytics] 的名称。
   - `target_year`：目标数据来源的特定年份。
   - `target_month`：目标所在的特定月份。
   - `target_day`：目标数据的来源日。

   >[!NOTE]
   >
   >您可以随时更改这些值。 执行此操作时，请确保执行变量单元格以应用更改。

## 查询数据 {#query-your-data}

在单个笔记本单元格中输入以下SQL查询。 通过选择其单元格，然后选择&#x200B;**[!UICONTROL 播放]**&#x200B;按钮来执行查询。 成功的查询结果或错误日志显示在执行的单元格下方。

当笔记本长时间处于非活动状态时，笔记本与[!DNL Query Service]之间的连接可能会中断。 在这种情况下，通过选择位于电源按钮右上角的&#x200B;**重新启动**&#x200B;按钮![重新启动按钮](/help/images/icons/restart.png)来重新启动[!DNL JupyterLab]。

笔记本内核将重置，但单元格将保留，重新运行所有单元格以继续之前停止的位置。

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

在上述查询中，`WHERE`子句中的时间戳设置为`target_year`的值。 通过将变量包含在大括号(`{}`)中，将其包含在SQL查询中。

查询的第一行包含可选变量`hourly_visitor`。 查询结果将作为Pandas数据流存储在此变量中。 将结果存储在数据流中允许您以后使用所需的[!DNL Python]包可视化查询结果。 在新单元格中执行以下[!DNL Python]代码以生成条形图：

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

#### 查询<!-- omit in toc -->

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

执行上述查询会将结果作为数据帧存储在`hourly_actions`中。 在新单元格中执行以下函数以预览结果：

```python
hourly_actions.head()
```

可以修改上述查询，以使用&#x200B;**WHERE**&#x200B;子句中的逻辑运算符返回指定日期范围的每小时操作计数：

#### 查询<!-- omit in toc -->

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

执行修改的查询会将结果作为数据流存储在`hourly_actions_date_range`中。 在新单元格中执行以下函数以预览结果：

```python
hourly_actions_date_rage.head()
```

### 每个访客会话的事件数 {#number-of-events-per-visitor-session}

以下查询返回指定日期内每个访客会话的事件数：

#### 查询<!-- omit in toc -->

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

执行以下[!DNL Python]代码以生成每个访问会话的事件数的直方图：

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

以下查询返回指定日期内最热门的十个页面：

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

### 按用户活动划分的活跃城市 {#active-cities-by-user-activity}

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

本教程演示了一些在 [!DNL Query Service] 笔记本中使用的 [!DNL Jupyter] 示例用例。 按照[使用Jupyter笔记本](./analyze-your-data.md)分析您的数据教程查看如何使用Data Access SDK执行类似的操作。
