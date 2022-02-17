---
keywords: 激活用户档案目标；激活目标；激活数据；激活电子邮件营销目标；激活云存储目标
title: 激活受众数据以批量配置文件导出目标
type: Tutorial
seo-title: Activate audience data to batch profile export destinations
description: 了解如何通过将区段发送到基于配置文件的批量目标来激活您在Adobe Experience Platform中拥有的受众数据。
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by sending segments to batch profile-based destinations.
exl-id: 82ca9971-2685-453a-9e45-2001f0337cda
source-git-commit: ee9ed1c17a566f37b4ad79df7c66f8b2ffb4b879
workflow-type: tm+mt
source-wordcount: '2188'
ht-degree: 0%

---

# 激活受众数据以批量配置文件导出目标

## 概述 {#overview}

本文介绍了在Adobe Experience Platform基于批量配置文件的目标（如云存储和电子邮件营销目标）中激活受众数据所需的工作流程。

## 先决条件 {#prerequisites}

要将数据激活到目标，您必须成功 [连接到目标](./connect-destination.md). 如果您尚未执行此操作，请转到 [目标目录](../catalog/overview.md)，浏览支持的目标，并配置要使用的目标。

## 选择您的目标 {#select-destination}

1. 转到 **[!UICONTROL 连接>目标]**，然后选择 **[!UICONTROL 目录]** 选项卡。

   ![“目标目录”选项卡](../assets/ui/activate-batch-profile-destinations/catalog-tab.png)

1. 选择 **[!UICONTROL 激活区段]** 在与要激活区段的目标对应的卡上，如下图所示。

   ![“激活区段”按钮](../assets/ui/activate-batch-profile-destinations/activate-segments-button.png)

1. 选择要用于激活区段的目标连接，然后选择 **[!UICONTROL 下一个]**.

   ![选择目标](../assets/ui/activate-batch-profile-destinations/select-destination.png)

1. 移到下一个部分 [选择区段](#select-segments).

## 选择您的区段 {#select-segments}

使用区段名称左侧的复选框选择要激活到目标的区段，然后选择 **[!UICONTROL 下一个]**.

![选择区段](../assets/ui/activate-batch-profile-destinations/select-segments.png)


## 计划区段导出 {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_schedule"
>title="计划"
>abstract="设置文件导出类型（完整文件或增量文件）和导出频率。"
>additional-url="https://www.adobe.com/go/destinations-profile-batch-en" text="在文档中了解更多信息"

[!DNL Adobe Experience Platform] 以 [!DNL CSV] 文件。 在 **[!UICONTROL 计划]** 页面，您可以配置要导出的每个区段的计划和文件名。 必须配置计划，但配置文件名是可选的。

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] 自动将每个文件的导出文件拆分为500万条记录（行）。 每行表示一个用户档案。
>
>拆分文件名后附加一个数字，表示该文件是较大导出的一部分，如下所示： `filename.csv`, `filename_2.csv`, `filename_3.csv`.

选择 **[!UICONTROL 创建计划]** 对应于要发送到目标的区段的按钮。

![“创建计划”按钮](../assets/ui/activate-batch-profile-destinations/create-schedule-button.png)

### 导出完整文件 {#export-full-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_exportoptions"
>title="文件导出选项"
>abstract="选择 **导出完整文件** 导出符合区段资格的所有配置文件的完整快照。 选择 **导出增量文件** 仅导出自上次导出以来符合区段资格条件的用户档案。 <br> 第一个增量文件导出包含符合该区段资格的所有配置文件，用作回填。 将来的增量文件仅包括自首次增量文件导出以来符合区段资格条件的配置文件。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#export-incremental-files" text="导出增量文件"

选择 **[!UICONTROL 导出完整文件]** 触发导出文件，该文件包含选定区段的所有配置文件资格的完整快照。

![导出完整文件](../assets/ui/activate-batch-profile-destinations/export-full-files.png)

1. 使用 **[!UICONTROL 频率]** 选择器以选择导出频率：

   * **[!UICONTROL 一次]**:计划一次性按需完整文件导出。
   * **[!UICONTROL 每日]**:在您指定的时间，安排每天一次完整文件导出。

