---
keywords: 飞艇属性；飞艇目标
title: 飞艇属性连接
description: 将Adobe受众数据作为受众属性无缝传递到飞艇，以便在飞艇中进行定位。
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: 72225ac673ed921b5857a14070660134949e7e3e
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---

# [!DNL Airship Attributes] 连接 {#airship-attributes-destination}

## 概述 {#overview}

[!DNL Airship] 是领先的客户参与平台，帮助您在客户生命周期的每个阶段都向用户传递有意义、个性化的全渠道信息。

此集成将Adobe配置文件数据传递到 [!DNL Airship] 作为 [属性](https://docs.airship.com/guides/audience/attributes/) 用于定位或触发。

要了解有关 [!DNL Airship]，请参见 [飞艇文档](https://docs.airship.com).

>[!TIP]
>
>此目标连接器和文档页面由 [!DNL Airship] 团队。 如有任何查询或更新请求，请直接通过以下电子邮件联系他们： [support.airship.com](https://support.airship.com/).

## 先决条件 {#prerequisites}

在将受众发送至 [!DNL Airship]，您必须：

* 在中启用属性 [!DNL Airship] 项目。
* 生成持有者令牌以进行身份验证。

>[!TIP]
>
>创建 [!DNL Airship] 帐户透过 [此注册链接](https://go.airship.eu/accounts/register/plan/starter/) 如果你还没有的话。

## 支持的受众 {#supported-audiences}

此部分介绍可将哪种类型的受众导出到此目标。

| 受众来源 | 受支持 | 描述 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md). |
| 自定义上传 | ✓ | 受众 [已导入](../../../segmentation/ui/overview.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏）和/或身份（根据字段映射）。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据受众评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 启用属性 {#enable-attributes}

Adobe Experience Platform配置文件属性与 [!DNL Airship] 属性，并且可以使用本页下面进一步演示的映射工具在Platform中轻松相互映射。

[!DNL Airship] 项目具有几个预定义属性和默认属性。 如果您有自定义属性，则必须在以下位置定义它： [!DNL Airship] 首先。 请参阅 [设置和管理属性](https://docs.airship.com/tutorials/audience/attributes/) 以了解详细信息。

## 生成持有者令牌 {#bearer-token}

转到 **[!UICONTROL 设置]** &quot; **[!UICONTROL API和集成]** 在 [飞艇仪表板](https://go.airship.com) 并选择 **[!UICONTROL 令牌]** 在左侧菜单中。

单击 **[!UICONTROL 创建令牌]**.

为令牌提供用户友好的名称，例如“Adobe属性目标”，并为角色选择“所有访问权限”。

单击 **[!UICONTROL 创建令牌]** 并将详细信息保存为机密。

## 用例 {#use-cases}

为了帮助您更好地了解您应该如何以及何时使用 [!DNL Airship Attributes] 目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 用例#1

利用Adobe Experience Platform中收集的配置文件数据，在任意 [!DNL Airship]的频道。 例如，利用 [!DNL Experience Platform] 用于设置位置属性的配置文件数据 [!DNL Airship]. 这样一来，酒店品牌就能为每位用户显示最近酒店位置的图像。

### 用例#2

利用Adobe Experience Platform中的属性进一步扩充 [!DNL Airship] 配置文件并将其与SDK或 [!DNL Airship] 预测数据。 例如，零售商可以创建具有会员状态和位置数据（来自Platform的属性）的受众，并且 [!DNL Airship] 预测会流失数据，以向居住在内华达州拉斯维加斯且具有高流失率的金会员状态用户发送极具针对性的消息。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两个部分中列出的字段。

### 向目标进行身份验证 {#authenticate}

要向目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

* **[!UICONTROL 持有者令牌]**：您从生成的持有者令牌 [!DNL Airship] 仪表板。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：输入可帮助您识别此目标的名称。
* **[!UICONTROL 描述]**：输入此目标的描述。
* **[!UICONTROL 域]**：选择美国或欧盟的数据中心，具体取决于哪个 [!DNL Airship] 数据中心适用于此目标。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将受众激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

请参阅 [将受众数据激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

## 映射注意事项 {#mapping-considerations}

[!DNL Airship] 属性可以在表示设备实例(如iPhone)的渠道上设置，也可以设置命名用户（将用户的所有设备映射到通用标识符，如客户ID）。 如果您的架构中将纯文本（未散列）电子邮件地址作为主要身份，请在 **[!UICONTROL 源属性]** 并将映射到 [!DNL Airship] 下右列的指定用户 **[!UICONTROL 目标身份]**，如下所示。

![指定用户映射](../../assets/catalog/mobile-engagement/airship/mapping.png)

对于应映射到通道（即设备）的标识符，请根据源映射到相应的通道。 下图显示了如何创建两个映射：

* 将IDFA iOS广告ID发送至 [!DNL Airship] iOS渠道
* Adobe `fullName` 属性至 [!DNL Airship] “全名”属性

>[!NOTE]
>
>使用显示在中的用户友好名称 [!DNL Airship] 仪表板。

**映射身份**

选择源字段：

![连接到飞艇属性](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

选择目标字段：

![连接到飞艇属性](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**映射属性**

选择源属性：

![选择源字段](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

选择目标属性：

![选择目标字段](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

验证映射：

![渠道映射](../../assets/catalog/mobile-engagement/airship/mapping.png)


## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据管理概述](../../../data-governance/home.md).
