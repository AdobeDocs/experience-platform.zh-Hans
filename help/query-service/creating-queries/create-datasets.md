---
keywords: Experience Platform;home;popular topics;query service;Query service;generate datasets;generate dataset;create dataset;
solution: Experience Platform
title: 根据查询结果生成数据集
topic: queries
type: Tutorial
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# 根据查询结果生成数据集

当查询用 [!DNL Query Service] 于生成查询中的数据集以用作输入到更多或其他服务（如、或）中时，会显 [!DNL Data Lake] 示其真 [!DNL Data Science Workspace]正的功 [!DNL Real-time Customer Profile][!DNL Analysis Workspace]能。

[!DNL Query Service] 允许从UI创建数据集。 按照以下步骤操作：

1. 使用连接的客户端编写查询并验证输出。
2. 登录UI [!DNL Platform] 并转到查询。
3. 在列表中查找查询并将鼠标悬停在行上。
4. Click **[!UICONTROL Create Dataset]**. ![图像](../images/queries/create-datasets/click-create-dataset.png)
5. 输入以您的LDAP ID为前缀的数据集名称(不必是唯一的，也不必是SQL安全的；系统根据此处给出的名称生成“表名”)。
6. 输入数据集描述，然后单击“ **[!UICONTROL 运行查询]**”。![图像](../images/queries/create-datasets/run-query.png)
7. 观看查询完成，然后转到数据集列表页以查看您刚刚创建的数据集。

创建数据集后，可以像中的任何其他数据集一样访问该数据集， [!DNL Data Lake] 并用于各种用例。

>[!NOTE]
>
>在实时实施中，必须在创 [!DNL Data Governance] 建数据集后应用标签。

## 使用预定义的模式生成数 [!DNL Experience Data Model] 据集

要生成具有预定义(XDM)模式 [!DNL Experience Data Model] 的数据集，您必须使用SQL语法。 有关您必须使用哪些语法的详细信息，请阅读《SQL语 [法指南》](../sql/syntax.md#create-table-as-select)。

## 输出数据集

通过此功能创建的模式集使用与SQL语句中定义的输出数据结构匹配的专门生成。 某些下游服务需要具有特定(XDM) [!DNL Experience Data Model] 模式的数据集。 在编写查询之前，验证下游服务的数据格式要求。