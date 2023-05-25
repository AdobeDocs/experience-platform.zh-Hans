---
title: Real-Time CDP B2B版本中的相关帐户
type: Documentation
description: 有关Experience PlatformReal-Time CDP B2B中相关帐户功能的概述和更多信息。
exl-id: 37fd2cdb-87c0-4e5e-9599-ad4f397f7c28
source-git-commit: 5d1488b26391d8ac758a2968194a6d070ad5b561
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 6%

---

# Real-Time CDP B2B版本中的相关帐户

## 概述 {#overview}

B2B企业通常将其客户信息存储在多个系统中，每个系统仅包含同一真实世界商业实体的部分甚至冲突数据。 这带来了巨大的挑战，难以准确了解客户的状况，从而降低了其B2B营销和销售工作的效率和有效性。

| ID | 名称 | 网站 | 行业 | State | Phone | 具有包含金额的未完成机会> `$1 million` |
|---|---|---|---|---|---|---|
| 1 | Acme | acme.com | 软件 | CA | (408)536-6000 |  |
| 2 | Acme | acm.com | 软件 | CA | 4085366000 | x |
| 3 | Acme Inc |  |  | CA | (408)5366000 |  |
| 4 | Acme咨询服务 | `http://www.acme.com/consulting` | 技术咨询 | NY | (212)471-0904 | x |
| 5 | Acme IT |  |  | CA |  |  |

{style="table-layout:auto"}

通过相关帐户， [!DNL Real-Time CDP B2B] 现在显示与正在浏览的帐户类似的帐户列表。

![显示Experience PlatformUI中相关帐户的屏幕。](/help/rtcdp/b2b-ai-ml-services/assets/related-accounts-in-ui.png)

使用此功能可在Experience PlatformUI中查看帐户配置文件的相关帐户配置文件，然后将相关帐户包含在区段定义中，以扩大您的影响范围或在区段中应用更广泛的标准。

## 启用相关的帐户服务 {#enable}

要启用服务，请选择 **[!UICONTROL 配置文件]** 在侧栏中，随后是 **[!UICONTROL 设置]**.

![Experience PlatformUI突出显示配置文件和设置。](../assets/../b2b-ai-ml-services/assets/related-account-settings.png)

选择旁边的切换 [!UICONTROL 启用相关帐户] 以启用该服务，然后选择 **[!UICONTROL 保存]**.

![帐户设置屏幕突出显示切换并保存。](../assets/../b2b-ai-ml-services/assets/related-account-toggle.png)

## 工作原理 {#how-it-works}

日常运行的机器学习作业使用分层算法，根据三个因素将类似的帐户配置文件聚类为不同的组：

* 父帐户链接
* Web域
* 帐户名称

成功处理作业后，帐户配置文件组的每个成员都使用“相关帐户”列表进行标记。 您可以在以下位置查看列表 **相关帐户** 帐户配置文件页中的帐户标签，并在段定义中使用相关帐户。

请参阅文档以了解有关 [配置文件扩充相关帐户作业](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).

## 如何查看相关帐户 {#how-to-view}

您可以查看在Experience PlatformUI中浏览的帐户的相关帐户。

请参阅文档以了解有关 [如何在UI中找到相关帐户](/help/rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab).

## 如何使用相关帐户 {#how-to-use}

您可以在分段中使用帐户和相关帐户。 是否要在区段定义中使用相关帐户取决于您的营销用例。 例如，您可以将相关帐户用于电子邮件营销或广告营销活动，在这些活动中，您可以接受较低的准确性以换取更广泛的访问范围。

查看 [分段示例](/help/rtcdp/segmentation/b2b.md#related-accounts) 使用相关帐户的ID。
