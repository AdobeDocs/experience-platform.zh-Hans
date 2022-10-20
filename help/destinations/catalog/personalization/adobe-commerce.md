---
title: (Beta)Adobe Commerce Destination Connector
description: 了解Adobe Commerce和Real-Time CDP商户如何通过提供高度相关的网站内容和促销活动(根据Real-Time CDP中构建和管理的客户区段进行自定义)来个性化购物体验。
source-git-commit: 51c5458f444220fb526eb9e82417ae6456857de6
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 1%

---

# （测试版）Adobe Commerce连接 {#adobe-commerce}

## 概述 {#overview}

>[!IMPORTANT]
> 
>的 **[!UICONTROL Adobe Commerce]** 连接器为测试版，且仅适用于选定数量的客户。

的 [!DNL Adobe Commerce] 目标连接器允许您选择一个或多个要激活到您的Experience Platform区段 [!DNL Adobe Commerce] 帐户为购物者提供动态个性化体验。 在 [!DNL Adobe Commerce]，则可以选择这些Adobe Experience Platform区段以个性化购物车中的独特选件，如“购买2获取1免费”。 您还可以显示主页横幅并通过促销优惠修改产品定价，所有这些优惠均根据Adobe Experience Platform区段进行自定义。

<!--## Use cases {#use-cases}

To help you better understand how and when you should use the *YourDestination* destination, here are sample use cases that Adobe Experience Platform customers can solve by using this destination.

### Use case #1 {#use-case-1}

*For mobile messaging platforms:*

*A home rental and sales platform wants to push mobile notifications to customers' Android and iOS devices to let them know that there are 100 updated listings in the area where they previously searched for a rental.*

### Use case #2 {#use-case-2}

*For social network platforms:*

*An athletic apparel brand wants to reach existing customers through their social media accounts. The apparel brand can ingest email addresses from their own CRM to Adobe Experience Platform, build segments from their own offline data, and send these segments to YourDestination, to display ads in their customers' social media feeds.*-->

## 先决条件 {#prerequisites}

此扩展位于目标目录中，面向已购买Real-time CDP Prime或Ultimate和Adobe Commerce的精选测试版客户。

测试版客户应有权访问：

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started/)
- [Adobe Commerce Cloud版本2.4.3或更高版本](https://business.adobe.com/products/magento/magento-commerce.html)

在Experience Platform中，创建以下内容：

- [架构](../../../xdm/schema/composition.md). 您创建的架构表示您计划从Adobe Commerce中摄取的数据。 [了解更多](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html) 关于如何创建包含特定于商务的字段组的架构。
- [数据集](../../../catalog/datasets/user-guide.md#create). 数据集是用于数据收集的存储和管理结构。 您需要使用上面创建的架构创建此数据集。
- [数据流](../../../edge/datastreams/overview.md#create). 允许数据从Adobe Experience Platform流到其他AdobeDX产品的ID。 此ID必须与您特定Adobe Commerce实例中的特定网站关联。 创建此数据流时，请指定您在上面创建的XDM架构。

完成先决条件后，请连接到 [!DNL Commerce] 目标。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

连接到 [!DNL Adobe Commerce] 目标：

1. 在 [平台界面](https://experience.adobe.com/platform/)，转到 **[!UICONTROL 目标]** > **[!UICONTROL 目录]**.
1. 选择 **[!UICONTROL 个性化]**.
1. 选择要突出显示的Adobe Commerce目标，然后选择 **[!UICONTROL 设置]**.
1. 按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 此目标中，您必须提供以下信息：

- **[!UICONTROL 名称]**:填写此目标的首选名称。
- **[!UICONTROL 描述]**:输入目标的描述。 例如，您可以提及您使用此目标的促销活动。 此字段为可选字段。
- **[!UICONTROL 集成别名]**:此值将作为JSON对象名称发送到Experience PlatformWeb SDK。
- **[!UICONTROL 数据流ID]**:这可确定区段将包含在页面响应中的数据收集数据流。 下拉菜单仅显示已启用目标配置的数据流。 请参阅 [配置数据流](../../../edge/datastreams/overview.md) 以了解更多详细信息。

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到 [!DNL Commerce] 目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

读取 [将用户档案和区段激活到用户档案请求目标](../../ui/activate-profile-request-destinations.md) 有关将受众区段激活到 [!DNL Commerce] 目标。

## 中的后续步骤 [!DNL Adobe Commerce]

现在，您已配置 [!DNL Commerce] 目标Experience Platform中，您需要配置 [!DNL Commerce Admin] 导入您创建的实时CDP区段。 请参阅 [[!DNL Commerce] 文档](https://docs.magento.com/user-guide/marketing/customer-segment-rtcdp.html) 以了解更多。

## 验证数据导出 {#exported-data}

在将Real-Time CDP区段激活到 [!DNL Adobe Commerce] 帐户，您将在 [!DNL Admin] 创建购物车价格规则时：

![Adobe Commerce管理员](../../assets/catalog/personalization/adobe-commerce/rtcdp-in-admin.png)

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，读取 [数据管理概述](/help/data-governance/home.md).
