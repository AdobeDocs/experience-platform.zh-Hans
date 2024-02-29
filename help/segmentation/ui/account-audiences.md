---
title: 帐户受众
description: 了解如何创建和使用帐户受众，以便在下游目标中定位帐户配置文件。
badgeB2B: label="B2B版本" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="B2P版本" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 047930d6-939f-4418-bbcb-8aafd2cf43ba
source-git-commit: 7d630c3673304060ad26375955602440a495f354
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 0%

---

# 帐户受众

>[!AVAILABILITY]
>
>帐户受众仅在 [Real-time Customer Data Platform的B2B版本](../../rtcdp/overview.md#rtcdp-b2b) 和 [Real-time Customer Data Platform的B2P版本](../../rtcdp/overview.md#rtcdp-b2p).

通过帐户分段，Adobe Experience Platform可让您从基于人员的受众到基于帐户的受众，全面轻松地体验营销分段。

帐户受众可用作基于帐户的目标中的输入，从而允许您在下游服务中定位这些帐户内的人员。 例如，您可以使用基于帐户的受众检索所有执行此类操作的帐户的记录 **非** 拥有首席运营官(COO)或首席营销官(CMO)职衔的人员的联系信息。

## 术语 {#terminology}

在开始使用帐户受众之前，请查看不同受众类型之间的差异：

- **帐户受众**：帐户受众是使用创建的受众 **帐户** 配置文件数据。 帐户配置文件数据可用于创建定向下游帐户内人员的受众。 有关帐户配置文件的更多信息，请阅读 [帐户个人资料概述](../../rtcdp/accounts/account-profile-overview.md).
- **人员受众**：人员受众是使用创建的受众 **客户** 配置文件数据。 客户个人资料数据可用于创建针对您企业客户群的受众。 欲知客户个人资料的更多信息，请阅读 [Real-time Customer Profile概述](../../profile/home.md).
- **潜在客户受众**：目标客户受众是使用创建的受众 **潜在客户** 配置文件数据。 Prospect配置文件数据可用于从未经身份验证的用户创建受众。 有关潜在客户配置文件的详细信息，请阅读 [潜在客户概要文件概述](../../profile/ui/prospect-profile.md).

## 访问 {#access}

要访问帐户受众，请选择 **[!UICONTROL 受众]** 在 **[!UICONTROL 帐户]** 部分。

![受众按钮在帐户部分中突出显示。](../images/ui/account-audiences/select.png)

此 [!UICONTROL 浏览] 此时将显示页面，其中包含组织的所有帐户受众的列表。

![此时将显示属于组织的帐户受众。](../images/ui/account-audiences/browse.png)

此视图列出有关受众的信息，包括名称、配置文件计数、来源、生命周期状态、创建日期和上次更新日期。

您还可以使用搜索和筛选功能快速搜索和排序特定帐户受众。 有关此功能的更多信息，请参阅 [分段UI指南](./overview.md#manage-audiences).

## 创建受众 {#create}

>[!NOTE]
>
>使用以下项目评估帐户受众 **批次** 和进行分段，并将每24小时进行一次评估。

要创建帐户受众，请选择 **[!UICONTROL 创建受众]** 在 [!UICONTROL 浏览] 页面。

![此 [!UICONTROL 创建受众] 按钮在帐户受众浏览页面上突出显示。](../images/ui/account-audiences/select-create-audience.png)

此时将显示“区段生成器”。 帐户属性和受众将显示在左侧导航栏中。 在 [!UICONTROL 属性] 选项卡，您可以同时添加平台创建和自定义属性。

![此时将显示“区段生成器”。 请注意，仅显示属性和受众。](../images/ui/account-audiences/segment-builder.png)

在创建帐户受众时，请注意，事件列在 **[!UICONTROL 人员]**，而不是作为自己的选项卡，因为这些属性与人员相关联。

![查找事件的位置，位于 [!UICONTROL 人员] 文件夹时，将高亮显示。](../images/ui/account-audiences/attributes.png)

在 [!UICONTROL 受众] 选项卡，您可以在创建自己的帐户受众时，添加先前创建的基于人员的受众以构建的。

![区段生成器中的受众选项卡会突出显示。](../images/ui/account-audiences/audiences.png)

有关使用区段生成器的更多信息，请参阅 [区段生成器UI指南](./segment-builder.md).

## 激活受众 {#activate}

>[!NOTE]
>
>只有有限数量的目标支持帐户受众。 在继续此过程之前，请确保您要激活的目标支持帐户受众。

创建帐户受众后，您可以将该受众激活到其他下游服务。

选择要激活的受众，然后选择 **[!UICONTROL 激活到目标]**.

![此 [!UICONTROL 激活到目标] 所选受众的快速操作菜单中会高亮显示按钮。](../images/ui/account-audiences/activate.png)

此 [!UICONTROL 激活目标] 页面。 有关激活过程的更多信息（包括支持的目标和有关字段映射的详细信息），请阅读 [激活帐户受众](/help/destinations/ui/activate-account-audiences.md) 教程。

## 后续步骤 {#next-steps}

阅读本指南后，您现在已更好地了解如何在Adobe Experience Platform中创建和使用帐户受众。 要了解如何在Platform中使用其他类型的受众，请阅读 [分段服务UI指南](./overview.md).

## 附录 {#appendix}

以下部分提供了有关帐户受众的其他信息。

### 帐户分段验证 {#validation}

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_eventLookbackWindow"
>title="最大回看窗口错误"
>abstract="体验事件的最大回溯时段为30天。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxDepth"
>title="最大嵌套容器深度错误"
>abstract="嵌套容器的最大深度为 **5**. 这意味着您 **无法** 创建受众时具有5个以上的嵌套容器。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxBreadth"
>title="最大规则数量错误"
>abstract="单个容器中的规则最大数量为 **5**. 这意味着你 **无法** 创建受众时，单个容器中包含五个以上的规则。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_crossEntityMaxDepth"
>title="最大跨实体金额错误"
>abstract="单个受众中可以使用的最大交叉实体数为 **5**. 跨实体是指在受众内的不同实体之间进行更改的情况。 例如，从帐户转至人员转至营销列表。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowCustomEntity"
>title="自定义实体错误"
>abstract="自定义实体为 **非** 允许。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_b2bBuiltInEntities"
>title="无效的B2B实体错误"
>abstract="仅允许使用以下B2B实体： `_xdm.context.account`， `_xdm.content.opportunity`， `_xdm.context.profile`， `_xdm.context.experienceevent`， `_xdm.context.account-person`， `_xdm.classes.opportunity-person`， `_xdm.classes.marketing-list-member`， `_xdm.classes.marketing-list`， `_xdm.context.campaign-member`、和 `_xdm.classes.campaign`."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_rhsMaxOptions"
>title="最大值错误"
>abstract="单个字段可以检查的最大值数为 **50**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowInSegmentByReference"
>title="inSegment事件错误"
>abstract="inSegment事件包括 **非** 允许。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowInSegmentByValue"
>title="inSegment事件错误"
>abstract="inSegment事件包括 **非** 允许。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowSequentialEvents"
>title="顺序事件错误"
>abstract="顺序事件包括 **非** 允许。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowMaps"
>title="映射类型属性错误"
>abstract="映射类型属性为 **非** 允许。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxNestedAggregationDepth"
>title="最大嵌套实体深度错误"
>abstract="嵌套数组的最大深度为 **5**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxObjectNestingLevel"
>title="最大嵌套对象数量错误"
>abstract="允许的最大嵌套对象数为 **10**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_generic"
>title="约束违规"
>abstract="受众违反了限制。 有关详细信息，请阅读链接的文档。"

使用帐户受众时，受众 **必须** 遵守以下限制：

>[!NOTE]
>
>以下列表显示了 **默认** 帐户受众的限制。 这些值 **五月** 根据组织管理员实施的设置进行更改。

- 体验事件的最大回顾时间范围为 **30天**.
- 嵌套容器的最大深度为 **5**.
   - 这意味着您 **无法** 创建受众时具有5个以上的嵌套容器。
- 单个容器中的规则最大数量为 **5**.
   - 这意味着您的受众 **无法** 有五个以上的规则组成您的受众。
- 可以使用的最大交叉实体数为 **5**.
   - 跨实体是指在受众内的不同实体之间进行更改的情况。 例如，从帐户转至人员转至营销列表。
- 自定义实体 **无法** 使用。
- 单个字段可以检查的最大值数为 **50**.
   - 例如，如果字段为“City Name”，则可以根据50个城市名称检查该值。
- 帐户受众 **无法** 使用 `inSegment` 事件。
- 帐户受众 **无法** 使用顺序事件。
- 帐户受众 **无法** 使用映射。
- 嵌套数组的最大深度为 **5**.
- 嵌套对象的最大数量为 **10**.
