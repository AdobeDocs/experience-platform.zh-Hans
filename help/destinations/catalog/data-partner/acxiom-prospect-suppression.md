---
title: Acxiom Prospect-Suppression
description: 将您的第一方受众导出到Acxiom目标，以允许Acxiom抑制已知或转换的客户。 然后，使用Acxiom源连接器从Acxiom中摄取并激活潜在客户列表，并删除已知或转换的客户。
last-substantial-update: 2024-03-14T00:00:00Z
badge: Beta 版
exl-id: d82e8cd3-970c-44af-99b0-ea154eb3655e
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1466'
ht-degree: 2%

---

# [!DNL Acxiom Prospect-Suppression]目标连接

>[!NOTE]
>
>[!DNL Acxiom Prospect-Suppression]目标为测试版。 此目标连接器和文档页面由Acxiom团队创建和维护。 如有任何查询或更新请求，请直接通过acxiom-adobe-help@acxiom.com联系。

## 概述 {#overview}

使用[!DNL Acxiom Prospect-Suppression]提供尽可能多的潜在客户受众。 此连接器从Real-time Customer Data Platform安全导出第一方数据，并通过屡获殊荣的卫生和身份解析运行该数据，该解析会生成要用作禁止列表的数据文件。 这将与[!DNL Acxiom Global]数据库匹配，该数据库允许为导入定制目标客户列表。 然后，使用[[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md)源连接器将潜在客户列表从Acxiom返回Real-Time CDP，并删除您的已知或转换的客户。

![将第一方数据导出到Acxiom，然后将目标客户数据导入回Real-Time CDP的营销图](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow.png)

Acxiom通过超过12,000个全球数据属性中的最大目录为业界表现最佳的受众提供了专门用于提供个性化体验的数据属性。 利用高质量数据的无限组合，创建和分发受众以满足特定的营销活动需求。

本教程提供了使用Adobe Experience Platform用户界面创建[!DNL Acxiom Prospect-Suppression]目标连接和数据流的步骤。 此连接器使用Amazon S3作为放置点向Acxiom潜在客户服务传送数据。 将文件导出到Amazon S3放置点后，请与Acxiom客户代表联系。

![已选择Acxiom目标的目标目录。](../../assets/catalog/data-partner/acxiom/image-destination-catalog.png)

## 用例 {#use-cases}

为了帮助您更好地了解您应如何以及何时使用[!DNL Acxiom Prospect-Suppression]目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 为潜在客户数据集创建禁止列表 {#create-suppression-list}

营销专业人员为了提高其外联战略的有效性，通常采用创建禁止名单。 此列表包括现有客户和特定区段，以确保在有针对性的营销活动中将其排除在潜在客户活动之外。 这种战略方法有助于优化受众，避免多余的沟通，并有助于更集中和更高效的营销工作。

例如，作为营销人员，您可能希望通过根据提供的分段和抑制标准向营销活动添加定向潜在客户配置文件来扩大营销活动范围。

用例通过目标和源连接器的组合执行。

您最初会使用此目标连接器导出现有的客户配置文件以用作禁止显示文件。 这可确保不包括现有客户记录。

Acxiom的服务将搜索文件、检索该文件并将其与其他选择标准一起使用，并生成目标客户文件。 然后，您将使用相应的[[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md)源连接器将潜在客户配置文件摄取到Adobe Real-Time CDP。

## 先决条件 {#prerequisites}

>[!IMPORTANT]
>
>* 若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

## 支持的受众 {#supported-audiences}

此部分介绍可将哪种类型的受众导出到此目标。

| 受众来源 | 支持 | 描述 |
|-----------------------------|-----------|---------------------------------------------------------------------------------------------------------------------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform[分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | x | 受众[已将](../../../segmentation/ui/audience-portal.md#import-audience)从CSV文件导入到Experience Platform中。 |

{style="table-layout:auto"}


## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|------------------|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如[目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)的选择配置文件属性屏幕中所选。 |
| 导出频率 | **[!UICONTROL 批次]** | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 阅读有关[基于批处理文件的目标](/help/destinations/destination-types.md#file-based)的详细信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在目标配置工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要验证到目标，请填写必填字段并选择&#x200B;**[!UICONTROL 连接到目标]**。

要在Experience Platform时访问存储段，您需要为以下凭据提供有效值：

| 凭据 | 描述 |
|---------------|----------------------------------------------------------------------------------------------------------|
| S3访问密钥 | 存储段的访问密钥ID。 您可以从[!DNL Acxiom]团队中检索此值。 |
| S3密钥 | 存储桶的密钥ID。 您可以从[!DNL Acxiom]团队中检索此值。 |
| 存储桶名称 | 这是将共享文件的存储段。 您可以从[!DNL Acxiom]团队中检索此值。 |

### 新建帐户

要定义新的Acxiom Managed S3位置，请执行以下操作：

![新帐户](../../assets/catalog/data-partner/acxiom/image-destination-new-account.png)

### 现有帐户

已使用[!DNL Acxiom Prospect Suppression]目标定义的帐户将显示在列表弹出窗口中。 选中后，您可以在右边栏中查看有关帐户的详细信息。 当您导航到&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 帐户]**&#x200B;时，从UI查看示例：

![现有帐户](../../assets/catalog/data-partner/acxiom/image-destination-account.png)

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![目标详细信息](../../assets/catalog/data-partner/acxiom/image-destination-details.png)

* **名称（必需）** — 目标将保存到的名称
* **描述** — 目标的简短用途说明
* **Bucket名称（必需）** - S3上设置的Amazon S3存储段的名称
* **文件夹路径（必需）** — 如果使用存储段中的子目录，则必须定义路径，或使用“/”引用根路径。
* **文件类型** — 选择导出文件应使用的格式Experience Platform。 目前，Acxiom处理所需的唯一文件类型是CSV

>[!IMPORTANT]
>
>在选择CSV选项&#x200B;*分隔符*、*引号字符*、*转义字符*、*空值*、*空值*、*压缩格式*&#x200B;和&#x200B;*包含清单文件*&#x200B;选项时，以下文档将更详细地解释这些设置[配置格式设置选项](../../ui/batch-destinations-file-formatting-options.md)。

![CSV选项](../../assets/catalog/data-partner/acxiom/image-destination-csv-options.png)

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
>
>* 若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请阅读[将受众数据激活到批处理配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md)。

### 映射建议

处理需要名称和地址元素，但并非所有元素都需要提供，请尽可能多地提供一些以帮助成功匹配。  下表列出了目标端的属性，这些属性由Acxiom处理使用，客户可将配置文件属性映射到这些属性。  这应被视为建议，因为并非所有元素都是必需的，并且源值将取决于帐户的需求。

| 目标字段 | Source描述 |
|--------------|-------------------------------------------------------------|
| name | Experience Platform中的`person.name.fullName`值。 |
| firstName | Experience Platform中的`person.name.firstName`值。 |
| 姓氏 | Experience Platform中的`person.name.lastName`值。 |
| address1 | Experience Platform中的`mailingAddress.street1`值。 |
| address2 | Experience Platform中的`mailingAddress.street2`值。 |
| 城市 | Experience Platform中的`mailingAddress.city`值。 |
| state | Experience Platform中的`mailingAddress.state`值。 |
| zip | Experience Platform中的`mailingAddress.postalCode`值。 |

{style="table-layout:auto"}

>[!NOTE]
>
>以上未列出的其他字段将包含在导出中，但Acxiom处理会忽略这些字段。

## 查看您的数据流

使用“复查”页可在提交之前查看数据流摘要

![审核](../../assets/catalog/data-partner/acxiom/image-destination-review.png)

## 验证数据导出 {#exported-data}

要验证数据是否已成功导出，请检查您的[!DNL Amazon S3 Storage]存储段并确保导出的文件包含预期的配置文件人口。

## 后续步骤

通过完成本教程，您已成功创建数据流以将批次数据从Experience Platform导出到[!DNL Acxiom]托管的S3位置。 您需要与Acxiom代表联系，并提供帐户名称、文件名和存储段路径，以便能够设置处理。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请阅读[数据治理概述](/help/data-governance/home.md)。

## 其他资源 {#additional-resources}

*Acxiom受众数据和分发：* https://www.acxiom.com/customer-data/audience-data-distribution/
