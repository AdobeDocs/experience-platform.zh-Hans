---
keywords: Experience Platform；主题；热门主题；查询服务；查询服务；生成数据集；生成数据集；创建数据集；
solution: Experience Platform
title: 根据查询服务中的结果生成数据集
topic: queries
type: Tutorial
description: 'Adobe Experience Platform查询服务允许从UI创建数据集。 创建数据集后，可以像在数据湖中访问任何其他数据集一样访问该数据集，并用于各种用例。 '
translation-type: tm+mt
source-git-commit: 97dc0b5fb44f5345fd89f3f56bd7861668da9a6e
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---


# 在查询服务中根据结果生成数据集

当使用查询在[!DNL Data Lake]中生成数据集以用作更多查询或其他服务（如[!DNL Data Science Workspace]、[!DNL Real-time Customer Profile]或[!DNL Analysis Workspace]）的输入时，将显示[!DNL Query Service]的真实威力。

[!DNL Query Service] 允许从UI创建数据集。按照以下步骤操作：

1. 使用连接的客户端编写查询并验证输出。
2. 登录[!DNL Platform] UI并转到查询。
3. 在列表中查找查询并将鼠标悬停在行上。
4. 单击&#x200B;**[!UICONTROL 创建数据集]**。 ![图像](../images/ui/output-dataset.png)
5. 输入以您的LDAP ID为前缀的数据集名称(不必是唯一的，也不必是SQL安全的；系统根据此处给出的名称生成“表名”)。
6. 输入数据集描述，然后单击&#x200B;**[!UICONTROL 运行查询]**。![图像](../images/ui/run-query.png)
7. 观看查询完成，然后转到数据集列表页以查看您刚刚创建的数据集。

创建数据集后，可以像[!DNL Data Lake]中的任何其他数据集一样访问该数据集并用于各种用例。

>[!NOTE]
>
>在实时实施中，必须在创建数据集后应用[!DNL Data Governance]标签。

## 使用预定义的[!DNL Experience Data Model]模式生成数据集

要生成具有预定义[!DNL Experience Data Model](XDM)模式的数据集，必须使用SQL语法。 有关您必须使用哪些语法的详细信息，请阅读[SQL语法指南](../sql/syntax.md#create-table-as-select)。

## 输出数据集

通过此功能创建的模式集使用与SQL语句中定义的输出数据结构匹配的专门生成。 某些下游服务需要具有特定[!DNL Experience Data Model](XDM)模式的数据集。 在编写查询之前，验证下游服务的数据格式要求。