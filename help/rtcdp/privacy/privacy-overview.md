---
title: 实时客户数据用户档案中的隐私
seo-title: 实时客户数据用户档案中的隐私
description: 实时客户数据用户档案使您能够简化数据操作遵守隐私法规的流程。
seo-description: 实时客户数据用户档案使您能够简化数据操作遵守隐私法规的流程。
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46

---


# 实时CDP中的隐私保护

实时客户数据平台（实时CDP）可帮助营销人员将来自多个企业系统的数据整合在一起，使他们能够更好地识别、理解和吸引客户。 Adobe将消费者数据隐私视为一项基本的设计原则，并提供各种控制来帮助营销人员管理其客户的数据隐私。

大多数实时CDP功能由Adobe Experience Platform提供支持。 本文档提供有关实时CDP支持的各种隐私增强技术的信息，并提供指向Experience Platform文档的链接以了解更多信息。

## 隐私服务

Adobe Experience Platform Privacy Service允许您简化数据操作遵守隐私法规(如一般数据保护规定(GDPR)和加利福尼亚消费者隐私法(CCPA))的流程。 由于实时CDP利用Experience Platform功能进行数据收集和存储，因此应在平台内管理GDPR和CCPA的访问和删除请求。 有关该 [服务的更详细介绍](../../privacy-service/home.md) ，请参阅隐私服务概述文档。

提交单个GDPR和CCPA数据主体请求以访问和删除客户数据有两种方法：

* 使用隐 [私服务UI](https://gdprui.cloud.adobe.io/) ，在可视工作区中创建和监视访问和删除请求。 有关分 [步说明，请参阅](../../privacy-service/ui/overview.md) Privacy Service UI教程。
* 使用 [Privacy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) （隐私服务API）通过RESTful API调用管理访问和删除请求。 有关分 [步说明，请参阅Privacy Service API教程](../../privacy-service/api/getting-started.md) 。

<!-- (Capability will not be available for November GA) 
## Opt-out capabilities

Real-time CDP provides two types of consumer opt-out capabilities:

1. **General opt-out**: (Waiting on info)
1. **Segment-level opt-out of sale**: Opt-out of sale requests are captured using the Profile Privacy mixin (see the section on "Handling opt-out requests" in the [Real-time Customer Profile overview](../../profile/home.md) for more information). Using this, you can exclude users who have opted out from a segment using boolean logic ("AND NOT") in the segment predicate.
-->

## 后续步骤

本文档简要介绍了实时CDP的隐私权功能。 有关提交访问／删除请求的最佳实践和步骤的更多详细信息，请参阅隐私 [服务文档](../../privacy-service/home.md)。