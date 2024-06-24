---
title: Zeta营销平台
description: Zeta Marketing Platform (ZMP)是一个基于云的系统，借助智能（专有数据和AI），可帮助您更有效地获取、发展和留住客户。
hide: true
hidefromtoc: true
source-git-commit: bf553371316d9d9cb368fc4d1be14196201ef680
workflow-type: tm+mt
source-wordcount: '1352'
ht-degree: 1%

---


# Zeta营销平台 {#zeta-marketing-platform}

## 概述 {#overview}

Zeta Marketing Platform (ZMP)是一个基于云的系统，借助智能（专有数据和AI），可帮助您更有效地获取、发展和留住客户。 有关更多详细信息，请参阅 [Zeta全球](https://zetaglobal.com/).

利用Adobe Experience Platform中提供的Zeta Marketing Platform连接器，您可以将Experience Platform与ZMP无缝同步。

>[!IMPORTANT]
>
>目标连接器和文档页面由创建和维护 *Zeta全球* 团队。 如有任何查询或更新请求，请通过以下电子邮件联系团队： [联系我们](https://zetaglobal.com/about/contact-us/).

## 用例 {#use-cases}

### 构建受众区段 {#use-case-build-audiences}

营销人员希望构建独一无二的受众配置文件，确定其最有价值的区段，并在Zeta营销平台支持的任何数字渠道中使用它们。 他们希望创建消费者个人资料的真实360视图，构建和激活有意义的受众。 有关Zeta营销平台支持的渠道的更多详细信息 [此处](https://zetaglobal.com/platform/integrations/).

### 使用广告定位用户 {#use-case-target-users}

广告商旨在通过ZetaDemand Side Platform(DSP)定位特定受众中的用户，因为这些用户会与自己的品牌进行交互。 有关Zeta DSP的详细信息，请单击 [此处](https://knowledgebase.zetaglobal.com/programmatic-user-guide/).

## 先决条件 {#prerequisites}

### Zeta营销平台先决条件

* 在设置与Zeta Marketing Platform目标的新连接之前，必须在Zeta Marketing Platform帐户中创建一个空的客户列表。 您必须选择其中一个客户列表作为指定目标，以接收您计划发送的Adobe Experience Platform受众。 您可以按照说明在ZMP中创建空的客户列表 [此处](https://knowledgebase.zetaglobal.com/zmp/creating-audiences#CreatingAudiences-CreatingaCustomerList).
* 尽管Adobe Experience Platform允许将多个受众激活到特定的ZMP目标实例，但强制要求每个ZMP目标实例只能接收一个Experience Platform受众。 要从Experience Platform中处理多个受众，请为每个受众创建其他ZMP目标实例，然后从下拉列表中选择其他客户列表。 此方法可确保不会覆盖目标ZMP受众。 请参阅 [填写目标详细信息](#destination-details) 以了解更多详细信息。
* 使用以下凭据配置目标：
   * 用户名： **api**
   * 密码：您的ZMP REST API密钥。 您可以通过登录到ZMP帐户并导航到 **设置** > **集成** > **密钥和应用程序** 部分。 请参阅 [ZMP文档](https://knowledgebase.zetaglobal.com/zmp/integrations) 以了解更多详细信息。

## 支持的身份 {#supported-identities}

[!DNL Zeta Marketing Platform] 支持激活下表中描述的自定义用户ID。 有关更多详细信息，请参阅 [身份](/help/identity-service/features/namespaces.md).

>[!IMPORTANT]
> Zeta营销平台目标要求您将源身份命名空间映射到ZMP `uid` 目标身份。 这有助于Zeta营销平台以独特的方式区分每个配置文件。

| 目标身份 | 描述 | 注意事项 | 注释 |
---------|----------|----------|----------|
| uid | ZMP用于区分客户个人资料的唯一ID | 必需 | 选择 `Email` 标准身份命名空间。 或者，您可以选择将自定义命名空间映射到 `uid` 如果客户配置文件没有电子邮件。 |
| email_md5_id | 发送电子邮件至MD5，表示每个客户配置文件 | 可选 | 当您希望使用电子邮件MD5值唯一标识客户配置文件时，请选择此目标标识。 由于Platform无法将纯文本转换为MD5，因此Experience Platform中的电子邮件地址必须采用MD5格式。 在此方案中，设置 `uid` （必需）添加到相同的电子邮件MD5值或其他适当的身份命名空间。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍可将哪种类型的受众导出到此目标。

| 受众来源 | 支持 | 描述 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md). |
| 自定义上传 | X | 受众 [已导入](../../../segmentation/ui/overview.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

>[!NOTE]
> 在Platform受众中添加或删除单个成员后，更新将发送到ZMP，以确保目标客户列表相应地同步。

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据区段评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要向目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

* **[!UICONTROL 用户名]**： `api`
* **[!UICONTROL 密码]**：您的ZMP REST API密钥。 您可以通过登录到ZMP帐户并导航到 **设置** > **集成** > **密钥和应用程序** 部分。 请参阅 [ZMP文档](https://knowledgebase.zetaglobal.com/zmp/integrations) 以了解更多详细信息。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![显示ZMP配置的图像](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-configure-new-destination.png)
* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL ZMP帐户站点ID]**：您的ZMP **站点ID** 要将受众发送到的位置。 您可以通过导航到 **设置** > **集成** > **密钥和应用程序** 部分。 可以找到更多信息 [此处](https://knowledgebase.zetaglobal.com/zmp/integrations).
* **[!UICONTROL ZMP段]**：ZMP站点ID帐户中要与Platform受众一起更新的客户列表区段。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

读取 [将配置文件和区段激活到流式区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

### 映射属性和身份 {#map}

以下是将用户档案导出到时的正确标识映射示例 [!DNL Zeta Marketing Platform].

选择源字段：
* 选择源身份命名空间(自定义或标准，例如 `Email`)唯一标识Adobe Experience Platform中的用户档案，并且 [!DNL Zeta Marketing Platform].
* 选择需要在中导出并更新的任何XDM源配置文件属性 [!DNL Zeta Marketing Platform].

选择目标字段：
* （必需）选择 `uid` 作为要将源身份命名空间映射到的目标身份。
* （可选）选择 `email_md5_id` 作为目标身份，您将代表电子邮件md5值的源身份命名空间映射到此身份。 由于Platform无法将纯文本转换为MD5，因此Experience Platform中的电子邮件地址必须采用MD5格式
* 根据需要选择任何其他目标映射。

![标识映射](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-mapping-example.png)

## 导出的数据/验证数据导出 {#exported-data}

从Experience Platform到Zeta Marketing Platform的受众成功激活会更新ZMP中的目标客户列表。 目标客户列表中的计数和样本配置文件将等于已成功激活的身份数。

![ZMP中的客户列表](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-customer-list-in-zmp.png)

从Experience Platform激活的每个受众成员也会显示在下 **受众** > **人员** 在ZMP中。 您还将能够查看 **客户列表** 在“单个客户”视图中属于某个配置文件的区段，如下所示。

![SingleCustomerViewInZMP](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-single-customer-view-in-zmp.png)

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 实施数据管理，请阅读 [数据管理概述](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

* [Zeta知识库](https://knowledgebase.zetaglobal.com/zmp/)
