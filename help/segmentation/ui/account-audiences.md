---
title: 帐户受众
description: 了解如何创建和使用帐户受众，以便在下游目标中定位帐户配置文件。
badgeB2B: label="B2B版本" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="B2P版本" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 047930d6-939f-4418-bbcb-8aafd2cf43ba
source-git-commit: c2f9bcd9aeb0073b8b26413ec29e2dff1ee5c80d
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 27%

---

# 帐户受众

>[!AVAILABILITY]
>
>帐户受众仅在Real-time Customer Data Platform](../../rtcdp/overview.md#rtcdp-b2b)的[B2B版本和Real-time Customer Data Platform](../../rtcdp/overview.md#rtcdp-b2p)的[B2P版本中可用。

通过帐户分段，Adobe Experience Platform可让您从基于人员的受众到基于帐户的受众，全面轻松地体验营销分段。

帐户受众可用作基于帐户的目标中的输入，从而允许您在下游服务中定位这些帐户内的人员。 例如，您可以使用基于帐户的受众检索&#x200B;**没有**&#x200B;的帐户的所有记录，这些帐户具有首席运营官(COO)或首席营销官(CMO)职衔的任何人员的联系信息。

## 术语 {#terminology}

在开始使用帐户受众之前，请查看不同受众类型之间的差异：

- **帐户受众**：帐户受众是使用&#x200B;**帐户**&#x200B;配置文件数据创建的受众。 帐户配置文件数据可用于创建定向下游帐户内人员的受众。 有关帐户配置文件的详细信息，请阅读[帐户配置文件概述](../../rtcdp/accounts/account-profile-overview.md)。
- **人员受众**：人员受众是使用&#x200B;**客户**&#x200B;个人资料数据创建的受众。 客户个人资料数据可用于创建针对您企业客户群的受众。 有关客户个人资料的更多信息，请阅读[实时客户个人资料概述](../../profile/home.md)。
- **潜在客户受众**：潜在客户受众是使用&#x200B;**潜在客户**&#x200B;个人资料数据创建的受众。 Prospect配置文件数据可用于从未经身份验证的用户创建受众。 有关潜在客户配置文件的详细信息，请阅读[潜在客户配置文件概述](../../profile/ui/prospect-profile.md)。

## 访问 {#access}

要访问帐户受众，请在&#x200B;**[!UICONTROL 帐户]**&#x200B;部分中选择&#x200B;**[!UICONTROL 受众]**。

![“帐户”部分中的“受众”按钮突出显示。](../images/ui/account-audiences/select.png)

此时将显示[!UICONTROL 浏览]页面，其中显示该组织的所有帐户受众列表。

![将显示属于组织的帐户受众。](../images/ui/account-audiences/browse.png)

此视图列出有关受众的信息，包括名称、配置文件计数、来源、生命周期状态、创建日期和上次更新日期。

您还可以使用搜索和筛选功能快速搜索和排序特定帐户受众。 有关此功能的详细信息，请参阅[受众门户概述](./audience-portal.md#manage-audiences)。

## 创建受众 {#create}

>[!NOTE]
>
>帐户受众是使用&#x200B;**批次**&#x200B;分段进行评估的，每24小时进行一次评估。

要创建帐户受众，请在[!UICONTROL 浏览]页面上选择&#x200B;**[!UICONTROL 创建受众]**。

![帐户受众浏览页面上突出显示[!UICONTROL 创建受众]按钮。](../images/ui/account-audiences/select-create-audience.png)

此时将显示“区段生成器”。 帐户属性和受众将显示在左侧导航栏中。 在[!UICONTROL 属性]选项卡下，您可以添加Platform创建和自定义属性。

![将显示区段生成器。 请注意，仅显示属性和受众。](../images/ui/account-audiences/segment-builder.png)

在创建帐户受众时，请注意，事件列在&#x200B;**[!UICONTROL 人员]**&#x200B;下，而不是作为他们自己的选项卡，因为这些属性与人员相关联。

![位于[!UICONTROL People]文件夹中的查找事件的位置突出显示。](../images/ui/account-audiences/attributes.png)

在[!UICONTROL 受众]选项卡下，您可以添加之前创建的基于人员的受众，以便在创建您自己的帐户受众时构建。

![区段生成器中的“受众”选项卡高亮显示。](../images/ui/account-audiences/audiences.png)

有关使用区段生成器的更多信息，请参阅[区段生成器UI指南](./segment-builder.md)。

## 激活受众 {#activate}

>[!NOTE]
>
>只有有限数量的目标支持帐户受众。 在继续此过程之前，请确保您要激活的目标支持帐户受众。

创建帐户受众后，您可以将该受众激活到其他下游服务。

选择要激活的受众，然后&#x200B;**[!UICONTROL 激活到目标]**。

![所选受众的快速操作菜单中突出显示[!UICONTROL 激活到目标]按钮。](../images/ui/account-audiences/activate.png)

此时会显示[!UICONTROL 激活目标]页面。 有关激活过程的更多信息（包括支持的目标和字段映射的详细信息），请阅读[激活帐户受众](/help/destinations/ui/activate-account-audiences.md)教程。

## 后续步骤 {#next-steps}

阅读本指南后，您现在已更好地了解如何在Adobe Experience Platform中创建和使用帐户受众。 要了解如何在Platform中使用其他类型的受众，请阅读[分段服务UI指南](./overview.md)。

## 附录 {#appendix}

以下部分提供了有关帐户受众的其他信息。

### 帐户分段验证 {#validation}

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_eventLookbackWindow"
>title="最长回溯时段错误"
>abstract="体验事件的最长回溯时段为 30 天。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxDepth"
>title="最大嵌套容器深度错误"
>abstract="最大嵌套容器深度为 **5**。这意味着在创建受众时，您&#x200B;**无法**&#x200B;拥有五个以上的嵌套容器。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxBreadth"
>title="最大规则数量错误"
>abstract="单个容器内的最大规则数为 **5**。这意味着在创建受众时，您&#x200B;**无法**&#x200B;在单个容器中拥有五个以上的规则。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_crossEntityMaxDepth"
>title="最大跨实体数量错误"
>abstract="单个受众中可使用的跨实体的最大数量为 **5**。跨实体是指您在受众内的不同实体之间进行切换。例如，从帐户到人员再到营销列表。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowCustomEntity"
>title="自定义实体错误"
>abstract="**不**&#x200B;允许使用自定义实体。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_b2bBuiltInEntities"
>title="无效 B2B 实体错误"
>abstract="仅允许使用以下 B2B 实体：`_xdm.context.account`、`_xdm.content.opportunity`、`_xdm.context.profile`、`_xdm.context.experienceevent`、`_xdm.context.account-person`、`_xdm.classes.opportunity-person`、`_xdm.classes.marketing-list-member`、`_xdm.classes.marketing-list`、`_xdm.context.campaign-member` 和 `_xdm.classes.campaign`。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_rhsMaxOptions"
>title="最大值错误"
>abstract="可在单个字段中检查的值的最大数量为 **50**。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowInSegmentByReference"
>title="inSegment 事件错误"
>abstract="**不**&#x200B;允许使用 inSegment 事件。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowInSegmentByValue"
>title="inSegment 事件错误"
>abstract="**不**&#x200B;允许使用 inSegment 事件。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowSequentialEvents"
>title="连续事件错误"
>abstract="**不**&#x200B;允许使用连续事件。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowMaps"
>title="Map-type 属性错误"
>abstract="**不**&#x200B;允许使用 Map-type 属性。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxNestedAggregationDepth"
>title="最大嵌套实体深度错误"
>abstract="最大嵌套数组深度为 **5**。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxObjectNestingLevel"
>title="最大嵌套对象数量错误"
>abstract="允许的最大嵌套对象数量为 **10**。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_generic"
>title="约束违规"
>abstract="受众违反了约束。请参阅链接的文档以了解更多详细信息。"

使用帐户受众时，受众&#x200B;**必须**&#x200B;符合以下约束：

>[!NOTE]
>
>以下列表显示了帐户受众的&#x200B;**default**&#x200B;约束。 这些值&#x200B;**可能**&#x200B;会发生变化，具体取决于组织管理员实施的设置。

- 体验事件的最大回顾时间范围为&#x200B;**30天**。
- 嵌套容器的最大深度为&#x200B;**5**。
   - 这意味着在创建受众时，您&#x200B;**无法**&#x200B;拥有五个以上的嵌套容器。
- 单个容器中的规则最大数量为&#x200B;**5**。
   - 这意味着您的受众&#x200B;**不能**&#x200B;包含组成受众的五个以上的规则。
- 可以使用的最大交叉实体数为&#x200B;**5**。
   - 跨实体是指您在受众内的不同实体之间进行切换。例如，从帐户到人员再到营销列表。
- 无法使用自定义实体&#x200B;****。
- 可在单个字段中检查的值的最大数量为 **50**。
   - 例如，如果字段为“City Name”，则可以根据50个城市名称检查该值。
- 帐户受众&#x200B;**不能**&#x200B;使用`inSegment`事件。
- 帐户受众&#x200B;**不能**&#x200B;使用顺序事件。
- 帐户受众&#x200B;**不能**&#x200B;使用映射。
- 最大嵌套数组深度为 **5**。
- 嵌套对象的最大数量为&#x200B;**10**。
