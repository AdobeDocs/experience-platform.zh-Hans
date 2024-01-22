---
title: 数据登陆区目标
description: 了解如何连接到数据登陆区以激活受众和导出数据集。
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 3%

---

# 数据登陆区目标

>[!IMPORTANT]
>
>此文档页面参考 [!DNL Data Landing Zone] *目标*. 此外， [!DNL Data Landing Zone] *源* 在源目录中。 欲知更多信息，请参阅 [[!DNL Data Landing Zone] 源](/help/sources/connectors/cloud-storage/data-landing-zone.md) 文档。


## 概述 {#overview}

[!DNL Data Landing Zone] 是 Adobe Experience Platform 提供的一个 [!DNL Azure Blob] 存储接口，它准许您访问安全、基于云的文件存储设施以将文件导出到 Platform 之外。您有权访问一个 [!DNL Data Landing Zone] 容器，并且所有容器的总数据量以您的Platform产品和服务许可证提供的总数据为限。 Platform及其应用程序服务的所有客户，例如 [!DNL Customer Journey Analytics]， [!DNL Journey Orchestration]， [!DNL Intelligent Services]、和 [!DNL Real-Time Customer Data Platform] 已配置一个 [!DNL Data Landing Zone] 每个沙盒的容器。 您可以通过读取文件并将文件写入容器 [!DNL Azure Storage Explorer] 或命令行界面。

[!DNL Data Landing Zone] 支持基于SAS的身份验证，其数据受标准保护 [!DNL Azure Blob] 存放安全机制处于静止状态并在传输中。 基于SAS的身份验证允许您安全地访问 [!DNL Data Landing Zone] 通过公共Internet连接的容器。 您无需更改网络即可访问 [!DNL Data Landing Zone] 容器，这意味着您无需为网络配置任何允许列表或跨区域设置。

Platform对上传到的所有文件实施严格的七天生存时间(TTL) [!DNL Data Landing Zone] 容器。 所有文件都会在七天后删除。

## 连接到您的 [!UICONTROL 数据登陆区] 通过API或用户界面进行存储 {#connect-api-or-ui}

