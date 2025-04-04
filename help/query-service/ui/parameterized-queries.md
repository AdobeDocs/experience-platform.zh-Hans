---
title: 参数化查询
description: 了解如何在Adobe Experience Platform UI中使用参数化查询。
exl-id: 5c5ac691-5e29-4262-ba53-84dcc56e744f
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 11%

---

# 参数化查询 {#parameterized-queries}

>[!CONTEXTUALHELP]
>id="platform_queryService_queryEditor_parameterizedQueries"
>title="参数化查询"
>abstract="使用参数化查询在执行时添加参数值。这允许您处理动态数据并针对不同的用例重用查询。在文本编辑器中使用 `'$'` 序言将查询参数输入到查询中。接下来，在编辑器下方的查询参数部分添加键值。"

查询服务支持在查询编辑器中使用参数化查询。 通过参数化查询，您现在可以对参数使用占位符，并在执行时添加参数值。 使用占位符，您可以使用动态数据，其中您不知道在执行语句之前值是什么。 您还可以提前准备查询，并将它们重复用于类似目的。 重用查询可节省大量工作，因为您可以避免为每个用例创建不同的SQL查询。

## 先决条件

在继续本指南之前，请阅读[查询编辑器UI指南](./user-guide.md)。 查询编辑器指南提供了有关如何在Experience Platform用户界面中编写、验证和运行客户体验数据查询的详细信息。

>[!NOTE]
>
>在Adobe Experience Platform UI中，仅在内联模板的父级支持参数化查询。 这意味着参数化查询仅在原始模板中使用时才有效。 子模板必须是静态模板，不能具有动态参数。 有关详细信息，请参阅[内联模板文档](../key-concepts/inline-templates.md)。

## 参数化查询语法 {#syntax}

参数化查询使用格式`'$YOUR_PARAMETER_NAME'`，并且可以使用点表示法连接。 下面显示了使用参数化查询的示例SQL语句。

```sql
INSERT INTO
   $Database_Name.Schema_Name.adwh_lkup_process_delta_log
   (process_name, merge_policy_id, process_status, process_date, create_ts, change_ts)
SELECT
   '$Table_Process_Name' process_name,
   hash('$Merge_PolicyID') merge_policy_id,
   '$process_status' process_status,
   to_date('$date_key') process_date,
   CURRENT_TIMESTAMP create_ts,
   CURRENT_TIMESTAMP change_ts;
```

## 创建参数化查询 {#create}

要在UI中创建参数化查询，请导航到查询编辑器。 有关更多说明，请参阅[访问查询编辑器](./user-guide.md#accessing-query-editor)一节。

在文本编辑器中使用 `'$'` 序言将查询参数输入到查询中。接下来，选择[!UICONTROL 控制台]旁边的&#x200B;**[!UICONTROL 查询参数]**&#x200B;选项卡，为键添加缺少的值。 如果您忽略向任何所需键添加值，则无法执行查询。 警报图标(![警报图标。](/help/images/icons/alert.png))出现在“查询参数”部分的任何空[!UICONTROL 值]输入字段旁边。

>[!NOTE]
>
>如果查询不采用参数，则仍可在查询编辑器中输入不必要的参数。 查询编辑器会忽略所有不必要的键值对，并且这些键值对查询的执行或结果没有影响。

![带有参数化查询的查询编辑器以及高亮显示的查询参数节。](../images/ui/parameterized-queries/parameterized-query.png)

>[!TIP]
>
>将选项卡从[!UICONTROL 查询参数]更改为[!UICONTROL 控制台]以查看查询的控制台输出。

## 使用查询日志详细信息检查参数值 {#check-parameter-values}

不能在模板中保存参数，因为使用的值不是永久性的。 但是，您可以检查[!UICONTROL 查询日志详细信息]页面以查找查询运行中使用的参数值。 在这种情况下，日志不会指示查询是参数化查询。 有关如何查找所用值的说明，请参阅[查询日志文档](./query-logs.md)。

![查询日志视图，其参数化查询的SQL在详细信息节中突出显示。](../images/ui/parameterized-queries/parameterized-query-logs.png)

<!-- improve screenshot above ^ I am waiting for a scheduled run to complete -->

## 计划参数化查询 {#schedule}

当您计划参数化查询时，将保存参数值。 要计划参数化查询，请按照指南中介绍的典型过程创建计划查询[创建查询计划](./query-schedules.md#create-schedule)，然后输入要在查询运行中使用的参数值。 此UI部分仅针对参数化查询显示。 有关具体说明，请参阅有关[为计划的参数化查询](./query-schedules.md#set-parameters)设置参数的章节。

>[!TIP]
>
>查询服务通过使用参数化查询支持预准备语句。 有关涉及的SQL语法的详细信息，请参阅[预准备语句语法指南](../sql/prepared-statements.md)。

## 后续步骤

通过阅读本文档，您已了解如何在Adobe Experience Platform UI中参数化查询并在计划的查询运行中使用它们。 本文档还重点说明了如何检查日志中查询执行中使用的参数值。

接下来，建议您阅读有关[监视计划查询](./monitor-queries.md)的指南，以便通过Experience Platform UI更好地了解所有查询作业的状态。
