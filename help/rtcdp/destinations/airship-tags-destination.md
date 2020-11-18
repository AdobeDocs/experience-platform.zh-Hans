---
keywords: airship tags;airship destination
title: 飞艇标记目标
seo-title: 飞艇标记目标
description: 将Adobe受众数据无缝传递给飞艇，作为飞艇内目标的受众标签。
seo-description: 将Adobe受众数据无缝传递给飞艇，作为飞艇内目标的受众标签。
translation-type: tm+mt
source-git-commit: 4b1bf5bbce57a22529c5d025c5bae10557400d54
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 1%

---


# （测试版）目 [!DNL Airship Tags] 标 {#airship-tags-destination}

>[!IMPORTANT]
>
>Adobe Experience Platform [!DNL Airship Tags] 的目的地目前处于测试阶段。 文档和功能可能会发生变化。

## 概述

[!DNL Airship] 是领先的客户互动平台，可帮助您在客户生命周期的每个阶段向用户提供有意义的个性化全渠道消息。

此集成将Adobe Experience Platform区段数据作 [!DNL Airship] 为标 [记传](https://docs.airship.com/guides/audience/tags/) 递给目标或触发。

要了解有关的更 [!DNL Airship]多信息，请参 [阅Airship Docs](https://docs.airship.com)。


>[!TIP]
>
>此文档页面由团队创 [!DNL Airship] 建。 如有任何查询或更新请求，请直接通过 [support.airship.com与他们联系](https://support.airship.com/)。

## 先决条件

在将您的Adobe Experience Platform区段发送 [!DNL Airship]到之前，您必须：

* 在项目中创建标记 [!DNL Airship] 组。
* 生成用于身份验证的承载令牌。

>[!TIP]
> 
>如果您尚 [!DNL Airship] 未通过 [此注册链接](https://go.airship.eu/accounts/register/plan/starter/) ，请创建帐户。

### 标记组

Adobe Experience Platform中的细分概念与Airship中的 [标签](https://docs.airship.com/guides/audience/tags/) 相似，在实施方面略有差异。 此集成将Experience Platform区段中用户 [成员资格的状态映射](https://experienceleague.adobe.com/docs/experience-platform/xdm/mixins/profile/segmentation.html?lang=en#mixins) ，以指示标记是否存在 [!DNL Airship] 。 例如，在更改为的平台区 `xdm:status` 段中， `realized`标记会添加到此渠道映射到的 [!DNL Airship] 用户档案或指定用户。 如果更 `xdm:status` 改为 `exited`，则删除标记。

要启用此集成，请在 *名称中创建*[!DNL Airship] 标记组 `adobe-segments`。

>[!IMPORTANT]
>
>创建新标记组时， **请勿选中** “”单选按钮[!DNL Allow these tags to be set only from your server]。 否则，Adobe标记集成将失败。

有关 [创建标记组的说](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) 明，请参阅管理标记组。

### 承载令牌

1. 转到 **[!UICONTROL Airship]** 仪表板 **[!UICONTROL 中的]** “设置 [”“API和集](https://go.airship.com) 成”，然 **[!UICONTROL 后在左侧菜]** 单中选择令牌。
1. 单击 **[!UICONTROL 创建令牌]**。
1. 为令牌提供用户友好名称，如“Adobe标记目标”，然后为角色选择“全部访问”。
1. 单击 **[!UICONTROL 创建令牌]** ，并将详细信息保存为机密。


## 用例

为了帮助您更好地了解如何以及何时使用目标， [!DNL Airship Tags] 以下是Adobe Experience Platform客户可通过使用此目标解决的示例使用案例。

### 用例#1

零售商或娱乐平台可以根据忠诚度客户创建用户用户档案，并将这些细分传递到移动 [!DNL Airship] 活动上进行消息定位。

### 用例#2

当用户进入或离开Adobe Experience Platform的特定细分时，实时触发一对一消息。

例如，零售商在Platform中设置牛仔裤品牌特定细分。 现在，当某人将其牛仔裤偏好设置为特定品牌时，该零售商可以触发移动消息。

## 连接到 [!DNL Airship Tags] {#connect-airship-tags}

1. 在“ **[!UICONTROL 目标]** ”>“ **[!UICONTROL 目录]**”中 **[!UICONTROL ，滚动至“移]** 动互动”类别。 选择 **[!DNL Airship Tags]**，然后选择 **[!UICONTROL 配置]**。

   >[!NOTE]
   >
   >如果与此目标的连接已存在，您可以在目标卡 **[!UICONTROL 上看到]** “激活”按钮。 有关激活和配置之 **[!UICONTROL 间差异]** 的详 **[!UICONTROL 细信]**&#x200B;息，请参 [阅目标工](/help/rtcdp/destinations/destinations-workspace.md#catalog) 作区文档的“目录”部分。

   ![连接到Airship标签](/help/rtcdp/destinations/assets/airship-tags-in-catalog.png)

2. 在“帐 **户** ”步骤中，如果之前已设置到目标的连接，请选择“现有 [!DNL Airship Tags] 帐户 **** ”，然后选择现有连接。 或者，您也可以选 **[!UICONTROL 择“新建帐户]** ”来设置新连接 [!DNL Airship Tags]。 选 **[!UICONTROL 择连接到目标]** ，以使用您从 [!DNL Airship] 仪表板生成的载体令牌将Adobe Experience Platform连接到您的 [!DNL Airship] 项目。

   >[!NOTE]
   >
   >Adobe Experience Platform支持身份验证过程中的凭据验证，如果您向您的帐户输入了不正确的凭据，则会显示错误 [!DNL Airship] 消息。 这可确保您没有使用错误的凭据完成工作流。

   ![连接到Airship标签](/help/rtcdp/destinations/assets/airshiptags1-connect-account.png)

3. 确认您的凭据并将Adobe Experience Platform连接到您的 [!DNL Airship] 项目后，您可以选 **[!UICONTROL 择]** “下一步 **[!UICONTROL ”以继续]** 设置步骤。

4. 在验 **[!UICONTROL 证步]** 骤中，输入 **[!UICONTROL 激活流]** 的名 **[!UICONTROL 称和]** 说明。 <br> 此外，在此步骤中，您还可以选择美国或欧盟数据中心，具体取决于 [!DNL Airship] 哪个数据中心适用于此目标。 最后，选择一个或多个将数据导出到目标的营销用例。 您可以从Adobe定义的营销用例中进行选择，也可以创建您自己的用例。 有关营销使用案例的更多信息， [请参阅实时CDP中的数据管理](/help/rtcdp/privacy/data-governance-overview.md#destinations) 。 有关各个Adobe定义的营销用例的信息，请参阅数据 [使用策略概述](/help/data-governance/policies/overview.md#core-actions)。 <br> 在 **[!UICONTROL 填写上面]** 的字段后，选择创建目标。

   ![连接到Airship标签](/help/rtcdp/destinations/assets/airshiptags2-select-domain.png)

5. 您的目标现在已创建。 如果要稍后 **[!UICONTROL 激活区段]** ，则可以选择保存并退出 **[!UICONTROL ，也可以选择下一步继续工作]** 流，然后选择要激活的区段。 无论哪种情况，在工作流的 [其余部分](#activate-segments)，请参阅下一节激活区段。

## 激活区段 {#activate-segments}

要将区段激活 [!DNL Airship Tags]到，请执行以下步骤：

1. 在“ **[!UICONTROL 目标”>]**“浏览” [!DNL Airship Tags] 中，选择要激活区段的目标。 ![激活流](/help/rtcdp/destinations/assets/airship-tags-activate1.png)
2. 单击目标的名称。 此操作将带您进入激活流程。
请注意，如果目标激活流已存在，您可以看到当前发送到目标的区段。 选 **[!UICONTROL 择右边栏]** 中的编辑激活，然后按照以下步骤修改激活详细信息。  ![激活流](/help/rtcdp/destinations/assets/airship-tags-activate2.png)
3. 选择 **[!UICONTROL 激活]**;
4. 在激活 **[!UICONTROL 目标工作流]** ，在选择区 **[!UICONTROL 段页面上]** ，选择要发送的区段 [!DNL Airship Tags]。
   ![细分到目标](/help/rtcdp/destinations/assets/airshiptags3-select-segments.png)
5. 在映 **[!UICONTROL 射步]** 骤中，从XDM模式中选择要映 [射到目](https://docs.adobe.com/content/help/zh-Hans/experience-platform/xdm/home.html) 标模式的属性和标识。 选 **[!UICONTROL 择“添加新映射]** ”以浏览模式并将其映射到相应的目标标识。
   ![身份映射初始屏幕](/help/rtcdp/destinations/assets/gcm-identity-mapping.png)
   [!DNL Airship] 可以在表示设备实例（如iPhone）的渠道上设置标记，也可以在将用户的所有设备映射到通用标识符（如客户ID）的指定用户上设置标记。 如果您的模式中有纯文本（未散列）电子邮件地址作为主标识，请在“源属性”中选 **[!UICONTROL 择电子邮件]** ，并在“目标标识” [!DNL Airship] 下右列中映射到指 **[!UICONTROL 定用户]**，如下所示。
   ![指定用](/help/rtcdp/destinations/assets/airshiptags7-mappingoption2.png)户映射对于应映射到渠道（即设备）的标识符，请根据源映射到相应的渠道。 以下图像显示如何将Google广告ID映射到 [!DNL Airship] Android渠道。
   ![连接到Airship标签](/help/rtcdp/destinations/assets/airshiptags4-select-source-identity.png)
   ![连接到Airship标签](/help/rtcdp/destinations/assets/airshiptags5-select-target-identity.png)
   ![渠道映射](/help/rtcdp/destinations/assets/airshiptags6-mappingoption1.png)

6. 在“区 **[!UICONTROL 段计划]** ”页上，计划当前处于禁用状态。 单 **[!UICONTROL 击]** “下一步”继续查看步骤。
7. 在“审 **[!UICONTROL 阅]** ”页面上，您可以看到所选内容的摘要。 选 **[!UICONTROL 择取消]** (Cancel **[!UICONTROL )以分解流，选择]** 返回 **[!UICONTROL (Back)以修改设置，或选择]** 完成(Finish)以确认选择并开始将数据发送到目标。

>[!IMPORTANT]
>
>在此步骤中，Adobe Experience Platform检查数据使用策略是否违反。 下面显示了违反策略的示例。 在解决违规之前，您无法完成区段激活工作流。 有关如何解决违反策略的信息，请参 [阅数据管理](/help/rtcdp/privacy/data-governance-overview.md#enforcement) 文档部分中的策略实施。

![确认选择](/help/rtcdp/destinations/assets/data-policy-violation.png)

如果未检测到任何违反策略的情况，请选 **[!UICONTROL 择“完成]** ”以确认您的选择，并让开始将数据发送到目标。

![确认选择](/help/rtcdp/destinations/assets/Airship-tags-review.png)


## 数据使用和管理 {#data-usage-governance}

处理 [!DNL Adobe Experience Platform] 数据时，所有目标都符合数据使用策略。 有关如何实施数 [!DNL Adobe Experience Platform] 据治理的详细信 [息，请参阅实时CDP中的数据治理](/help/rtcdp/privacy/data-governance-overview.md)。

