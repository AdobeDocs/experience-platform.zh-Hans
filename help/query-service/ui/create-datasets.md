---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；生成数据集；生成数据集；创建数据集；
solution: Experience Platform
title: 从查询结果生成输出数据集
type: Tutorial
description: Adobe Experience Platform查询服务允许从UI创建数据集。 创建数据集后，可以像数据湖中的任何其他数据集一样访问它，并将其用于各种用例。
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# 从查询结果生成输出数据集

[!DNL Query Service]允许您使用查询在[!DNL Data Lake]中生成数据集。 然后，这些数据集可以用作更多查询或其他服务（如[!DNL Data Science Workspace]、实时客户档案或[!DNL Analysis Workspace]）的输入。

## 从Adobe Experience Platform用户界面生成数据集

要从Adobe Experience Platform用户界面(UI)创建数据集，请执行以下步骤：

1. 使用连接的客户端创建查询并验证输出。 要了解如何使用[!DNL Query Editor]编写查询，请阅读有关编写查询[&#128279;](./user-guide.md#writing-queries)的[!DNL Query Editor]用户界面指南。

2. 在Experience Platform UI中，依次导航到&#x200B;**[!UICONTROL 查询]**&#x200B;和&#x200B;**[!UICONTROL 模板]**&#x200B;选项卡，然后选择您创建的查询。 有关如何在Experience Platform UI中查看为您的组织创建和保存的查询的更多详细信息，请阅读[[!DNL Query Service] 概述](./overview.md#browse)。

3. 在“查询详细信息”面板中，选择&#x200B;**[!UICONTROL 以CTAS身份运行]**。

   ![查询工作区[!UICONTROL 模板]选项卡（选择[!UICONTROL 作为CTAS运行]）突出显示。](../images/ui/create-datasets/run-as-ctas.png)

4. 在显示的对话框中，输入在LDAP ID前面加盖的数据集名称。 数据集名称不必是唯一或SQL安全的。 请注意，将根据您在此处创建的数据集名称生成数据集的表名称。

5. 接下来，在[!UICONTROL 描述]字段中输入数据集的描述，然后选择&#x200B;**[!UICONTROL 以CTAS身份运行]**。

   ![包含数据集详细信息的“输出数据集”对话框，并[!UICONTROL 作为CTAS运行]突出显示](../images/ui/create-datasets/run-query.png)

6. 查询运行完成后，导航到&#x200B;**[!UICONTROL 数据集]**&#x200B;以查看您创建的数据集。 要了解有关如何在Experience Platform UI中使用数据集时执行常见操作的更多信息，请参阅[数据集UI指南](../../catalog/datasets/user-guide.md)。

创建数据集后，可以像[!DNL Data Lake]中的任何其他数据集一样访问它，并将其用于各种用例。

>[!NOTE]
>
>在实时实施中，您必须在创建数据集之后应用“数据管理”标签。 要了解有关如何将数据使用标签应用于数据集的更多信息，请参阅[数据使用标签概述](../../data-governance/labels/overview.md)。

## 使用预定义的[!DNL Experience Data Model]架构生成数据集

使用SQL语法生成具有预定义[!DNL Experience Data Model] (XDM)架构的数据集。 有关[!DNL Query Service]支持的语法的详细信息，请参阅[SQL语法指南](../sql/syntax.md#create-table-as-select)。

## 输出数据集

通过此功能创建的数据集是使用与SQL语句中定义的输出数据结构匹配的临时模式生成的。 某些下游服务需要使用特定XDM架构的数据集。 在编写查询之前，请验证下游服务的数据格式要求。

## 后续步骤

阅读本文档后，您现在应该了解如何使用[!DNL Query Service]从Experience Platform UI生成数据集。 有关如何在Experience Platform UI中访问、写入和执行查询的更多信息，请参阅[[!DNL Query Service] UI概述](./overview.md)。
