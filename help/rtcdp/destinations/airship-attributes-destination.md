---
keywords: airship attributes;airship destination
title: 飞艇属性目标
seo-title: 飞艇属性目标
description: 将Adobe受众数据无缝传递给飞艇，作为飞艇内目标的受众属性。
seo-description: 将Adobe受众数据无缝传递给飞艇，作为飞艇内目标的受众属性。
translation-type: tm+mt
source-git-commit: 4b1bf5bbce57a22529c5d025c5bae10557400d54
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 1%

---


# （测试版）目 [!DNL Airship Attributes] 标 {#airship-attributes-destination}

>[!IMPORTANT]
>
>Adobe Experience Platform [!DNL Airship Attributes] 的目的地目前处于测试阶段。 文档和功能可能会发生变化。

## 概述 {#overview}

[!DNL Airship] 是领先的客户互动平台，可帮助您在客户生命周期的每个阶段向用户提供有意义的个性化全渠道消息。

此集成将Adobe用户档案数据作为 [!DNL Airship] 属性 [传递](https://docs.airship.com/guides/audience/attributes/) ，以进行定位或触发。

要了解有关的更 [!DNL Airship]多信息，请参 [阅Airship Docs](https://docs.airship.com)。


>[!TIP]
>
>此文档页面由团队创 [!DNL Airship] 建。 如有任何查询或更新请求，请直接通过 [support.airship.com与他们联系](https://support.airship.com/)。

## 先决条件 {#prerequisites}

在将受众区段发送到之前， [!DNL Airship]您必须：

* 在项目中启用 [!DNL Airship] 属性。
* 生成用于身份验证的承载令牌。

>[!TIP]
>
>如果您尚 [!DNL Airship] 未通过 [此注册链接](https://go.airship.eu/accounts/register/plan/starter/) ，请创建帐户。

### 启用属性 {#enable-attributes}

Adobe Experience Platform用户档案属性与属性类 [!DNL Airship] 似，可使用本页下面进一步演示的映射工具在平台中轻松地相互映射。

[!DNL Airship] 项目具有多个预定义和默认属性。 如果您有自定义属性，则必须首先定义该 [!DNL Airship] 属性。 有关详 [细信息，请参阅设置和](https://docs.airship.com/tutorials/audience/attributes/) 管理属性。

### 承载令牌 {#bearer-token}

1. 转到 **[!UICONTROL Airship]** 仪表板 **[!UICONTROL 中的]** “设置 [”“API和集](https://go.airship.com) 成”，然 **[!UICONTROL 后在左侧菜]** 单中选择令牌。
1. 单击 **[!UICONTROL 创建令牌]**。
1. 为令牌提供用户友好名称，如“Adobe属性目标”，然后为角色选择“全部访问”。
1. 单击 **[!UICONTROL 创建令牌]** ，并将详细信息保存为机密。


## 用例 {#use-cases}

为了帮助您更好地了解如何以及何时使用目标， [!DNL Airship Attributes] 以下是Adobe Experience Platform客户可通过使用此目标解决的示例使用案例。

### 用例#1

利用在Adobe Experience Platform收集的用户档案数据，在任何渠道内个性化消息和丰 [!DNL Airship]富内容。 例如，利用 [!DNL Experience Platform] 用户档案数据在中设置位置属 [!DNL Airship]性。 这将使酒店品牌能够为每个用户显示最近的酒店位置的图像。

### 用例#2

利用Adobe Experience Platform的属性进一步丰富 [!DNL Airship] 用户档案并将其与SDK或预测性数据 [!DNL Airship] 相结合。 例如，零售商可以创建包含忠诚度状态和位置数据（来自平台的属性）的细分 [!DNL Airship] ，并预测客户流失数据，以向生活在内华达州拉斯维加斯、且极有可能进行搅动的黄金忠诚度状态用户发送高度定向的消息。

## 连接到 [!DNL Airship Attributes] {#connect-airship-attributes}

1. 在“ **[!UICONTROL 目标]** ”>“ **[!UICONTROL 目录]**”中 **[!UICONTROL ，滚动至“移]** 动互动”类别。 选择 **[!DNL Airship Attributes]**，然后选择 **[!UICONTROL 配置]**。

   >[!NOTE]
   >
   >如果与此目标的连接已存在，您可以在目标卡 **[!UICONTROL 上看到]** “激活”按钮。 有关激活和配置之 **[!UICONTROL 间差异]** 的详 **[!UICONTROL 细信]**&#x200B;息，请参 [阅目标工](/help/rtcdp/destinations/destinations-workspace.md#catalog) 作区文档的“目录”部分。

   ![连接到飞艇属性](/help/rtcdp/destinations/assets/airship-attributes-in-catalog.png)

2. 在“帐 **户** ”步骤中，如果之前已设置到目标的连接，请选择“现有 [!DNL Airship Attributes] 帐户 **** ”，然后选择现有连接。 或者，您也可以选 **[!UICONTROL 择“新建帐户]** ”来设置新连接 [!DNL Airship Attributes]。 选 **[!UICONTROL 择连接到目标]** ，以使用您从 [!DNL Airship] 仪表板生成的载体令牌将Adobe Experience Platform连接到您的 [!DNL Airship] 项目。

   >[!NOTE]
   >
   >Adobe Experience Platform支持身份验证过程中的凭据验证，如果您向您的帐户输入了不正确的凭据，则会显示错误 [!DNL Airship] 消息。 这可确保您没有使用错误的凭据完成工作流。

   ![连接到飞艇属性](/help/rtcdp/destinations/assets/airship1-connect-to-airship.png)

3. 确认您的凭据并将Adobe Experience Platform连接到您的 [!DNL Airship] 项目后，您可以选 **[!UICONTROL 择]** “下一步 **[!UICONTROL ”以继续]** 设置步骤。

4. 在验 **[!UICONTROL 证步]** 骤中，输入 **[!UICONTROL 激活流]** 的名 **[!UICONTROL 称和]** 说明。 <br> 此外，在此步骤中，您还可以选择美国或欧盟数据中心，具体取决于 [!DNL Airship] 哪个数据中心适用于此目标。 最后，选择一个或多个将数据导出到目标的营销用例。 您可以从Adobe定义的营销用例中进行选择，也可以创建您自己的用例。 有关营销使用案例的更多信息， [请参阅实时CDP中的数据管理](/help/rtcdp/privacy/data-governance-overview.md#destinations) 。 有关各个Adobe定义的营销用例的信息，请参阅数据 [使用策略概述](/help/data-governance/policies/overview.md#core-actions)。 <br> 在 **[!UICONTROL 填写上面]** 的字段后，选择创建目标。

   ![连接到飞艇属性](/help/rtcdp/destinations/assets/airship2-select-airship-domain.png)

5. 您的目标现在已创建。 如果要稍后 **[!UICONTROL 激活区段]** ，则可以选择保存并退出 **[!UICONTROL ，也可以选择下一步继续工作]** 流，然后选择要激活的区段。 无论哪种情况，在工作流的 [其余部分](#activate-segments)，请参阅下一节激活区段。

## 激活区段 {#activate-segments}

要将区段激活 [!DNL Airship Attributes]到，请执行以下步骤：

1. 在“ **[!UICONTROL 目标”>]**“浏览” [!DNL Airship Attributes] 中，选择要激活区段的目标。
   ![激活流](/help/rtcdp/destinations/assets/airship-attributes-activate1.png)
1. 单击目标的名称。 此操作将带您进入激活流程。
请注意，如果目标激活流已存在，您可以看到当前发送到目标的区段。 选 **[!UICONTROL 择右边栏]** 中的编辑激活，然后按照以下步骤修改激活详细信息。 ![激活流](/help/rtcdp/destinations/assets/airship-attributes-activate2.png)
1. 选择 **[!UICONTROL 激活]**;
1. 在激活 **[!UICONTROL 目标工作流]** ，在选择区 **[!UICONTROL 段页面上]** ，选择要发送的区段 [!DNL Airship Attributes]。
   ![细分到目标](/help/rtcdp/destinations/assets/airship3-select-segments-to-export.png)
1. 在映 **[!UICONTROL 射步]** 骤中，从XDM模式中选择要映 [射到目](https://docs.adobe.com/content/help/zh-Hans/experience-platform/xdm/home.html) 标模式的属性和标识。 选 **[!UICONTROL 择“添加新映射]** ”以浏览模式并将其映射到相应的目标标识。
   ![身份映射初始屏幕](/help/rtcdp/destinations/assets/gcm-identity-mapping.png)
   [!DNL Airship] 属性可以在表示设备实例（如iPhone）的渠道上设置，也可以在将用户的所有设备映射到通用标识符（如客户ID）的指定用户上设置。 如果您的模式中有纯文本（未散列）电子邮件地址作为主标识，请在“源属性”中选 **[!UICONTROL 择电子邮件]** ，并在“目标标识” [!DNL Airship] 下右列中映射到指 **[!UICONTROL 定用户]**，如下所示。
   ![指定用](/help/rtcdp/destinations/assets/airshiptags7-mappingoption2.png)户映射对于应映射到渠道（即设备）的标识符，请根据源映射到相应的渠道。 下图显示了如何创建两个映射：

   * iOS渠道的IDFA iOS [!DNL Airship] 广告ID
   * Adobe `fullName` 属性 [!DNL Airship] 为“全名”属性

   >[!NOTE]
   >
   >使用在为属性映射选择仪表板字段时 [!DNL Airship] 显示在目标中的用户友好名称。

   **映射标识**选择源字段：
   ![连接到飞艇属性](/help/rtcdp/destinations/assets/airship5-select-source-identity.png)选择目标字段：
   ![连接到飞艇属性](/help/rtcdp/destinations/assets/airship6-select-target-identity.png)

   **映射属性**

   选择源属性：
   ![选择源字段](/help/rtcdp/destinations/assets/airship7-select-source-attributes.png)选择目标属性：
   ![选择目标字段](/help/rtcdp/destinations/assets/airship8-select-target-attribute.png)验证映射：
   ![渠道映射](/help/rtcdp/destinations/assets/airship9-mapping-final.png)

1. 在“区 **[!UICONTROL 段计划]** ”页上，计划当前处于禁用状态。 单 **[!UICONTROL 击]** “下一步”继续查看步骤。 ![当前禁用计划](/help/rtcdp/destinations/assets/airship10-scheduling-step-is-disabled-for-now.png)

1. 在“审 **[!UICONTROL 阅]** ”页面上，您可以看到所选内容的摘要。 选 **[!UICONTROL 择取消]** (Cancel **[!UICONTROL )以分解流，选择]** 返回 **[!UICONTROL (Back)以修改设置，或选择]** 完成(Finish)以确认选择并开始将数据发送到目标。

>[!IMPORTANT]
>
>在此步骤中，Adobe Experience Platform检查数据使用策略是否违反。 下面显示了违反策略的示例。 在解决违规之前，您无法完成区段激活工作流。 有关如何解决违反策略的信息，请参 [阅数据管理](/help/rtcdp/privacy/data-governance-overview.md#enforcement) 文档部分中的策略实施。

![确认选择](/help/rtcdp/destinations/assets/data-policy-violation.png)

如果未检测到任何违反策略的情况，请选 **[!UICONTROL 择“完成]** ”以确认您的选择，并让开始将数据发送到目标。

![审查](/help/rtcdp/destinations/assets/airship11-review-step.png)

## 数据使用和管理 {#data-usage-governance}

处理 [!DNL Adobe Experience Platform] 数据时，所有目标都符合数据使用策略。 有关如何实施数 [!DNL Adobe Experience Platform] 据治理的详细信 [息，请参阅实时CDP中的数据治理](/help/rtcdp/privacy/data-governance-overview.md)。
