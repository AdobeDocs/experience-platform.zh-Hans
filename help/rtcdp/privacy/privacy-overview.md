---
keywords: data governance rtcdp;rtcdp data governance;real time customer data profile data governance;privacy rtcdp;rtcdp privacy
title: 实时客户数据用户档案中的隐私
seo-title: 实时客户数据用户档案中的隐私
description: 实时客户用户档案使您能够简化数据操作遵守隐私法规的流程。
seo-description: 实时客户用户档案使您能够简化数据操作遵守隐私法规的流程。
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---


# 实时CDP中的隐私保护

[!DNL Real-time Customer Data Platform] （实时CDP）可帮助营销人员将来自多个企业系统的数据整合在一起，使他们能够更好地识别、理解和吸引客户。 Adobe将消费者数据隐私视为一项基本的设计原则，并提供各种控件来帮助营销人员管理其客户的数据隐私。

大多数实时CDP功能由Adobe Experience Platform提供支持。 本文档提供有关实时CDP支持的各种隐私增强技术的信息，并提供文档链 [!DNL Experience Platform] 接以了解更多信息。

## [!DNL Privacy Service]

Adobe Experience Platform [!DNL Privacy Service] 允许您简化数据操作流程，使其符合隐私法规( [!DNL General Data Protection Regulation] 如(GDPR)和 [!DNL California Consumer Privacy Act] (CCPA))。 由于实时CDP利用数 [!DNL Experience Platform] 据收集和存储功能，因此应在中管理GDPR和CCPA的访问和删除请求 [!DNL Platform]。 有关服 [务的更详细介绍](../../privacy-service/home.md) ，请参阅Privacy Service概述文档。

提交个人GDPR和CCPA数据主体请求以访问和删除客户数据有两种方法：

* 使用[ [!DNLPrivacy ServiceUI]](https://gdprui.cloud.adobe.io/) ，在可视工作区中创建和监视访问和删除请求。 有关 [分步说明](../../privacy-service/ui/overview.md) ，请参阅Privacy ServiceUI教程。
* 使用 [[!DNLPrivacy ServiceAPI]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) ，通过RESTful API调用管理访问和删除请求。 有关分 [步说明](../../privacy-service/api/getting-started.md) ，请参阅Privacy ServiceAPI教程。

<!-- (Capability will not be available for November GA) 
## Opt-out capabilities

Real-time CDP provides two types of consumer opt-out capabilities:

1. **General opt-out**: (Waiting on info)
1. **Segment-level opt-out of sale**: Opt-out of sale requests are captured using the Profile Privacy mixin (see the section on "Handling opt-out requests" in the [Real-time Customer Profile overview](../../profile/home.md) for more information). Using this, you can exclude users who have opted out from a segment using boolean logic ("AND NOT") in the segment predicate.
-->

## 后续步骤

本文档简要介绍了实时CDP的隐私功能。 有关提交访问／删除请求的最佳实践和步骤的详细信息，请参阅 [Privacy Service文档](../../privacy-service/home.md)。