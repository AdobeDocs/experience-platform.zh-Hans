---
title: 内部网站搜索数据类型
description: 本文档概述了内部站点搜索XDM数据类型。
source-git-commit: eaea904ddda6b7ffee6f52cd4af897c2a8885714
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 5%

---

# [!UICONTROL 内部网站搜索] 数据类型

[!UICONTROL 内部网站搜索] 是一种标准的XDM数据类型，用于描述内部站点搜索，包括所有相关搜索行为和详细信息。

![](../images/data-types/internal-site-search.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `autoCompleteClicked` | [!UICONTROL 布尔型] | 指示访客是使用建议的搜索值还是自动完成的搜索值执行搜索。 |
| `autoCompleteTypedValue` | [!UICONTROL 字符串] | 对于自动完成方案，用户有时会放弃搜索并从下拉菜单中选择特定术语。 此值跟踪用户为生成一组建议的搜索词而开始键入的内容。 |
| `autoCompleteValue` | [!UICONTROL 字符串] | 对于自动完成方案，用户有时会放弃搜索并从下拉菜单中选择特定术语。 此值用于跟踪所选的特定术语。 |
| `instances` | [!UICONTROL 整数] | 内部网站搜索发生的次数。 |
| `locationInPage` | [!UICONTROL 字符串] | 当页面上存在多个搜索框时，应使用此值标识用户用于搜索的特定位置。 |
| `nullInstances` | [!UICONTROL 整数] | 内部网站搜索发生的次数，其结果为零。 |
| `numberOfResults` | [!UICONTROL 整数] | 返回的搜索结果总数。 |
| `postalCode` | [!UICONTROL 字符串] | 用于搜索的邮政编码（如果适用）。 |
| `productFindingMethods` | [!UICONTROL 字符串] | 具有促销捆绑的内部网站搜索词值。 此值指示在查看产品之前立即搜索的术语。 |
| `radiusDistance` | [!UICONTROL 整数] | 与 `radiusType`，表示搜索半径的选定距离。 |
| `radiusType` | [!UICONTROL 整数] | 所选的距离类型 `radiusDistance`，英里或公里。 |
| `refinementInstances` | [!UICONTROL 整数] | 优化内部网站搜索的次数。 |
| `refinementType` | 字符串数组 | 列出应用于搜索结果的细化类型。 示例包括部门、品牌、价格、店内、评级、颜色、材料等。 |
| `refinementValue` | [!UICONTROL 字符串] | 已优化为的值。 |
| `resultsPageNumber` | [!UICONTROL 整数] | 对于分页搜索结果，此值跟踪访客正在查看的结果页面。 |
| `resultsPerPage` | [!UICONTROL 整数] | 对于分页搜索结果，此值跟踪每页显示的搜索结果数。 |
| `searchType` | [!UICONTROL 字符串] | 捕获正在执行的搜索方法（如果适用）。 示例包括提前键入搜索、直接键入搜索或网站可能具有的任何其他类型的自定义搜索功能。 |
| `sortOrder` | [!UICONTROL 字符串] | 与 `sortType`，表示搜索结果的排序顺序（升序或降序）。 |
| `term` | [!UICONTROL 字符串] | 访客输入的内部网站搜索词。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/internal-site-search.schema.json).
