---
title: 受众验证
description: 了解Experience Platform如何验证您的受众，以确保它们在下游取得更好的表现。
source-git-commit: 52439e55d3c48631488b17b6b04256bcbbe37bcb
workflow-type: tm+mt
source-wordcount: '1630'
ht-degree: 1%

---


# 受众验证

在Adobe Experience Platform中编写受众定义时，受众验证提供内置的验证和护栏，以确保受众不仅准确，而且具有稳定性和可扩展性。

通过遵循受众定义最佳实践，您可以确保受众可以更快地评估，确保即使受众规模增长时逻辑仍保持高效，并降低高流量期间评估失败的风险。 优化的受众还可以提高到目标的激活速度，减少实时个性化延迟，并维护整体沙盒稳定性。

当您在区段生成器中构建受众时，Experience Platform会实时运行这些验证。 添加超过验证阈值的事件或属性时，您会在区段生成器界面中立即收到反馈。

## 验证类型 {#validation-types}

在受众上运行受众验证时，可以违反两种不同类型的结构：关键验证结构和性能优化结构。

如果违反了关键验证结构，系统将阻止您保存受众以保护沙盒的稳定性。 如果违反了性能优化构造，您将能够保存受众，但&#x200B;*强烈建议您*&#x200B;更新受众定义以避免性能问题。

## 验证检查 {#validation-checks}

目前，支持以下验证：

| 验证检查 | 类型 | 阈值 |
| ---------------- | ---- | --------- |
| 逻辑复杂性 | 关键性验证 | 受众定义包含太多查询，导致不必要的逻辑复杂性。 |
| 顺序事件 | 关键性验证 | 受众定义中有6个以上的顺序事件。 |
| 汇总计数 | 性能优化 | 受众定义中有3个以上的聚合函数。 |
| 嵌套数据 | 性能优化 | 受众定义中的嵌套数据（数组或映射数据类型）深度超过2级。 |
| 受众规模 | 性能优化 | 受众资格大小大于沙盒中配置文件总数的30%。 |

### [!BADGE 关键验证]{type=Negative}逻辑复杂性 {#logical-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_rewritescheck"
>title="查询效率警报"
>abstract="您的受众包含太多查询，这会导致不必要的逻辑复杂性。 在继续之前，请简化受众定义。"

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_cnfcomplexitycheck"
>title="逻辑复杂性"
>abstract="您的受众包含太多查询，这会导致不必要的逻辑复杂性。 在继续之前，请简化受众定义。"

逻辑复杂性验证会分析受众定义中逻辑语句(AND、OR、NOT)的结构。 具体而言，它会查找会强制系统为每个配置文件执行过多比较的受众定义。

如果您的受众定义中每个用户档案的比较次数过多，则复杂性增加会导致每个用户档案的评估速度变慢。 因此，这增加了受众评估所需的总体时间。

要避免触发此验证，请简化受众定义。 如果您无法理解自己的受众定义，则说明定义过于复杂，Experience Platform评估受众可能需要较长时间。

**示例**

假设您希望查找居住在某些州的客户。 通过检查配置文件的状态值是否与列出的45个值之一匹配，您&#x200B;_可能_&#x200B;无法高效地写入此内容，如下所示：

+++ 受众定义效率低下

```
State.equals("AL", "AK", "AZ", "AR", "CA", "CO", "CT", "DE", "FL", "GA","HI", "ID", "IL", "IN", "IA", "KS", "KY", "LA", "ME", "MD", "MA", "MI", "MN", "MS", "MO", "MT", "NE", "NV", "NH", "NJ", "NM", "NY", "NC", "ND", "OH", "OK", "OR", "PA", "RI", "SC", "SD", "TN", "TX", "UT")
```

+++

但是，通过使用not check ，您只需检查用户档案是否没有列出的5个值之一，从而提高查询效率。

+++ 高效的受众定义

```
not(State.equals("VT", "VA", "WA", "WV", "WI", "WY" ))
```

+++

或者，假设您希望在试用计划中查找加拿大客户。 另一种效率较低的方法是在您的试用计划中查找加拿大人，方法是手动逐个排除所有其它计划，并检查该配置文件是否不在任何计划中。

+++ 受众定义效率低下

```
NOT(
    plan.equals("basic") OR
    plan.equals("standard") OR
    plan.equals("premium") OR
    plan.equals("enterprise")
) AND NOT (
    region.equals("us-east") OR
    region.equals("us-west") OR
    region.equals("eu-central") OR
    region.equals("apac")
)
```

+++

相反，您应该直接，并定向要包含的特定计划。

+++ 高效的受众定义

```
plan.equals("trial") AND region.equals("canada")
```

+++

### [!BADGE 关键验证]{type=Negative}顺序事件复杂性 {#sequential-event-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_chaincountcheck"
>title="事件序列限制"
>abstract="您的受众包含太多连续事件。 受众定义中最多只能有6个顺序事件。 请先从受众定义中删除一些顺序事件，然后再继续。"

序列事件复杂性验证将序列中的序列事件数量限制为6个事件。

顺序分段是Experience Platform中计算最复杂的操作之一，因为系统需要扫描客户的体验事件的整个历史记录，按时间戳对事件进行排序，并验证指定的顺序是否与您的查询匹配。 因此，当链增长时，系统需要计算的排列数会急剧增加。

要避免触发此验证，请通过定义历程的开始、中间和结束来专注于顺序链的基础知识。 即时步骤通常隐含在最终转换中。