1. 使用 **[!UICONTROL 时间]** 选择器，以选择一天中的时间 [!DNL UTC] 格式，应在何时进行导出。

   >[!IMPORTANT]
   >
   >由于内部Experience Platform进程的配置方式，第一次增量文件或完整文件导出可能不包含所有回填数据。 <br> <br> 为确保完整文件和增量文件的回填数据导出完整且最新，Adobe建议在次日的中午12点（格林威治标准时间）之后设置第一个文件导出时间。 未来版本将解决此限制。

1. 使用 **[!UICONTROL 日期]** 选择器以选择应进行导出的日期或间隔。 对于每日导出，最佳做法是将开始和结束日期设置为与下游平台中的促销活动持续时间保持一致。

   >[!IMPORTANT]
   >
   > 选择导出间隔时，该间隔的最后一天不会包含在导出中。 例如，如果选择的间隔为1月4日至11日，则最后一次文件导出将在1月10日进行。

1. 选择 **[!UICONTROL 创建]** 以保存计划。


### 导出增量文件 {#export-incremental-files}

选择 **[!UICONTROL 导出增量文件]** 触发导出，其中第一个文件是所选区段所有配置文件资格的完整快照，而后续文件是自上次导出以来的增量配置文件资格。

>[!IMPORTANT]
>
>第一个导出的增量文件包含符合区段资格并可用作回填的所有配置文件。

![导出增量文件](../assets/ui/activate-batch-profile-destinations/export-incremental-files.png)

1. 使用 **[!UICONTROL 频率]** 选择器以选择导出频率：

   * **[!UICONTROL 每日]**:在您指定的时间，计划每天一次增量文件导出。
   * **[!UICONTROL 每小时]**:计划每3、6、8或12小时执行一次增量文件导出。

1. 使用 **[!UICONTROL 时间]** 选择器，以选择一天中的时间 [!DNL UTC] 格式，应在何时进行导出。

   >[!IMPORTANT]
   >
   >由于内部Experience Platform进程的配置方式，第一次增量文件或完整文件导出可能不包含所有回填数据。 <br> <br> 为确保完整文件和增量文件的回填数据导出完整且最新，Adobe建议在次日的中午12点（格林威治标准时间）之后设置第一个文件导出时间。 未来版本将解决此限制。

1. 使用 **[!UICONTROL 日期]** 选择器以选择应执行导出的间隔。 最佳做法是设置开始和结束日期，以与下游平台中促销活动的持续时间保持一致。

   >[!IMPORTANT]
   >
   >导出中不包括间隔的最后一天。 例如，如果选择的间隔为1月4日至11日，则最后一次文件导出将在1月10日进行。

1. 选择 **[!UICONTROL 创建]** 以保存计划。

### 配置文件名 {#file-names}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_filename"
>title="配置文件名"
>abstract="对于基于文件的目标，每个区段会生成唯一的文件名。 使用文件名编辑器创建和编辑唯一的文件名或保留默认名称。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#file-names" text="在文档中了解更多信息"

默认文件名由目标名称、区段ID以及日期和时间指示器组成。 例如，您可以编辑导出的文件名以区分不同的营销活动，或将数据导出时间附加到文件中。

选择铅笔图标以打开模式窗口并编辑文件名。 文件名长度限制为255个字符。

![配置文件名](../assets/ui/activate-batch-profile-destinations/configure-name.png)

在文件名编辑器中，您可以选择要添加到文件名的不同组件。

![编辑文件名选项](../assets/ui/activate-batch-profile-destinations/activate-workflow-configure-step-2.png)

无法从文件名中删除目标名称和区段ID。 除了这些外，您还可以添加以下内容：

* **[!UICONTROL 区段名称]**:可将区段名称附加到文件名。
* **[!UICONTROL 日期和时间]**:在添加 `MMDDYYYY_HHMMSS` 格式或生成文件时间的Unix 10位时间戳。 如果希望文件在每次增量导出时都生成一个动态文件名，请选择其中一个选项。
* **[!UICONTROL 自定义文本]**:向文件名中添加自定义文本。

选择 **[!UICONTROL 应用更改]** 以确认您的选择。

