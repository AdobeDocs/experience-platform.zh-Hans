---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 根据查询结果生成数据集
topic: queries
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---


# 根据查询结果生成数据集

当查询被用于生成数据湖中的数据集以用于输入更多查询或其他服务(如数据科学工作区、实时客户用户档案或Analysis Workspace)时，查询服务的真正威力就会被揭示出来。

查询服务允许从UI创建数据集。 按照以下步骤操作：

1. 使用连接的客户端编写查询并验证输出。
2. 登录到平台UI并转到查询。
3. 在列表中查找查询并将鼠标悬停在行上。
4. 单击 **创建数据集**。 ![图像](../images/queries/create-datasets/click-create-dataset.png)
5. 输入以您的LDAP ID为前缀的数据集名称(不必是唯一的，也不必是SQL安全的； 系统根据此处给出的名称生成“表名”)。
6. 输入数据集描述，然后单击“ **运行查询**”。![图像](../images/queries/create-datasets/run-query.png)
7. 观看查询完成，然后转到数据集列表页以查看您刚刚创建的数据集。

创建数据集后，可以像数据湖中的任何其他数据集一样访问该数据集，并用于各种用例。

>[!NOTE]
>
>在实时实施中，必须在创建数据集后应用“数据管理”标签。

## 使用预定义的体验数据模型模式生成数据集

要使用预定义的体验数据模型(XDM)模式生成数据集，您必须使用SQL语法。 有关您必须使用哪些语法的详细信息，请阅读《SQL语 [法指南》](../sql/syntax.md#create-table-as-select)。

## 输出数据集

通过此功能创建的模式集使用与SQL语句中定义的输出数据结构匹配的专门生成。 某些下游服务需要具有特定体验数据模型(XDM)模式的数据集。 在编写查询之前，验证下游服务的数据格式要求。