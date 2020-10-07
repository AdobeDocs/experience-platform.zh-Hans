---
keywords: Experience Platform;home;popular topics;query service;Query service;Power BI;power bi;connect to query service;
solution: Experience Platform
title: 与Power BI连接
topic: connect
description: 此文档将逐步介绍如何将Power BI与Adobe Experience Platform查询服务相连。
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# 连接 [!DNL Power BI] (PC)

PC用户可从https://powerbi.microsoft.com/en-us/desktop/ [!DNL Power BI] 进行 [安装](https://powerbi.microsoft.com/en-us/desktop/)。

## Set up [!DNL Power BI]

安装完 [!DNL Power BI] 毕后，需要设置必要的组件以支持PostgreSQL连接器。 按照以下步骤操作：

- 查找并安 `npgsql`装一个。NET驱动程序包，用于PostgreSQL，这是PowerBI连接的正式方式。

- 选择v4.0.10（更新版本当前导致错误）。

- 在“自定义设置”屏幕的“Npgsql GAC安装”下，选 **[!UICONTROL 择“将安装在本地硬盘上”]**。 未安装GAC将导致Power BI稍后失败。

- 重新启动Windows。

- 查找桌 [!DNL PowerBI] 面评估版。

## 连接 [!DNL Power BI] 到 [!DNL Query Service]

执行这些准备步骤后，您可以连 [!DNL Power BI] 接到 [!DNL Query Service]:

- Open [!DNL Power BI].

- 单击 **[!UICONTROL 顶部菜单]** 功能区中的“获取数据”。

- 选择 **[!UICONTROL PostgreSQL数据库]**，然后单击 **[!UICONTROL “连接”]**。

- 输入服务器和数据库的值。 **[!UICONTROL 服务器]** 是在连接详细信息下找到的主机。 对于生产，请向 `:80` 主机字符串的末尾添加端口。 **[!UICONTROL 数据库]** 可以是“all”或数据集表名。 （尝试一个CTAS派生的数据集。）

- 单击 **[!UICONTROL 高级选项]**，然后取消选 **[!UICONTROL 中包括关系列]**。 请勿选中使 **[!UICONTROL 用完整层次结构导航]**。

- *(为数据库声明“all”时为可选，但建议使用* )输入SQL语句。

>[!NOTE]
>
>如果未提供SQL语句，则将 [!DNL Power BI] 预览数据库中的所有表。 对于分层数据，应使用自定义SQL语句。 如果表模式为平面，则它将使用或不使用自定义SQL语句。 复合类型尚不受支 [!DNL Power BI] 持——要从复合类型获取基元类型，您需要编写SQL语句来导出它们。

```sql
SELECT web.webPageDetails.name AS Page_Name, 
SUM(web.webPageDetails.pageviews.value) AS Page_Views 
FROM _TABLE_ 
WHERE TIMESTAMP >= to_timestamp('2018-11-20')
GROUP BY web.webPageDetails.name 
ORDER BY SUM(web.webPageDetails.pageviews.value) DESC 
LIMIT 10
```

- 选择“[!UICONTROL DirectQuery]”或“[!UICONTROL Import]”模式。 在 [!UICONTROL DirectQuery] 模式下，所有查询都将发送到以 [!DNL Query Service] 执行。 在 [!UICONTROL 导入] 模式下，数据将导入 [!DNL Power BI]。

- 单击&#x200B;**[!UICONTROL 确定]**。现在， [!DNL Power BI] 连接到 [!DNL Query Service] 并在没有错误时生成预览。 预览呈现数字列存在已知问题。 继续执行下一步。

- 单击 **[!UICONTROL 加载]** ，将数据集导入 [!DNL Power BI]。
