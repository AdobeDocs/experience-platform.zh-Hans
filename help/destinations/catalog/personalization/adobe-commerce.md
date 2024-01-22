---
title: Adobe Commerce目标连接器
description: 了解Adobe Commerce和Real-Time CDP商家如何通过提供高度相关的网站内容和促销活动，针对Real-Time CDP中构建和管理的客户受众进行自定义，从而个性化购物体验。
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 3%

---

# Adobe Commerce连接 {#adobe-commerce}

## 概述 {#overview}

此 [!DNL Adobe Commerce] 目标连接器允许您选择一个或多个Real-Time CDP受众以激活到您的 [!DNL Adobe Commerce] 帐户，为购物者提供动态的个性化体验。 范围 [!DNL Adobe Commerce]之后，您可以选择这些Real-Time CDP受众来个性化购物车中的独特优惠，例如“购买2 get 1免费”。 您还可以显示主页横幅，并通过促销选件修改产品定价，所有这些选件都是根据Adobe Real-Time CDP受众自定义的。

## 先决条件 {#prerequisites}

目标目录中提供了此连接器，以供已购买Real-Time CDP Prime或Ultimate以及Adobe Commerce的客户使用。

要使用此目标连接，请确保您有权访问：

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer控制台](https://developer.adobe.com/developer-console/docs/guides/getting-started/). 通过访问开发人员控制台，您可以查看所需的服务帐户和凭据信息 [完成配置](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html#configure-the-extension) Adobe Commerce扩展的URL名称。
- [Adobe Commerce Cloud版本2.4.4或更高版本](https://business.adobe.com/products/magento/magento-commerce.html)

在Experience Platform中，创建以下内容：

- [架构](../../../xdm/schema/composition.md). 您创建的架构表示您计划从Adobe Commerce中摄取的数据。 [了解详情](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html) 有关如何创建包含特定于Commerce的字段组的架构。
- [数据集](../../../catalog/datasets/user-guide.md#create). 数据集是用于数据收集的存储和管理结构。 您可以使用上面创建的架构创建此数据集。
- [数据流](../../../datastreams/overview.md#create). 允许数据从Adobe Experience Platform流向其他AdobeDX产品的ID。 此ID必须关联到您的特定Adobe Commerce实例中的特定网站。 创建此数据流时，请指定您在上面创建的XDM架构。

完成先决条件后，连接到 [!DNL Commerce] 目标。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 查看目标]** 和 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到 [!DNL Adobe Commerce] 目标：

1. 在 [平台界面](https://experience.adobe.com/platform/)，转到 **[!UICONTROL 目标]** > **[!UICONTROL 目录]**.
1. 选择 **[!UICONTROL 个性化]**.
1. 选择要突出显示的Adobe Commerce目标，然后选择 **[!UICONTROL 设置]**.
1. 请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

同时 [设置](../../ui/connect-destination.md) 此目标必须提供以下信息：

- **[!UICONTROL 名称]**：填写此目标的首选名称。
- **[!UICONTROL 描述]**：输入目标的描述。 例如，您可以提及要将此目标用于哪个营销活动。 此字段为可选字段。
- **[!UICONTROL 集成别名]**：此值作为JSON对象名称发送到Experience PlatformWeb SDK。
- **[!UICONTROL 数据流ID]**：确定哪个数据收集数据流包含响应页面时包含的受众。 下拉菜单仅显示已启用目标配置的数据流。请参阅 [配置数据流](../../../datastreams/overview.md) 以了解更多详细信息。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将受众激活到 [!DNL Commerce] 目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

读取 [激活配置文件和受众以配置文件请求目标](../../ui/activate-edge-personalization-destinations.md) 有关将受众激活到 [!DNL Commerce] 目标。

## 中的后续步骤 [!DNL Adobe Commerce]

现在您已配置 [!DNL Commerce] 目标，您需要安装Experience Platform [!DNL Audience Activation] 中的扩展 [!DNL Commerce] 并配置 [!DNL Commerce Admin] 以导入您创建的Real-Time CDP受众。 请参阅 [[!DNL Commerce] 文档](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html) 了解更多信息。

## 验证Commerce中的受众激活 {#exported-data}

在将Real-Time CDP受众激活到您的 [!DNL Adobe Commerce] 帐户，您将看到这些受众在转到 _管理员_ 侧栏，然后转到 **[!UICONTROL 客户]** > **[!UICONTROL Real-Time CDP受众]**.

![Real-Time CDP受众功能板](../../assets/catalog/personalization/adobe-commerce/audience-library.png)

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 实施数据管理，请阅读 [数据管理概述](/help/data-governance/home.md).
