---
keywords: 飞艇标签；飞艇目的地
title: 飞艇标记目标
seo-title: 飞艇标记目标
description: 将Adobe受众数据无缝传递给飞艇，作为飞艇内目标的受众标签。
seo-description: 将Adobe受众数据无缝传递给飞艇，作为飞艇内目标的受众标签。
translation-type: tm+mt
source-git-commit: 95f57f9d1b3eeb0b16ba209b9774bd94f5758009
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 1%

---


# （测试版）[!DNL Airship Tags]目标{#airship-tags-destination}

>[!IMPORTANT]
>
>Adobe Experience Platform的[!DNL Airship Tags]目标当前为beta。 文档和功能可能会发生变化。

## 概述

[!DNL Airship] 是领先的客户互动平台，可帮助您在客户生命周期的每个阶段向用户提供有意义的个性化全渠道消息。

此集成将Adobe Experience Platform区段数据作为[标记](https://docs.airship.com/guides/audience/tags/)传递到[!DNL Airship]中，以进行定位或触发。

要进一步了解[!DNL Airship]，请参阅[飞艇文档](https://docs.airship.com)。


>[!TIP]
>
>此文档页面由[!DNL Airship]团队创建。 如有任何查询或更新请求，请直接与[support.airship.com](https://support.airship.com/)联系。

## 先决条件

在将您的Adobe Experience Platform区段发送到[!DNL Airship]之前，您必须：

* 在[!DNL Airship]项目中创建标记组。
* 生成用于身份验证的承载令牌。

>[!TIP]
> 
>如果尚未通过[此注册链接](https://go.airship.eu/accounts/register/plan/starter/)创建[!DNL Airship]帐户。

### 标记组

Adobe Experience Platform中的细分概念与Airship中的[Tags](https://docs.airship.com/guides/audience/tags/)相似，在实施方面略有差异。 此集成将Experience Platform段](https://experienceleague.adobe.com/docs/experience-platform/xdm/mixins/profile/segmentation.html?lang=en#mixins)中用户的[成员身份的状态映射到[!DNL Airship]标记的存在或不存在。 例如，在`xdm:status`变为`realized`的平台区段中，标记将添加到[!DNL Airship]渠道或此用户档案映射到的已命名用户。 如果`xdm:status`变为`exited`，则删除标记。

要启用此集成，请在[!DNL Airship]中创建名为`adobe-segments`的&#x200B;*标记组*。

>[!IMPORTANT]
>
>创建新标记组&#x200B;**时，请勿选中**&#x200B;显示“[!DNL Allow these tags to be set only from your server]”的单选按钮。 否则，Adobe标记集成将失败。

有关创建标记组的说明，请参阅[管理标记组](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups)。

### 承载令牌

转到[飞艇仪表板](https://go.airship.com)中的&#x200B;**[!UICONTROL 设置]**&quot; **[!UICONTROL API和集成]**，并在左侧菜单中选择&#x200B;**[!UICONTROL 令牌]**。

单击&#x200B;**[!UICONTROL 创建令牌]**。

为令牌提供用户友好名称，如“Adobe标记目标”，然后为角色选择“全部访问”。

单击&#x200B;**[!UICONTROL 创建令牌]**&#x200B;并将详细信息另存为机密信息。

## 用例

为了帮助您更好地了解应如何以及何时使用[!DNL Airship Tags]目标，以下是Adobe Experience Platform客户可通过使用此目标解决的示例使用案例。

### 用例#1

零售商或娱乐平台可以根据忠诚客户创建用户用户档案，并将这些细分传递到[!DNL Airship]，以便在移动活动上实现消息定位。

### 用例#2

当用户进入或离开Adobe Experience Platform的特定细分时，实时触发一对一消息。

例如，零售商在Platform中设置牛仔裤品牌特定细分。 现在，当某人将其牛仔裤偏好设置为特定品牌时，该零售商可以触发移动消息。

## 连接到[!DNL Airship Tags] {#connect-airship-tags}

在&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 目录]**&#x200B;中，滚动到&#x200B;**[!UICONTROL 移动互动]**&#x200B;类别。 选择&#x200B;**[!DNL Airship Tags]**，然后选择&#x200B;**[!UICONTROL 配置]**。

>[!NOTE]
>
>如果与此目标的连接已存在，您可以在目标卡上看到&#x200B;**[!UICONTROL 激活]**&#x200B;按钮。 有关&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之间差异的详细信息，请参阅目标工作区文档的[Catalog](../../ui/destinations-workspace.md#catalog)部分。

![连接到Airship标签](../../assets/catalog/mobile-engagement/airship-tags/catalog.png)

在&#x200B;**帐户**&#x200B;步骤中，如果您之前已设置到[!DNL Airship Tags]目标的连接，请选择&#x200B;**[!UICONTROL 现有帐户]**&#x200B;并选择您的现有连接。 或者，您也可以选择&#x200B;**[!UICONTROL 新帐户]**&#x200B;来设置到[!DNL Airship Tags]的新连接。 选择&#x200B;**[!UICONTROL 连接到目标]**，以使用您从[!DNL Airship]仪表板生成的载体令牌将Adobe Experience Platform连接到您的[!DNL Airship]项目。

>[!NOTE]
>
>Adobe Experience Platform支持身份验证过程中的凭据验证，如果您向[!DNL Airship]帐户输入了不正确的凭据，则会显示错误消息。 这可确保您没有使用错误的凭据完成工作流。

![连接到Airship标签](../../assets/catalog/mobile-engagement/airship-tags/connect-account.png)

确认您的凭据并将Adobe Experience Platform连接到您的[!DNL Airship]项目后，您可以选择&#x200B;**[!UICONTROL Next]**&#x200B;继续执行&#x200B;**[!UICONTROL 设置]**&#x200B;步骤。

在&#x200B;**[!UICONTROL 身份验证]**&#x200B;步骤中，为激活流输入&#x200B;**[!UICONTROL 名称]**&#x200B;和&#x200B;**[!UICONTROL 说明]**。

此外，在此步骤中，您还可以选择美国或欧盟数据中心，具体取决于哪个[!DNL Airship]数据中心适用于此目标。 最后，选择一个或多个将数据导出到目标的营销用例。 您可以从Adobe定义的营销用例中进行选择，也可以创建您自己的用例。 有关市场营销用例的详细信息，请参阅[数据使用策略概述](../../../data-governance/policies/overview.md)。

在填写上面的字段后，选择&#x200B;**[!UICONTROL 创建目标]**。

![连接到Airship标签](../../assets/catalog/mobile-engagement/airship-tags/select-domain.png)

您的目标现在已创建。 如果您希望稍后激活区段，可以选择&#x200B;**[!UICONTROL 保存并退出]**，也可以选择&#x200B;**[!UICONTROL 下一步]**&#x200B;继续工作流并选择要激活的区段。 在任一情况下，请参阅工作流其余部分的下一节[激活区段](#activate-segments)。

## 激活区段{#activate-segments}

要将区段激活到[!DNL Airship Tags]，请执行以下步骤：

在&#x200B;**[!UICONTROL 目标>浏览]**&#x200B;中，选择要激活区段的[!DNL Airship Tags]目标。

![激活流](../../assets/catalog/mobile-engagement/airship-tags/browse.png)

单击目标的名称。 此操作将带您进入激活流程。

请注意，如果目标激活流已存在，您可以看到当前发送到目标的区段。 选择右边栏中的&#x200B;**[!UICONTROL 编辑激活]**，然后按照以下步骤修改激活详细信息。

![激活流](../../assets/catalog/mobile-engagement/airship-tags/activate.png)

选择&#x200B;**[!UICONTROL 激活]**。 在&#x200B;**[!UICONTROL 激活目标]**&#x200B;工作流的&#x200B;**[!UICONTROL 选择区段]**&#x200B;页面上，选择要发送到[!DNL Airship Tags]的区段。

![细分到目标](../../assets/catalog/mobile-engagement/airship-tags/select-segments.png)

在&#x200B;**[!UICONTROL 映射]**&#x200B;步骤中，从[XDM](../../../xdm/home.md)模式中选择要映射到目标模式的属性和标识。 选择&#x200B;**[!UICONTROL 添加新映射]**&#x200B;以浏览您的模式并将其映射到相应的目标标识。

![身份映射初始屏幕](../../assets/catalog/mobile-engagement/airship-tags/identity-mapping.png)

[!DNL Airship] 可以在表示设备实例（如iPhone）的渠道上设置标记，也可以在将用户的所有设备映射到通用标识符（如客户ID）的指定用户上设置标记。如果您的模式中有纯文本（未散列化）电子邮件地址作为主要标识，请在&#x200B;**[!UICONTROL 源属性]**&#x200B;中选择电子邮件字段，并映射到右列&#x200B;**[!UICONTROL 目标标识]**&#x200B;下的[!DNL Airship]指定用户，如下所示。

![指定用户映射](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

对于应映射到渠道（即设备）的标识符，根据源映射到相应的渠道。 下图显示了如何将Google广告ID映射到[!DNL Airship] Android渠道。

![连接到飞艇标](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![签连接到飞艇标](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![签通道映射](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

在&#x200B;**[!UICONTROL 区段计划]**&#x200B;页上，当前禁用计划。 单击&#x200B;**[!UICONTROL 下一步]**&#x200B;继续执行审阅步骤。

在&#x200B;**[!UICONTROL 评论]**&#x200B;页面上，您可以看到您所做选择的摘要。 选择&#x200B;**[!UICONTROL 取消]**&#x200B;以分组流，选择&#x200B;**[!UICONTROL 返回]**&#x200B;以修改设置，或选择&#x200B;**[!UICONTROL 完成]**&#x200B;以确认您的选择并开始将数据发送到目标。

>[!IMPORTANT]
>
>在此步骤中，Adobe Experience Platform检查数据使用策略是否违反。 下面显示了违反策略的示例。 在解决违规之前，您无法完成区段激活工作流。 有关如何解决策略违规的信息，请参阅数据治理文档部分中的[策略实施](../../../data-governance/enforcement/auto-enforcement.md)。

![确认选择](../../assets/common/data-policy-violation.png)

如果未检测到任何违反策略的情况，请选择&#x200B;**[!UICONTROL 完成]**&#x200B;以确认您的选择，并开始将数据发送到目标。

![确认选择](../../assets/catalog/mobile-engagement/airship-tags/review.png)


## 数据使用和管理{#data-usage-governance}

处理数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据管理的详细信息，请参见[数据管理概述](../../../data-governance/home.md)。

