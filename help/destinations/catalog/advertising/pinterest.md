---
title: pinterest客户列表连接
description: 从您的客户列表、访问过您的网站的人或已在Pinterest上与您的内容交互的人中创建受众。
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 8a48ce4185f8044b8563d0435dcec17030b90830
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 4%

---

# [!DNL Pinterest Customer List]连接

## 概述 {#overview}

从您的客户列表、访问过您的网站的人或已在Pinterest上与您的内容交互的人中创建受众。

>[!IMPORTANT]
>
>此目标由Pinterest团队构建。 如有任何查询或更新请求，请直接通过https://help.pinterest.com/en/contact联系。

## 先决条件 {#prerequisites}

* 用户需要使用Pinterest帐户进行身份验证，该帐户有权访问他们要将受众添加到的广告商帐户。 有关共享广告商帐户的详细信息，可在[此处](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts)找到。 具体来说，用户需要“受众”访问级别。
* 可在[此处](https://help.pinterest.com/en/business/article/audience-targeting)找到有关客户列表身份格式的详细信息。

## 支持的身份 {#supported-identities}

[!DNL Pinterest Customer List]目标支持激活下表中描述的标识。 了解有关[标识](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started)的更多信息。

在目标激活工作流的[映射步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)中，将所需的标识映射到目标字段&#x200B;*pinterest_audience*。 标识是在数据摄取到Pinterest时识别和解析的。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 将&#x200B;*GAID*&#x200B;源标识命名空间映射到目标标识字段&#x200B;*pinterest_audience*。 标识是在数据摄取到Pinterest时识别和解析的。 |
| IDFA | [!DNL Apple ID for Advertisers] | 将&#x200B;*IDFA*&#x200B;源标识命名空间映射到目标标识字段&#x200B;*pinterest_audience*。 标识是在数据摄取到Pinterest时识别和解析的。 |
| EMAIL | 电子邮件地址（纯文本或使用SHA256算法进行哈希处理） | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 <br>将&#x200B;*Email*&#x200B;或&#x200B;*Email_LC_SHA256*&#x200B;源身份命名空间映射到目标身份字段&#x200B;*pinterest_audience*。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您正在导出具有Pinterest客户列表目标中所用标识符（姓名、电话号码或其他）的受众所有成员。 |
| 导出频率 | **[!UICONTROL 正在流式传输]** | 流目标为基于API的“始终运行”连接。 一旦根据受众评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 用例 {#use-cases}

为了帮助您更好地了解您应如何以及何时使用[!DNL Pinterest Customer List]目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 用例#1

从您的客户列表、访问过您的网站的人或已在Pinterest上与您的内容交互的人中创建受众。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 广告帐户ID]**：您的Pinterest广告商ID。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请阅读[将配置文件和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请参阅[数据治理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans)。

## 其他资源 {#additional-resources}

请参阅[Pinterest帮助中心页面](https://help.pinterest.com/en/business/article/audience-targeting)以获取更多信息。

+++ 查看更改日志


| 发行月份 | 更新类型 | 描述 |
|---|---|---|
| 2023 年 11 月 | 功能和文档更新 | Real-Time CDP中的Pinterest目标现在使用v5广告商API。 |

{style="table-layout:auto"}


+++
