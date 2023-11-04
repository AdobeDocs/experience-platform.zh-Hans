---
title: Pega客户决策中心连接
description: 使用Adobe Experience Platform中的Pega客户决策中心目标将配置文件属性和受众成员资格数据发送到Pega客户决策中心，以便做出次优决策。
exl-id: 0546da5d-d50d-43ec-bbc2-9468a7db4d90
source-git-commit: 05e996f9e33e0d8be3d15a9ab3baaaf6d8152b5a
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 2%

---

# Pega客户决策中心连接

## 概述 {#overview}

使用 [!DNL Pega Customer Decision Hub] Adobe Experience Platform中要将配置文件属性和受众成员资格数据发送到的目标 [!DNL Pega Customer Decision Hub] 获得下一个最佳操作决策。

从Adobe Experience Platform分析受众成员资格，加载到时 [!DNL Pega Customer Decision Hub]，可用作自适应模型中的预测器，并帮助提供正确的上下文和行为数据以便做出下一个最佳操作决策。

>[!IMPORTANT]
>
>此目标连接器和文档页面由Pegasystems创建和维护。 如有任何查询或更新请求，请直接联系Pega [此处](mailto:support@pega.com).

## 用例

为了帮助您更好地了解您应该如何以及何时使用 [!DNL Customer Decision Hub] 目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 电信

营销人员希望利用提供的基于数据科学模型的下一个最佳操作的见解。 [!DNL Pega Customer Decision Hub] 用于客户参与。 [!DNL Pega Customer Decision Hub] 严重依赖于客户意图 — 例如“Interest_In_5G”、“Interest_in_Unlimited_Dataplan”或“Interest_in_iPhone_accessories”。

### 金融服务

营销人员希望优化为订阅或取消订阅退休金计划或退休计划快讯的客户提供的优惠。 金融服务公司可以从自己的CRM中将多个客户ID摄取到Adobe Experience Platform，从自己的离线数据构建受众，并将进入和退出受众的用户档案发送到 [!DNL Pega Customer Decision Hub] 在对外频道中做出次佳动作(NBA)决策。

## 先决条件 {#prerequisites}

在使用此目标将数据导出到Adobe Experience Platform之前，请确保在中完成以下先决条件 [!DNL Pega Customer Decision Hub]：

* 配置 [Adobe Experience Platform配置文件和受众成员资格集成组件](https://docs.pega.com/component/customer-decision-hub/adobe-experience-platform-profile-and-segment-membership-integration-component) 在您的 [!DNL Pega Customer Decision Hub] 实例。
* 配置OAuth 2.0 [使用客户端凭据进行客户端注册](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) 授予类型 [!DNL Pega Customer Decision Hub] 实例。
* 配置 [实时运行数据流](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) 的Adobe受众会员资格数据流 [!DNL Pega Customer Decision Hub] 实例。

## 支持的身份 {#supported-identities}

[!DNL Pega Customer Decision Hub] 支持激活下表中描述的自定义用户ID。 有关更多详细信息，请参阅 [身份](/help/identity-service/namespaces.md).

| 目标身份 | 描述 |
|---|---|
| *客户ID* | 通用用户标识符，用于唯一标识中的配置文件 [!DNL Pega Customer Decision Hub] 和Adobe Experience Platform |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 导出具有标识符(*客户ID*)、属性（姓氏、名字、位置等） 和受众会员资格数据。 |
| 导出频率 | **[!UICONTROL 流]** | 流式目标始终基于API连接。 一旦在Experience Platform中更新了用户档案，连接器就会根据受众评估将更新发送到下游目标平台。 有关更多信息，请参阅 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

#### OAuth 2客户端凭据身份验证 {#oauth-2-client-credentials-authentication}

![用户界面屏幕的图像，在该屏幕中，您可以使用带有客户端凭据身份验证的OAuth 2连接到Pega CDH目标](../../assets/catalog/personalization/pega/pega-api-authentication-oauth2-client-credentials.png)

填写下面的字段并选择 **[!UICONTROL 连接到目标]**：

* **[!UICONTROL 访问令牌URL]**：您网站上的OAuth 2访问令牌URL [!DNL Pega Customer Decision Hub] 实例。
* **[!UICONTROL 客户端ID]**：OAuth 2 [!DNL client ID] 您生成的 [!DNL Pega Customer Decision Hub] 实例。
* **[!UICONTROL 客户端密码]**：OAuth 2 [!DNL client secret] 您生成的 [!DNL Pega Customer Decision Hub] 实例。

### 填写目标详细信息 {#destination-details}

在建立与 [!DNL Pega Customer Decision Hub]，为目标提供以下信息：

![显示Pega CDH目标详细信息中已完成字段的UI屏幕图像](../../assets/catalog/personalization/pega/pega-connect-destination.png)

要配置目标的详细信息，请填写必填字段并选择 **[!UICONTROL 下一个]**.

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 主机名]**：将配置文件导出为JSON数据的Pega客户决策中心主机名。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

