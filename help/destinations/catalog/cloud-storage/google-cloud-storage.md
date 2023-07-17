---
title: (Beta) Google Cloud Storage连接
description: 了解如何连接到Google Cloud Storage并激活受众或导出数据集。
exl-id: ab274270-ae8c-4264-ba64-700b118e6435
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 0%

---

# (Beta)[!DNL Google Cloud Storage]连接

>[!IMPORTANT]
>
>此目标目前为测试版，仅适用于有限数量的客户。 要请求访问 [!DNL Google Cloud Storage] 连接，请联系您的Adobe代表并提供您的 [!DNL Organization ID].

## 概述 {#overview}

创建实时出站连接至 [!DNL Google Cloud Storage] 定期将数据文件从Adobe Experience Platform导出到您自己的存储桶中。

## 连接到您的 [!DNL Google Cloud Storage] 通过API或用户界面进行存储 {#connect-api-or-ui}

* 连接到您的 [!DNL Google Cloud Storage] 存储位置使用Platform用户界面，请阅读部分 [连接到目标](#connect) 和 [将受众激活到此目标](#activate) 下面的。
* 连接到您的 [!DNL Google Cloud Storage] 存储位置以编程方式读取 [使用流服务API教程将受众激活到基于文件的目标](../../api/activate-segments-file-based-destinations.md).

## 支持的受众 {#supported-audiences}

此部分介绍可以导出到此目标的所有受众。

所有目标都支持激活通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md).

此外，此目标还支持激活下表中描述的受众。

| 受众类型 | 描述 |
---------|----------|
| 自定义上传 | 从CSV文件引入到Experience Platform中的受众。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及适用的架构字段，如 [目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频率 | **[!UICONTROL 批次]** | 批量目标将文件导出到下游平台，增量为3、6、8、12或24小时。 详细了解 [基于文件的批处理目标](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 用于连接您的计算机的先决条件设置 [!DNL Google Cloud Storage] 帐户 {#prerequisites}

为了将平台连接到 [!DNL Google Cloud Storage]，您必须首先为以下各项启用互操作性： [!DNL Google Cloud Storage] 帐户。 要访问互操作性设置，请打开 [!DNL Google Cloud Platform] 并选择 **[!UICONTROL 设置]** 从 **[!UICONTROL 云存储]** 选项。

![突出显示了Cloud Storage和设置的Google Cloud Platform功能板。](../../../sources/images/tutorials/create/google-cloud-storage/nav.png)

此 **[!UICONTROL 设置]** 页面。 从这里，您可以看到与您的 [!DNL Google] 项目ID以及有关您的项目的详细信息 [!DNL Google Cloud Storage] 帐户。 要访问互操作性设置，请选择 **[!UICONTROL 互操作性]** 从顶部标题中。

![Google Cloud Platform仪表板中突出显示的互操作性选项卡。](../../../sources/images/tutorials/create/google-cloud-storage/project-access.png)

此 **[!UICONTROL 互操作性]** 页面包含有关身份验证、访问密钥以及与服务帐户关联的默认项目的信息。 要为您的服务帐户生成新的访问密钥ID和秘密访问密钥，请选择 **[!UICONTROL 为服务帐户创建密钥]**.

![Google Cloud Platform仪表板中突出显示的为服务帐户控制创建密钥。](../../../sources/images/tutorials/create/google-cloud-storage/interoperability.png)

您可以使用新生成的访问密钥ID和秘密访问密钥来连接 [!DNL Google Cloud Storage] Platform帐户。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](/help/destinations/ui/connect-destination.md). 在目标配置工作流中，填写下面两节中列出的字段。

### 向目标进行身份验证 {#authenticate}

要向目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

* **[!UICONTROL 访问密钥ID]**：由61个字符组成的字母数字字符串，用于验证您的 [!DNL Google Cloud Storage] Platform帐户。 有关如何获得此值的信息，请阅读 [先决条件](#prerequisites) 部分。
* **[!UICONTROL 访问密钥]**：由40个字符组成的base64编码字符串，用于验证您的 [!DNL Google Cloud Storage] Platform帐户。 有关如何获得此值的信息，请阅读 [先决条件](#prerequisites) 部分。
* **[!UICONTROL 加密密钥]**：（可选）您可以附加RSA格式公钥以向导出的文件添加加密。 在下图中查看正确格式化的加密密钥示例。

  ![图像显示UI中格式正确的PGP密钥的示例](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

有关这些值的详细信息，请阅读 [Google Cloud Storage HMAC密钥](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 指南。 有关如何生成您自己的访问密钥ID和秘密访问密钥的步骤，请参阅 [[!DNL Google Cloud Storage] 源概述](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：填写此目标的首选名称。
* **[!UICONTROL 描述]**：可选。 例如，您可以提及要将此目标用于哪个营销活动。
* **[!UICONTROL 存储段名称]**：输入 [!DNL Google Cloud Storage] 要由此目标使用的存储段。
* **[!UICONTROL 文件夹路径]**：输入将托管导出文件的目标文件夹的路径。
* **[!UICONTROL 文件类型]**：选择导出文件应使用的格式Experience Platform。 选择 [!UICONTROL CSV] 选项，您还可以 [配置文件格式选项](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 压缩格式]**：选择Experience Platform应用于导出文件的压缩类型。
* **[!UICONTROL 包含清单文件]**：如果您希望导出包含清单JSON文件，并且该文件包含有关导出位置、导出大小等的信息，请打开此选项。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将受众激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

参见 [将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众激活到此目标的说明。

### 计划

在 **[!UICONTROL 计划]** 步骤，您可以 [设置导出计划](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) 您的 [!DNL Google Cloud Storage] 目标位置，您还可以 [配置导出文件的名称](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### 映射属性和身份 {#map}

在 **[!UICONTROL 映射]** 步骤，您可以选择为用户档案导出哪些属性和标识字段。 您还可以选择将导出文件中的标头更改为所需的任何友好名称。 有关详细信息，请查看 [映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 在激活批次目标UI教程中。

## （测试版）导出数据集 {#export-datasets}

此目标支持数据集导出。 有关如何设置数据集导出的完整信息，请阅读教程：

* 操作方法 [使用Platform用户界面导出数据集](/help/destinations/ui/export-datasets.md).
* 操作方法 [使用流服务API以编程方式导出数据集](/help/destinations/api/export-datasets.md).

## 验证数据导出是否成功 {#exported-data}

要验证数据是否已成功导出，请查看 [!DNL Google Cloud Storage] 存储桶并确保导出的文件包含预期的用户档案人口。
