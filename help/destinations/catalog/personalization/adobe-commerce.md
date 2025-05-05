---
title: Adobe Commerce目标连接器
description: 了解Adobe Commerce和Real-Time CDP商家如何通过提供高度相关的网站内容和促销活动，针对Real-Time CDP中构建和管理的客户受众进行自定义，从而个性化购物体验。
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 3%

---

# Adobe Commerce连接 {#adobe-commerce}

## 概述 {#overview}

[!DNL Adobe Commerce]目标连接器允许您选择一个或多个要激活到您的[!DNL Adobe Commerce]帐户的Real-Time CDP受众，以便为购物者提供动态的个性化体验。 在[!DNL Adobe Commerce]内，您可以选择这些Real-Time CDP受众来个性化购物车中的独特优惠，例如“购买2 get 1免费”。 您还可以显示主页横幅，并通过促销选件修改产品定价，所有这些选件都是根据Adobe Real-Time CDP受众自定义的。

## 先决条件 {#prerequisites}

目标目录中提供了此连接器，以供已购买Real-Time CDP Prime或Ultimate和Adobe Commerce的客户使用。

要使用此目标连接，请确保您有权访问：

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started/)。 通过访问开发人员控制台，您可以查看在Adobe Commerce中[完成扩展的配置](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html?lang=zh-Hans#configure-the-extension)所需的服务帐户和凭据信息。
- [Adobe Commerce Cloud版本2.4.4或更高版本](https://business.adobe.com/products/magento/magento-commerce.html)

在Experience Platform中，创建以下内容：

- [架构](../../../xdm/schema/composition.md)。 您创建的架构表示您计划从Adobe Commerce中摄取的数据。 [了解更多](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html?lang=zh-Hans)有关如何创建包含特定于Commerce的字段组的架构。
- [数据集](../../../catalog/datasets/user-guide.md#create)。 数据集是用于数据收集的存储和管理结构。 您可以使用上面创建的架构创建此数据集。
- [数据流](../../../datastreams/overview.md#create)。 允许数据从Adobe Experience Platform流向其他Adobe DX产品的ID。 此ID必须关联到您的特定Adobe Commerce实例中的特定网站。 创建此数据流时，请指定您在上面创建的XDM架构。

完成先决条件后，连接到[!DNL Commerce]目标。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到[!DNL Adobe Commerce]目标，请执行以下操作：

1. 在[Experience Platform界面](https://experience.adobe.com/platform/)中，转到&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 目录]**。
1. 选择&#x200B;**[!UICONTROL Personalization]**。
1. 选择Adobe Commerce目标以突出显示它，然后选择&#x200B;**[!UICONTROL 设置]**。
1. 按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

- **[!UICONTROL 名称]**：填写此目标的首选名称。
- **[!UICONTROL 描述]**：输入目标的描述。 例如，您可以提及要将此目标用于哪个营销活动。 此字段为可选字段。
- **[!UICONTROL 集成别名]**：此值作为JSON对象名称发送到Experience Platform Web SDK。
- **[!UICONTROL 数据流ID]**：这决定了哪个数据收集数据流包含响应页面时包含的受众。 下拉菜单仅显示已启用目标配置的数据流。有关详细信息，请参阅[配置数据流](../../../datastreams/overview.md)。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

## 将受众激活到[!DNL Commerce]目标 {#activate}

>[!IMPORTANT]
> 
>若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

有关将受众激活到[!DNL Commerce]目标的说明，请阅读[将配置文件和受众激活到配置文件请求目标](../../ui/activate-edge-personalization-destinations.md)。

## [!DNL Adobe Commerce]中的后续步骤

现在您已在Experience Platform中配置了[!DNL Commerce]目标，您需要在[!DNL Commerce]中安装[!DNL Audience Activation]扩展并配置[!DNL Commerce Admin]以导入您创建的Real-Time CDP受众。 请参阅[[!DNL Commerce] 文档](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html?lang=zh-Hans)以了解详情。

## 验证Commerce中的Audience Activation {#exported-data}

在将Real-Time CDP受众激活到您的[!DNL Adobe Commerce]帐户后，您将看到这些受众在您转到&#x200B;_管理员_&#x200B;侧边栏，然后转到&#x200B;**[!UICONTROL 客户]** > **[!UICONTROL Real-Time CDP受众]**&#x200B;时可用。

![Real-Time CDP受众信息板](../../assets/catalog/personalization/adobe-commerce/audience-library.png)

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请阅读[数据治理概述](/help/data-governance/home.md)。
