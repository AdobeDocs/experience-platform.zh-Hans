---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Power BI连接
topic: connect
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# 使用Power BI(PC)连接

PC用户可以从https://powerbi.microsoft.com/en-us/desktop/安装Power BI [](https://powerbi.microsoft.com/en-us/desktop/)。

## 设置Power Bi

安装Power BI后，您需要设置必要的组件以支持PostgreSQL连接器。 按照以下步骤操作：

- 查找并安 `npgsql`装PowerBI连接的正式方式是PostgreSQL的。NET驱动程序包。

- 选择v4.0.10（较新版本当前会导致错误）。

- 在“自定义设置”屏幕的“Npgsql GAC安装”下，选择“ **将安装在本地硬盘上”**。 未安装GAC将导致Power BI稍后失败。

- 重新启动Windows。

- 查找PowerBI Desktop评估版。

## 将Power BI连接到查询服务

执行这些准备步骤后，您可以将Power BI连接到查询服务：

- 打开Power BI。

- 单击 **顶部菜单功能区中的** “获取数据”。

- 选择 **PostgreSQL数据库**，然后单击 **Connect**。

- 输入服务器和数据库的值。 **服务器** 是在连接详细信息下找到的主机。 对于生产，将端 `:80` 口添加到主机字符串的末尾。 **数据库** 可以是“all”或数据集表名称。 （尝试一个CTAS派生的数据集。）

- 单击“ **高级选项**”，然后取消选 **中“包括关系列”**。 请勿选中使用 **完整层次结构导航**。

- *（为数据库声明“all”时为可选，但建议使用）* 输入SQL语句。

>[!NOTE] 如果未提供SQL语句，则Power BI将预览数据库中的所有表。 对于分层数据，应使用自定义SQL语句。 如果表模式是平的，则它将使用或不使用自定义SQL语句。 Power BI尚不支持复合类型——要从复合类型中获取简单类型，您需要编写SQL语句才能导出它们。

```sql
SELECT web.webPageDetails.name AS Page_Name, 
SUM(web.webPageDetails.pageviews.value) AS Page_Views 
FROM _TABLE_ 
WHERE _ACP_YEAR=2018 AND _ACP_MONTH=11 AND _ACP_DAY=20 
GROUP BY web.webPageDetails.name 
ORDER BY SUM(web.webPageDetails.pageviews.value) DESC 
LIMIT 10
```

- 选择 **DirectQuery** 或 **Import** 模式。 在“ **导入** ”模式下，数据将以power BI导入。 在 **DirectQuery模式中** ，所有查询都将发送到查询服务以执行。

- 单击&#x200B;**确定**。现在，Power BI连接到查询服务，并在没有错误时生成预览。 预览呈现数字列存在已知问题。 继续执行下一步。

- 单击 **加载** ，将数据集导入Power BI。
