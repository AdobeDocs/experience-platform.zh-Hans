---
title: Merkury企业标识目标
description: 了解如何使用Adobe Experience Platform UI创建Merkury Enterprise Identity目标连接。
last-substantial-update: 2024-07-20T00:00:00Z
exl-id: a5452183-289c-49c3-9574-e09b0153dc00
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 3%

---

# Merkury企业标识目标

>[!NOTE]
>
>目标连接器和文档页面由[!DNL Merkury]团队创建和维护。 有关查询或更新请求，请联系您的[!DNL Merkury]客户代表。

## 概述

使用 [!DNL Merkury Enterprise Identity] 目标来建立更准确、更全面、更有洞察力的消费者档案。通过改进的配置文件数据，营销人员可以更好地提供见解、区段和模型，从而更准确地定位和预测建模。

![显示Merkury与Experience Platform之间互连的图表，包括引入和激活](../../assets/catalog/data-partners/merkury-identity/media/image1.png)

按照此文档页面中的步骤创建[!DNL Merkury Identity]目标连接并激活受众，以便使用Adobe Experience Platform用户界面进行识别和扩充。

>[!NOTE]
>
>如果要使用[!DNL Merkury Connect]帐户将受众激活到媒体目标，请改用[!DNL Merkury Connections]目标。

![Experience Platform目标目录中突出显示的Merkury Enterprise标识目标卡。](../../assets/catalog/data-partners/merkury-identity/media/image2.png)

## 用例

[!DNL Merkury Enterprise Identity]目标提供安全传输以下[!DNL Merkury]功能的消费者PII的功能：

* **数据质量**：通过数据卫生和标准化提高使用者配置文件数据质量。 [!DNL Merkury]包含美国邮政卫生和移动标识，以支持最先进的直邮营销用例。
* **身份解析**：通过[!DNL Merkury]个人和家庭ID生成准确、全面的客户单一视图。 Merkury ID提供了由[!DNL Merkury]提供的2.68亿以上的美国成人消费者身份综合图表支持的深层配置文件链接。
* **扩充**：使用[!DNL Merkury Data]获得更好的见解和个性化。 [!DNL Merkury Data]包括超过10,000个可用数据属性，这些属性包括人口统计、生活方式、财务、生活事件和来自[!DNL Merkury Data Suite]的购买数据。

>[!NOTE]
>
>这些用例通过目标和源连接器的组合执行。 客户将从导出其现有客户记录开始，以便使用此目标连接器进行扩充。 [!DNL Merkury]的服务将搜索文件、检索文件、使用[!DNL Merkury]的数据扩充文件并生成文件。 然后，客户将使用相应的[!DNL Merkury]个Source连接器源卡将水合的客户配置文件摄取回Adobe Real-Time CDP。

## 先决条件

>[!IMPORTANT]
>
>* 若要连接到目标，您需要&#x200B;**查看目标**&#x200B;和&#x200B;**管理目标**、**激活目标**、**查看配置文件**&#x200B;和&#x200B;**查看区段** [[访问控制权限]](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/access-control/home#permissions)。 阅读[[访问控制概述]](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/access-control/ui/overview)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**查看标识图形** [[访问控制权限]](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/access-control/home#permissions)。\！[选择工作流中突出显示的身份命名空间以将受众激活到目标。](../../assets/catalog/data-partners/merkury-identity/media/image3.png)

## 支持的身份 {#supported-identities}

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | 当源身份是GAID命名空间时，选择GAID目标身份。 |
| IDFA | 广告商的Apple ID | 当源身份是IDFA命名空间时，选择IDFA目标身份。 |
| ECID | Experience Cloud ID | 表示ECID的命名空间。 此命名空间还可以由以下别名引用：“Adobe Marketing Cloud ID”、“Adobe Experience Cloud ID”、“Adobe Experience Platform ID”。 有关详细信息，请参阅[ECID](/help/identity-service/features/ecid.md)上的以下文档。 |
| phone_sha256 | 使用SHA256算法散列的电话号码 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL 应用转换]**&#x200B;选项，以使[!DNL Experience Platform]在激活时自动对数据进行哈希处理。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL 应用转换]**&#x200B;选项，以使[!DNL Experience Platform]在激活时自动对数据进行哈希处理。 |
| extern_id | 自定义用户标识 | 当源身份是自定义命名空间时，请选择此目标身份。 |

{style="table-layout:auto"}

## 支持的受众

此部分介绍可将哪种类型的受众导出到此目标。

