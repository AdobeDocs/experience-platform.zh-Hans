---
solution: Experience Platform
title: 使用查询服务浏览、验证和处理功能板数据集
type: Documentation
description: 了解如何使用查询服务在Experience Platform中探索和处理为配置文件、受众和目标仪表板提供支持的原始数据集。
exl-id: 0087dcab-d5fe-4a24-85f6-587e9ae74fb8
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 0%

---

# 使用[!DNL Query Service]浏览、验证和处理仪表板数据集

Adobe Experience Platform通过Experience PlatformUI中提供的功能板，可提供有关贵组织配置文件、受众和目标数据的重要信息。 然后，您可以使用Adobe Experience Platform [!DNL Query Service]浏览、验证和处理为数据湖中的这些仪表板提供支持的原始数据集。

## [!DNL Query Service] 入门

Adobe Experience Platform [!DNL Query Service]支持营销人员通过使用标准SQL查询Data Lake中的数据，从而从其数据中获得见解。 [!DNL Query Service]提供了一个用户界面和API，可用于加入数据湖中的任何数据集，并将查询结果捕获为新数据集，以用于报表、机器学习或将其摄取到实时客户个人资料中。

要了解有关[!DNL Query Service]及其在Experience Platform中的角色的更多信息，请先阅读[[!DNL Query Service] 概述](../query-service/home.md)。

## 访问可用数据集

您可以使用[!DNL Query Service]查询个人资料、受众和目标仪表板的原始数据集。 要查看您的可用数据集，请在Experience PlatformUI中，在左侧导航中选择&#x200B;**数据集**&#x200B;以打开数据集仪表板。 仪表板列出您组织的所有可用数据集。 将显示每个列出数据集的详细信息，包括其名称、数据集所遵循的架构以及最近一次摄取运行的状态。

![左侧导航中突出显示“数据集”选项卡的数据集浏览仪表板。](./images/query/browse-datasets.png)

### 系统生成的数据集 {#system-generated-datasets}

>[!IMPORTANT]
>
>默认情况下，系统生成的数据集处于隐藏状态。 默认情况下，[!UICONTROL 浏览]选项卡仅显示您已将数据摄取到的数据集。

要查看系统生成的数据集，请选择过滤器图标（![A过滤器图标）。](/help/images/icons/filter.png))。

![突出显示筛选器图标的数据集浏览选项卡。](./images/query/filter-datasets.png)

出现一个侧栏，其中包含两个切换：[!UICONTROL 包含在配置文件]和[!UICONTROL 显示系统数据集]。 选择[!UICONTROL 显示系统数据集]的切换按钮，将系统生成的数据集包含在数据集的可浏览列表中。

![突出显示显示系统数据集切换的“数据集浏览”选项卡。](./images/query/show-system-datasets.png)

### 配置文件属性数据集 {#profile-attribute-datasets}

配置文件仪表板分析绑定到您的组织定义的合并策略。 对于每个活动合并策略，数据湖中都有一个可用的配置文件属性数据集。

这些数据集的命名约定是&#x200B;**Profile-Snapshot-Export**，后跟系统生成的随机字母数值。 例如： `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`。

要了解每个配置文件快照导出数据集的完整架构，您可以使用Experience PlatformUI中的数据集查看器[&#128279;](../catalog/datasets/user-guide.md)预览和浏览数据集。

![配置文件快照导出数据集的预览。](images/query/profile-attribute.png)

#### 将配置文件属性数据集映射到合并策略ID

分配给每个系统生成的配置文件属性数据集的字母数字值是一个随机字符串，可映射到您的组织创建的某个合并策略的合并策略ID。 在`adwh_dim_merge_policies`数据集中维护了每个合并策略ID与其相关配置文件属性数据集字符串的映射。

`adwh_dim_merge_policies`数据集包含以下字段：

* `merge_policy_name`
* `merge_policy_id`
* `merge_policy`
* `dataset_id`

可以使用Experience Platform中的查询编辑器UI浏览此数据集。 要了解有关使用查询编辑器的更多信息，请参阅[查询编辑器UI指南](../query-service/ui/user-guide.md)。

### 受众元数据数据集

数据湖中有一个可用的受众元数据数据集，其中包含您组织的每个受众的元数据。

此数据集的命名约定是&#x200B;**Segmentdefinition-Snapshot-Export**，后跟一个字母数字值。 例如：`Segmentdefinition-Snapshot-Export-acf28952-2b6c-47ed-8f7f-016ac3c6b4e7`

要了解每个区段定义快照导出数据集的完整架构，您可以在Experience PlatformUI中使用数据集查看器[&#128279;](../catalog/datasets/user-guide.md)预览和浏览数据集。

### 目标元数据数据集

您组织的所有激活目标的元数据将作为数据湖中的原始数据集提供。

此数据集的命名约定是&#x200B;**DIM_Destination**。

要了解DIM目标数据集的完整架构，您可以在Experience PlatformUI中使用数据集查看器[&#128279;](../catalog/datasets/user-guide.md)预览和浏览数据集。

![DIM_Destination数据集的预览。](images/query/destinations-metadata.png)

## 客户数据平台(CDP)分析报表

CDP分析数据模型功能会公开支持各种个人资料、目标和分段构件的分析的SQL。 您可以自定义这些SQl查询模板，以便为营销和KPI用例创建CDP报告。

CDP报告可提供有关您的配置文件数据及其与受众和目标的关系的见解。 有关如何[将CDP分析数据模型应用于特定KPI用例](./data-models/cdp-insights-data-model-b2c.md)的详细信息，请参阅CDP分析数据模型文档。

## 示例查询

以下示例查询包括可在[!DNL Query Service]中使用的示例SQL，用于浏览、验证和处理为仪表板提供支持的原始数据集。

### 按身份列出的配置文件计数

此配置文件分析提供数据集中所有合并配置文件中的身份细分。

>[!NOTE]
>
>按身份划分的配置文件总数（也就是为每个命名空间显示的值相加）可能高于合并的配置文件总数，因为一个配置文件可能具有多个与其关联的命名空间。 例如，如果客户在多个渠道上与您的品牌互动，则多个命名空间将与该个人客户关联。

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

### 按受众列出的配置文件计数

此受众分析提供数据集中每个受众中合并的用户档案总数。 此数字是将受众合并策略应用于配置文件数据以将配置文件片段合并在一起，从而形成受众中每个人的单个配置文件的结果。

```sql
Select          
        concat_ws('-', key, source_namespace) audience_id,
        count(1) count_of_profiles
      from
        (
            Select
              Upper(key) as source_namespace,
              explode(value)
            from
              (
                  Select
                    explode(Audiencemembership)
                  from
                    Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
              )
        )
      group by
      audience_id
```

## 后续步骤

通过阅读本指南，您现在可以使用[!DNL Query Service]执行多个查询以浏览和处理原始数据集，从而支持您的个人资料、受众和目标仪表板。

要了解有关每个功能板及其量度的更多信息，请从文档导航中的可用功能板列表中选择一个功能板。
