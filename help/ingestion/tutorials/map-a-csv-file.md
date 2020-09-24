---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;
solution: Experience Platform
title: 将CSV文件映射到XDM模式
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '1350'
ht-degree: 2%

---


# 将CSV文件映射到XDM模式

要将CSV数据引入 [!DNL Adobe Experience Platform]其中，必须将数据映射 [!DNL Experience Data Model] 到(XDM)模式。 本教程介绍如何使用用户界面将CSV文件映射到 [!DNL Platform] XDM模式。

此外，本教程的附录还提供了有关使用映射函数的更 [多信息](#mapping-functions)。

## 入门指南

本教程需要对以下组件有一个有效的了解 [!DNL Platform]:

- [[!DNL体验数据模型（XDM系统）]](../../xdm/home.md):组织客户体验数 [!DNL Platform] 据的标准化框架。
- [[!DNL批量摄取]](../batch-ingestion/overview.md):从用户提供的 [!DNL Platform] 数据文件中摄取数据的方法。

本教程还要求您已创建数据集以将CSV数据引入。 有关在UI中创建数据集的步骤，请参阅数 [据摄取教程](./ingest-batch-data.md)。

## 选择目标

登录到 [[!DNLAdobe Experience Platform]](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏中选]** 择工作流 **[!UICONTROL ，以访问工作流工]** 作区。

从工作流 **[!UICONTROL 屏幕]** ，选择数 **[!UICONTROL 据摄取部分下的]** “将CSV映射 **[!UICONTROL 到XDM模式]** ”，然后选 ****&#x200B;择启动。

![](../images/tutorials/map-a-csv-file/workflows.png)

将显 **[!UICONTROL 示将CSV映射到XDM模式]** ，从目标步骤 **[!UICONTROL 开始]** 。 选择要收录到的入站数据的数据集。 您可以使用现有数据集或创建新数据集。

**使用现有数据集**

要将CSV数据引入现有数据集，请选择“使 **[!UICONTROL 用现有数据集]**”。 您可以使用搜索函数或通过滚动面板中现有数据集的列表来检索现有数据集。

![](../images/tutorials/map-a-csv-file/use-existing-dataset.png)

要将CSV数据引入新数据集，请选择 **[!UICONTROL 创建新数据集]** ，并在提供的字段中输入数据集的名称和说明。 通过使用搜索函数或滚动模式提供的列表来选择模式。 选择 **[!UICONTROL 下一]** 步以继续。

![](../images/tutorials/map-a-csv-file/create-new-dataset.png)

## 添加数据

将出 **[!UICONTROL 现添加数]** 据步骤。 将CSV文件拖放到提供的空间中，或选择“选 **[!UICONTROL 择文件]** ”以手动输入CSV文件。

![](../images/tutorials/map-a-csv-file/add-data.png)

上载 **[!UICONTROL 文件后]** ，将显示“示例数据”部分，其中显示前十行数据。 确认数据已按预期上传后，选择“下 **[!UICONTROL 一步]**”。

![](../images/tutorials/map-a-csv-file/sample-data.png)

## 将CSV字段映射到XDM模式字段

将出 **[!UICONTROL 现]** “映射”步骤。 CSV文件的列列列在源字段 **[!UICONTROL 下]**，其对应的XDM模式字段列在 **[!UICONTROL 目标字段下]**。 未选择的目标字段以红色列出。 您可以使用筛选器字段选项缩小可用源字段的列表。

>[!TIP]
>
>[!DNL Platform] 根据您选择的目标模式或数据集，为自动映射字段提供智能建议。 您可以手动调整映射规则以适合您的用例。

要将CSV列映射到XDM字段，请选择该列的相应模式字段旁的目标图标。

![](../images/tutorials/map-a-csv-file/mapping.png)

将出 **[!UICONTROL 现“选择模式]** ”字段窗口。 在此，您可以导航XDM模式的结构，并找到要将CSV列映射到的字段。 单击XDM字段以将其选中，然后单击“ **[!UICONTROL 选择]**”。

![](../images/tutorials/map-a-csv-file/select-schema-field.png)

完成其余未映射源字段的步骤后，“映射”屏 **[!UICONTROL 幕将重新显示]** ，选定的XDM字段现在显示在“ **[!UICONTROL 目标”字段下]**。

![](../images/tutorials/map-a-csv-file/field-mapped.png)

在映射字段时，您还可以包含根据输入源字段计算值的函数。 有关详细 [信息](#mapping-functions) ，请参阅附录中的映射函数部分。

### 添加计算字段

计算字段允许根据输入模式中的属性创建值。 然后，可将这些值分配给目标模式中的属性，并提供名称和说明以便更轻松地引用。

选择“添 **[!UICONTROL 加计算字段]** ”按钮以继续。

![](../images/tutorials/map-a-csv-file/add-calculate-field.png)

将出 **[!UICONTROL 现“创建计算字段]** ”面板。 左对话框包含计算字段中支持的字段、函数和运算符。 选择一个选项卡以开始向表达式编辑器添加函数、字段或运算符。

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| 选项卡 | 描述 |
| --------- | ----------- |
| 字段 | “字段”选项卡列表源模式中可用的字段和属性。 |
| 函数 | 函数选项卡列表可用于转换数据的函数。 |
| 运算符 | “运算符”选项卡列表可用于转换数据的运算符。 |

您可以使用中心的表达式编辑器手动添加字段、函数和运算符。 选择要开始创建表达式的编辑器。

![](../images/tutorials/map-a-csv-file/expression-editor.png)

选择 **[!UICONTROL 保存]** ，以继续。

映射屏幕将随新创建的源字段重新显示。 应用相应的目标字段并选 **[!UICONTROL 择]** “完成”以完成映射。

![](../images/tutorials/map-a-csv-file/new-field.png)

## 监视数据流

映射和创建CSV文件后，您可以监视通过它摄取的数据。 有关监视数据流的详细信息，请参阅有关监视流数据 [流的教程](../../ingestion/quality/monitor-data-flows.md)。

## 后续步骤

通过遵循本教程，您已成功将平面CSV文件映射到XDM模式并将其引入 [!DNL Platform]。 此数据现在可供下游服务 [!DNL Platform] 使用，如 [!DNL Real-time Customer Profile]。 有关详细信息， [请参阅[!DNL实时客户用户档案]](../../profile/home.md) 的概述。

## 附录

以下部分提供了有关将CSV列映射到XDM字段的其他信息。

### 映射函数

某些映射函数可用于根据在源字段中输入的内容计算和计算值。 要使用函数，请在“源字段”下 **[!UICONTROL 键入该函数]** ，并输入相应的语法和输入。

例如，要连接 **城市****和国家／地区** CSV字段并将其分配 **到城市** XDM字段，请将源字段设置为 `concat(city, ", ", county)`。

![](../images/tutorials/map-a-csv-file/mapping-function.png)

下表列表了所有支持的映射函数，包括示例表达式及其结果输出。

| 函数 | 描述 | 示例表达式 | 示例输出 |
| -------- | ----------- | ----------------- | ------------- |
| concat | 连接给定字符串。 | concat（&quot;嗨， &quot;, &quot;there&quot;, &quot;!&quot;） | `"Hi, there!"` |
| 爆炸 | 根据正则表达式拆分字符串并返回一组部分。 | explode（&quot;嗨，那儿！&quot;, &quot; &quot;） | `["Hi,", "there"]` |
| instr | 返回子字符串的位置／索引。 | instr(&quot;adobe<span>.com&quot;, &quot;com&quot;) | 6 |
| replacestr | 替换搜索字符串（如果存在于原始字符串中）。 | replaceestr(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;这是字符串替换测试&quot; |
| substr | 返回给定长度的子字符串。 | substr（&quot;这是子字符串测试&quot;, 7, 8） | &quot; a subst&quot; |
| lower /<br>lcase | 将字符串转换为小写。 | lower(&quot;HeLLo&quot;)<br>lcase(&quot;HeLLo&quot;) | “hello” |
| 上/<br>下 | 将字符串转换为大写。 | upper(&quot;HeLLo&quot;)<br>ucase(&quot;HeLLo&quot;) | “您好” |
| 拆分 | 在分隔符上拆分输入字符串。 | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| 加入 | 使用分隔符连接对象列表。 | `join(" ", ["Hello", "world"]`) | “你好世界” |
| 凝聚 | 返回给定列表中的第一个非空对象。 | coalesce(null、null、null、“first”、null、“second”) | “first” |
| 解码 | 如果将键和键值对列表拼合为数组，则函数返回值（如果找到键），或返回默认值（如果数组中存在）。 | decode(&quot;k2&quot;, &quot;k1&quot;, &quot;v1&quot;, &quot;k2&quot;, &quot;v2&quot;, &quot;default&quot;) | &quot;v2&quot; |
| ii | 计算给定的布尔表达式，并根据结果返回指定值。 | iif(&quot;s&quot;。equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |
| min | 返回给定参数的最小值。 使用自然订购。 | min(3, 1, 4) | 1 |
| max | 返回给定参数的最大值。 使用自然订购。 | max(3, 1, 4) | 4 |
| 第 | 检索第一个给定参数。 | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| 最后 | 检索最后一个给定参数。 | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| uuid /<br>guid | 生成伪随机ID。 | uuid()<br>guid() | {UNIQUE_ID} |
| now | 检索当前时间。 | now() | `2019-10-23T10:10:24.556-07:00[America/Los_Angeles]` |
| timestamp | 检索当前Unix时间。 | timestamp() | 1571850624571 |
| 格式 | 根据指定的格式设置输入日期的格式。 | format({DATE}, &quot;yyyy-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | 根据指定的格式将时间戳转换为日期字符串。 | dformat(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | “2019年10月23日11:24” |
| 日期 | 将日期字符串转换为ZonedDateTime对象（ISO 8601格式）。 | date（&quot;2019年10月23日11:24&quot;） | &quot;2019-10-23T11:24:00+00:00&quot; |
| date_part | 检索日期的部分。 支持以下组件值： <br><br><br>“年<br>”<br><br>“yy<br>”第4季度<br>“<br><br><br><br>”<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>“q”、“q”、“”、“ead”。“ 12”“mi”“n”“第二”“毫秒””。 | date_part(date(&quot;2019-10-17 11:55:12&quot;), &quot;MM&quot;) | 10 |
| set_date_part | 在给定日期替换组件。 接受以下组件： <br><br>&quot;年&quot;<br>&quot;<br>yy&quot;月<br><br>&quot;<br>&quot;<br>mm&quot;<br><br>&quot;<br>m&quot; dd&quot;日<br>&quot;<br><br>&quot;<br>&quot;小时&quot;<br><br><br><br><br><br><br><br>&quot;分钟&quot;&quot;mi&quot;mi&quot;n&quot;&quot;第二&quot;&quot; | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time /<br>make_timestamp | 从部分创建日期。 | make_date_time(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| current_timestamp | 返回当前时间戳。 | current_timestamp() | 1571850624571 |
| current_date | 返回不带时间组件的当前日期。 | current_date() | 《2019年11月18日》 |