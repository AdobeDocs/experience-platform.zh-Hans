---
title: Pega客户决策中心连接
description: 使用Adobe Experience Platform中的Pega客户决策中心目标，将用户档案属性和区段成员资格数据发送到Pega客户决策中心，以便进行下一个最佳决策。
exl-id: 0546da5d-d50d-43ec-bbc2-9468a7db4d90
source-git-commit: f06afec31b7fa550a612280b8ad665b8393ee2e3
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 1%

---

# Pega客户决策中心连接

## 概述 {#overview}

使用 [!DNL Pega Customer Decision Hub] 目标，以将配置文件属性和区段成员资格数据发送到 [!DNL Pega Customer Decision Hub] 为下一个最佳行动决策提供支持。

来自Adobe Experience Platform的配置文件区段成员资格，加载到 [!DNL Pega Customer Decision Hub]，可用作自适应模型中的预测器，并帮助提供正确的上下文和行为数据以用于下一最佳行动决策。

>[!IMPORTANT]
>
>此文档页面由Pegassystems创建。 如有任何查询或更新请求，请直接联系Pega [此处](mailto:support@pega.com).

## 用例

为了帮助您更好地了解应如何以及何时应使用 [!DNL Customer Decision Hub] 目标中，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 电信

营销人员希望利用数据科学提供的基于模型的下一个最佳行动的分析，具体方式为 [!DNL Pega Customer Decision Hub] 客户参与。 [!DNL Pega Customer Decision Hub] 严重依赖于客户意图 — 例如“Interest_In_5G”、“Interest_in_Unlimited_Dataplan”或“Interest_in_iPhone_accessories”。

### 金融服务

营销人员希望优化从“养老金计划”或“退休计划”快讯订阅或退订的客户优惠。 金融服务公司可以将多个客户ID从其自己的CRM摄取到Adobe Experience Platform中，从其自己的离线数据构建区段，并将进入和退出区段的用户档案发送到 [!DNL Pega Customer Decision Hub] 在出站频道中获得次佳动作(NBA)决策。

## 先决条件 {#prerequisites}

在使用此目标将数据导出到Adobe Experience Platform之前，请确保在 [!DNL Pega Customer Decision Hub]:

* 在 [!DNL Pega Customer Decision Hub] 实例。
* 配置OAuth 2.0 [使用客户端凭据进行客户端注册](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) 您的 [!DNL Pega Customer Decision Hub] 实例。
* 配置 [实时运行数据流](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) ，以获取您的Adobe区段成员资格数据流 [!DNL Pega Customer Decision Hub] 实例。

## 支持的身份 {#supported-identities}

[!DNL Pega Customer Decision Hub] 支持激活下表所述的自定义用户ID。 有关更多详细信息，请参阅 [标识](/help/identity-service/namespaces.md).

| Target标识 | 描述 |
|---|---|
| *客户ID* | 唯一标识中用户档案的通用用户标识符 [!DNL Pega Customer Decision Hub] 和Adobe Experience Platform |

{style=&quot;table-layout:auto&quot;}

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | 导出具有标识符(*客户ID*)、属性（姓氏、名字、位置等） 和区段成员资格数据。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标是始终基于API的连接。 在Experience Platform中更新用户档案后，根据区段评估，连接器会立即将更新发送到目标平台下游。 有关更多信息，请参阅 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 连接到目标 {#connect}

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

### 对目标进行身份验证 {#authenticate}

#### OAuth 2客户端凭据身份验证 {#oauth-2-client-credentials-authentication}

![UI屏幕的图像，您可以在该屏幕中使用带有客户端凭据身份验证的OAuth 2连接到Pega CDH目标](../../assets/catalog/personalization/pega/pega-api-authentication-oauth2-client-credentials.png)

填写以下字段并选择 **[!UICONTROL 连接到目标]**:

* **[!UICONTROL 访问令牌URL]**:您上的OAuth 2访问令牌URL [!DNL Pega Customer Decision Hub] 实例。
* **[!UICONTROL 客户端ID]**:OAuth 2 [!DNL client ID] 在 [!DNL Pega Customer Decision Hub] 实例。
* **[!UICONTROL 客户端密钥]**:OAuth 2 [!DNL client secret] 在 [!DNL Pega Customer Decision Hub] 实例。

### 填写目标详细信息 {#destination-details}

在与 [!DNL Pega Customer Decision Hub]，请提供目标的以下信息：

![显示Pega CDH目标详细信息的已完成字段的UI屏幕图像](../../assets/catalog/personalization/pega/pega-connect-destination.png)

要配置目标的详细信息，请填写必填字段并选择 **[!UICONTROL 下一个]**.

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL 主机名]**:配置文件将导出为json数据的Pega客户决策中心主机名。

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

请参阅 [将受众数据激活到流配置文件导出目标](../../ui/activate-streaming-profile-destinations.md) 有关将受众区段激活到此目标的说明。

### 目标属性 {#attributes}

在 [[!UICONTROL 选择属性]](../../ui/activate-streaming-profile-destinations.md#select-attributes) 步骤，Adobe建议您从 [合并模式](../../../profile/home.md#profile-fragments-and-union-schemas). 选择唯一标识符以及要导出到目标的任何其他XDM字段。

### 映射示例：激活用户档案更新 [!DNL Pega Customer Decision Hub]

以下示例用于将用户档案导出到 [!DNL Pega Customer Decision Hub].

选择源字段：

* 选择标识符(例如：CustomerID)作为源标识，用于唯一标识Adobe Experience Platform中的用户档案，以及 [!DNL Pega Customer Decision Hub].
* 选择需要在 [!DNL Pega Customer Decision Hub].

选择目标字段：

* 选择 `CustomerID` 命名空间作为目标标识。
* 选择需要映射到相应XDM源配置文件属性的目标配置文件属性名称。

![身份映射](../../assets/catalog/personalization/pega/pega-source-destination-mapping.png)

## 导出的数据/验证数据导出 {#exported-data}

成功更新用户档案的区段成员资格将在Pega营销区段成员资格数据存储中插入区段标识符、名称和状态。 会员资格数据与使用 [!DNL Pega Customer Decision Hub]，如下所示。
![UI屏幕的图像，您可以在该屏幕中使用客户配置文件设计器将Adobe区段成员资格数据与客户关联](../../assets/catalog/personalization/pega/pega-profile-designer-associate.png)

区段成员资格数据用于Pega下一最佳行动设计器参与策略以实现下一最佳行动决策，如下所示。
![UI屏幕的图像，您可以在Pega Next-Best-Action Designer的参与策略中将区段成员资格字段添加为条件](../../assets/catalog/personalization/pega/pega-profile-designer-engagment.png)

客户区段成员资格数据字段作为预测器添加到自适应模型中，如下所示。
![UI屏幕的图像，您可以在其中使用Prediction Studio将区段成员资格字段添加为自适应模型中的谓词](../../assets/catalog/personalization/pega/pega-profile-designer-adaptivemodel.png)

## 其他资源 {#additional-resources}

请参阅 [设置OAuth 2.0客户端注册](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) in [!DNL Pega Customer Decision Hub].

请参阅 [为数据流创建实时运行](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) in [!DNL Pega Customer Decision Hub].

请参阅 [在客户配置文件设计器中管理客户记录](https://docs.pega.com/whats-new-pega-platform/manage-customer-records-customer-profile-designer-86).

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，请查看 [数据管理概述](/help/data-governance/home.md).
