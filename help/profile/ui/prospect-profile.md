---
title: 目标客户配置文件
description: 了解如何使用第三方信息创建和使用潜在客户配置文件来收集有关未知客户的信息。
type: Documentation
exl-id: 194d25d6-88ae-4a7a-9b79-39120bced5c7
source-git-commit: e7c0551276d31d6809ace096c00e0dc2665090e6
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 1%

---

# 潜在客户轮廓

通过Adobe Experience Platform，无论客户在何处或何时与您的品牌互动，您都可以为其推动协调、一致且相关的体验。

潜在客户配置文件用于表示尚未与您的公司联系但您想联系的人员。 利用潜在客户配置文件，您可以使用来自可信第三方合作伙伴的属性来补充您的客户配置文件。

## 浏览 {#browse}

要访问目标客户配置文件，请在&#x200B;**[!UICONTROL 目标客户]**&#x200B;部分中选择&#x200B;**[!UICONTROL 配置文件]**。

显示&#x200B;**[!UICONTROL 浏览]**&#x200B;页面。 此时将显示您组织的所有潜在客户配置文件的列表。

![已突出显示[!UICONTROL 配置文件]按钮，显示目标客户配置文件的[!UICONTROL 浏览]页面。](../images/prospect-profile/browse-profiles.png)

>[!IMPORTANT]
>
>虽然客户配置文件与潜在客户配置文件之间的大多数浏览功能相同，但您&#x200B;**无法**&#x200B;按合并策略浏览潜在客户配置文件。 这是因为潜在客户配置文件自动受系统设计的基于时间的合并策略的控制。 有关合并策略的详细信息，请参阅[合并策略概述](../merge-policies/overview.md)。

有关浏览配置文件的详细信息，请参阅配置文件用户指南](./user-guide.md#browse-identity)的[浏览部分。

## 目标客户配置文件详细信息 {#profile-details}

>[!IMPORTANT]
>
>在Adobe Experience Platform中驻留25天后，潜在客户配置文件将自动过期。

要查看有关特定目标客户配置文件的详细信息，请在[!UICONTROL 浏览]页面上选择一个配置文件。

![在浏览页面上突出显示目标客户配置文件。](../images/prospect-profile/select-specific-profile.png)

此时将显示有关目标客户用户档案的信息，包括与用户档案和受众成员资格关联的属性。

![将显示目标客户配置文件详细信息页面。](../images/prospect-profile/profile-details.png)

有关这些选项卡的详细信息，请阅读配置文件用户指南](./user-guide.md#profile-detail)的[查看配置文件详细信息部分。

您还可以通过选择&#x200B;**[!UICONTROL 查看JSON]**&#x200B;查看JSON格式的所有属性。

![目标客户配置文件详细信息页面上突出显示[!UICONTROL 查看JSON]按钮。](../images/prospect-profile/profile-select-view-json.png)

出现[!UICONTROL 查看JSON]对话框。 潜在客户配置文件的属性现在显示为JSON表单。

![目标客户配置文件的属性以JSON形式显示。](../images/prospect-profile/profile-view-json.png)

## 建议的用例 {#use-cases}

要了解如何在Experience Platform中将目标客户配置文件功能与其他Platform功能结合使用，请阅读以下用例文档：

- [通过潜在客户发现功能吸引和赢取新客户](../../rtcdp/partner-data/prospecting.md)

## 后续步骤

阅读本指南后，您现在了解了如何在Adobe Experience Platform中使用潜在客户配置文件。 要了解如何在受众中使用这些潜在客户配置文件，请阅读[潜在客户受众指南](../../segmentation/types/prospect-audiences.md)。
