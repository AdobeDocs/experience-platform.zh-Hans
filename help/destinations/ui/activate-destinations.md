---
keywords: 激活目标；激活目标；激活数据
title: 将用户档案和区段激活到目标
type: Tutorial
seo-title: 将用户档案和区段激活到目标
description: 通过将区段映射到目标，激活您在Adobe Experience Platform中拥有的数据。 要完成此操作，请按照以下步骤操作。
seo-description: 通过将区段映射到目标，激活您在Adobe Experience Platform中拥有的数据。 要完成此操作，请按照以下步骤操作。
exl-id: c3792046-ffa8-4851-918f-98ced8b8a835
source-git-commit: 70be44e919070df910d618af4507b600ad51123c
workflow-type: tm+mt
source-wordcount: '2566'
ht-degree: 0%

---

# 将用户档案和区段激活到目标

## 概述 {#overview}

通过将区段映射到目标，激活[!DNL Adobe Experience Platform]中的数据。 要完成此操作，请按照以下步骤操作。

## 先决条件 {#prerequisites}

要将数据激活到目标，您必须已成功[连接目标](./connect-destination.md)。 如果尚未执行此操作，请转到[目标目录](../catalog/overview.md)，浏览支持的目标，然后设置一个或多个目标。

## 激活数据{#activate-data}

激活工作流中的步骤因目标类型而略有不同。 以下列出了所有目标类型的完整工作流。

## 选择要将数据激活到{#select-destination}的目标

适用于：所有目标

在Adobe Experience Platform用户界面中，导航到&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 浏览]**，然后单击与要激活区段的目标对应的&#x200B;**[!UICONTROL 激活]**&#x200B;按钮，如下图所示。

![激活到目标](../assets/ui/activate-destinations/browse-tab-activate.png)

按照下一节中的步骤选择要激活的区段。

## [!UICONTROL 选择区] 段步骤  {#select-segments}

适用于：所有目标

![选择区段步骤](../assets/ui/activate-destinations/select-segments-icon.png)

在&#x200B;**[!UICONTROL 激活目标]**&#x200B;工作流的&#x200B;**[!UICONTROL 选择区段]**&#x200B;页面上，选择一个或多个要激活到目标的区段。 选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续执行下一步。

![细分到目标](../assets/ui/activate-destinations/email-select-segments.png)

## [!UICONTROL 标识映] 射步骤  {#identity-mapping}

适用于：社交目标和Google客户匹配广告目标

![标识映射步骤](../assets/ui/activate-destinations/identity-mapping-icon.png)

对于社交目标，您必须选择源属性或标识命名空间以在目标中映射为目标标识。

## 示例：在[!DNL Facebook Custom Audience] {#example-facebook}中激活受众数据

以下是在[!DNL Facebook]中激活受众数据时正确标识映射的示例。

选择源字段：

