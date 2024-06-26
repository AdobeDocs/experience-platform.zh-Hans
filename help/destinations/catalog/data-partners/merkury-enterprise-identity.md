---
title: Merkury企业标识目标
description: 了解如何使用Adobe Experience Platform UI创建Merkury Enterprise Identity目标连接。
hide: true
hidefromtoc: true
source-git-commit: 66a0a085e696dbe13d0368da395f655c7ca01a97
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 2%

---


# Merkury企业标识目标

>[!NOTE]
>
>目标连接器和文档页面由Merkury团队创建和维护。 如有任何查询或更新请求，请联系您的Merkury客户代表。

## 概述

使用Merkury Enterprise Identity目标构建更准确、全面且富有洞察力的消费者用户档案。 通过改进的配置文件数据，营销人员可以更好地提供见解、区段和模型，从而更准确地定位和预测建模。

![显示Merkury与Experience Platform之间的互连关系（包括引入和激活）的图表](../../assets/catalog/data-partners/merkury-identity/media/image1.png)

按照此文档页面中的步骤操作，创建一个Merkury Identity目标连接，并激活受众，以便使用Adobe Experience Platform用户界面进行识别和扩充。

>[!NOTE]
>
>如果您希望使用Merkury Connect帐户将受众激活到媒体目标，请改用我们的Merkury Connections目标。

![Experience Platform目标目录中高亮显示的Merkury企业身份目标卡。](../../assets/catalog/data-partners/merkury-identity/media/image2.png)

## 用例

Merkury Enterprise Identity Destination为以下Merkury功能提供了安全传输消费者PII的功能：

* **数据质量**：通过数据卫生和标准化提高消费者个人资料数据质量。 Merkury包含美国邮政卫生和移动识别，以支持最先进的直邮营销用例。
* **身份解析**：通过Merkury个人和家庭ID生成准确、全面的客户单一视图。 Merkury ID提供了深度个人资料链接，由Merkury提供的涉及2.68亿以上的美国成人消费者身份的综合图表提供支持。
* **扩充**：利用Merkury数据获得更好的见解和个性化。 Merkury数据包括10,000多种可用数据属性，这些属性涵盖人口统计、生活方式、财务、生活事件以及Merkury数据包中的购买数据。

>[!NOTE]
>
>这些用例通过目标和源连接器的组合执行。 客户将从导出其现有客户记录开始，以便使用此目标连接器进行扩充。 Merkury的服务将搜索文件、检索文件、使用Merkury的数据扩充文件并生成文件。 然后，客户将使用相应的Merkury Source连接器源卡将水合的客户配置文件摄取回Adobe Real-Time CDP。

## 先决条件

