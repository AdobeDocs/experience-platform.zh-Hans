---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；生成数据集；生成数据集；创建数据集；
solution: Experience Platform
title: 从查询结果生成输出数据集
type: Tutorial
description: Adobe Experience Platform查询服务允许从UI创建数据集。 创建数据集后，可以像数据湖中的任何其他数据集一样访问该数据集，并用于各种用例。
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# 从查询结果生成输出数据集

[!DNL Query Service] 允许您使用查询在中生成数据集 [!DNL Data Lake]. 然后，这些数据集可用作更多查询或其他服务的输入，例如 [!DNL Data Science Workspace]、实时客户档案，或 [!DNL Analysis Workspace].

## 从Adobe Experience Platform用户界面生成数据集

要从Adobe Experience Platform用户界面(UI)创建数据集，请执行以下步骤：

1. 使用连接的客户端创建查询并验证输出。 要了解如何使用编写查询 [!DNL Query Editor]，请阅读 [!DNL Query Editor] UI指南 [编写查询时](./user-guide.md#writing-queries).

2. 在Platform UI中，导航到 **[!UICONTROL 查询]** 后接 **[!UICONTROL 模板]** 选项卡，然后选择已创建的查询。 有关如何在Platform UI中查看为贵组织创建和保存的查询的更多详细信息，请参阅 [[!DNL Query Service] 概述](./overview.md#browse).

3. 在“查询详细信息”面板中，选择 **[!UICONTROL 输出数据集]**.

   ![突出显示了“选择输出”数据集的“查询”工作区“模板”选项卡。](../images/ui/create-datasets/output-dataset.png)

4. 在显示的对话框中，输入以LDAP ID为前缀的数据集名称。 数据集名称不必是唯一的，也不必是SQL安全的。 请注意，将根据您在此处创建的数据集名称生成数据集的表名称。

5. 接下来，在 [!UICONTROL 描述] 字段并选择 **[!UICONTROL 运行查询]**.

   ![输出数据集对话框，其中突出显示数据集详细信息并运行查询](../images/ui/create-datasets/run-query.png)

6. 查询运行完成后，导航到 **[!UICONTROL 数据集]** 以查看您创建的数据集。 要详细了解如何在Platform UI中使用数据集时执行常见操作，请参阅 [数据集UI指南](../../catalog/datasets/user-guide.md).

创建数据集后，可以像中的任何其他数据集一样访问该数据集 [!DNL Data Lake] 用于各种用例。

>[!NOTE]
>
>在实时实施中，您必须在创建数据集后应用“数据管理”标签。 要了解有关如何将数据使用标签应用于数据集的更多信息，请参阅 [数据使用标签概述](../../data-governance/labels/overview.md).

## 使用预定义的数据集生成 [!DNL Experience Data Model] 架构

使用SQL语法生成预定义的数据集 [!DNL Experience Data Model] (XDM)架构。 有关支持的语法的更多信息 [!DNL Query Service]，请阅读 [SQL语法指南](../sql/syntax.md#create-table-as-select).

## 输出数据集

通过此功能创建的数据集是使用与SQL语句中定义的输出数据结构匹配的临时模式生成的。 某些下游服务需要具有特定XDM架构的数据集。 在编写查询之前，验证下游服务的数据格式要求。

## 后续步骤

阅读本文档后，您现在应该了解如何使用 [!DNL Query Service] 以从Platform UI生成数据集。 有关如何在Platform UI中访问、编写和执行查询的更多信息，请参阅 [[!DNL Query Service] UI概述](./overview.md).