>[!IMPORTANT]
> 
>如果未选择 **[!UICONTROL 日期和时间]** 组件中，文件名将为静态文件，新导出的文件将使用每次导出时都会覆盖存储位置上的先前文件。 在从存储位置向电子邮件营销平台运行定期导入作业时，建议使用此选项。

配置完所有区段后，选择 **[!UICONTROL 下一个]** 继续。

## 选择配置文件属性 {#select-attributes}

对于基于用户档案的目标，您必须选择要发送到目标目标的用户档案属性。


1. 在 **[!UICONTROL 选择属性]** 页面，选择 **[!UICONTROL 添加新字段]**.

   ![添加新映射](../assets/ui/activate-batch-profile-destinations/add-new-field.png)

1. 选择 **[!UICONTROL 架构字段]** 中。

   ![选择源字段](../assets/ui/activate-batch-profile-destinations/select-target-field.png)

1. 在 **[!UICONTROL 选择字段]** ，选择要发送到目标的XDM属性，然后选择 **[!UICONTROL 选择]**.

   ![“选择源字段”页](../assets/ui/activate-batch-profile-destinations/target-field-page.png)

1. 要添加更多映射，请重复步骤1至3。

>[!NOTE]
>
> Adobe Experience Platform会使用您的架构中四个推荐的常用属性来预填充您的选择： `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

文件导出将按以下方式有所不同，具体取决于 `segmentMembership.status` 已选中：
* 如果 `segmentMembership.status` 字段，导出的文件包括 **[!UICONTROL 活动]** 初始完整快照中的成员和 **[!UICONTROL 活动]** 和 **[!UICONTROL 过期]** 成员。
* 如果 `segmentMembership.status` 字段，导出的文件仅包含 **[!UICONTROL 活动]** 初始完整快照和后续增量导出中的成员。

![推荐属性](../assets/ui/activate-batch-profile-destinations/mandatory-deduplication.png)

### 必需属性 {#mandatory-attributes}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_mandatorykey"
>title="关于必填属性"
>abstract="选择所有导出的配置文件都应包含的XDM架构属性。 不会将没有必填项的用户档案导出到目标。 不选择强制键会导出所有符合条件的用户档案，而不考虑其属性。"
>additional-url="http://www.adobe.com/go/destinations-mandatory-attributes-en" text="在文档中了解更多信息"

“必选属性”是用户启用的复选框，可确保所有配置文件记录都包含选定的属性。 例如：所有导出的用户档案都包含电子邮件地址&#x200B;。

您可以将属性标记为必填项，以确保 [!DNL Platform] 仅导出包含特定属性的用户档案。 因此，它可用作附加的过滤形式。 将属性标记为必填项是 **not** 必需。

不选择强制属性会导出所有符合条件的用户档案，而不考虑其属性。

建议其中一个属性是 [唯一标识符](../../destinations/catalog/email-marketing/overview.md#identity) 从您的架构中。 有关必需属性的更多信息，请参阅 [电子邮件营销目标](../../destinations/catalog/email-marketing/overview.md#identity) 文档。

### 重复数据删除键 {#deduplication-keys}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_deduplicationkey"
>title="关于重复数据删除键"
>abstract="通过选择重复数据删除键，消除导出文件中同一用户档案的多个记录。 选择一个命名空间或最多两个XDM架构属性作为重复数据删除键值。 未选择重复数据删除键可能会导致导出文件中出现重复的配置文件条目。"
>additional-url="http://www.adobe.com/go/destinations-deduplication-keys-en" text="在文档中了解更多信息"

重复数据删除键是用户定义的主键，可确定用户希望删除其配置文件的身份&#x200B;。

重复数据删除键消除了在一个导出文件中存在多个相同用户档案记录的可能性。

在中，可通过三种方式来使用重复数据删除键 [!DNL Platform]:

* 使用单个身份命名空间作为 [!UICONTROL 重复数据删除键]
* 使用 [!DNL XDM] 用户档案 [!UICONTROL 重复数据删除键]
* 使用 [!DNL XDM] 用作复合键的轮廓

>[!IMPORTANT]
>
> 您可以将单个身份命名空间导出到目标，并且该命名空间会自动设置为重复数据删除键。 不支持将多个命名空间发送到目标。
> 
> 不能将身份命名空间和配置文件属性的组合用作重复数据删除键。

### 重复数据删除示例 {#deduplication-example}

此示例说明了重复数据删除的工作方式，具体取决于所选的重复数据删除键。

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

**用户档案B**

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

### 重复数据删除用例1:无重复数据删除 {#deduplication-use-case-1}

如果不使用重复数据删除，则导出文件将包含以下条目。

| personalEmail | firstName | lastName |
|---|---|---|
| johndoe@example.com | 约翰 | Doe |
| johndoe@example.com | 约翰 | D |


### 重复数据删除用例2:基于身份命名空间的重复数据删除 {#deduplication-use-case-2}

假定重复数据删除由 [!DNL Email] 命名空间中，导出文件将包含以下条目。 配置文件B是符合区段资格条件的最新配置文件，因此它是唯一一个要导出的配置文件。

| 电子邮件* | personalEmail | firstName | lastName |
|---|---|---|---|
| johndoe_1@example.com | johndoe@example.com | 约翰 | D |
| johndoe_2@example.com | johndoe@example.com | 约翰 | D |

### 重复数据删除用例3:基于单个配置文件属性的重复数据删除 {#deduplication-use-case-3}

假定重复数据删除由 `personal Email` 属性中，导出文件将包含以下条目。 配置文件B是符合区段资格条件的最新配置文件，因此它是唯一一个要导出的配置文件。

| personalEmail* | firstName | lastName |
|---|---|---|
| johndoe@example.com | 约翰 | D |


### 重复数据删除用例4:基于两个配置文件属性进行重复数据删除 {#deduplication-use-case-4}

假定由复合键值进行重复数据删除 `personalEmail + lastName`，则导出文件将包含以下条目。

| personalEmail* | lastName* | firstName |
|---|---|---|
| johndoe@example.com | D | 约翰 |
| johndoe@example.com | Doe | 约翰 |


Adobe建议选择身份命名空间，例如 [!DNL CRM ID] 或将电子邮件地址作为重复数据删除键，以确保所有用户档案记录都进行唯一标识。

>[!NOTE]
> 
>如果任何数据使用标签已应用于数据集（而非整个数据集）中的某些字段，则在以下情况下会对激活强制执行这些字段级别标签：
>
>* 区段定义中使用了这些字段。
>* 这些字段配置为目标目标的投影属性。
>
> 例如，如果字段 `person.name.firstName` 具有与目标的营销操作冲突的某些数据使用标签，则在审核步骤中将显示数据使用策略违规。 有关更多信息，请参阅 [Adobe Experience Platform中的数据管理](../../rtcdp/privacy/data-governance-overview.md#destinations).

## 审阅 {#review}

在 **[!UICONTROL 审阅]** 页面，则可以查看所选内容的摘要。 选择 **[!UICONTROL 取消]** 来分解流量， **[!UICONTROL 返回]** 修改设置，或 **[!UICONTROL 完成]** 以确认您的选择并开始向目标发送数据。

>[!IMPORTANT]
>
>在此步骤中，Adobe Experience Platform会检查是否存在数据使用策略违规。 下面显示了违反策略的示例。 在解决违规之前，无法完成区段激活工作流。 有关如何解决策略违规的信息，请参阅 [策略执行](../../rtcdp/privacy/data-governance-overview.md#enforcement) 在“数据管理文档”一节中。

![数据策略违规](../assets/common/data-policy-violation.png)

如果未检测到任何策略违规，请选择 **[!UICONTROL 完成]** 以确认您的选择并开始向目标发送数据。

![审阅](../assets/ui/activate-batch-profile-destinations/review.png)

## 验证区段激活 {#verify}


对于电子邮件营销目标和云存储目标，Adobe Experience Platform会创建 `.csv` 文件。 希望每天在您的存储位置中创建一个新文件。 默认文件格式为：
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

您将连续三天收到的文件可能如下所示：

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

这些文件在您的存储位置中的存在，即表明激活成功。 要了解导出文件的结构，您可以 [下载.csv文件示例](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). 此样例文件包含配置文件属性 `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`和 `personalEmail.address`.