| **受众** | **支持** | **描述** | **来源** |
|---|---|---|---|
| Segmentation Service | ✓ | 通过Experience Platform [[分段服务]](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/segmentation/home)生成的受众。 |
| 自定义上传 | x | 受众[[已将]](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/segmentation/ui/overview#import-audience)从CSV文件导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率

有关目标导出类型和频率的信息，请参阅下表。

| **受众** | **支持** | **描述来源** |
|---|---|---|      
| Segmentation Service | ✓ | 通过Experience Platform [[分段服务]](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/segmentation/home)生成的受众。 |
| 自定义上传 | X | 受众[[已将]](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/segmentation/ui/overview#import-audience)从CSV文件导入Experience Platform。 |

{style="table-layout:auto"}

## 连接到目标

>[!IMPORTANT]
>
>若要连接到目标，您需要&#x200B;**查看目标**&#x200B;和&#x200B;**管理和激活数据集目标** [[访问控制权限]](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/access-control/home#permissions)。 阅读[[访问控制概述]](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/access-control/ui/overview)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[[目标配置教程]](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/destinations/ui/connect-destination)中描述的步骤操作。 在目标配置工作流中，填写下面两个部分中列出的字段。

### 验证目标

要验证到目标，请填写必填字段并选择&#x200B;**连接到目标**。

要在Experience Platform上访问存储段，您需要为以下凭据提供有效值：

| **凭据** | **描述** |
|---|---|
| 访问密钥 | 存储段的访问密钥ID。 您可以从Merkury团队检索此值。 |
| 密钥 | 存储桶的密钥ID。 您可以从Merkury团队检索此值。 |
| 存储桶名称 | 这是将共享文件的存储段。 您可以从Merkury团队检索此值。 |

{style="table-layout:auto"}

![新目标创建屏幕](../../assets/catalog/data-partners/merkury-identity/media/image4.png)

### 填写目标详细信息

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![目标详细信息的屏幕快照](../../assets/catalog/data-partners/merkury-identity/media/image6.png)


* **名称（必需）** — 目标将保存到的名称
* **描述** — 目标的简短用途说明
* **Bucket名称（必需）** - S3上设置的Amazon S3存储段的名称
* **文件夹路径（必需）** — 如果使用存储段中的子目录，则必须定义路径，或使用“/”引用根路径。
* **文件类型** — 选择Experience Platform应用于导出文件的格式。 请咨询您的Merkury团队，了解您帐户所需的文件类型。

>[!NOTE]
>
>当选择CSV选项、分隔符、引号字符、转义字符、空值、空值、压缩格式和包括清单文件选项时，请咨询您的Merkury团队，以获取适合您帐户的相应设置。

csv选项![&#128279;](../../assets/catalog/data-partners/merkury-identity/media/image8.png)的图像

### 现有帐户

已使用Merkury Enterprise Identity目标定义的帐户将显示在列表弹出窗口中。 选中后，您可以在右边栏中查看有关帐户的详细信息。 当您导航到&#x200B;**目标** > **帐户**&#x200B;时，从UI查看示例；

![目标帐户页面中的目标帐户屏幕截图](../../assets/catalog/data-partners/merkury-identity/media/image5.png)


### 启用警报

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/destinations/ui/alerts)。

完成提供目标连接的详细信息后，选择&#x200B;**下一步**。

## 激活此目标的受众

>[!IMPORTANT]
>
>* 若要激活数据，您需要&#x200B;**查看目标**、**激活目标**、**查看配置文件**&#x200B;和&#x200B;**查看区段**&#x200B;访问控制权限。 请阅读访问控制概述或联系您的产品管理员以获取所需权限。
>* 要导出身份，您需要&#x200B;**查看身份图形**&#x200B;访问控制权限。

有关将受众激活到此目标的说明，请阅读[将受众数据激活到批处理配置文件导出目标](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)。

## 映射建议

对[!DNL Merkury]端文件的正确处理需要名称和地址元素。 虽然并非所有元素都是必需的，但尽可能多地提供将有助于成功匹配。

下表提供了映射建议，其中列出了[!DNL Merkury]处理所使用的目标端属性，客户可以将配置文件属性映射到这些属性。 将这些元素视为建议，因为并非所有元素都是必需的，并且源值将取决于帐户的需求。

| 目标字段 | Source描述 |
|---|---|
| ID | 用于通过[!DNL Merkury Enterprise Identity] Source连接器将[!DNL Merkury]数据映射到Experience Platform的标识字段 |
| Input_First_Name | Experience Platform中的`person.name.firstName`值。 |
| Input_Last_Name | Experience Platform中的`person.name.lastName`值。 |
| Input_Address_Line_1 | Experience Platform中的`mailingAddress.street`值。 |
| 输入城市 | Experience Platform中的`mailingAddress.city`值。 |
| Input_State_Providle_Code | Experience Platform中的`mailingAddress.state`值。 如果状态采用双字符代码形式，则使用。 |
| Input_State_Providle_Name | Experience Platform中的`mailingAddress.state`值。 如果状态是完整的状态名称，则使用 |
| Input_Post_Code | Experience Platform中的`mailingAddress.postalCode`值。 |
| 输入电子邮件地址 | 您希望映射为配置文件电子邮件地址的值。 |
| Input_Phone | 要映射为配置文件电话号码的值。 |

{style="table-layout:auto"}

## 验证数据导出

要验证数据是否已成功导出，请检查您的Amazon S3存储段，并确保导出的文件包含预期的配置文件人口。

## 数据使用和治理

在处理您的数据时，所有Adobe Experience Platform目标都符合数据使用策略。 有关Adobe Experience Platform如何实施数据治理的详细信息，请阅读[数据管理概述](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/data-governance/home)。

## 后续步骤

通过学习本教程，您已成功创建数据流以将配置文件数据从Experience Platform导出到[!DNL Merkury]托管的S3位置。 接下来，您需要联系[!DNL Merkury]代表，提供帐户名称、文件名和存储段路径，以便能够设置处理。
