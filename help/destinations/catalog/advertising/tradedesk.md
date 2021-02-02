---
keywords: 广告；贸易部门；
title: 交易台目的地
seo-title: 交易台目的地
description: '交易台是一个自助平台，可供广告购买者跨展示广告、视频和移动库存来源执行重定向和受众目标数字活动。 '
seo-description: 交易台是一个自助平台，可供广告购买者跨展示广告、视频和移动库存来源执行重定向和受众目标数字活动。
translation-type: tm+mt
source-git-commit: 95f57f9d1b3eeb0b16ba209b9774bd94f5758009
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 1%

---


# [!DNL The Trade Desk] 目标

## 概述 {#overview}

[!DNL The Trade Desk] 目标可帮助您将用户档案数据发送 [!DNL The Trade Desk]到。

[!DNL The Trade Desk] 是一个自助平台，让广告购买者跨展示广告、视频和移动库存来源执行重定向和受众目标数字活动。

要将用户档案数据发送到[!DNL The Trade Desk]，您必须先连接到目标。

## 目标规范{#destination-specs}

请注意特定于[!DNL The Trade Desk]目标的以下详细信息：

* 可以将以下[标识](../../../identity-service/namespaces.md)发送到[!DNL The Trade Desk]目标：[!DNL The Trade Desk ID]、[!DNL IDFA]、[!DNL GAID]。

## 用例 {#use-cases}

作为营销人员，我希望能够使用由[!DNL Trade Desk IDs]或设备ID构建的细分来创建重新定位或受众目标数字活动。

## 导出类型{#export-type}

**[!DNL Segment export]** -您将区段(受众)的所有成员导出到目标。

## 连接到目标{#connect-destination}

在&#x200B;**[!UICONTROL 连接]** > **[!UICONTROL 目标]**&#x200B;中，选择[!DNL The Trade Desk]，然后选择&#x200B;**[!UICONTROL 配置]**。

![配置交易台目标](../../assets/catalog/advertising/tradedesk/configure.png)

>[!NOTE]
>
>如果与此目标的连接已存在，您可以在目标卡上看到&#x200B;**[!UICONTROL 激活]**&#x200B;按钮。 有关&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之间差异的详细信息，请参阅目标工作区文档的[Catalog](../../ui/destinations-workspace.md#catalog)部分。
>
>![激活交易台目标](../../assets/catalog/advertising/tradedesk/activate.png)

在[!UICONTROL 身份验证]步骤中，您需要输入[!DNL The Trade Desk]连接详细信息：

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:将来帮助您识别此目标的描述。
* **[!UICONTROL 帐户ID]**:您的 [!DNL Trade Desk] [!UICONTROL 帐户ID]。
* **[!UICONTROL 客户端机密]**:客户 `clientSecret` 端凭据中使 [!DNL OAuth2] 用的参数。
* **[!UICONTROL 服务器位置]**:询问您的 [!DNL The Trade Desk] 代表您应使用哪个区域服务器。这些是可供选择的区域服务器：

   * **[!UICONTROL 欧洲]**
   * **[!UICONTROL 新加坡]**
   * **[!UICONTROL 东京]**
   * **[!UICONTROL 北美洲东]**
   * **[!UICONTROL 北美洲西]**
   * **[!UICONTROL 拉丁美洲]**

* **[!UICONTROL 营销用例]**:市场营销用例指明要将数据导出到目标的目的。您可以从Adobe定义的营销用例中进行选择，也可以创建自己的营销用例。 有关市场营销用例的详细信息，请参阅Adobe Experience Platform的[数据治理](../../../data-governance/policies/overview.md)页。 有关各个Adobe定义的营销用例的信息，请参阅[数据使用策略概述](../../../data-governance/policies/overview.md)。

![交易台身份验证步骤](../../assets/catalog/advertising/tradedesk/authenticate.png)

单击&#x200B;**[!UICONTROL 创建目标]**。 您的目标现在已创建。 如果要稍后激活区段，可单击[!UICONTROL 保存并退出]，也可选择[!UICONTROL 下一步]继续工作流并选择要激活的区段。 在任一情况下，请参阅工作流其余部分的下一节[激活区段](#activate-segments)。

## 激活区段{#activate-segments}

有关区段用户档案工作流的信息，请参阅[将激活和区段激活到目标](../../ui/activate-destinations.md#select-attributes)。

在[区段计划](../../ui/activate-destinations.md#segment-schedule)步骤中，您必须手动将区段映射到目标中相应的ID或友好名称。

在映射区段时，建议您使用[!DNL Platform]区段名称或更短的区段名称，以便于使用。 但是，目标中的区段ID或名称不需要与[!DNL Platform]帐户中的区段ID或名称匹配。 您在映射字段中插入的任何值都将反映在目标中。

如果您使用多个设备映射(cookie ID、[!DNL IDFA]、[!DNL GAID])，请确保对所有三个映射使用相同的映射值。 [!DNL The Trade Desk] 将所有数据聚合到单个细分中，并进行设备级细分。

![区段映射ID](../../assets/common/segment-mapping-id.png)

## 导出的数据{#exported-data}

要验证数据是否已成功导出到[!DNL The Trade Desk]目标，请检查您的[!DNL The Trade Desk]帐户。 如果激活成功，则受众将填充到您的帐户中。
