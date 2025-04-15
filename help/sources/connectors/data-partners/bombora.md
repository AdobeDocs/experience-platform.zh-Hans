---
title: 庞博拉意图
description: 了解Experience Platform上的Bombora Intent源。
last-substantial-update: 2025-03-26T00:00:00Z
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="B2P版本" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: d2e81207-8ef5-4e52-bbac-a2fa262d8d08
source-git-commit: 9ab2c4725d2188f772bde1f7a89db2bb47c7a46b
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 1%

---

# [!DNL Bombora Intent]

[!DNL Bombora]是一个全面的受众解决方案，专门用于B2B意图数据。 [!DNL Bombora Intent]是Adobe Experience Platform源，可用于将您的[!DNL Bombora]帐户连接到Experience Platform并集成您的帐户意图数据。

使用[!DNL Bombora Intent]源，您可以集成[!DNL Bombora's]公司激增意向数据，以识别积极研究您的产品或服务的客户。 使用[!DNL Bombora]优先处理市场内帐户，以创建精确的区段并执行超针对性的ABM营销活动，确保您的营销工作将重点放在最有可能转化的帐户上。 此外，您还可以利用意图驱动型策略来优化广告支出、提高参与度并最大限度地提高ROI。

阅读本文档以了解有关[!DNL Bombora]源的先决条件信息。

## 用例 {#use-cases}

请阅读以下内容，以了解可应用于[!DNL Bombora]源的用例示例。

### Demand-Side Platform (DSP)集成

作为B2B营销人员，您可以在Real-Time CDP中创建帐户列表，识别对您的产品表现出高意图的公司，然后在[!DNL Bombora]中激活此列表，该列表直接与DSP集成，从而允许您使用[!DNL Bombora's]数据运行有针对性的程序化广告营销活动。 这可确保您的广告支出专注于最有可能转化的公司。

### Account-Based Marketing (ABM)功能

作为B2B营销人员，您可以根据第一方和第三方意图信号构建帐户列表。 然后，您可以在[!DNL Bombora]中激活此列表，其中ABM功能允许您专门针对这些帐户的员工，确保您的广告可触及决策者而不是广泛的受众。

### 多渠道ABM激活

作为B2B营销人员，您可以在Real-Time CDP中创建帐户列表，识别意图较强的公司并在[!DNL Bombora]中激活它以跨多个渠道运行目标营销活动。 在付费社交媒体上，您可以在目标帐户（如[!DNL Linkedin]和[!DNL Facebook]）上向专业人员提供个性化广告。

使用原生广告平台，您可以确保内容在相关上下文中可提供给决策者。 您还可以将营销活动扩展到高级电视，向关键帐户投放广告。 这种多渠道方法可确保跨平台发送一致的消息，从而最大限度地提高参与度和转化率。

## 先决条件 {#prerequisites}

在将[!DNL Bombora]连接到Experience Platform之前，请阅读以下部分以了解先决步骤。

### IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表。 未能将特定于地区的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 列入允许列表有关详细信息，请参阅[IP地址](../../ip-address-allow-list.md)页。

### 在Experience Platform上配置权限

若要将您的[!DNL Bombora]帐户连接到Experience Platform，您必须同时为您的帐户启用&#x200B;**[!UICONTROL 查看源]**&#x200B;和&#x200B;**[!UICONTROL 管理源]**&#x200B;权限。 请联系您的产品管理员以获取必要的权限。 有关详细信息，请阅读[访问控制UI指南](../../../access-control/abac/ui/permissions.md)。

### 文件和目录的命名约束

在命名云存储文件或目录时，必须考虑以下列出的限制：

* 目录和文件组件名称不能超过255个字符。
* 目录和文件名不能以正斜杠(`/`)结尾。 如果提供，它将自动删除。
* 以下保留URL字符必须正确转义： `! ' ( ) ; @ & = + $ , % # [ ]`
* 不允许使用以下字符： `" \ / : | < > * ?`。
* 不允许使用非法的URL路径字符。 诸如`\uE000`之类的代码点虽然在NTFS文件名中有效，但不是有效的Unicode字符。 此外，不允许使用某些ASCII或Unicode字符，如控制字符（0x00到0x1F、\u0081等）。 有关HTTP/1.1中Unicode字符串的规则，请参阅[RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
* 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、点字符(.)和两个点字符(..)。

### 收集所需的凭据

Experience Platform上的[!DNL Bombora]由[!DNL Google Cloud Storage]托管。 为了成功验证您的[!DNL Bombora]帐户，您必须为以下凭据提供适当的值：

| 凭据 | 描述 |
| --- | --- |
| 访问密钥 ID | [!DNL Bombora]访问密钥ID。 这是一个由61个字符组成的字母数字字符串，向Experience Platform验证您的帐户时需要使用该字符串。 |
| 访问密钥 | [!DNL Bombora]访问密钥。 这是一个40字符、以base-64编码的字符串，向Experience Platform验证您的帐户时需要使用该字符串。 |
| 存储桶名称 | 将从其中提取数据的[!DNL Bombora]存储段。 |

有关这些凭据的详细信息，请阅读[[!DNL Google Cloud Storage] HMAC密钥指南](https://cloud.google.com/storage/docs/authentication/hmackeys#overview)。 有关如何生成自己的访问密钥的步骤，请阅读 [!DNL Google Cloud Storage] 源概述](../cloud-storage/google-cloud-storage.md#prerequisite-setup-for-connecting-your-google-cloud-storage-account)中的[先决条件指南。

## [!DNL Bombora]架构 {#schema}

有关[!DNL Bombora]架构和数据结构的信息，请阅读此部分。

[!DNL Bombora]架构称为&#x200B;**帐户意图每周**。 它是关于指定帐户和主题的每周意图信息（匿名B2B购买者研究和内容使用）。 数据采用parquet格式。

| 字段名称 | 数据类型 | 必需 | 业务密钥 | 注释 |
| --- | --- | --- | --- | --- |
| `Account_Name` | 字符串 | TRUE | 是 | 公司的正式名称。 |
| `Domain` | 字符串 | TRUE | 是 | 表明意图的已识别帐户的域。 |
| `Topic_Id` | 字符串 | TRUE | 是 | [!DNL Bombora]主题ID |
| `Topic_Name` | 字符串 | TRUE | | [!DNL Bombora]主题名称。 |
| `Cluster_Name` | 字符串 | TRUE | | 给定主题的[!DNL Bombora]上的群集名称。 |
| `Cluster_Id` | 字符串 | TRUE | | 与给定主题关联的集群ID。 |
| `Composite_Score` | 整数 | TRUE | | 复合分数表示指定时间段内给定主题的域消耗模式。 复合分数是介于0和100之间的值，其中100表示可能的最高分数，0表示可能的最低分数。 超过60的复合分数表示领域对特定主题的兴趣增加。 这也称为“激增”。 |
| `Partition_Date` | 日期 | TRUE | | 快照的日历日期。 每周末以`mm/dd/yyyy`格式完成此工作。 |

{style="table-layout:auto"}

>[!TIP]
>
>对架构所做的任何更改都将提前发送给Adobe。 为了支持无缝模式演变，保持向后兼容性至关重要。 Experience Platform强制实施仅限添加器的版本化方法，确保对架构的任何更新都是无损的。 这意味着严格禁止重大更改，并且只允许增强或扩展现有架构的更改。

## 在用户界面中将您的[!DNL Bombora]帐户连接到Experience Platform

完成先决条件设置后，请阅读有关[将您的 [!DNL Bombora] 帐户连接到Experience Platform](../../tutorials/ui/create/data-partners/bombora.md)的教程以开始集成。

## 常见问题解答 {#faq}

请阅读本节以获取有关[!DNL Bombora]源的常见问题解答。

### 我是否需要与[!DNL Bombora]签订现有合同才能在Real-Time CDP B2B edition中使用其帐户意图数据？

+++回答

是，您必须与[!DNL Bombora]签订有效合同才能在Experience Platform和Real-Time CDP B2B edition中访问和使用其意图数据。 该集成利用您与[!DNL Bombora]的现有协议在Experience Platform和Real-Time CDP中摄取和激活帐户意图信号。

+++

### 此集成中是否支持[!DNL Bombora]中的自定义字段？

+++回答

目前，您只能使用标准[!DNL Bombora]字段进行摄取和激活。 要查看支持的字段列表，请阅读[[!DNL Bombora] 架构指南](#schema)以了解有关字段可用性的详细信息。

+++

### 我能否临时将数据从[!DNL Bombora]摄取到Experience Platform？

+++回答

是，您可以临时从[!DNL Bombora]引入数据。 您可以创建新数据流以摄取最新意图数据，只要有来自[!DNL Bombora]的新数据。 但是，一次只能有一个活动数据流。 因此，在创建新数据流之前，请确保删除现有数据流。

+++

### 意图数据的验证流程是什么，如何检查哪个意图数据已链接到特定帐户？

+++回答

要验证意图数据并确定哪些意图信号已链接到特定帐户，请使用[Adobe Experience Platform查询服务](../../../query-service/home.md)（通过AccountID）

+++

### 如何查找特定公司的意图？

+++回答

在[查询服务](../../../query-service/home.md)中执行SQL查询，以使用公司名称或AccountID搜索目的数据。 要查看特定公司的所有意图数据，您可以使用公司名称或AccountID在Query Service中运行SQL查询以获取所有关联的意图信号。

+++


### 我在Experience Platform中发现帐户匹配过程存在问题，我该怎么办？

+++回答

解决办法取决于具体问题：

* **Experience Platform中的公司域不正确或缺少公司域**：如果问题源自帐户数据中的公司域值不正确，请更新Experience Platform中的公司域字段以确保准确匹配。
* **数据流中的字段映射不正确**：如果问题是由数据流中的公司域字段路径不正确导致的，请更新数据流配置以引用正确的字段路径。

+++

### 如何删除Experience Platform中的目的数据？

+++回答

您必须[删除数据集](../../../catalog/datasets/user-guide.md#delete-a-dataset)才能删除Experience Platform中的意图数据。

+++

### 使用哪个字段将[!DNL Bombora]中的帐户与Experience Platform匹配？

+++回答

`accountOrganization.domain`字段用于匹配帐户。 如果您的组织使用其他自定义字段来存储网站名称，请确保您提供正确的字段路径，以便进行准确映射。

+++

### 在Experience Platform中更新公司域时会发生什么？

+++回答

更新公司域时，将在下次数据流运行时应用新域值。 这可确保：

* 未来意图数据摄取使用更新的域进行帐户匹配。
* 任何以前不匹配的意图信号现在可能正确与预期帐户对齐。
* 不会对过去摄取的仅数据新数据进行追溯性更改，传入数据将反映更新。

+++

### 域匹配过程是怎样的？

+++回答

Experience Platform中的域匹配基于与已清理的域字段值的精确匹配。 Experience Platform会自动删除前缀(例如https:/<span>/www.)，并保留顶级域(例如adobe.com)。 匹配需要精确的域值，不支持模糊匹配或子域。

+++

### 可在何处使用意图数据？

+++回答

可在[帐户受众](../../../segmentation/types/account-audiences.md)中使用意图数据来增强定位、分段和个性化。 通过利用意图信号，企业可以识别对特定主题表现出高度兴趣的客户，并与他们互动，从而优化营销和销售推广。

+++