* 如果您使用的电子邮件地址没有散列，请选择`Email`命名空间作为源标识。
* 如果根据[!DNL Facebook] [电子邮件散列要求](../catalog/social/facebook.md#email-hashing-requirements)将命名空间接收时的客户电子邮件地址哈希化为[!DNL Platform]，请选择`Email_LC_SHA256`作为源标识。
* 如果您的命名空间包含非哈希电话号码，请选择`PHONE_E.164`作为源标识。 [!DNL Platform] 将对电话号码进行哈希处理以符合 [!DNL Facebook] 要求。
* 如果根据[!DNL Facebook] [电话号码散列要求](../catalog/social/facebook.md#phone-number-hashing-requirements)将数据接收时的电话号码散列到[!DNL Platform]中，请选择`Phone_SHA256`命名空间作为源标识。
* 如果您的命名空间包含[!DNL Apple]设备ID，请选择`IDFA`作为源标识。
* 如果您的命名空间包含[!DNL Android]设备ID，请选择`GAID`作为源标识。
* 如果您的命名空间包含其他类型的标识符，请选择`Custom`标识符作为源标识。

选择目标字段：

* 当源命名空间为`Email`或`Email_LC_SHA256`时，选择`Email_LC_SHA256`命名空间作为目标标识。
* 当源命名空间为`PHONE_E.164`或`Phone_SHA256`时，选择`Phone_SHA256`命名空间作为目标标识。
* 当您的源命名空间为`IDFA`或`GAID`时，选择`IDFA`或`GAID`命名空间作为目标标识。
* 当源命名空间为自定义命名空间时，选择`Extern_ID`作为目标标识。

![身份映射](../assets/ui/activate-destinations/identity-mapping.png)

未散列命名空间的数据在激活时由[!DNL Platform]自动散列。

属性源数据不会自动散列。 当源字段包含未哈希化属性时，请选中&#x200B;**[!UICONTROL 应用转换]**&#x200B;选项，以使[!DNL Platform]自动对激活上的数据进行哈希处理。
![身份映射转换](../assets/ui/activate-destinations/identity-mapping-transformation.png)

 

## 示例：在[!DNL Google Customer Match] {#example-gcm}中激活受众数据

这是在[!DNL Google Customer Match]中激活受众数据时正确标识映射的示例。

选择源字段：

* 如果您使用的电子邮件地址没有散列，请选择`Email`命名空间作为源标识。
* 如果根据[!DNL Google Customer Match] [电子邮件散列要求](../catalog/social/../advertising/google-customer-match.md)将命名空间接收时的客户电子邮件地址哈希化为[!DNL Platform]，请选择`Email_LC_SHA256`作为源标识。
* 如果您的命名空间包含非哈希电话号码，请选择`PHONE_E.164`作为源标识。 [!DNL Platform] 将对电话号码进行哈希处理以符合 [!DNL Google Customer Match] 要求。
* 如果根据[!DNL Facebook] [电话号码散列要求](../catalog/social/../advertising/google-customer-match.md)将数据接收时的电话号码散列到[!DNL Platform]中，请选择`Phone_SHA256_E.164`命名空间作为源标识。
* 如果您的命名空间包含[!DNL Apple]设备ID，请选择`IDFA`作为源标识。
* 如果您的命名空间包含[!DNL Android]设备ID，请选择`GAID`作为源标识。
* 如果您的命名空间包含其他类型的标识符，请选择`Custom`标识符作为源标识。

选择目标字段：

* 当源命名空间为`Email`或`Email_LC_SHA256`时，选择`Email_LC_SHA256`命名空间作为目标标识。
* 当源命名空间为`PHONE_E.164`或`Phone_SHA256_E.164`时，选择`Phone_SHA256_E.164`命名空间作为目标标识。
* 当您的源命名空间为`IDFA`或`GAID`时，选择`IDFA`或`GAID`命名空间作为目标标识。
* 当源命名空间为自定义命名空间时，选择`User_ID`作为目标标识。

![身份映射](../assets/ui/activate-destinations/identity-mapping-gcm.png)

未散列命名空间的数据在激活时由[!DNL Platform]自动散列。

属性源数据不会自动散列。 当源字段包含未哈希化属性时，请选中&#x200B;**[!UICONTROL 应用转换]**&#x200B;选项，以使[!DNL Platform]自动对激活上的数据进行哈希处理。
![身份映射转换](../assets/ui/activate-destinations/identity-mapping-gcm-transformation.png)

## **[!UICONTROL 计划步]** 骤 {#scheduling}

适用于：电子邮件营销目标和云存储目标

![计划步骤](../assets/ui/activate-destinations/scheduling-icon.png)

[!DNL Adobe Experience Platform] 以文件形式导出电子邮件营销和云存储目 [!DNL CSV] 标的数据在&#x200B;**[!UICONTROL 计划]**&#x200B;步骤中，您可以配置要导出的每个区段的计划和文件名。 必须配置计划，但配置文件名是可选的。

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] 以每个文件500万条记录（行）自动拆分导出文件。每行表示一个用户档案。
>
>拆分文件名后面附加一个数字，指示文件是较大导出的一部分，如下所示：`filename.csv`、`filename_2.csv`、`filename_3.csv`。

选择与要发送到目标的区段对应的&#x200B;**[!UICONTROL 创建计划]**&#x200B;按钮。

![创建计划按钮](../assets/ui/activate-destinations/create-schedule-button.png)

### 导出完整文件{#export-full-files}

选择&#x200B;**[!UICONTROL 导出完整文件]**，以使导出的文件包含符合该段条件的所有用户档案的完整快照。

![导出完整文件](../assets/ui/activate-destinations/export-full-files.png)

1. 使用&#x200B;**[!UICONTROL Frequency]**&#x200B;选择器在一次性（**[!UICONTROL 一次]**）或&#x200B;**[!UICONTROL 每日]**&#x200B;导出之间进行选择。 导出完整文件&#x200B;**[!UICONTROL Daily]**&#x200B;时，每天从开始日期到UTC（东部时间晚上7:00）的结束日期导出文件。
2. 使用&#x200B;**[!UICONTROL Time]**&#x200B;选择器以[!DNL UTC]格式选择应在何时进行导出。 导出文件&#x200B;**[!UICONTROL Daily]**&#x200B;时，每天将文件从开始日期导出到选择时的结束日期。

   >[!IMPORTANT]
   >
   >在一天的某个时间导出文件的选项当前为测试版，并且仅对选定数量的客户可用。

3. 使用&#x200B;**[!UICONTROL 日期]**&#x200B;选择器选择应进行导出的日期或间隔。
4. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以保存计划。

### 导出增量文件{#export-incremental-files}

选择&#x200B;**[!UICONTROL 导出增量文件]**&#x200B;以使导出的文件仅包含上次导出后限定该段的用户档案。

>[!IMPORTANT]
>
>第一个导出的增量文件包括符合某个区段资格的所有用户档案，这些区段用作回填。

![导出增量文件](../assets/ui/activate-destinations/export-incremental-files.png)

1. 使用&#x200B;**[!UICONTROL Frequency]**&#x200B;选择器在&#x200B;**[!UICONTROL Daily]**&#x200B;或&#x200B;**[!UICONTROL Hourly]**&#x200B;导出中进行选择。 导出增量文件&#x200B;**[!UICONTROL Daily]**&#x200B;时，每天从开始日期到UTC（东部标准时间早7:00）中午12:00结束日期导出文件。
   * 选择&#x200B;**[!UICONTROL 每小时]**&#x200B;时，使用&#x200B;**[!UICONTROL 每]**&#x200B;选择器在&#x200B;**[!UICONTROL 3]**、**[!UICONTROL 6]**、**[!UICONTROL 8]**&#x200B;和&#x200B;**[!UICONTROL 12]**&#x200B;小时选项之间进行选择。

      >[!IMPORTANT]
      >
      >每3、6、8或12小时导出增量文件的选项目前处于测试阶段，并且仅对选定数量的客户可用。 非测试版客户每天可以导出增量文件一次。

2. 使用&#x200B;**[!UICONTROL Time]**&#x200B;选择器以[!DNL UTC]格式选择应在何时进行导出。

   >[!IMPORTANT]
   >
   >选择导出的一天时间选项仅对选定数量的客户可用。 非测试版客户每天可以在UTC中午12:00（东部标准时间早上7:00）导出增量文件一次。

3. 使用&#x200B;**[!UICONTROL 日期]**&#x200B;选择器选择应进行导出的日期或间隔。
4. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以保存计划。

### 配置文件名{#file-names}

默认文件名由目标名称、区段ID以及日期和时间指示器组成。 例如，您可以编辑导出的文件名以区分不同的活动，或将数据导出时间附加到文件。

选择铅笔图标以打开模态窗口并编辑文件名。 文件名限制为255个字符。

![配置文件名](../assets/ui/activate-destinations/configure-name.png)

在文件名编辑器中，可以选择要添加到文件名中的不同组件。

![编辑文件名选项](../assets/ui/activate-destinations/activate-workflow-configure-step-2.png)

无法从文件名中删除目标名称和区段ID。 除了这些外，您还可以添加以下内容：

* **[!UICONTROL 区段名称]**:您可以将段名称追加到文件名。
* **[!UICONTROL 日期和时间]**:在添加格 `MMDDYYYY_HHMMSS` 式或生成文件时的Unix 10位时间戳之间进行选择。如果您希望您的文件在每次增量导出时都生成动态文件名，请选择其中一个选项。
* **[!UICONTROL 自定义文本]**:将自定义文本添加到文件名。

选择&#x200B;**[!UICONTROL 应用更改]**&#x200B;以确认您的选择。

>[!IMPORTANT]
> 
>如果您未选择&#x200B;**[!UICONTROL 日期和时间]**&#x200B;组件，则文件名将是静态的，新导出的文件将使用每次导出覆盖存储位置上的以前文件。 当从存储位置将循环导入作业运行到电子邮件营销平台时，建议使用此选项。

配置完所有区段后，请选择&#x200B;**[!UICONTROL 下一步]**&#x200B;继续。

## **[!UICONTROL 区段计]** 划  {#segment-schedule}

适用于：广告目标，社交目标

![细分计划步骤](../assets/ui/activate-destinations/segment-schedule-icon.png)

在&#x200B;**[!UICONTROL 区段计划]**&#x200B;页上，可以设置向目标发送数据的开始日期以及向目标发送数据的频率。

>[!IMPORTANT]
>
>对于社交目标，您必须在此步骤中选择受众的来源。 只有在下图中选择其中一个选项后，才能继续执行下一步。

![Facebook来源受众](../assets/catalog/social/facebook/facebook-origin-audience.png)

>[!IMPORTANT]
>
>对于Google客户匹配，在激活[!DNL IDFA]或[!DNL GAID]区段时，必须在此步骤中提供[!UICONTROL 应用程序ID]。

![输入应用程序id](../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

## **[!UICONTROL 选择属]** 性步骤  {#select-attributes}

适用于：电子邮件营销目标和云存储目标

![选择属性步骤](../assets/ui/activate-destinations/select-attributes-icon.png)

在&#x200B;**[!UICONTROL 选择属性]**&#x200B;页面上，选择&#x200B;**[!UICONTROL 添加新字段]**，然后选择要发送到目标的属性。

>[!NOTE]
>
> Adobe Experience Platform使用您的模式中四个推荐的常用属性预填充您的选择：`person.name.firstName`、`person.name.lastName`、`personalEmail.address`、`segmentMembership.status`。

根据是否选择`segmentMembership.status`，文件导出将按以下方式不同：
* 如果选择了`segmentMembership.status`字段，则导出的文件在初始完整快照中包括&#x200B;**[!UICONTROL Active]**&#x200B;成员，在后续增量导出中包括&#x200B;**[!UICONTROL Active]**&#x200B;和&#x200B;**[!UICONTROL Expired]**&#x200B;成员。
* 如果未选择`segmentMembership.status`字段，则导出的文件在初始完整快照和后续增量导出中仅包含&#x200B;**[!UICONTROL Active]**&#x200B;成员。

![推荐属性](../assets/ui/activate-destinations/mandatory-deduplication.png)

### 必选属性{#mandatory-attributes}

您可以将属性标记为必填，以确保[!DNL Platform]仅导出包含特定属性的用户档案。 因此，它可以用作额外的过滤形式。 将属性标记为必填项是&#x200B;**不**。

不选择必选属性将导出所有限定的用户档案，而不管其属性。

建议其中一个属性是模式的[唯一标识符](../../destinations/catalog/email-marketing/overview.md#identity)。 有关必选属性的详细信息，请参阅[电子邮件营销目标](../../destinations/catalog/email-marketing/overview.md#identity)文档中的标识部分。

### 外部重复数据删除键{#deduplication-keys}

>[!IMPORTANT]
>
>使用外部重复数据删除键的选项目前处于测试阶段，并且仅对选定数量的客户可用。

外部重复数据删除键消除了在一个导出文件中具有相同用户档案的多个记录的可能性。

在[!DNL Platform]中有三种使用外部重复数据删除键的方法：

* 使用单个身份命名空间作为[!UICONTROL 外部重复数据删除键]
* 将[!DNL XDM]用户档案中的单个用户档案属性用作[!UICONTROL 外部重复数据删除键]
* 将[!DNL XDM]用户档案的两个用户档案属性组合用作复合键

>[!IMPORTANT]
>
> 您可以将单个标识命名空间导出到目标，该命名空间会自动设置为外部重复数据删除键。 不支持向目标发送多个命名空间。
> 
> 不能将标识命名空间和用户档案属性的组合用作外部重复数据删除键。

### 外部重复数据删除示例{#deduplication-example}

此示例说明了外部重复数据删除的工作方式，具体取决于选定的外部重复数据删除键。

让我们考虑以下两个用户档案。

**用户档案A**

```json
{
  "identityMap": {
    "Email": [
      {
        "id": "johndoe_1@example.com"
      },
      {
        "id": "johndoe_2@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "existing",
        "lastQualificationTime": "2021-03-10 10:03:08"
      }
    }
  },
  "person": {
    "name": {
      "lastName": "Doe",
      "firstName": "John"
    }
  },
  "personalEmail": {
    "address": "johndoe@example.com"
  }
}
```

**用户档案 B**

```json
{
  "identityMap": {
    "Email": [
      {
        "id": "johndoe_1@example.com"
      },
      {
        "id": "johndoe_2@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "existing",
        "lastQualificationTime": "2021-04-10 11:33:28"
      }
    }
  },
  "person": {
    "name": {
      "lastName": "D",
      "firstName": "John"
    }
  },
  "personalEmail": {
    "address": "johndoe@example.com"
  }
}
```

### 外部重复数据删除用例1:无外部重复数据删除

不使用外部重复数据删除，导出文件将包含以下条目。

| personalEmail | firstName | lastName |
|---|---|---|
| johndoe@example.com | 约翰 | Doe |
| johndoe@example.com | 约翰 | D |


### 外部重复数据删除用例2:外部重复数据删除基于身份命名空间

假定由[!DNL Email]命名空间外部重复数据删除，导出文件将包含以下条目。 用户档案 B是符合区段资格的最新版本，因此它是唯一导出的版本。

| 电子邮件* | personalEmail | firstName | lastName |
|---|---|---|---|
| johndoe_1@example.com | johndoe@example.com | 约翰 | D |
| johndoe_2@example.com | johndoe@example.com | 约翰 | D |

### 外部重复数据删除用例3:外部重复数据删除基于单一用户档案属性

假定外部重复数据删除为`personal Email`属性，则导出文件将包含以下条目。 用户档案 B是符合区段资格的最新版本，因此它是唯一导出的版本。

| personalEmail* | firstName | lastName |
|---|---|---|
| johndoe@example.com | 约翰 | D |


### 外部重复数据删除用例4:外部重复数据删除基于两个用户档案属性(复合外部重复数据删除键)

假定按复合键`personalEmail + lastName`进行外部重复数据删除，导出文件将包含以下条目。

| personalEmail* | lastName* | firstName |
|---|---|---|
| johndoe@example.com | D | 约翰 |
| johndoe@example.com | Doe | 约翰 |


Adobe建议选择一个身份命名空间（如[!DNL CRM ID]或电子邮件地址）作为外部重复数据删除密钥，以确保所有用户档案记录都是唯一标识的。

>[!NOTE]
> 
>如果任何激活使用标签已应用到数据集（而非整个数据集）中的某些字段，则在以下条件下将执行这些字段级别标签：
>
>* 这些字段用于区段定义。
>* 字段将配置为目标目标的投影属性。

>
> 
例如，如果字段`person.name.firstName`具有与目标的营销操作冲突的特定数据使用标签，则在审核步骤中将显示数据使用策略违规。 有关详细信息，请参阅Adobe Experience Platform中的[数据治理](../../rtcdp/privacy/data-governance-overview.md#destinations)。

## **[!UICONTROL 查看步]** 骤 {#review}

适用于：所有目标

![审阅步骤](../assets/ui/activate-destinations/review-icon.png)

在&#x200B;**[!UICONTROL 查看]**&#x200B;页面上，您可以看到所选内容的摘要。 选择&#x200B;**[!UICONTROL 取消]**&#x200B;以分组流，选择&#x200B;**[!UICONTROL 返回]**&#x200B;以修改设置，或选择&#x200B;**[!UICONTROL 完成]**&#x200B;以确认您的选择，并开始将数据发送到目标。

>[!IMPORTANT]
>
>在此步骤中，Adobe Experience Platform将检查数据使用策略违规。 下面显示了违反策略的示例。 在解决违规之前，您无法完成区段激活工作流。 有关如何解决策略违规的信息，请参阅数据治理文档部分中的[策略实施](../../rtcdp/privacy/data-governance-overview.md#enforcement)。

![数据策略违规](../assets/common/data-policy-violation.png)

如果未检测到任何策略违规，请选择&#x200B;**[!UICONTROL 完成]**&#x200B;以确认您的选择，并开始将数据发送到目标。

![确认选择](../assets/ui/activate-destinations/confirm-selection.png)

## 验证区段激活是否成功{#verify-activation}

### 电子邮件营销目标和云存储目标{#esp-and-cloud-storage}

对于电子邮件营销目标和云存储目标，Adobe Experience Platform会在您提供的存储位置创建制表符分隔的`.csv`文件。 期望每天在您的存储位置创建新文件。 默认文件格式为：
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

您连续三天收到的文件可能如下所示：

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

这些文件在您的存储位置中的存在是成功激活的确认。 要了解导出的文件的结构，您可以[下载示例.csv文件](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv)。 此示例文件包括用户档案属性`person.firstname`、`person.lastname`、`person.gender`、`person.birthyear`和`personalEmail.address`。

## 广告目的地

在要激活数据的相应广告目标中检查您的帐户。 如果激活成功，则受众会填充到您的广告平台中。

## 社交目标

对于[!DNL Facebook]，成功的激活意味着将在[[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/)中以编程方式创建[!DNL Facebook]自定义受众。 由于用户对已激活的区段具有资格或取消资格，将会添加和删除该受众中的区段成员资格。

>[!TIP]
>
>Adobe Experience Platform与[!DNL Facebook]之间的集成支持历史受众回填。 在将区段激活到目标时，所有历史区段资格都将发送到[!DNL Facebook]。

## 禁用激活{#disable-activation}

要禁用现有激活流，请执行以下步骤：

1. 在左侧导航栏中选择&#x200B;**[!UICONTROL 目标]**，然后单击&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡，然后单击目标名称。
2. 单击右边栏中的&#x200B;**[!UICONTROL 已启用]**&#x200B;控件以更改激活流状态。
3. 在&#x200B;**更新激活流状态**&#x200B;窗口中，选择&#x200B;**确认**&#x200B;以禁用数据流。