请参阅 [将受众数据激活到流式配置文件导出目标](../../ui/activate-streaming-profile-destinations.md) 有关将受众激活到此目标的说明。

### 目标属性 {#attributes}

在 [[!UICONTROL 选择属性]](../../ui/activate-streaming-profile-destinations.md#select-attributes) 步骤，Adobe建议您从 [合并架构](../../../profile/home.md#profile-fragments-and-union-schemas). 选择要导出到目标的唯一标识符和任何其他XDM字段。

### 映射示例：在中激活配置文件更新 [!DNL Pega Customer Decision Hub] {#mapping-example}

以下是将用户档案导出到时的正确标识映射示例 [!DNL Pega Customer Decision Hub].

选择源字段：

* 选择标识符（例如：CustomerID）作为源标识，以唯一标识Adobe Experience Platform中的用户档案，并且 [!DNL Pega Customer Decision Hub].
* 选择需要在中导出和更新的XDM源配置文件属性更改 [!DNL Pega Customer Decision Hub].

选择目标字段：

* 选择 `CustomerID` 命名空间作为目标标识。
* 选择需要映射到相应XDM源配置文件属性的目标配置文件属性名称。

![标识映射](../../assets/catalog/personalization/pega/pega-source-destination-mapping.png)

## 导出的数据/验证数据导出 {#exported-data}

成功更新用户档案的受众成员资格会在Pega营销受众成员资格数据存储中插入受众标识符、名称和状态。 成员资格数据在中使用客户配置文件设计器与客户关联 [!DNL Pega Customer Decision Hub]，如下所示。
![UI屏幕的图像，在该屏幕中，您可以使用Customer Profile Designer将Adobe受众成员资格数据关联到客户](../../assets/catalog/personalization/pega/pega-profile-designer-associate.png)

受众会员资格数据用于Pega下一最佳操作设计器参与策略中，以实现下一最佳操作决策，如下所示。
![UI屏幕的图像，您可以在其中添加受众成员资格字段作为Pega下一个最佳操作设计器的参与策略中的条件](../../assets/catalog/personalization/pega/pega-profile-designer-engagment.png)

客户受众会员资格数据字段在自适应模型中作为预测项添加，如下所示。
![UI屏幕的图像，在该屏幕中，您可以使用Prediction Studio将受众成员资格字段添加为自适应模型中的预测器](../../assets/catalog/personalization/pega/pega-profile-designer-adaptivemodel.png)

## 其他资源 {#additional-resources}

请参阅 [设置OAuth 2.0客户端注册](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) 在 [!DNL Pega Customer Decision Hub].

请参阅 [为数据流创建实时运行](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) 在 [!DNL Pega Customer Decision Hub].

请参阅 [在客户配置文件设计器中管理客户记录](https://docs.pega.com/whats-new-pega-platform/manage-customer-records-customer-profile-designer-86).

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据管理概述](/help/data-governance/home.md).