>[!IMPORTANT]
>
>* 要连接到目标，您需要 **查看目标** 和 **管理目标**， **激活目标**， **查看配置文件**、和 **查看区段** [[访问控制权限]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions). 阅读 [[访问控制概述]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **查看身份图** [[访问控制权限]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions).\！[选择工作流中突出显示的身份命名空间以将受众激活到目标。](../../assets/catalog/data-partners/merkury-identity/media/image3.png)

## 支持的身份 {#supported-identities}

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| GAID | Google广告ID | 当源身份是GAID命名空间时，选择GAID目标身份。 |
| IDFA | 广告商的Apple ID | 当源身份是IDFA命名空间时，选择IDFA目标身份。 |
| ECID | Experience Cloud ID | 表示ECID的命名空间。 此命名空间还可以由以下别名引用：“Adobe Marketing Cloud ID”、“Adobe Experience Cloud ID”、“Adobe Experience Platform ID”。 请参阅以下文档： [ECID](/help/identity-service/features/ecid.md) 以了解更多信息。 |
| phone_sha256 | 使用SHA256算法散列的电话号码 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码。 当源字段包含未哈希处理的属性时，请检查 **[!UICONTROL 应用转换]** 选项，拥有 [!DNL Platform] 在激活时自动散列数据。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希处理的属性时，请检查 **[!UICONTROL 应用转换]** 选项，拥有 [!DNL Platform] 在激活时自动散列数据。 |
| extern_id | 自定义用户标识 | 当源身份是自定义命名空间时，请选择此目标身份。 |

{style="table-layout:auto"}

## 支持的受众

此部分介绍可将哪种类型的受众导出到此目标。

| **受众** | **支持** | **描述** | **来源** |
|---|---|---|---|
| Segmentation Service | ✓ {\f13 } | 通过Experience Platform生成的受众 [[分段服务]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home). |
| 自定义上传 | x | 受众 [[已导入]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/overview#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率

有关目标导出类型和频率的信息，请参阅下表。

|**Audience**|**Supported**|**Description origin**|            
|---|---|---|      
|Segmentation Service|✓|Audiences generated through the Experience Platform [[Segmentation Service]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home).|
Custom uploads|X|Audiences [[imported]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/overview#import-audience) into Experience Platform from CSV files.

{style="table-layout:auto"}

## 连接到目标

>[!IMPORTANT]
>
>要连接到目标，您需要 **查看目标** 和 **管理和激活数据集目标** [[访问控制权限]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions). 阅读 [[访问控制概述]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [[目标配置教程]](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/connect-destination). 在目标配置工作流中，填写下面两个部分中列出的字段。

### 验证目标

要向目标进行身份验证，请填写必填字段并选择 **连接到目标**.

要在Experience Platform时访问存储段，您需要为以下凭证提供有效值：

| **凭据** | **描述** |
|---|---|
| 访问密钥 | 存储段的访问密钥ID。 您可以从Merkury团队检索此值。 |
| 密钥 | 存储桶的密钥ID。 您可以从Merkury团队检索此值。 |
| 存储桶名称 | 这是将共享文件的存储段。 您可以从Merkury团队检索此值。 |

{style="table-layout:auto"}

![新建目标创建屏幕](../../assets/catalog/data-partners/merkury-identity/media/image4.png)

### 填写目标详细信息

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![目标详细信息的屏幕截图](../../assets/catalog/data-partners/merkury-identity/media/image6.png)


* **名称（必填）**  — 保存目标的名称
* **描述**  — 简短说明目标的用途
* **存储段名称（必需）** - S3上设置的Amazon S3存储段的名称
* **文件夹路径（必需）**  — 如果使用存储段中的子目录，则必须定义路径，或使用“/”引用根路径。
* **文件类型**  — 选择导出文件应使用的格式Experience Platform。 请咨询您的Merkury团队，了解您帐户所需的文件类型。

>[!NOTE]
>
>当选择CSV选项时，将会显示分隔符、引号字符、转义字符、空值、空值、压缩格式和包括清单文件选项，请咨询您的Merkury团队为您的帐户提供合适的设置。

![csv选项图像](../../assets/catalog/data-partners/merkury-identity/media/image8.png)

### 现有帐户

已使用Merkury Enterprise Identity目标定义的帐户将显示在列表弹出窗口中。 选中后，您可以在右边栏中查看有关帐户的详细信息。 从UI查看示例，当您导航到 **目标** > **帐户**；

![目标帐户页面中的目标帐户屏幕截图](../../assets/catalog/data-partners/merkury-identity/media/image5.png)


### 启用警报

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/alerts).

完成提供目标连接的详细信息后，选择 **下一个**.

## 激活此目标的受众

>[!IMPORTANT]
>
>* 要激活数据，您需要具有查看目标、激活目标、查看配置文件和查看区段访问控制权限。 请阅读访问控制概述或联系您的产品管理员以获取所需权限。
>* 要导出身份，您需要具有查看身份图形访问控制权限。

读取 [将受众数据激活到批量配置文件导出目标](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations) 有关将受众激活到此目标的说明。

## 映射建议

在Merkury端正确处理文件需要名称和地址元素。 虽然并非所有元素都是必需的，但尽可能多地提供将有助于成功匹配。

映射建议如下表所示，其中列出了Merkury处理使用且客户可以将配置文件属性映射到的目标端属性。 将这些元素视为建议，因为并非所有元素都是必需的，并且源值将取决于帐户的需求。

| 目标字段 | 源描述 |
|---|---|
| ID | 用于通过Merkury Enterprise身份解析源连接器将Merkury数据映射到Experience Platform的“身份”字段 |
| Input_First_Name | 此 `person.name.firstName` Experience Platform值。 |
| Input_Last_Name | 此 `person.name.lastName` Experience Platform值。 |
| Input_Address_Line_1 | 此 `mailingAddress.street` Experience Platform值。 |
| 输入城市 | 此 `mailingAddress.city` Experience Platform值。 |
| Input_State_Providle_Code | 此 `mailingAddress.state` Experience Platform值。 如果状态采用双字符代码形式，则使用。 |
| Input_State_Providle_Name | 此 `mailingAddress.state` Experience Platform值。 如果状态是完整的状态名称，则使用 |
| Input_Post_Code | 此 `mailingAddress.postalCode` Experience Platform值。 |
| 输入电子邮件地址 | 您希望映射为配置文件电子邮件地址的值。 |
| Input_Phone | 要映射为配置文件电话号码的值。 |

{style="table-layout:auto"}

## 验证数据导出

要验证数据是否已成功导出，请检查您的Amazon S3存储段，并确保导出的文件包含预期的配置文件人口。

## 数据使用和治理

在处理您的数据时，所有Adobe Experience Platform目标都符合数据使用策略。 有关Adobe Experience Platform如何实施数据管理的详细信息，请参阅 [数据管理概述](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home).

## 后续步骤

通过学习本教程，您已成功创建了一个数据流以将配置文件数据从Experience Platform导出到Merkury管理的S3位置。 接下来，您需要联系Merkury代表，提供帐户名称、文件名和存储段路径，以便能够设置处理。