* 要连接到 [!UICONTROL 数据登陆区] 存储位置使用Platform用户界面，请阅读以下章节 [连接到目标](#connect) 和 [将受众激活到此目标](#activate) 下。
* 要连接到 [!UICONTROL 数据登陆区] 存储位置以编程方式读取 [使用流服务API教程将受众激活到基于文件的目标](../../api/activate-segments-file-based-destinations.md).

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 受支持 | 描述 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md). |
| 自定义上传 | ✓ | 受众 [已导入](../../../segmentation/ui/overview.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及适用的架构字段（例如，PPID），如 [目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频率 | **[!UICONTROL 批次]** | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 详细了解 [批处理基于文件的目标](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

请注意，在使用 [!DNL Data Landing Zone] 目标。

### 连接您的 [!DNL Data Landing Zone] 容器至 [!DNL Azure Storage Explorer]

您可以使用 [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/products/storage/storage-explorer/) 管理您的内容 [!DNL Data Landing Zone] 容器。 开始使用 [!DNL Data Landing Zone]，您必须先检索凭据，然后在其中输入 [!DNL Azure Storage Explorer]，并连接 [!DNL Data Landing Zone] 容器至 [!DNL Azure Storage Explorer].

在 [!DNL Azure Storage Explorer] UI中，选择左侧导航栏中的连接图标。 此 **选择资源** 窗口出现，为您提供连接选项。 选择 **[!DNL Blob container]** 以连接到 [!DNL Data Landing Zone] 存储。

![选择Azure UI中突出显示的资源。](/help/sources/images/tutorials/create/dlz/select-resource.png)

接下来，选择 **共享访问签名URL (SAS)** 作为连接方法，然后选择 **下一个**.

![选择Azure UI中高亮显示的连接方法。](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

选择连接方法后，必须提供 **显示名称** 和 **[!DNL Blob]容器SAS URL** 与您的 [!DNL Data Landing Zone] 容器。

>[!BEGINSHADEBOX]

### 检索凭据 [!DNL Data Landing Zone] {#retrieve-dlz-credentials}

您必须使用平台API来检索 [!DNL Data Landing Zone] 凭据。 用于检索凭据的API调用描述如下。 有关获取标头所需值的信息，请参阅 [Adobe Experience Platform API快速入门](/help/landing/api-guide.md) 指南。

**API格式**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

| 查询参数 | 描述 |
| --- | --- |
| `dlz_destination` | 此 `dlz_destination` 类型允许API将登陆区域目标容器与您可用的其他类型容器区分开来。 |

{style="table-layout:auto"}

**请求**

以下请求示例检索现有登陆区域的凭据。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**响应**

以下响应将返回登陆区域的凭据信息，包括您当前的 `SASToken` 和 `SASUri`，和 `storageAccountName` 与您的登陆区域容器对应的标记。

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3df123",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| 属性 | 描述 |
| --- | --- |
| `containerName` | 您的登陆区域的名称。 |
| `SASToken` | 登陆区域的共享访问签名令牌。 此字符串包含授权请求所需的所有信息。 |
| `SASUri` | 登陆区域的共享访问签名URI。 此字符串是您要进行身份验证的登陆区域的URI及其对应的SAS令牌的组合， |

{style="table-layout:auto"}

### 更新 [!DNL Data Landing Zone] 凭据 {#update-dlz-credentials}

您还可以在需要时刷新凭据。 您可以更新 `SASToken` 向发出POST请求 `/credentials` 的端点 [!DNL Connectors] API。

**API格式**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh
```

| 查询参数 | 描述 |
| --- | --- |
| `dlz_destination` | 此 `dlz_destination` 类型允许API将登陆区域目标容器与您可用的其他类型容器区分开来。 |
| `refresh` | 此 `refresh` 操作允许您重置登陆区域凭据并自动生成新的 `SASToken`. |

{style="table-layout:auto"}

**请求**

以下请求将更新您的登陆区域凭据。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**响应**

以下响应会返回以下项的更新值： `SASToken` 和 `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

>[!ENDSHADEBOX]

提供您的显示名称(`containerName`)和 [!DNL Data Landing Zone] SAS URL，如上所述API调用中所返回，然后选择 **下一个**.

![输入在Azure UI中突出显示的连接信息。](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

此 **摘要** 窗口，为您提供设置的概述，包括有关您的设置的信息 [!DNL Blob] 端点和权限。 准备就绪后，选择 **连接**.

![Azure UI中显示的设置摘要。](/help/sources/images/tutorials/create/dlz/summary.png)

连接成功更新您的 [!DNL Azure Storage Explorer] 包含您的UI [!DNL Data Landing Zone] 容器。

![Azure UI中高亮显示的DLZ用户容器摘要。](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

与您的 [!DNL Data Landing Zone] 容器已连接到 [!DNL Azure Storage Explorer]，您现在可以开始将文件从Experience Platform导出到 [!DNL Data Landing Zone] 容器。 要导出文件，必须建立到 [!DNL Data Landing Zone] Experience PlatformUI中的目标，如下节所述。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 查看目标]** 和 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). 在目标配置工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

确保已将 [!DNL Data Landing Zone] 容器至 [!DNL Azure Storage Explorer] 如 [先决条件](#prerequisites) 部分。 因为 [!DNL Data Landing Zone] 是Adobe配置的存储，您无需在Experience PlatformUI中执行任何进一步的步骤即可向目标进行身份验证。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：填写此目标的首选名称。
* **[!UICONTROL 描述]**：可选。 例如，您可以提及要将此目标用于哪个营销活动。
* **[!UICONTROL 文件夹路径]**：输入目标文件夹的路径，该文件夹将托管导出的文件。
* **[!UICONTROL 文件类型]**：选择导出的文件应使用的格式Experience Platform。 选择 [!UICONTROL CSV] 选项，您还可以 [配置文件格式选项](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 压缩格式]**：选择Experience Platform应用于导出文件的压缩类型。
* **[!UICONTROL 包含清单文件]**：如果您希望导出包含清单JSON文件，并且该文件包含有关导出位置、导出大小等的信息，请打开此选项。 清单的命名格式为 `manifest-<<destinationId>>-<<dataflowRunId>>.json`. 查看 [示例清单文件](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). 清单文件包含以下字段：
   * `flowRunId`：和 [数据流运行](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) 生成了导出的文件。
   * `scheduledTime`：导出文件时的时间（UTC时间）。
   * `exportResults.sinkPath`：存储位置中存储导出文件的路径。
   * `exportResults.name`：导出文件的名称。
   * `size`：导出文件的大小（以字节为单位）。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

请参阅 [将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众激活到此目标的说明。

### 正在计划

在 **[!UICONTROL 正在计划]** 步骤，您可以 [设置导出计划](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) 您的 [!DNL Data Landing Zone] 目标位置，您还可以 [配置导出文件的名称](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### 映射属性和身份 {#map}

在 **[!UICONTROL 映射]** 步骤，您可以为配置文件选择要导出的属性和标识字段。 您还可以选择将导出文件中的标头更改为所需的任何友好名称。 有关详细信息，请查看 [映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 在激活批次目标UI教程中。

## 导出数据集 {#export-datasets}

此目标支持数据集导出。 有关如何设置数据集导出的完整信息，请阅读教程：

* 操作方法 [使用Platform用户界面导出](/help/destinations/ui/export-datasets.md).
* 操作方法 [使用流服务API以编程方式导出数据集](/help/destinations/api/export-datasets.md).

## 验证数据导出是否成功 {#exported-data}

要验证数据是否已成功导出，请检查 [!DNL Data Landing Zone] 存储并确保导出的文件包含预期的配置文件人口。
