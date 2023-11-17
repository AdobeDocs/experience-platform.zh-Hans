---
title: pinterest客户列表连接
description: 从您的客户列表、访问过您的网站的人或已在Pinterest上与您的内容交互的人中创建受众。
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 5cef3bbc7f2246a91ecca807825d830f240c8d45
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 3%

---

# [!DNL Pinterest Customer List] 连接

>[!IMPORTANT]
>
>* 从2023年11月16日开始，您可以在目标目录中并排看到两张Pinterest信息卡。 这是由于升级到Pinterest广告商API，该API用于将数据导出到Pinterest。 现有的Pinterest目标连接器已重命名为 **[!UICONTROL （弃用）Pinterest]** 还有张新卡 **[!UICONTROL （新）Pinterest]** 现在可供您使用。
>* 使用 **[!UICONTROL （新）Pinterest]** 将目录中的任意营销活动连接到Pinterest。 如果您有任何到以下项的活动数据流： **[!UICONTROL （弃用）Pinterest]** 目标，请阅读 [升级文档](/help/destinations/catalog/advertising/pinterest-upgrade.md) 了解您的措施项以确保不会中断您的营销活动。

## 概述 {#overview}

从您的客户列表、访问过您的网站的人或已在Pinterest上与您的内容交互的人中创建受众。

>[!IMPORTANT]
>
>此目标由Pinterest团队构建。 如有任何查询或更新请求，请直接通过https://help.pinterest.com/en/contact联系。

## 先决条件 {#prerequisites}

* 用户需要使用Pinterest帐户进行身份验证，该帐户有权访问他们要将受众添加到的广告商帐户。 有关共享广告商帐户的详细信息，请参阅 [此处](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). 具体来说，用户需要“受众”访问级别。
* 有关客户列表身份格式的详细信息，请参阅 [此处](https://help.pinterest.com/en/business/article/audience-targeting).

## 支持的身份 {#supported-identities}

此 [!DNL Pinterest Customer List] 目标支持激活下表中描述的标识。 了解有关 [身份](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

在 [映射步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 在目标激活工作流中，将所需的身份映射到目标字段 *pinterest_audience*. 标识是在数据摄取到Pinterest时识别和解析的。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 映射 *GAID* 源身份命名空间到目标身份字段 *pinterest_audience*. 标识是在数据摄取到Pinterest时识别和解析的。 |
| IDFA | [!DNL Apple ID for Advertisers] | 映射 *IDFA* 源身份命名空间到目标身份字段 *pinterest_audience*. 标识是在数据摄取到Pinterest时识别和解析的。 |
| EMAIL | 电子邮件地址（纯文本或使用SHA256算法进行哈希处理） | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 <br> 映射 *电子邮件* 或 *Email_LC_SHA256* 源身份命名空间到目标身份字段 *pinterest_audience*. |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您正在导出具有Pinterest客户列表目标中所用标识符（姓名、电话号码或其他）的受众所有成员。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据受众评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 用例 {#use-cases}

为了帮助您更好地了解您应该如何以及何时使用 [!DNL Pinterest Customer List] 目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 用例#1

从您的客户列表、访问过您的网站的人或已在Pinterest上与您的内容交互的人中创建受众。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

同时 [设置](../../ui/connect-destination.md) 此目标必须提供以下信息：

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 广告帐户ID]**：您的Pinterest广告商ID。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

读取 [将用户档案和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据管理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans).

## 其他资源 {#additional-resources}

请参阅 [pinterest帮助中心页面](https://help.pinterest.com/en/business/article/audience-targeting) 以了解其他信息。

+++ 查看更改日志


| 发行月份 | 更新类型 | 描述 |
|---|---|---|
| 2023 年 11 月 | 功能和文档更新 | Real-Time CDP中的Pinterest目标现在使用v5广告商API。 |

{style="table-layout:auto"}


+++
