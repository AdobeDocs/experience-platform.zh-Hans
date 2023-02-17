---
title: Real-Time CDP B2B版中的相关帐户
type: Documentation
description: 有关Real-Time CDP B2BExperience Platform中相关帐户功能的概述和更多信息。
exl-id: 37fd2cdb-87c0-4e5e-9599-ad4f397f7c28
source-git-commit: 5d1488b26391d8ac758a2968194a6d070ad5b561
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 6%

---

# Real-Time CDP B2B版中的相关帐户

## 概述 {#overview}

B2B企业通常将其客户信息存储在多个系统中，每个系统仅包含相同实际业务实体的部分甚至冲突数据。 这给准确了解客户带来了巨大挑战，从而降低其B2B营销和销售工作的效率和有效性。

| ID | 名称 | 网站 | 行业 | State | Phone | 拥有具有金额的开放机会> `$1 million` |
|---|---|---|---|---|---|---|
| 1 | Acme | acme.com | 软件 | CA | (408)536-6000 |  |
| 2 | Acme | acm.com | 软件 | CA | 4085366000 | x |
| 3 | Acme Inc |  |  | CA | (408)5366000 |  |
| 4 | Acme Consulting Service | `http://www.acme.com/consulting` | 技术咨询 | 纽约 | (212)471-0904 | x |
| 5 | Acme IT |  |  | CA |  |  |

{style=&quot;table-layout:auto&quot;}

通过相关帐户， [!DNL Real-Time CDP B2B] 现在，会显示与您正在浏览的帐户类似的帐户列表。

![屏幕显示Experience PlatformUI中的相关帐户。](/help/rtcdp/b2b-ai-ml-services/assets/related-accounts-in-ui.png)

使用此功能可在Experience PlatformUI中查看帐户配置文件的相关帐户配置文件，然后将相关帐户包含在区段定义中，以扩大您的范围或在区段中应用更广泛的标准。

## 启用相关帐户服务 {#enable}

要启用服务，请选择 **[!UICONTROL 用户档案]** 在侧栏中，后跟 **[!UICONTROL 设置]**.

![Experience PlatformUI突出显示配置文件和设置。](../assets/../b2b-ai-ml-services/assets/related-account-settings.png)

选择旁边的切换开关 [!UICONTROL 启用相关帐户] 启用服务，然后选择 **[!UICONTROL 保存]**.

![帐户设置屏幕突出显示切换和保存。](../assets/../b2b-ai-ml-services/assets/related-account-toggle.png)

## 工作原理 {#how-it-works}

日常运行的机器学习作业使用分层算法根据三个因素将相似帐户配置文件聚类为组：

* 父帐户链接
* Web域
* 帐户名称

成功处理作业后，帐户配置文件组的每个成员都将标记为“相关帐户”列表。 您可以在 **相关帐户** ，并在区段定义中使用相关帐户。

有关 [配置文件扩充相关帐户作业](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).

## 如何查看相关帐户 {#how-to-view}

您可以在Experience PlatformUI中查看您正在浏览的帐户的相关帐户。

有关 [如何在UI中查找相关帐户](/help/rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab).

## 如何使用相关帐户 {#how-to-use}

您可以在分段中使用帐户和相关帐户。 是否在区段定义中使用相关帐户的决定取决于您的营销用例。 例如，您可以将相关帐户用于电子邮件营销或广告促销活动，在这些活动中，您可能会接受较低的准确性，以换取更广泛的访问。

查看 [分段示例](/help/rtcdp/segmentation/b2b.md#related-accounts) 使用相关帐户的ID。
