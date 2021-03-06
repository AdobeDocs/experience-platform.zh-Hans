---
title: Real-Time CDP B2B版中的相关帐户
type: Documentation
description: 有关Experience PlatformReal-time CDP B2B中相关帐户功能的概述和更多信息。
exl-id: 37fd2cdb-87c0-4e5e-9599-ad4f397f7c28
source-git-commit: 5be8eac1603f1b81e45b4c0aeace5c2017b46149
workflow-type: tm+mt
source-wordcount: '386'
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

通过相关帐户， [!DNL Real-time CDP B2B] 现在，会显示与您正在浏览的帐户类似的帐户列表。

![屏幕显示Experience PlatformUI中的相关帐户。](/help/rtcdp/b2b-ai-ml-services/assets/related-accounts-in-ui.png)

使用此功能可在Experience PlatformUI中查看帐户配置文件的相关帐户配置文件，然后将相关帐户包含在区段定义中，以扩大您的范围或在区段中应用更广泛的标准。

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
