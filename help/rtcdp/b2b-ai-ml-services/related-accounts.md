---
title: Real-Time CDP B2B版本中的相关帐户
type: Documentation
description: 有关Experience PlatformReal-Time CDP B2B中相关帐户功能的概述和更多信息。
feature: Get Started, Profiles, B2B
badgeB2B: label="B2B版本" type="Informative" url="https://helpx.adobe.com/cn/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 37fd2cdb-87c0-4e5e-9599-ad4f397f7c28
source-git-commit: 82535ec3ac2dd27e685bb591fdf661d3ab5dd2c9
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 4%

---

# Real-Time CDP B2B版本中的相关帐户

## 概述 {#overview}

B2B企业通常将其客户信息存储在多个系统中，每个系统仅包含同一真实世界商业实体的部分甚至冲突数据。 这就带来了巨大的挑战，难以准确了解客户的状况，从而降低了其B2B营销和销售工作的效率和有效性。

| ID | 名称 | 网站 | 行业 | State | 电话 | 具有金额> `$1 million`的未完成机会 |
|---|---|---|---|---|---|---|
| 1 | Acme | acme.com | 软件 | CA | (408)536-6000 |   |
| 2 | Acme | acm.com | 软件 | CA | 4085366000 | x |
| 3 | Acme Inc |   |   | CA | (408)5366000 |   |
| 4 | Acme咨询服务 | `http://www.acme.com/consulting` | 技术咨询 | 纽约 | (212)471-0904 | x |
| 5 | Acme IT |   |   | CA |   |   |

{style="table-layout:auto"}

通过相关帐户，[!DNL Real-Time CDP B2B]现在会显示与正在浏览的帐户类似的帐户列表。

![显示Experience PlatformUI中相关帐户的屏幕。](/help/rtcdp/b2b-ai-ml-services/assets/related-accounts-in-ui.png)

使用此功能可在Experience PlatformUI中查看帐户配置文件的相关帐户配置文件，然后将相关帐户包含在区段定义中，以扩大您的影响范围或在受众中应用更广泛的标准。

## 启用相关的帐户服务 {#enable}

要启用该服务，请在侧栏中选择&#x200B;**[!UICONTROL 配置文件]**，然后选择&#x200B;**[!UICONTROL 设置]**。

![Experience PlatformUI突出显示配置文件和设置。](../assets/../b2b-ai-ml-services/assets/related-account-settings.png)

选择[!UICONTROL 启用相关帐户]旁边的切换以启用该服务，然后选择&#x200B;**[!UICONTROL 保存]**。

![帐户设置屏幕突出显示切换并保存。](../assets/../b2b-ai-ml-services/assets/related-account-toggle.png)

## 工作原理 {#how-it-works}

日常运行的机器学习作业使用分层算法，根据三个因素将类似的帐户配置文件聚类为不同的组：

* 父帐户链接
* Web 域
* 帐户名称

成功处理作业后，帐户配置文件组的每个成员都将使用相关帐户列表进行标记。 您可以在“帐户配置文件”页的&#x200B;**相关帐户**&#x200B;选项卡中查看列表，并在区段定义中使用相关帐户。

有关[配置文件扩充相关帐户作业](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)的详细信息，请参阅文档。

## 如何查看相关帐户 {#how-to-view}

您可以查看在Experience PlatformUI中浏览的帐户的相关帐户。

有关[如何在UI](/help/rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)中查找相关帐户的详细信息，请参阅文档。

## 如何使用相关帐户 {#how-to-use}

您可以在分段中使用帐户和相关帐户。 是否在区段定义中使用相关帐户取决于您的营销用例。 例如，您可以将相关帐户用于电子邮件营销或广告营销活动，在这些活动中，您可以接受较低的准确性以换取更广泛的访问范围。

查看使用相关帐户的[分段示例](/help/rtcdp/segmentation/b2b.md#related-accounts)。
