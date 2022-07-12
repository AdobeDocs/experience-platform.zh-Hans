---
title: Pinterest客户列表连接
description: 从客户列表创建受众、访问过您网站的人员或已在Pinterest上与您的内容进行交互的人员。
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 3%

---

# [!DNL Pinterest Customer List] 连接

## 概述 {#overview}

从客户列表创建受众、访问过您网站的人员或已在Pinterest上与您的内容进行交互的人员。

>[!IMPORTANT]
>
>此目标由Pinterest团队构建。 如有任何查询或更新请求，请直接通过https://help.pinterest.com/en/contact联系。

## 先决条件 {#prerequisites}

* 用户需要使用Pinterest帐户进行身份验证，该帐户有权访问要向其添加受众的广告商帐户。 有关共享广告商帐户的详细信息，请参阅 [此处](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). 具体而言，用户将需要“受众”访问级别。
* 有关客户列表标识格式的详细信息 [此处](https://help.pinterest.com/en/business/article/audience-targeting).

## 支持的身份 {#supported-identities}

的 [!DNL Pinterest Customer List] 目标支持激活下表中描述的身份。 详细了解 [标识](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

在 [映射步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 在目标激活工作流中，将所需的身份映射到目标字段 *pinterest_audience*. 身份在将数据摄取到Pinterest中时进行区分和解析。

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 映射 *GAID* 目标标识字段的源标识命名空间 *pinterest_audience*. 身份在将数据摄取到Pinterest中时进行区分和解析。 |
| IDFA | [!DNL Apple ID for Advertisers] | 映射 *IDFA* 目标标识字段的源标识命名空间 *pinterest_audience*. 身份在将数据摄取到Pinterest中时进行区分和解析。 |
| 电子邮件 | 电子邮件地址（使用SHA256算法进行明文或哈希处理） | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 <br> 映射 *电子邮件* 或 *Email_LC_SHA256* 目标标识字段的源标识命名空间 *pinterest_audience*. |

{style=&quot;table-layout:auto&quot;}

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您要导出区段（受众）的所有成员，以及在Pinterest客户列表目标中使用的标识符（名称、电话号码或其他）。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 用例 {#use-cases}

为了帮助您更好地了解应如何以及何时应使用 [!DNL Pinterest Customer List] 目标中，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 用例#1

从客户列表创建受众、访问过您网站的人员或已在Pinterest上与您的内容进行交互的人员。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 此目标中，您必须提供以下信息：

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL 广告商ID]**:您的Pinterest广告商ID。

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

读取 [激活用户档案和区段以流式传输区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，请查看 [数据管理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans).

## 其他资源 {#additional-resources}

请参阅 [Pinterest帮助中心页面](https://help.pinterest.com/en/business/article/audience-targeting) 以了解其他信息。
