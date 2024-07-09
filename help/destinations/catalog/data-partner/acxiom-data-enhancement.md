---
title: Acxiom数据增强
description: 使用此连接器可在Real-Time CDP中将第一方Adobe配置文件激活到Acxiom，以便跨营销渠道扩充和使用。 然后，您可以使用Acxiom源导入具有增强数据的用户档案，并在Real-Time CDP中使用这些用户档案。
last-substantial-update: 2024-03-14T00:00:00Z
badge: Beta 版
exl-id: 59edc43d-ae8e-4c3d-820c-b5be1c4483f9
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 2%

---

# [!DNL Acxiom Data Enhancement] 目标连接

>[!NOTE]
>
>此 [!DNL Acxiom Data Enhancement] 目标为测试版。  此目标连接器和文档页面由Acxiom团队创建和维护。 如有任何查询或更新请求，请直接通过acxiom-adobe-help@acxiom.com联系。

## 概述 {#overview}

使用 [!DNL Acxiom Data Enhancement] 连接器，为您的客户配置文件提供其他描述性数据，用于分析、分段和定位应用程序。 利用数百个可用元素，可更好地细分和建模数据，从而实现更准确的定位和预测建模。

![将第一方数据导出到Acxiom，然后将扩充数据导入回Real-Time CDP的营销图](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow-data-enhancement.png)

本教程提供了创建 [!DNL Acxiom Data Enhancement] 目标连接和数据流(使用Adobe Experience Platform用户界面)。 此连接器用于向使用Amazon S3作为放置点的Acxiom增强服务传送数据。

![已选择Acxiom目标的目标目录。](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-catalog.png)

## 用例 {#use-cases}

为了帮助您更好地了解您应该如何以及何时使用 [!DNL Acxiom Data Enhancement] 目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 增强客户数据 {#enhance-customer-data}

营销专业人士应使用此连接器，通过将选定的描述性元素附加到客户配置文件中，并使用这些元素更好地定位活动，以提高其外联策略的效率。

例如，作为营销人员，您可能希望通过用其他数据丰富现有受众的用户档案，从而加深对现有受众的了解。 这样做将改进分段和定位策略，从而提高营销活动的个性化和转化。

用例通过目标和源连接器的组合执行。

首先，您可以导出现有客户记录以使用此目标连接器进行扩充。 Acxiom的服务将搜索文件、检索文件、使用Acxiom的数据扩充文件并生成文件。

然后，客户将使用相应的 [Acxiom数据摄取](/help/sources/connectors/data-partners/acxiom-data-ingestion.md) 源卡，用于将水合的客户配置文件提取回Adobe Real-Time CDP。

## 先决条件 {#prerequisites}

>[!IMPORTANT]
>
>* 要连接到目标，您需要 **[!UICONTROL 查看目标]** 和 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

## 支持的受众 {#supported-audiences}

此部分介绍可将哪种类型的受众导出到此目标。

| 受众来源 | 支持 | 描述 |
|-----------------------------|-----------|---------------------------------------------------------------------------------------------------------------------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md). |
| 自定义上传 | x | 受众 [已导入](../../../segmentation/ui/audience-portal.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}


## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|------------------|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如 [目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频率 | **[!UICONTROL 批次]** | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 详细了解 [批处理基于文件的目标](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要 **[!UICONTROL 查看目标]** 和 **[!UICONTROL 管理和激活数据集目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在目标配置工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要向目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

要在Experience Platform时访问存储段，您需要为以下凭据提供有效值：

| 凭据 | 描述 |
|---------------|----------------------------------------------------------------------------------------------------------|
| S3访问密钥 | 存储段的访问密钥ID。 此值可取自 [!DNL Acxiom] 团队。 |
| S3密钥 | 存储桶的密钥ID。 此值可取自 [!DNL Acxiom] 团队。 |
| 存储桶名称 | 这是将共享文件的存储段。 此值可取自 [!DNL Acxiom] 团队。 |

### 新建帐户

要定义新的Acxiom Managed S3位置，请执行以下操作：

![新建帐户](../../assets/catalog/data-partner/acxiom/image-destination-new-account.png)

### 现有帐户

已使用 [!DNL Acxiom Data Enhancement] 目标显示在列表弹出窗口中。 选中后，您可以在右边栏中查看有关帐户的详细信息。 从UI查看示例，当您导航到 **[!UICONTROL 目标]** > **[!UICONTROL 帐户]**；

![现有帐户](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-account.png)

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![目标详细信息](../../assets/catalog/data-partner/acxiom/image-destination-details.png)

* **名称（必填）**  — 保存目标的名称
* **描述**  — 简短说明目标的用途
* **存储段名称（必需）** - S3上设置的Amazon S3存储段的名称
* **文件夹路径（必需）**  — 如果使用存储段中的子目录，则必须定义路径，或使用“/”引用根路径。
* **文件类型**  — 选择导出文件应使用的格式Experience Platform。 目前，Acxiom处理所需的唯一文件类型是CSV

>[!IMPORTANT]
>
>选择CSV选项时， *分隔符*， *引号字符*， *转义字符*， *空值*， *空值*， *压缩格式*、和 *包含清单文件* 选项，以下文档将更详细地解释这些设置 [配置格式选项](../../ui/batch-destinations-file-formatting-options.md).

![CSV选项](../../assets/catalog/data-partner/acxiom/image-destination-csv-options.png)

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
>
>* 要激活数据，您需要 **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

读取 [将受众数据激活到批量配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md) 有关将受众激活到此目标的说明。

### 映射建议

在Acxiom端正确处理文件需要名称和地址元素。 虽然并非所有元素都是必需的，但尽可能多地提供将有助于成功匹配。

下表列出了目标端的属性，这些属性由Acxiom处理使用，客户可将配置文件属性映射到这些属性。 将这些元素视为建议，因为并非所有元素都是必需的，并且源值将取决于帐户的需求。

| 目标字段 | Source描述 |
|--------------|-------------------------------------------------------------|
| name | 此 `person.name.fullName` Experience Platform值。 |
| firstName | 此 `person.name.firstName` Experience Platform值。 |
| 姓氏 | 此 `person.name.lastName` Experience Platform值。 |
| address1 | 此 `mailingAddress.street1` Experience Platform值。 |
| address2 | 此 `mailingAddress.street2` Experience Platform值。 |
| 城市 | 此 `mailingAddress.city` Experience Platform值。 |
| state | 此 `mailingAddress.state` Experience Platform值。 |
| zip | 此 `mailingAddress.postalCode` Experience Platform值。 |

>[!NOTE]
>
>如果映射数据流中未列出的其他字段，这些字段将包含在数据导出中，但Acxiom处理会忽略这些字段。

## 验证数据导出 {#exported-data}

要验证数据是否已成功导出，请检查 [!DNL Amazon S3 Storage] 存储桶并确保导出的文件包含预期的用户档案人口。

## 后续步骤

通过学习本教程，您已成功创建了一个数据流以将配置文件数据从Experience Platform导出到 [!DNL Acxiom] 托管的S3位置。 接下来，您需要联系Acxiom代表，提供帐户名称、文件名和存储段路径，以便能够设置处理。

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 实施数据管理，请阅读 [数据管理概述](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

*Acxiom信息库：* https://www.acxiom.com/wp-content/uploads/2022/02/fs-acxiom-infobase_AC-0268-22.pdf
