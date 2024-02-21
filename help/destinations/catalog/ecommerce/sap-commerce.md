---
title: SAP Commerce连接
description: 使用SAP Commerce目标连接器更新SAP帐户中的客户记录。
last-substantial-update: 2024-02-20T00:00:00Z
source-git-commit: 9bb2cf5adcd48f9d111ba04b8c93129367dd12f8
workflow-type: tm+mt
source-wordcount: '2245'
ht-degree: 2%

---

# [!DNL SAP Commerce] 连接

[!DNL SAP Commerce]，以前称为 [[!DNL Hybris]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html)，是一个用于B2B和B2C企业的基于云的电子商务平台解决方案，作为SAP客户体验产品组合的一部分提供。 [[!DNL SAP] 订阅帐单](https://www.sap.com/products/financial-management/subscription-billing.html) 是产品组合中的一个产品，它通过标准化的集成简化了销售和支付体验，支持完整的订阅生命周期管理。

此 [!DNL Adobe Experience Platform] [目标](/help/destinations/home.md) 使用 [[!DNL SAP Subscription Billing] 客户管理API](https://api.sap.com/api/BusinessPartner_APIs/path/PUT_customers-customerNumber)，在中更新您的客户详细信息 [!DNL SAP Commerce] 从现有Experience Platform受众进行激活。

向您的验证的说明 [!DNL SAP Commerce] 实例位于 [向目标进行身份验证](#authenticate) 部分。

## 用例 {#use-cases}

为了帮助您更好地了解您应该如何以及何时使用 [!DNL SAP Commerce] 目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

[!DNL SAP Commerce] 客户存储与您的业务互动的个人或组织实体的相关信息。 您的团队使用中现有的客户 [!DNL SAP Commerce] 以构建Experience Platform受众。 将这些受众发送至 [!DNL SAP Commerce]，则其信息会更新，并且会为每个客户分配一个属性，其值作为指示客户属于哪个受众的受众名称。

## 先决条件 {#prerequisites}

请参阅以下部分，了解必须在Experience Platform中设置的任何先决条件， [!DNL SAP Commerce] ，以了解在使用之前必须收集的信息 [!DNL SAP Commerce] 目标。

### Experience Platform先决条件 {#prerequisites-in-experience-platform}

将数据激活到之前 [!DNL SAP Commerce] 目标，您必须拥有 [架构](/help/xdm/schema/composition.md)， a [数据集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)、和 [受众](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html) 创建于 [!DNL Experience Platform].

请参阅Experience Platform文档 [受众成员资格详细信息架构字段组](/help/xdm/field-groups/profile/segmentation.md) 如果您需要有关受众状态的指南。

### 的先决条件 [!DNL SAP Commerce] 目标 {#prerequisites-destination}

请注意以下先决条件，以便将数据从Platform导出到 [!DNL SAP Commerce] 帐户：

#### 您必须拥有 [!DNL SAP Subscription Billing] 帐户 {#prerequisites-account}

为了将数据从Platform导出到 [!DNL SAP Commerce] 帐户，您需要拥有 [!DNL SAP Subscription Billing] 帐户。 如果您没有有效的计费帐户，请联系贵机构的 [!DNL SAP] 客户经理。 请参阅 [[!DNL SAP] 平台配置](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) 文档，以了解其他详细信息。

#### 生成服务密钥 {#prerequisites-service-key}

* 此 [!DNL SAP Commerce] 服务密钥允许您访问 [!DNL SAP Subscription Billing] 通过Experience Platform的API。 请参阅 [!DNL SAP Commerce] [使用客户端ID和客户端密钥创建服务密钥](https://help.sap.com/docs/CLOUD_TO_CASH_OD/1216e7b79c984675b0a6f0005e351c74/87c11a0f5dc3494eaf3baa355925c030.html#create-a-service-key-with-client-id-and-client-secret) 创建服务密钥。 [!DNL SAP Commerce] 要求您满足以下条件：
   * 客户端ID
   * 客户端密码
   * URL。 URL模式如下所示： `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. 此值稍后将用于获取 `Region` 和 `Endpoint`.

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

#### 在中创建自定义引用 [!DNL SAP Subscription Billing] {#prerequisites-custom-reference}

要在中更新Experience Platform受众状态，请执行以下操作 [!DNL SAP Subscription Billing]，则在Platform中选择的每个受众都需要一个自定义参考字段。

要创建自定义引用，请登录 [!DNL SAP Subscription Billing] 帐户并导航到 **[主数据和配置]** > **[自定义引用]** 页面。 接下来，选择 **[!UICONTROL 创建]** 为在Platform中选择的每个受众添加新引用。 在后续操作中，您将需要这些引用字段名称 [计划受众导出和示例](#schedule-segment-export-example) 步骤。

有关如何创建自定义的示例 **[!UICONTROL 引用类型]** 范围 [!DNL SAP Subscription Billing] 如下所示：
![此图像显示了在SAP订阅帐单中创建自定义引用的位置。](../../assets/catalog/ecommerce/sap-commerce/create-custom-reference.png)

有关其他指导，请参阅 [!DNL SAP Subscription Billing] [自定义引用](https://help.sap.com/docs/CLOUD_TO_CASH_OD/80d121f216af43648e79664efe5595f7/85696a63c8d8453a934e86c9413a25cf.html?version=2023-11-27) 文档。

### 收集所需的凭据 {#gather-credentials}

连接 [!DNL SAP Commerce] 要Experience Platform，必须提供以下连接属性的值：

| 凭据 | 描述 |
| --- | --- |
| 客户端ID | 的值 `clientId` 服务密钥。 |
| 客户端密码 | 的值 `clientSecret` 服务密钥。 |
| 端点 | 的值 `url` 在服务密钥中，它类似于 `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| 区域 | 您的数据中心位置。 此区域出现在 `url` 且其值类似于 `eu10` 或 `us10`. 例如，如果 `url` 是 `https://eu10.revenue.cloud.sap/api` 您需要 `eu10`. |

## 护栏 {#guardrails}

的API请求 [!DNL SAP Cloud Management service] 受 [速率限制](https://help.sap.com/docs/btp/sap-business-technology-platform/account-administration-rate-limiting). 当超出速率限制时，您将会遇到 `HTTP 429 Too Many Requests` 响应状态代码。

## 支持的身份 {#supported-identities}

[!DNL SAP Commerce] 支持更新下表中描述的标识。 了解有关 [身份](/help/identity-service/features/namespaces.md).

| 目标身份 | 描述 | 注意事项 |
| --- | --- | --- |
| `customerNumberSAP` | 贵机构中已经存在的个人或企业客户的客户标识符 [!DNL SAP Commerce] 帐户。 | 必需 |

## 支持的受众 {#supported-audiences}

此部分介绍可导出到此目标的所有受众。

此目标支持激活通过Experience Platform生成的所有受众 [分段服务](../../../segmentation/home.md).

此目标还支持激活下表所述的受众。

| 受众类型 | 描述 |
---------|----------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md). |
| 自定义上传 | ✓ | 受众 [已导入](../../../segmentation/ui/overview.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | <ul><li>您正在导出受众的所有成员以及所需的架构字段 *（例如：电子邮件地址、电话号码、姓氏）*，根据您的字段映射。</li><li> 对于Platform中的每个选定受众，将 [!DNL SAP Commerce] 从Platform更新了其他属性的受众状态。</li></ul> |
| 导出频率 | **[!UICONTROL 流]** | <ul><li>流目标为基于API的“始终运行”连接。 当基于受众评估在Experience Platform中更新用户档案时，连接器将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两个部分中列出的字段。

范围 **[!UICONTROL 目标]** > **[!UICONTROL 目录]**，搜索 [!DNL SAP Commerce]. 或者，您可以将其定位到 **[!UICONTROL 电子商务]** 类别。

### 验证目标 {#authenticate}

填写下面的必填字段。 请参阅 [生成服务密钥](#prerequisites-service-key) 部分获取任何指导。

| 字段 | 描述 |
| --- | --- |
| **[!UICONTROL 客户端ID]** | 的值 `clientId` 服务密钥。 |
| **[!UICONTROL 客户端密码]** | 的值 `clientSecret` 服务密钥。 |
| **[!UICONTROL 端点]** | 的值 `url` 在服务密钥中，它类似于 `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| **[!UICONTROL 区域]** | 您的数据中心位置。 此区域出现在 `url` 且其值类似于 `eu10` 或 `us10`. 例如，如果 `url` 是 `https://eu10.revenue.cloud.sap/api` 您需要 `eu10`. |

要验证目标，请选择 **[!UICONTROL 连接到目标]**.
![Platform UI中显示如何对目标进行身份验证的图像。](../../assets/catalog/ecommerce/sap-commerce/authenticate-destination.png)

如果提供的详细信息有效，UI将显示 **[!UICONTROL 已连接]** 带有绿色复选标记的状态。 然后，您可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。
![Platform UI中的图像，显示身份验证后要填充的目标详细信息。](../../assets/catalog/ecommerce/sap-commerce/destination-details.png)

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 客户类型]**：选择其中一项 ***个人*** 或 ***企业*** 取决于受众中的实体。 此 [!DNL SAP Subscription Billing] [架构](https://api.sap.com/api/BusinessPartner_APIs/schema) 根据映射到 `customerType` 属性。 如果所选内容为 ***企业***，然后是必需映射，如 `firstName` 和 `lastName` 对于单个客户而言，必需填写的表单将被忽略，并且 `company` 成为强制性的，反之亦然。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

读取 [将用户档案和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

### 映射属性和身份 {#map}

要正确地将受众数据从Adobe Experience Platform发送到 [!DNL SAP Commerce] 目标，您必须完成字段映射步骤。 映射包括在您的Platform帐户中的Experience Data Model (XDM)架构字段与其在目标目标中的相应等效字段之间创建链接。 要将XDM字段正确映射到 [!DNL SAP Commerce] 目标字段，请执行以下步骤：

#### 映射 `customerNumberSAP` 身份

此 `customerNumberSAP` 标识是此目标的强制映射。 请按照以下步骤对其进行映射：
1. 在 **[!UICONTROL 映射]** 步骤，选择 **[!UICONTROL 添加新映射]**. 您现在可以在屏幕上看到新的映射行。
   ![突出显示包含添加新映射按钮的Platform UI屏幕截图。](../../assets/catalog/ecommerce/sap-commerce/mapping-add-new-mapping.png)
1. 在 **[!UICONTROL 选择源字段]** 窗口中，选择 **[!UICONTROL 选择身份命名空间]** 并选择 `customerNumberSAP`.
   ![Platform UI屏幕截图选择电子邮件作为源属性以映射为身份。](../../assets/catalog/ecommerce/sap-commerce/mapping-select-source-identity.png)
1. 在 **[!UICONTROL 选择目标字段]** 窗口中，选择 **[!UICONTROL 选择身份命名空间]** 并选择 `customerNumber` 身份。
   ![Platform UI屏幕截图选择电子邮件作为目标属性以映射为身份。](../../assets/catalog/ecommerce/sap-commerce/mapping-select-target-identity.png)

| 源字段 | 目标字段 | 必需 |
| --- | --- | --- |
| `IdentityMap: customerNumberSAP` | `Identity: customerNumber` | 是 |

下面显示了具有标识映射的示例：
![Platform UI中的图像，显示了customerNumber标识映射示例。](../../assets/catalog/ecommerce/sap-commerce/mapping-identities.png)

#### 映射属性

要添加任何其他要在XDM配置文件架构与 [!DNL SAP Subscription Billing] 帐户，请重复以下步骤：
1. 在 **[!UICONTROL 映射]** 步骤，选择 **[!UICONTROL 添加新映射]**. 您现在可以在屏幕上看到新的映射行。
   ![突出显示包含添加新映射按钮的Platform UI屏幕截图。](../../assets/catalog/ecommerce/sap-commerce/mapping-add-new-mapping.png)
1. 在 **[!UICONTROL 选择源字段]** 窗口中，选择 **[!UICONTROL 选择属性]** 类别并选择XDM属性。
   ![Platform UI屏幕截图选择姓氏作为源属性。](../../assets/catalog/ecommerce/sap-commerce/mapping-select-source-attribute.png)
1. 在 **[!UICONTROL 选择目标字段]** 窗口，选择 **[!UICONTROL 选择自定义属性]** 类别并键入的名称 [!DNL SAP Subscription Billing] 客户列表中的属性 [架构](https://api.sap.com/api/BusinessPartner_APIs/schema) 属性。
   ![将lastName定义为target属性的平台UI屏幕快照。](../../assets/catalog/ecommerce/sap-commerce/mapping-select-target-attribute.png)

>[!IMPORTANT]
>
> 目标字段名称区分大小写，且应与 [!DNL SAP Subscription Billing] 属性名称。 唯一的例外是 `country` 您应使用的位置 `countryCode` 而是。 [!DNL SAP Subscription Billing] 支持alpha-2 (ISO 3166)国家/地区代码。 该值区分大小写，且必须介于0至3个字符之间，因此，请确保您所提供的内容与定义完全相同，否则您将遇到错误： `The country code {} does not exist` 或 `size must be between 0 and 3`.

#### 地图 `mandatory` 所选客户类型的属性

必需的属性映射取决于 **[!UICONTROL 客户类型]** 你选择的。 要映射必需属性，请从下面选择：

>[!BEGINTABS]

>[!TAB 个人客户]

| 源字段 | 目标字段 | 必需 |
| --- | --- | --- |
| `xdm: person.lastName` | `Attribute: lastName` | 是 |
| `xdm: workAddress.countryCode` | `Attribute: countryCode` | 是 |

>[!TAB 企业客户]

| 源字段 | 目标字段 | 必需 |
| --- | --- | --- |
| `xdm: b2b.companyName` | `Attribute: company` | 是 |
| `xdm: workAddress.countryCode` | `Attribute: countryCode` | 是 |

>[!ENDTABS]

#### 映射其他属性

然后，您可以在XDM配置文件架构和 [!DNL SAP Subscription Billing] [架构](https://api.sap.com/api/BusinessPartner_APIs/schema) 客户属性，如下所示：

>[!BEGINTABS]

>[!TAB 个人客户]

| 源字段 | 目标字段 | 必需 |
| --- | --- | --- |
| `xdm: person.name.firstName` | `Attribute: firstName` | 否 |
| `xdm: workAddress.street1` | `Attribute: street` | 否 |
| `xdm: workAddress.city` | `Attribute: city` | 否 |

下面显示了客户为个人的具有强制和可选属性映射的示例：
![Platform UI中的图像展示了一个具有强制和可选属性映射的示例，其中客户为个人。](../../assets/catalog/ecommerce/sap-commerce/mapping-attributes-individual.png)

>[!TAB 企业客户]

| 源字段 | 目标字段 | 必需 |
| --- | --- | --- |
| `xdm: workAddress.street1` | `Attribute: street` | 否 |
| `xdm: workAddress.city` | `Attribute: city` | 否 |

下面显示了客户为公司的具有强制和可选属性映射的示例：
![Platform UI中的图像，显示了一个具有强制和可选属性映射的示例，其中客户是公司。](../../assets/catalog/ecommerce/sap-commerce/mapping-attributes-corporate.png)

>[!ENDTABS]

完成提供目标连接的映射后，选择 **[!UICONTROL 下一个]**.

### 计划受众导出和示例 {#schedule-segment-export-example}

执行 [计划受众导出](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 步骤，您必须手动将Platform受众映射到 [属性](#prerequisites-attribute) 在 [!DNL SAP Subscription Billing].

有关计划受众导出步骤的示例，步骤中包含 [!DNL SAP Commerce] **[!UICONTROL 映射Id]** 高亮显示，如下所示：
![Platform中的图像显示了填充了映射ID的计划受众导出。](../../assets/catalog/ecommerce/sap-commerce/schedule-segment-export.png)

要实现此目的，请选择每个区段，然后输入自定义引用的名称。 [!DNL SAP Subscription Billing] 在 [!DNL SAP Commerce] **[!UICONTROL 映射Id]** 目标连接器字段。 有关创建自定义参考的指导，请参阅 [在中创建自定义引用 [!DNL SAP Subscription Billing]](#prerequisites-custom-reference) 部分。

>[!IMPORTANT]
>
> 请勿使用自定义引用标签作为值。
>![该图像指示您不应使用自定义参考标签值进行映射。](../../assets/catalog/ecommerce/sap-commerce/custom-reference-dont-use-label-for-mapping.png)

例如，如果您选择的Experience Platform受众为 `sap_audience1` 您希望将其状态更新到 [!DNL SAP Subscription Billing] 自定义引用 `SAP_1`，请在 [!DNL SAP_Commerce] **[!UICONTROL 映射Id]** 字段。

示例 **[!UICONTROL 引用类型]** 从 [!DNL SAP Subscription Billing] 如下所示：
![此图像显示了在SAP订阅帐单中创建自定义引用的位置。](../../assets/catalog/ecommerce/sap-commerce/create-custom-reference.png)

有关计划受众导出步骤的示例，其中包含选定的受众及其对应的受众 [!DNL SAP Commerce] **[!UICONTROL 映射Id]** 高亮显示，如下所示：
![Platform中的图像显示了填充了映射ID的计划受众导出。](../../assets/catalog/ecommerce/sap-commerce/schedule-segment-export-example.png)

如中所示的值 **[!UICONTROL 映射Id]** 字段应完全匹配 [!DNL SAP Subscription Billing] **[!UICONTROL 引用类型]** 值。

对每个激活的Platform受众重复此部分。

根据上图所示，您已选择两个受众，映射将如下所示： | [!DNL SAP Commerce] 受众名称 | [!DNL SAP Subscription Billing] **[!UICONTROL 引用类型]** | [!DNL SAP Commerce] **[!UICONTROL 映射Id]** 值 | | — | — | — | | sap_audience1 | `SAP_1` | `SAP_1` | | SAP受众2 | `SAP_2` | `SAP_2` |

## 验证数据导出 {#exported-data}

要验证您是否正确设置了目标，请执行以下步骤：

登录到 [!DNL SAP Subscription Billing] 帐户，然后导航到 **[!UICONTROL 联系人]** 页面检查受众状态。 列表可以配置为显示自定义引用的列并显示相应的受众状态。
![SAP订阅帐单的图像，其中显示客户概述页面，列标题显示受众名称和单元格受众状态](../../assets/catalog/ecommerce/sap-commerce/customer-overview.png)

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据管理概述](/help/data-governance/home.md).

## 错误和故障排除 {#errors-and-troubleshooting}

请参阅 [[!DNL SAP Subscription Billing] 错误类型](https://help.sap.com/docs/CLOUD_TO_CASH_OD/987aec876092428f88162e438acf80d6/1a6a0dd6129c48e8b235190a1b5409fa.html) 文档页面，其中列出了可能的错误类型及其响应代码。

## 其他资源 {#additional-resources}

其他有用信息来自 [!DNL SAP] 文档如下所示：
* [载入SAP订阅帐单](https://help.sap.com/docs/CLOUD_TO_CASH_OD/1216e7b79c984675b0a6f0005e351c74/e4b8badf7d124026991e4ab6b57d2a33.html)

### Changelog

此部分捕获此目标连接器的功能和重要文档更新。

+++ 查看更改日志

| 发行月份 | 更新类型 | 描述 |
|---|---|---|
| 2024 年 1 月 | 初始版本 | 初始目标版本和文档发布。 |

{style="table-layout:auto"}

+++