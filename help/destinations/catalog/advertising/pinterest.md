---
title: Pinterest客户列表连接
description: 从客户列表创建受众、访问过您网站的人员或已在Pinterest上与您的内容进行交互的人员。
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 3d7151645bc90a2dcbd6b31251ed459029ab77c9
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 2%

---

# [!DNL Pinterest Customer List] 连接

## 概述 {#overview}

从客户列表创建受众、访问过您网站的人员或已在Pinterest上与您的内容进行交互的人员。

>[!IMPORTANT]
>
>此目标由Pinterest团队构建。 如有任何查询或更新请求，请直接通过https://help.pinterest.com/en/contact联系。

## 先决条件 {#prerequisites}

* 用户需要使用Pinterest帐户进行身份验证，该帐户有权访问要向其添加受众的广告商帐户。 有关共享广告商帐户的详细信息，请在[此处](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts)找到。 具体而言，用户将需要“受众”访问级别。
* 有关客户列表标识格式的详细信息，请参见[此处](https://help.pinterest.com/en/business/article/audience-targeting)。


## 支持的身份 {#supported-identities}

[!DNL Pinterest Customer List]目标支持激活下表中描述的身份。 了解有关[identities](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started)的更多信息。

在目标激活工作流的[映射步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)中，将所需的标识映射到目标字段&#x200B;*pinterest_audience*。 身份在将数据摄取到Pinterest中时进行区分和解析。

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 将&#x200B;*GAID*&#x200B;源标识命名空间映射到目标标识字段&#x200B;*pinterest_audience*。 身份在将数据摄取到Pinterest中时进行区分和解析。 |
| IDFA | [!DNL Apple ID for Advertisers] | 将&#x200B;*IDFA*&#x200B;源标识命名空间映射到目标标识字段&#x200B;*pinterest_audience*。 身份在将数据摄取到Pinterest中时进行区分和解析。 |
| 电子邮件 | 电子邮件地址（使用SHA256算法进行明文或哈希处理） | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 <br> 将Emailor  ** Email_ *LC_SHA256* 源标识命名空间映射到目标标识字段 *pinterest_audience*。 |

{style=&quot;table-layout:auto&quot;}

## 导出类型 {#export-type}

**区段导出**  — 您要导出区段（受众）的所有成员，以及在Pinterest客户列表目标中使用的标识符（名称、电话号码或其他）。

## 用例 {#use-cases}

为了帮助您更好地了解应如何以及何时使用[!DNL Pinterest Customer List]目标，以下是Adobe Experience Platform客户可通过使用此目标解决的示例用例。


### 用例#1

从客户列表创建受众、访问过您网站的人员或已在Pinterest上与您的内容进行交互的人员。

## 连接到目标 {#connect}

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。



### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL 帐户ID]**:您的Pinterest广告帐户ID。

## 将区段激活到此目标 {#activate}

有关将受众区段激活到此目标的说明，请阅读[将配置文件和区段激活到流区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。

## 数据使用和管理 {#data-usage-governance}

处理数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据管理的详细信息，请参阅[数据管理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html)。

## 其他资源 {#additional-resources}

有关其他信息，请参阅[Pinterest帮助中心页面](https://help.pinterest.com/en/business/article/audience-targeting)。