**示例**

假设您要定位那些查看过产品、将该产品添加到购物车并购买了它的用户。 一种效率较低的方法将检查用户路径的每个单独状态。 例如，以下查询会经历以下事件序列：登录到网站 — >搜索产品 — >查看产品页面 — >添加到购物车 — >导航到结帐 — >购买事件

+++ 受众定义效率低下

```
chain(xEvent, timestamp, [ A: WHAT(eventType = "login"), B: WHAT(eventType = "search"), C: WHAT(eventType = "productView"), D: WHAT(eventType = "addToCart"), E: WHAT(eventType = "checkout"), F: WHAT(eventType = "purchase") ])
```

+++

但是，通过将序列缩减到其开头、中间和结尾，您只需要拥有3个事件长度的事件序列，从而可以实现更高效的查询。 例如，以下查询将经过以下事件序列：查看产品页面 — >添加到购物车 — >购买事件

+++ 高效的受众定义

```
chain(xEvent, timestamp, [ A: WHAT(eventType = "productView"), B: WHAT(eventType = "addToCart"), C: WHAT(eventType = "purchase") ])
```

+++

### [!BADGE 性能优化]{type=Caution}聚合计数 {#aggregated-count}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_countaggregationcheck"
>title="计数筛选器警告"
>abstract="您的受众具有过多聚合事件。 您的受众中应最多使用3个聚合事件。 为避免出现性能问题，您应该从受众定义中删除一些聚合事件。"

聚合计数检查将受众中使用的聚合事件数限制为3个条件。

标准事件只需要找到单个匹配事件即可授予用户资格。 但是，聚合事件需要读取和分析用户的&#x200B;**整个事件历史记录**，然后才能做出决定，这会导致处理时间变慢并使用更多聚合事件。

要避免触发此验证，请仅在受众定义完全必要时使用特定计数。 例如，如果您只需要知道用户是否参与过一次，则可以使用标准“存在”逻辑，而不是使用“计数> 0”事件。

### [!BADGE 性能优化]{type=Caution}嵌套数据复杂性 {#nested-data-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_arraydepthcheck"
>title="嵌套数据警告"
>abstract="受众具有太多嵌套数据层。 您的受众中应当最多使用2层数据。 为避免出现性能问题，您应该简化受众定义。"

嵌套数据复杂性验证将受众定义中的嵌套数据数量限制为2层。

虽然Experience Platform支持使用数组和映射对象来存储复杂的数据类型，但解压缩嵌套结构以查找值需要更复杂的遍历逻辑。 数组中嵌套的数据越深，检索进行验证所需的时间就越长。

如果您经常对深嵌套属性执行分段，则可能需要联系您的数据工程团队，以将该属性复制到用户档案架构中的更高级别以便于访问。

### [!BADGE 性能优化]{type=Caution}受众规模 {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_profilestorecheck"
>title="受众规模警告"
>abstract="受众撰写的范围太广。 您应该避免编写符合沙盒中总用户档案数30%以上的受众定义。 为避免出现性能问题，您应该收紧受众定义。"

受众规模验证会检查您的受众定义是否过于宽泛，以至于您的沙盒中超过30%的总配置文件符合受众条件。

虽然Experience Platform可以处理大量受众，但受众定义过于模糊（例如“所有活跃客户”）可能会增加评估时间和激活延迟。

如果您需要创建符合您的配置文件存储区30%以上条件的受众，请确保使用灵活的受众评估进行受众的第一次评估。 通过按需评估来评估受众，可以降低大量受众对日常分段工作的整体影响。

## 后续步骤

阅读本指南后，您可以更好地了解Experience Platform如何运行自动验证以改进评估、稳定性和可扩展性。 有关使用UI创建受众的更多信息，请阅读[区段生成器文档](./ui/segment-builder.md)。

## 附录

以下附录列出了有关Experience Platform中受众验证的常见问题解答。

### 常见问题 {#faq}

**如果忽略警告并保存受众，会发生什么情况？**

+++ 回答

对于性能优化警告，将保存受众，并且系统将尝试对其进行评估。 但是，处理速度可能会显着减慢。 在极端情况下，如果数据量足够大，则分段作业可能会失败或超时，从而迫使您重新设计受众。

对于严重验证错误，您将无法保存受众。

+++

**我是否可以请求增加“顺序事件”限制？**

+++ 回答

不行。 这是一道硬护栏，旨在保护整个Experience Platform环境的稳定性。 如果您的序列需要超过6个步骤，则能够强烈指示应简化逻辑或将其划分为两个不同的受众（例如“参与”受众和“转化”受众）。

+++

**这些新验证会破坏我现有的受众吗？**

+++ 回答

这些验证在&#x200B;**创作**&#x200B;时运行。 因此，您的现有受众将继续按原样运行。 但是，如果您尝试编辑违反这些规则的现有受众，则需要先优化该受众，然后才能保存更改。

+++

**我有复杂的数据要求。 如何避免“嵌套数据”警告？**

+++ 回答

在数据建模层最好避免“嵌套数据”警告。 一些提示包括与您的数据工程团队合作以扁平化XDM架构并将关键属性（如`subscriptionStatus`和`loyaltyTier`）提升到配置文件的最上层。

+++

**这些检查是否同时适用于草稿和已发布的受众？**

+++ 回答

是，这些检查适用于Experience Platform中评估的&#x200B;*所有*&#x200B;受众。

+++
