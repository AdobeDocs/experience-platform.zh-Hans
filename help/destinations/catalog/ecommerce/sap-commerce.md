---
title: SAP Commerce连接
description: 使用SAP Commerce目标连接器更新SAP帐户中的客户记录。
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 3bd1a2a7-fb56-472d-b9bd-603b94a8937e
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '2175'
ht-degree: 3%

---

# [!DNL SAP Commerce]连接

[!DNL SAP Commerce] （以前称为[[!DNL Hybris]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html)）是适用于B2B和B2C企业的基于云的电子商务平台解决方案，作为SAP客户体验产品组合的一部分提供。 [[!DNL SAP] 订阅帐单](https://www.sap.com/products/financial-management/subscription-billing.html)是产品组合中的产品，通过标准化的集成，通过简化的销售和付款体验实现完整的订阅生命周期管理。

此[!DNL Adobe Experience Platform] [目标](/help/destinations/home.md)使用[[!DNL SAP Subscription Billing] 客户管理API](https://api.sap.com/api/BusinessPartner_APIs/path/PUT_customers-customerNumber)，在激活后从现有Experience Platform受众在[!DNL SAP Commerce]内更新您的客户详细信息。

下面的[!DNL SAP Commerce]向目标身份验证[部分中进一步提供了向您的](#authenticate)实例进行身份验证的说明。

## 用例 {#use-cases}

为了帮助您更好地了解您应如何以及何时使用[!DNL SAP Commerce]目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

[!DNL SAP Commerce]客户存储有关与您业务互动的个人或组织实体的信息。 您的团队使用[!DNL SAP Commerce]中的现有客户来构建Experience Platform受众。 将这些受众发送至[!DNL SAP Commerce]后，其信息会更新，并且会为每个客户分配一个属性，其值作为受众名称，指示客户属于哪个受众。

## 先决条件 {#prerequisites}

请参阅以下各节，了解在Experience Platform和[!DNL SAP Commerce]中必须设置的任何先决条件，以及在使用[!DNL SAP Commerce]目标之前必须收集的信息。

### Experience Platform先决条件 {#prerequisites-in-experience-platform}

在将数据激活到[!DNL SAP Commerce]目标之前，您必须在[中创建一个](/help/xdm/schema/composition.md)架构[、](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)数据集[和](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html)受众[!DNL Experience Platform]。

如果您需要有关受众状态的指导，请参阅Experience Platform文档，了解[受众成员资格详细信息架构字段组](/help/xdm/field-groups/profile/segmentation.md)。

### [!DNL SAP Commerce]目标的先决条件 {#prerequisites-destination}

请注意以下先决条件，以便将数据从Experience Platform导出到您的[!DNL SAP Commerce]帐户：

#### 您必须拥有[!DNL SAP Subscription Billing]帐户 {#prerequisites-account}

要将数据从Experience Platform导出到您的[!DNL SAP Commerce]帐户，您需要拥有[!DNL SAP Subscription Billing]帐户。 如果您没有有效的帐单帐户，请与您的[!DNL SAP]帐户管理员联系。 有关其他详细信息，请参阅[[!DNL SAP] 平台配置](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf)文档。

#### 生成服务密钥 {#prerequisites-service-key}

* [!DNL SAP Commerce]服务密钥允许您通过Experience Platform访问[!DNL SAP Subscription Billing] API。 请参阅[!DNL SAP Commerce] [创建具有客户端ID和客户端密钥的服务密钥](https://help.sap.com/docs/CLOUD_TO_CASH_OD/1216e7b79c984675b0a6f0005e351c74/87c11a0f5dc3494eaf3baa355925c030.html#create-a-service-key-with-client-id-and-client-secret)以创建服务密钥。 [!DNL SAP Commerce] 要求您满足以下条件：
   * 客户端 ID
   * 客户端密码
   * URL。 URL模式如下： `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`。 此值稍后将用于获取`Region`和`Endpoint`的值。

+++选择以查看服务键的示例

```json
{ 
    "url": "https://eu10.revenue.cloud.sap/api",
    "uaa": {
        "clientid": "XXX",
        "clientsecret": "XXX",
        "url": "https://subscriptionbilling.authentication.eu10.hana.ondemand.com",
        "identityzone": "subscriptionbilling",
        "identityzoneid": "XXX",
        "tenantid": "XXX",
        "tenantmode": "dedicated",
        "sburl": "https://internal-xsuaa.authentication.eu10.hana.ondemand.com",
        "apiurl": "https://api.authentication.eu10.hana.ondemand.com",
        "verificationkey": "XXX",
        "xsappname": "XXX",
        "subaccountid": "XXX",
        "uaadomain": "authentication.eu10.hana.ondemand.com",
        "zoneid": "XXX",
        "credential-type": "binding-secret"
    },
    "vendor": "SAP"
}
```

+++

#### 在[!DNL SAP Subscription Billing]中创建自定义引用 {#prerequisites-custom-reference}

要在[!DNL SAP Subscription Billing]中更新Experience Platform受众状态，您需要为Experience Platform中选择的每个受众都提供一个自定义参考字段。

要创建自定义引用，请登录到您的[!DNL SAP Subscription Billing]帐户并导航到&#x200B;**[主数据和配置]** > **[自定义引用]**&#x200B;页面。 接下来，选择&#x200B;**[!UICONTROL Create]**&#x200B;以为Experience Platform中选择的每个受众添加新引用。 在随后的[计划受众导出和示例](#schedule-segment-export-example)步骤中，您将需要这些参考字段名称。

下面显示了如何在&#x200B;**[!UICONTROL Reference Type]**&#x200B;中创建自定义[!DNL SAP Subscription Billing]的示例：
![显示在SAP订阅帐单中创建自定义引用的位置的图像。](../../assets/catalog/ecommerce/sap-commerce/create-custom-reference.png)

有关其他指导，请参阅[!DNL SAP Subscription Billing] [自定义引用](https://help.sap.com/docs/CLOUD_TO_CASH_OD/80d121f216af43648e79664efe5595f7/85696a63c8d8453a934e86c9413a25cf.html?version=2023-11-27)文档。

### 收集所需的凭据 {#gather-credentials}

要将[!DNL SAP Commerce]连接到Experience Platform，必须提供以下连接属性的值：

| 凭据 | 描述 |
| --- | --- |
| 客户端 ID | 服务键中`clientId`的值。 |
| 客户端密码 | 服务键中`clientSecret`的值。 |
| 终结点 | 服务键中`url`的值类似于`https://subscriptionbilling.authentication.eu10.hana.ondemand.com`。 |
| 区域 | 您的数据中心位置。 该区域存在于`url`中，其值类似于`eu10`或`us10`。 例如，如果`url`是`https://eu10.revenue.cloud.sap/api`，您需要`eu10`。 |

## 护栏 {#guardrails}

对[!DNL SAP Cloud Management service]的API请求遵循[速率限制](https://help.sap.com/docs/btp/sap-business-technology-platform/account-administration-rate-limiting)。 如果超过速率限制，您将遇到`HTTP 429 Too Many Requests`响应状态代码。

## 支持的身份 {#supported-identities}

[!DNL SAP Commerce]支持更新下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
| --- | --- | --- |
| `customerNumberSAP` | 您的[!DNL SAP Commerce]帐户中已存在个人或企业客户的客户标识符。 | 必需 |

## 支持的受众 {#supported-audiences}

此部分介绍可导出到此目标的所有受众。

此目标支持激活通过Experience Platform [分段服务](../../../segmentation/home.md)生成的所有受众。

此目标还支持激活下表所述的受众。

| 受众类型 | 支持 | 描述 |
| ------------- | --------- | ----------- |
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ | 受众[已从CSV文件将](../../../segmentation/ui/audience-portal.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Profile-based]** | <ul><li>您正在导出受众的所有成员，以及所需的架构字段&#x200B;*（例如：电子邮件地址、电话号码、姓氏）*（根据字段映射）。</li><li> 对于Experience Platform中的每个选定受众，相应的[!DNL SAP Commerce]附加属性将从Experience Platform中更新为其受众状态。</li></ul> |
| 导出频率 | **[!UICONTROL Streaming]** | <ul><li>流目标为基于API的“始终运行”连接。 当基于受众评估在Experience Platform中更新用户档案时，连接器会将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。</li></ul> |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>若要连接到目标，您需要&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

在&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**&#x200B;内，搜索[!DNL SAP Commerce]。 或者，您可以在&#x200B;**[!UICONTROL eCommerce]**&#x200B;类别下找到它。

### 验证目标 {#authenticate}

填写下面的必填字段。 有关任何指导，请参阅[生成服务密钥](#prerequisites-service-key)部分。

| 字段 | 描述 |
| --- | --- |
| **[!UICONTROL Client ID]** | 服务键中`clientId`的值。 |
| **[!UICONTROL Client secret]** | 服务键中`clientSecret`的值。 |
| **[!UICONTROL Endpoint]** | 服务键中`url`的值类似于`https://subscriptionbilling.authentication.eu10.hana.ondemand.com`。 |
| **[!UICONTROL Region]** | 您的数据中心位置。 该区域存在于`url`中，其值类似于`eu10`或`us10`。 例如，如果`url`是`https://eu10.revenue.cloud.sap/api`，您需要`eu10`。 |

要验证目标，请选择&#x200B;**[!UICONTROL Connect to destination]**。
![来自Experience Platform UI的图像，显示如何对目标进行身份验证。](../../assets/catalog/ecommerce/sap-commerce/authenticate-destination.png)

如果提供的详细信息有效，则UI会显示&#x200B;**[!UICONTROL Connected]**&#x200B;状态并显示绿色复选标记。 然后，您可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。
![Experience Platform UI中的图像，显示身份验证后要填充的目标详细信息。](../../assets/catalog/ecommerce/sap-commerce/destination-details.png)

* **[!UICONTROL Name]**：将来用于识别此目标的名称。
* **[!UICONTROL Description]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL Type of Customer]**：根据受众中的实体，选择&#x200B;***个人***&#x200B;或&#x200B;***公司***。 [!DNL SAP Subscription Billing] [架构](https://api.sap.com/api/BusinessPartner_APIs/schema)根据映射到`customerType`属性的该选择切换必填字段。 如果选择的是&#x200B;***公司***，则单个客户所需的强制映射（如`firstName`和`lastName`）将被忽略，`company`将变为强制映射，反之亦然。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请阅读[将配置文件和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。

### 映射属性和身份 {#map}

要将受众数据从Adobe Experience Platform正确发送到[!DNL SAP Commerce]目标，您必须完成字段映射步骤。 映射包括在Experience Platform帐户中的Experience Data Model (XDM)架构字段与其与目标中的相应等效字段之间创建链接。 要将XDM字段正确映射到[!DNL SAP Commerce]目标字段，请执行以下步骤：

#### 映射`customerNumberSAP`标识

`customerNumberSAP`标识是此目标的必需映射。 请按照以下步骤对其进行映射：

1. 在&#x200B;**[!UICONTROL Mapping]**&#x200B;步骤中，选择&#x200B;**[!UICONTROL Add new mapping]**。 您现在可以在屏幕上看到新的映射行。
   ![突出显示了“添加新映射”按钮的Experience Platform UI屏幕截图。](../../assets/catalog/ecommerce/sap-commerce/mapping-add-new-mapping.png)
1. 在&#x200B;**[!UICONTROL Select source field]**&#x200B;窗口中，选择&#x200B;**[!UICONTROL Select identity namespace]**&#x200B;并选择`customerNumberSAP`。
   ![Experience Platform UI屏幕截图选择电子邮件作为要映射为标识的源属性。](../../assets/catalog/ecommerce/sap-commerce/mapping-select-source-identity.png)
1. 在&#x200B;**[!UICONTROL Select target field]**&#x200B;窗口中，选择&#x200B;**[!UICONTROL Select identity namespace]**&#x200B;并选择`customerNumber`标识。
   ![Experience Platform UI屏幕截图选择电子邮件作为要映射为身份的目标属性。](../../assets/catalog/ecommerce/sap-commerce/mapping-select-target-identity.png)

| 源字段 | 目标字段 | 必需 |
| --- | --- | --- |
| `IdentityMap: customerNumberSAP` | `Identity: customerNumber` | 是 |

下面显示了具有标识映射的示例：
![Experience Platform UI中的图像显示customerNumber标识映射示例。](../../assets/catalog/ecommerce/sap-commerce/mapping-identities.png)

#### 映射属性

要添加任何其他要在XDM配置文件架构和[!DNL SAP Subscription Billing]帐户之间更新的属性，请重复以下步骤：

1. 在&#x200B;**[!UICONTROL Mapping]**&#x200B;步骤中，选择&#x200B;**[!UICONTROL Add new mapping]**。 您现在可以在屏幕上看到新的映射行。
   ![突出显示了“添加新映射”按钮的Experience Platform UI屏幕截图。](../../assets/catalog/ecommerce/sap-commerce/mapping-add-new-mapping.png)
1. 在&#x200B;**[!UICONTROL Select source field]**&#x200B;窗口中，选择&#x200B;**[!UICONTROL Select attributes]**&#x200B;类别并选择XDM属性。
   ![选择“姓氏”作为源属性的Experience Platform UI屏幕截图。](../../assets/catalog/ecommerce/sap-commerce/mapping-select-source-attribute.png)
1. 在&#x200B;**[!UICONTROL Select target field]**&#x200B;窗口中，选择&#x200B;**[!UICONTROL Select custom attributes]**&#x200B;类别并从客户[!DNL SAP Subscription Billing]架构[属性的列表中键入](https://api.sap.com/api/BusinessPartner_APIs/schema)属性的名称。
   ![Experience Platform UI屏幕截图，其中lastName被定义为target属性。](../../assets/catalog/ecommerce/sap-commerce/mapping-select-target-attribute.png)

>[!IMPORTANT]
>
> 目标字段名称区分大小写，且应与[!DNL SAP Subscription Billing]属性名称匹配。 唯一的例外是`country`，您应该改用`countryCode`。 [!DNL SAP Subscription Billing]支持alpha-2 (ISO 3166)国家/地区代码。 该值区分大小写，且必须介于0至3个字符之间，因此，请确保您所提供的内容与定义完全相同，否则您将遇到错误： `The country code {} does not exist`或`size must be between 0 and 3`。

#### 映射所选客户类型的`mandatory`属性

必需的属性映射取决于您选择的&#x200B;**[!UICONTROL Type of Customer]**。 要映射必需属性，请从下面选择：

>[!BEGINTABS]

>[!TAB 个人客户]

| 源字段 | 目标字段 | 必需 |
| --- | --- | --- |
| `xdm: person.lastName` | `Attribute: lastName` | 是 |
| `xdm: workAddress.countryCode` | `Attribute: countryCode` | 是 |

>[!TAB 公司客户]

| 源字段 | 目标字段 | 必需 |
| --- | --- | --- |
| `xdm: b2b.companyName` | `Attribute: company` | 是 |
| `xdm: workAddress.countryCode` | `Attribute: countryCode` | 是 |

>[!ENDTABS]

#### 映射其他属性

然后，您可以在XDM配置文件架构与客户的[!DNL SAP Subscription Billing] [架构](https://api.sap.com/api/BusinessPartner_APIs/schema)属性之间添加任何其他映射，如下所示：

>[!BEGINTABS]

>[!TAB 个人客户]

| 源字段 | 目标字段 | 必需 |
| --- | --- | --- |
| `xdm: person.name.firstName` | `Attribute: firstName` | 否 |
| `xdm: workAddress.street1` | `Attribute: street` | 否 |
| `xdm: workAddress.city` | `Attribute: city` | 否 |

下面显示了客户为个人的具有强制和可选属性映射的示例：
![Experience Platform UI中的图像显示了一个具有强制和可选属性映射的示例，其中客户是个人。](../../assets/catalog/ecommerce/sap-commerce/mapping-attributes-individual.png)

>[!TAB 公司客户]

| 源字段 | 目标字段 | 必需 |
| --- | --- | --- |
| `xdm: workAddress.street1` | `Attribute: street` | 否 |
| `xdm: workAddress.city` | `Attribute: city` | 否 |

下面显示了客户为公司的具有强制和可选属性映射的示例：
![Experience Platform UI中的图像显示了一个具有强制和可选属性映射的示例，其中客户是公司。](../../assets/catalog/ecommerce/sap-commerce/mapping-attributes-corporate.png)

>[!ENDTABS]

完成提供目标连接的映射后，请选择&#x200B;**[!UICONTROL Next]**。

### 计划受众导出和示例 {#schedule-segment-export-example}

执行[计划受众导出](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling)步骤时，必须手动将Experience Platform受众映射到[中的](#prerequisites-attribute)属性[!DNL SAP Subscription Billing]。

下面显示了突出显示[!DNL SAP Commerce] **[!UICONTROL Mapping ID]**&#x200B;位置的计划受众导出步骤示例：
![Experience Platform中的图像显示了填充了映射ID的计划受众导出。](../../assets/catalog/ecommerce/sap-commerce/schedule-segment-export.png)

为此，请选择每个区段，然后在[!DNL SAP Subscription Billing] [!DNL SAP Commerce]目标连接器字段中输入来自&#x200B;**[!UICONTROL Mapping ID]**&#x200B;的自定义引用的名称。 有关创建自定义引用的指导，请参阅[在 [!DNL SAP Subscription Billing]](#prerequisites-custom-reference)中创建自定义引用。

>[!IMPORTANT]
>
> 请勿使用自定义引用标签作为值。
> &#x200B;>![此图像指示您不应使用自定义参考标签值进行映射。](../../assets/catalog/ecommerce/sap-commerce/custom-reference-dont-use-label-for-mapping.png)

例如，如果您选择的Experience Platform受众为`sap_audience1`，并且希望将其状态更新到[!DNL SAP Subscription Billing]自定义引用`SAP_1`中，请在[!DNL SAP_Commerce] **[!UICONTROL Mapping ID]**&#x200B;字段中指定此值。

下面显示了&#x200B;**[!UICONTROL Reference Type]**&#x200B;中的示例[!DNL SAP Subscription Billing]：
![显示在SAP订阅帐单中创建自定义引用的位置的图像。](../../assets/catalog/ecommerce/sap-commerce/create-custom-reference.png)

下面显示了一个计划受众导出步骤的示例，该步骤选择了一个受众并突出显示了其对应的[!DNL SAP Commerce] **[!UICONTROL Mapping ID]**：
![Experience Platform中的图像显示了填充了映射ID的计划受众导出。](../../assets/catalog/ecommerce/sap-commerce/schedule-segment-export-example.png)

如上所示，**[!UICONTROL Mapping ID]**&#x200B;字段中的值应与[!DNL SAP Subscription Billing] **[!UICONTROL Reference Type]**&#x200B;值完全匹配。

对每个激活的Experience Platform受众重复此部分。

根据上图所示，您已选择两个受众，映射将如下所示：

| [!DNL SAP Commerce]受众名称 | [!DNL SAP Subscription Billing] **[!UICONTROL Reference Type]** | [!DNL SAP Commerce] **[!UICONTROL Mapping ID]**&#x200B;值 |
| --- | --- | --- |
| sap_audience1 | `SAP_1` | `SAP_1` |
| SAP受众2 | `SAP_2` | `SAP_2` |

## 验证数据导出 {#exported-data}

要验证您是否正确设置了目标，请执行以下步骤：

登录到[!DNL SAP Subscription Billing]帐户，然后导航到&#x200B;**[!UICONTROL Contacts]**&#x200B;页面以检查受众状态。 列表可以配置为显示自定义引用的列并显示相应的受众状态。
![显示客户概述页面的SAP订阅帐单图像，列标题显示受众名称和单元格受众状态](../../assets/catalog/ecommerce/sap-commerce/customer-overview.png)

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请参阅[数据治理概述](/help/data-governance/home.md)。

## 错误和故障排除 {#errors-and-troubleshooting}

有关可能的错误类型及其响应代码的列表，请参阅[[!DNL SAP Subscription Billing] 错误类型](https://help.sap.com/docs/CLOUD_TO_CASH_OD/987aec876092428f88162e438acf80d6/1a6a0dd6129c48e8b235190a1b5409fa.html)文档页面。

## 其他资源 {#additional-resources}

[!DNL SAP]文档中的其他有用信息如下：

* [入门SAP订阅帐单](https://help.sap.com/docs/CLOUD_TO_CASH_OD/1216e7b79c984675b0a6f0005e351c74/e4b8badf7d124026991e4ab6b57d2a33.html)

### Changelog

此部分捕获此目标连接器的功能和重要文档更新。

+++ 查看更改日志

| 发行月份 | 更新类型 | 描述 |
|---|---|---|
| 2024 年 1 月 | 初始版本 | 初始目标版本和文档发布。 |

{style="table-layout:auto"}

+++
