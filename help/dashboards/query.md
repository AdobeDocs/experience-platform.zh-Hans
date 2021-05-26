---
solution: Experience Platform
title: 探索和处理支持Experience Platform功能板的原始数据集
type: Documentation
description: 了解如何使用查询服务来探索和处理在Experience Platform中为配置文件、区段和目标功能板提供动力的原始数据集。
source-git-commit: 1facf7079213918c2ef966b704319827eaa4a53d
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 1%

---


# 使用查询服务浏览、验证和处理功能板数据集

Adobe Experience Platform通过Experience PlatformUI中提供的功能板，提供有关贵组织的配置文件、区段和目标数据的重要信息。 然后，您可以使用Adobe Experience Platform查询服务来浏览、验证和处理在数据湖中为这些功能板提供支持的原始数据集。

## 查询服务入门

Adobe Experience Platform查询服务允许使用标准SQL在数据湖中查询数据，从而支持营销人员从其数据中获得洞察。 查询服务提供了用户界面和API，可用于连接数据湖中的任何数据集，并捕获查询结果作为新数据集，以用于报告、机器学习或将摄取到实时客户配置文件中。

要进一步了解查询服务及其在Experience Platform中的角色，请首先阅读[查询服务概述](../query-service/home.md)。

## 可用的数据集

您可以使用查询服务来查询配置文件、区段和目标功能板的原始数据集。 以下各节介绍了可在数据湖中找到的原始数据集。

### 配置文件属性数据集

对于“实时客户配置文件”中的每个活动合并策略，数据湖中都有一个可用的配置文件属性数据集。

这些数据集的命名约定为&#x200B;**配置文件属性**，后跟字母数字值。 例如：`Profile Attribute 14adf268-2a20-4dee-bee6-a6b0e34616a9`

要了解每个数据集的完整架构，您可以使用Experience PlatformUI中的数据集查看器预览和浏览数据集。

### 区段元数据数据集

数据湖中有一个可用的区段元数据数据集，其中包含贵组织每个区段的元数据。

此数据集的命名约定为&#x200B;**配置文件区段定义**，后跟一个字母数字值。 例如：`Profile Segment Definition 6591ba8f-1422-499d-822a-543b2f7613a3`

要了解数据集的完整架构，您可以使用Experience PlatformUI中的数据集查看器预览和浏览该架构。

![](images/query/segment-metadata.png)

### 目标元数据数据集

您组织的所有激活目标的元数据可作为数据湖中的原始数据集使用。

此数据集的命名约定为&#x200B;**DIM_Destination**。

要了解数据集的完整架构，您可以使用Experience PlatformUI中的数据集查看器预览和浏览该架构。

![](images/query/destinations-metadata.png)

## 示例查询

以下示例查询包括示例SQL，可在查询服务中使用该示例SQL来浏览、验证和处理支持功能板的原始数据集。

### 按身份划分的用户档案计数

此配置文件分析可划分数据集中所有合并配置文件的身份。 按身份划分的用户档案总数（即将每个命名空间显示的值相加）可能大于合并的用户档案总数，因为一个用户档案可能具有与其关联的多个命名空间。 例如，如果客户在多个渠道上与您的品牌交互，则多个命名空间将与该个别客户关联。

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
              profile_attribute_14adf268-2a20-4dee-bee6-a6b0e34616a9
        )
     group by
        namespace;
```

### 按区段划分的用户档案计数

此受众分析可提供数据集中每个区段内合并用户档案的总数。 此数字是将区段合并策略应用于配置文件数据的结果，以便将配置文件片段合并在一起，为区段中的每个人形成一个配置文件。

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
                    profile_attribute_14adf268-2a20-4dee-bee6-a6b0e34616a9
              )
        )
      group by
      segment_id
```

## 后续步骤

通过阅读本指南，您现在可以使用查询服务执行多个查询，以浏览和处理为配置文件、区段和目标功能板提供支持的原始数据集。

要进一步了解每个功能板及其量度，请从文档导航的可用功能板列表中选择一个功能板。
