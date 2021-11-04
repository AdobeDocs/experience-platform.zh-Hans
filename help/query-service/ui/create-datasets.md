---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；生成数据集；生成数据集；创建数据集；
solution: Experience Platform
title: 在查询服务中根据结果生成数据集
topic-legacy: queries
type: Tutorial
description: Adobe Experience Platform查询服务允许从UI创建数据集。 创建数据集后，可以像数据湖中的任何其他数据集一样访问该数据集，并将其用于各种用例。
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# 在查询服务中根据结果生成数据集

的真正力量 [!DNL Query Service] 查询用于在中生成数据集时显示 [!DNL Data Lake] 用作输入到更多查询或其他服务(例如 [!DNL Data Science Workspace], [!DNL Real-time Customer Profile]或 [!DNL Analysis Workspace].

[!DNL Query Service] 允许从UI创建数据集。 请执行以下步骤：

1. 使用连接的客户端编写查询并验证输出。
2. 登录到 [!DNL Platform] UI，然后转到“查询”。
3. 在列表中查找查询，并将鼠标悬停在行上。
4. 选择 **[!UICONTROL 创建数据集]**. ![图像](../images/ui/create-datasets/output-dataset.png)
5. 输入一个数据集名称，前面附加有您的LDAP ID(不必唯一或SQL安全；系统会根据此处提供的名称生成“表名”)。
6. 输入数据集描述并选择 **[!UICONTROL 运行查询]**.![图像](../images/ui/create-datasets/run-query.png)
7. 观看查询结束，然后转到数据集列表页面以查看刚刚创建的数据集。

创建数据集后，可以像 [!DNL Data Lake] 和用于各种用例。

>[!NOTE]
>
>在实时实施中，必须在创建数据集后应用“数据管理”标签。

## 生成预定义的数据集 [!DNL Experience Data Model] 模式

生成预定义的数据集 [!DNL Experience Data Model] (XDM)架构，则必须使用SQL语法。 有关必须使用的语法的更多信息，请阅读 [SQL语法指南](../sql/syntax.md#create-table-as-select).

## 输出数据集

通过此功能创建的数据集是使用与SQL语句中定义的输出数据结构匹配的临时架构生成的。 某些下游服务需要具有特定 [!DNL Experience Data Model] (XDM)模式。 在编写查询之前，验证下游服务的数据格式要求。
