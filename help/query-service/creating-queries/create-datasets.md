---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 根据查询结果生成数据集
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# 根据查询结果生成数据集

当使用查询在数据湖中生成数据集以用作输入更多查询或其他服务(如数据科学工作区、实时客户用户档案或分析工作区)时，查询服务的真正威力就会显现出来。

查询服务允许从UI创建数据集。 按照以下步骤操作：

1. 使用连接的客户端编写查询并验证输出。
2. 登录到平台UI并转到查询。
3. 在列表中查找您的查询，并将鼠标悬停在该行上。
4. 单击 **创建数据集**。 ![图像](../images/queries/create-datasets/click-create-dataset.png)
5. 输入数据集名称，前缀有您的LDAP ID(不必是唯一的或SQL安全的；系统根据此处给出的名称生成“表名”)。
6. 输入数据集描述，然后单击“运 **行查询”**。![图像](../images/queries/create-datasets/run-query.png)
7. 观看查询完成，然后转到数据集列表页面以查看您刚刚创建的数据集。

创建数据集后，可以像在数据湖中访问任何其他数据集一样访问该数据集，并用于各种用例。

>[!NOTE] 在实时实施中，必须在创建数据集后应用“数据管理”标签。

## 使用预定义的体验数据模型模式生成数据集

要使用预定义的体验数据模型(XDM)模式生成数据集，您必须使用SQL语法。 有关您必须使用哪些语法的详细信息，请阅读《 [SQL语法指南》](../sql/syntax.md#create-table-as-select)。

## 输出数据集

通过此功能创建的数据集使用与SQL语句中定义的输出数据结构相匹配的专门模式生成。 某些下游服务需要具有特定体验数据模型(XDM)模式的数据集。 在编写查询之前，验证下游服务的数据格式要求。