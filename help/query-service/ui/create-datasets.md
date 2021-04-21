---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；生成数据集；生成数据集；创建数据集；
solution: Experience Platform
title: 在查询服务中根据结果生成数据集
topic-legacy: queries
type: Tutorial
description: Adobe Experience Platform 查询 Service允许从UI创建数据集。 创建数据集后，可以像Data Lake中的任何其他数据集一样访问该数据集，并用于各种用例。
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# 在查询服务中根据结果生成数据集

当使用查询在[!DNL Data Lake]中生成数据集以用作更多查询或其他服务（如[!DNL Data Science Workspace]、[!DNL Real-time Customer Profile]或[!DNL Analysis Workspace]）中的输入时，将显示[!DNL Query Service]的真正威力。

[!DNL Query Service] 允许从UI创建数据集。按照以下步骤操作：

1. 使用连接的客户端编写查询并验证输出。
2. 登录到[!DNL Platform] UI并转到查询。
3. 在列表中查找查询并将鼠标悬停在行上。
4. 单击 **[!UICONTROL Create Dataset]**。![图像](../images/ui/output-dataset.png)
5. 输入以LDAP ID为前缀的数据集名称(不必是唯一的或SQL安全的；系统根据此处提供的名称生成“表名”)。
6. 输入数据集描述，然后单击&#x200B;**[!UICONTROL Run Query]**。![图像](../images/ui/run-query.png)
7. 观看查询完成，然后转到数据集列表页以查看刚刚创建的数据集。

创建数据集后，可以像[!DNL Data Lake]中的任何其他数据集一样访问该数据集，并用于各种用例。

>[!NOTE]
>
>在实时实施中，必须在创建数据集后应用[!DNL Data Governance]标签。

## 使用预定义的[!DNL Experience Data Model]模式生成数据集

要生成具有预定义[!DNL Experience Data Model](XDM)模式的数据集，您必须使用SQL语法。 有关您必须使用哪些语法的详细信息，请阅读[SQL语法指南](../sql/syntax.md#create-table-as-select)。

## 输出数据集

通过此功能创建的模式集使用与SQL语句中定义的输出数据结构匹配的临时数据生成。 某些下游服务需要具有特定[!DNL Experience Data Model](XDM)模式的数据集。 在编写查询之前，请验证下游服务的数据格式要求。
