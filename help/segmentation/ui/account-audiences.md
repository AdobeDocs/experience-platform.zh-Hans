---
title: 帐户受众
description: 了解如何创建和使用帐户受众，以便在下游目标中定位帐户配置文件。
badgeLimitedAvailability: label="有限可用性" type="Caution"
badgeB2B: label="B2B版本" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
source-git-commit: 77ba3bd55c2f2ac217612880b83b731919aa14af
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---


# 帐户受众

>[!AVAILABILITY]
>
>帐户受众仅在 [Real-time Customer Data Platform的B2B版本](../../rtcdp/b2b-overview.md). 此外，帐户受众功能当前正在 **有限可用性**. 请联系Adobe客户关怀或您的Adobe代表，请求访问此功能。

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

## 创建受众 {#create}

要创建帐户受众，请选择 **[!UICONTROL 创建受众]** 在 [!UICONTROL 浏览] 页面。

![此 [!UICONTROL 创建受众] 按钮在帐户受众浏览页面上突出显示。](../images/ui/account-audiences/select-create-audience.png)

此时将显示“区段生成器”。 帐户属性显示在左侧导航栏中。

![此时将显示“区段生成器”。 请注意，仅显示属性。](../images/ui/account-audiences/segment-builder.png)

在创建帐户受众时，请注意，事件列在 **[!UICONTROL 人员]**，而不是作为自己的选项卡，因为这些属性与人员相关联。

![查找事件的位置，位于 [!UICONTROL 人员] 文件夹时，将高亮显示。](../images/ui/account-audiences/attributes.png)

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
