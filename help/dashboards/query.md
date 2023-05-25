---
solution: Experience Platform
title: 使用查询服务浏览、验证和处理功能板数据集
type: Documentation
description: 了解如何使用查询服务来探索和处理原始数据集，以便在Experience Platform中提升用户档案、区段和目标仪表板的性能。
exl-id: 0087dcab-d5fe-4a24-85f6-587e9ae74fb8
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 0%

---

# 使用以下方式浏览、验证和处理功能板数据集 [!DNL Query Service]

Adobe Experience Platform通过Experience PlatformUI中提供的功能板，提供有关您组织的配置文件、区段和目标数据的重要信息。 然后，您可以使用Adobe Experience Platform [!DNL Query Service] 探索、验证和处理数据湖中用于驱动这些功能板的原始数据集。

## 快速入门 [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] 支持营销人员通过使用标准SQL在Data Lake中查询数据，从他们的数据中获取见解。 [!DNL Query Service] 提供了一个用户界面和API，可用于连接数据湖中的任何数据集，并将查询结果捕获为新数据集，以用于报表、机器学习或将其摄取到Real-time Customer Profile中。

要了解有关 [!DNL Query Service] 及其在Experience Platform中的角色，请首先阅读 [[!DNL Query Service] 概述](../query-service/home.md).

## 访问可用数据集

您可以使用 [!DNL Query Service] 查询用户档案、区段和目标功能板的原始数据集。 要查看可用数据集，请在Experience PlatformUI中，选择 **数据集** 在左侧导航中打开数据集仪表板。 仪表板列出您组织的所有可用数据集。 将显示每个列出数据集的详细信息，包括其名称、数据集所遵循的架构以及最近一次摄取运行的状态。

![左侧导航中突出显示“数据集”选项卡的数据集浏览仪表板。](./images/query/browse-datasets.png)

### 系统生成的数据集

>[!IMPORTANT]
>
>默认情况下，系统生成的数据集是隐藏的。 默认情况下， [!UICONTROL 浏览] 选项卡仅显示您已将数据摄取到的数据集。

要查看系统生成的数据集，请选择过滤器图标(![过滤器图标。](./images/query/filter.png))。

![突出显示过滤器图标的数据集浏览选项卡。](./images/query/filter-datasets.png)

此时会显示一个侧栏，其中包含两个切换， [!UICONTROL 包含在配置文件中] 和 [!UICONTROL 显示系统数据集]. 选择切换 [!UICONTROL 显示系统数据集] 在数据集的可浏览列表中包含系统生成的数据集。

![突出显示显示系统数据集切换开关的数据集浏览选项卡。](./images/query/show-system-datasets.png)

### 配置文件属性数据集

配置文件仪表板分析绑定到您的组织定义的合并策略。 对于每个活动的合并策略，数据湖中都有一个可用的配置文件属性数据集。

这些数据集的命名规则是 **Profile-Snapshot-Export** 后跟系统生成的随机字母数字值。 例如：`Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`。

要了解每个配置文件快照导出数据集的完整架构，您可以预览和浏览数据集 [使用数据集查看器](../catalog/datasets/user-guide.md) 在Experience PlatformUI中。

![配置文件快照导出数据集的预览。](images/query/profile-attribute.png)

#### 将配置文件属性数据集映射到合并策略ID

分配给每个系统生成的配置文件属性数据集的字母数字值是一个随机字符串，可映射到您的组织创建的某个合并策略的合并策略ID。 每个合并策略ID与其相关配置文件属性数据集字符串的映射在 `adwh_dim_merge_policies` 数据集。

此 `adwh_dim_merge_policies` 数据集包含以下字段：

* `merge_policy_name`
* `merge_policy_id`
* `merge_policy`
* `dataset_id`

可以使用Experience Platform中的查询编辑器UI浏览此数据集。 要了解有关使用查询编辑器的更多信息，请参阅 [查询编辑器UI指南](../query-service/ui/user-guide.md).

### 区段元数据数据集

数据湖中有一个可用的区段元数据数据集，其中包含您组织的每个区段的元数据。

此数据集的命名约定是 **段定义 — 快照 — 导出** 后跟一个字母数字值。 例如：`Segmentdefinition-Snapshot-Export-acf28952-2b6c-47ed-8f7f-016ac3c6b4e7`

要了解每个区段定义快照导出数据集的完整架构，您可以预览和浏览数据集 [使用数据集查看器](../catalog/datasets/user-guide.md) 在Experience PlatformUI中。

![区段定义 — 快照 — 导出数据集的预览。](images/query/segment-metadata.png)

### 目标元数据数据集

贵组织所有已激活目标的元数据作为原始数据集在数据湖中提供。

此数据集的命名约定是 **DIM_Destination**.

要了解DIM目标数据集的完整架构，您可以预览和浏览数据集 [使用数据集查看器](../catalog/datasets/user-guide.md) 在Experience PlatformUI中。

![DIM_Destination数据集的预览。](images/query/destinations-metadata.png)

## （测试版）客户数据平台(CDP)分析报表

>[!IMPORTANT]
>
>CDP分析数据模型功能处于测试阶段。 其功能和文档可能会发生更改。

CDP分析数据模型功能可公开支持各种用户档案、目标和分段构件的分析的SQL。 您可以自定义这些SQl查询模板，以便为营销和KPI用例创建CDP报告。

CDP报告可让您深入了解用户档案数据及其与区段和目标的关系。 有关如何执行操作的详细信息，请参阅CDP分析数据模型文档 [将CDP分析数据模型应用于您的特定KPI用例](./cdp-insights-data-model.md).

## 示例查询

以下示例查询包含可用于以下示例的SQL： [!DNL Query Service] 探索、验证和处理为功能板提供支持的原始数据集。

### 按身份列出的配置文件计数

此配置文件分析提供数据集中所有合并配置文件中的身份划分。

>[!NOTE]
>
>按身份划分的配置文件总数（即为每个命名空间显示的值相加）可能高于合并的配置文件总数，因为一个配置文件可能具有多个与其关联的命名空间。 例如，如果客户在多个渠道上与您的品牌互动，则多个命名空间将与该个人客户关联。

**查询**

```sql
Select
        Key namespace,
        count(1) count_of_profiles
     from
        (
           Select
               explode(identitymap)
           from
              Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
        )
     group by
        namespace;
```

### 按区段列出的配置文件计数

此受众分析提供数据集中每个区段内合并的用户档案总数。 此数字是将区段合并策略应用于配置文件数据以将配置文件片段合并在一起，从而为区段中的每个人形成一个配置文件的结果。

```sql
Select          
        concat_ws('-', key, source_namespace) segment_id,
        count(1) count_of_profiles
      from
        (
            Select
              Upper(key) as source_namespace,
              explode(value)
            from
              (
                  Select
                    explode(Segmentmembership)
                  from
                    Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
              )
        )
      group by
      segment_id
```

## 后续步骤

通过阅读本指南，您现在可以使用 [!DNL Query Service] 执行多个查询以浏览和处理用于支持您的个人资料、区段和目标功能板的原始数据集。

要了解有关每个功能板及其量度的更多信息，请从文档导航中的可用功能板列表中选择一个功能板。
