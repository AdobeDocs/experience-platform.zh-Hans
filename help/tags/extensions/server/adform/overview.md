---
keywords: adform集成； adform；
title: 用于未经身份验证的重定位的Adform集成
description: 此Adobe Experience Platform集成允许您根据ECID重新定位用户。
last-substantial-update: 2025-03-26T00:00:00Z
exl-id: 37eb9453-fc3c-481e-94ea-54d9b1545631
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 1%

---

# [!DNL Adform]扩展概述

[[!DNL Adform]](https://www.adformhelp.com/hc/en-us/articles/29635608709137-Use-the-Adform-S2S-Site-Tracking-Extension-With-Adobe-Experience-Cloud)扩展在Adobe Experience Platform中启用服务器端事件转发，允许广告商、媒体代理和发布者直接将数据与Adform的ID Fusion系统同步。 此集成使企业能够跨多个渠道吸引受众，提高促销活动效果，并提供量身定制的解决方案以完善数字广告策略并最大限度地提高广告支出效率。

与传统客户端跟踪不同，此扩展通过利用第一方ID(具体而言，是与Adform同步的ECID (Experience Cloud ID))，消除了对第三方Cookie的需求。 这允许无缝的受众重定向，而无需客户端JavaScript部署。

本指南介绍如何安装、配置和部署扩展，以将事件通过Adobe的Edge Network从品牌的数字资产转发到Adform，从而实现访客的无缝重定向。

## 异地重定位

通过异地重定位，您可以重新吸引访问您的网站但未转化的潜在客户。 Adform可帮助您在各种平台上触及这些受众，从而增强品牌知名度并增加转化机会。 使用此集成可以：

* 在不使用第三方Cookie的情况下重新吸引未知访客。
* 直接在ECID上激活受众，而无需使用第三方Cookie替代标识符或数字资产上的其他标记。

Adform可帮助您：

* 轻松地将ECID上表示的第一方受众转换为数字广告促销活动的可寻址ID。
* 将ECID关联到40多个可竞价ID解决方案，以针对目标受众优化您的访问范围、频率和性能。

### 通过[!DNL Adform]激活服务器端受众 {#server-side-activation}

与传统客户端ID部署不同，此集成不需要您在数字资产上部署ID供应商的解决方案。 相反，它利用已与Adform同步的ECID来启用服务器端受众激活。 主要优势包括：

* **没有客户端JavaScript部署**：您不需要管理客户端访客识别逻辑或将客户端ID解密为较长的稳定版本。
* **无缝的受众同步**： ECID将映射到Adform的内部ID图形，从而允许跨平台高效地重新定位。
* **扩展范围和重复数据删除**： ID Fusion图形将ECID连接到多个标识符，确保高质量的受众匹配。

## 先决条件 {#prerequisites}

在将Adform与Adobe集成之前，请确保满足以下先决条件：

1. **Adobe Web SDK设置**：必须实施Adobe Web SDK以便于数据收集和事件转发。

2. **CDP或连接SKU**：您必须拥有Adobe客户数据平台(CDP) Prime、Ultimate SKU或连接SKU，才能实现无缝的客户端和服务器端通信。

3. **Adobe Experience Platform Edge Network配置**：
   * 确保将Edge Network配置为支持实时事件转发以实现异地重定位。 有关详细信息，请参阅Adobe的[事件转发快速入门指南](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/tags/event-forwarding/getting-started)。
   * 此步骤对于高效地将数据发送到Adform的服务器端端点至关重要。

满足这些先决条件后，您可以继续配置和部署[!DNL Adform]扩展。

## 配置 [!DNL Adform] 扩展 {#configure-adform-extension}

要配置[!DNL Adform]扩展，请按照以下部分中列出的步骤操作。

### 安装和配置扩展

导航到事件转发UI中的[!DNL Adform extension]并输入所需的值：

| 输入 | 描述 |
| --- | --- |
| 跟踪设置ID | Adform为跟踪事件提供的唯一标识符。 |
| 全局域 | 使用`a1.adform.net`优化性能并避免区域延迟问题。 |

输入这些详细信息后保存配置。

<!-- ![Installing and configuring the Adform extension in Adobe Experience Platorm]() -->

### 定义跟踪参数

“track”操作是主要事件规则。 它根据预定义的操作触发，通常为`page load.`包括以下参数：

**必需的参数：**

| 参数 | 描述 |
| --- | --- |
| `Page Name` | 标识页面或用户操作。 |
| `User Agent` | 捕获用于受众匹配的信息。 |
| `IP Address` | 对于准确定位和重新定位至关重要。 |

**建议的参数：**

| 参数 | 描述 |
| --- | --- |
| `Page URL` | 标识页面或用户操作。 |
| `Referral URL` | 捕获用于受众匹配的信息。 |
| `ECID` | 对于准确定位和重新定位至关重要。 |
| `Source Domain` | 对于准确定位和重新定位至关重要。 |

<!-- ![Tracking parameters for Adform]() -->

### 附加规则

必须将扩展附加到规则才能正常运行。 如果未设置任何条件，请创建一个全局规则以确保该规则始终运行。

>[!NOTE]
>
>如果该扩展未触发，请验证它是否附加到Adobe Experience Platform数据收集中的有效规则。

<!-- ![Attach a rule to the Adform extension]() -->

## 验证和部署

确保已正确安装和配置该扩展，并且已映射所有必需的数据元素，包括：

* [ECID](/help/identity-service/features/ecid.md)
* 页面名称
* 反向链接URL
* 用户代理
* IP地址

输入所有必填字段并完成测试后，选择&#x200B;**生成**&#x200B;以部署扩展。

## 后续步骤

您现在应该了解Adform如何与Adobe的服务器端功能集成，并评估集成在您现有基础架构中的可行性。 有关详细信息，请参阅[Adform的官方文档](https://www.adformhelp.com/hc/en-us/articles/29635608709137-Use-the-Adform-S2S-Site-Tracking-Extension-With-Adobe-Experience-Cloud)。
