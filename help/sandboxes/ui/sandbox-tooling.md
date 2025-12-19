---
title: 沙盒工具
description: 在沙盒之间无缝导出和导入沙盒配置。
exl-id: f1199ab7-11bf-43d9-ab86-15974687d182
source-git-commit: fad8cc977ec6928420abab4fd3dafca7475c33c4
workflow-type: tm+mt
source-wordcount: '3448'
ht-degree: 6%

---

# 沙盒工具

>[!NOTE]
>
>沙盒工具是同时支持[!DNL Real-Time Customer Data Platform]和[!DNL Journey Optimizer]的基础功能，可提高开发周期效率和配置准确性。<br><br>您需要具有以下两个基于角色的访问控制权限才能使用沙盒工具功能：<br>- `manage-sandbox`或`view-sandbox`<br>- `manage-package`

提高沙盒之间的配置准确性，并通过沙盒工具功能在沙盒之间无缝导出和导入沙盒配置。 使用沙盒工具缩短实现实施过程的价值时间，并在沙盒之间移动成功的配置。

您可以使用沙盒工具功能选择不同的对象并将它们导出到包中。 包可以包含单个对象或多个对象。<!--or an entire sandbox.-->包中包含的任何对象必须来自同一沙盒。

## 沙盒工具支持的对象 {#supported-objects}

沙盒工具功能允许您将[!DNL Adobe Real-Time Customer Data Platform]和[!DNL Adobe Journey Optimizer]对象导出到包中。

### 实时客户数据平台对象 {#real-time-cdp-objects}

>[!BEGINSHADEBOX]

### 多实体受众导入的变化

在[B2B架构升级](../../rtcdp/b2b-architecture-upgrade.md)后，如果在升级之前发布了包含这些受众的包，则您将无法再导入具有B2B属性和体验事件的多实体受众。 这些受众将无法导入，且无法自动转换为新架构。

要解决此限制，您必须创建一个具有更新受众的新包，然后使用沙盒工具将它们导入各自的目标沙盒中。


>[!ENDSHADEBOX]

下表列出了当前支持沙盒工具的[!DNL Adobe Real-Time Customer Data Platform]对象：

| 平台 | 对象 | 详细信息 |
| --- | --- | --- |
| 客户数据平台 | 源 | <ul><li>出于安全原因，源帐户凭据未复制到目标沙盒中，需要手动更新。</li><li>默认情况下，源数据流将以草稿状态复制。</li></ul> **注意：**&#x200B;目前，沙盒工具仅支持基于批次的源数据流。 不支持基于流的源数据流。 |
| 客户数据平台 | 受众 | <ul><li>仅支持&#x200B;**[!UICONTROL Customer Audience]**&#x200B;类型&#x200B;**[!UICONTROL Segmentation service]**。</li><li>用于同意和管理的现有标签将复制到同一导入作业中。</li><li> 检查合并策略依赖关系时，系统将自动选择具有相同XDM类的目标沙盒中的默认合并策略。</li><li>如果在导入受众时检测到具有相同名称的现有对象，则沙盒工具将始终重用现有对象，以避免对象扩散。</li></ul> |
| 客户数据平台 | 身份标识 | <ul><li>在Target沙盒中创建时，系统将自动删除重复的Adobe标准身份命名空间。</li><li>仅当在合并架构中启用受众规则中的所有属性时，才能复制受众。 必须先为统一配置文件移动和启用必要的架构。</li></ul> |
| 客户数据平台 | 架构/字段组/数据类型 | <ul><li>用于同意和管理的现有标签将复制到同一导入作业中。</li><li>您可以灵活地导入未启用“统一配置文件”选项的架构。 架构关系边缘用例未包含在包中。</li><li>如果在导入架构/字段组时检测到具有相同名称的现有对象，则沙盒工具将始终重用现有对象，以避免对象扩散。</li></ul> |
| 客户数据平台 | 数据集 | 在复制数据集时，默认情况下将禁用统一配置文件设置。 |
| 客户数据平台 | 同意和治理政策 | 将用户创建的自定义策略添加到包中，并在沙盒之间移动它们。 |

以下对象已导入，但处于草稿或已禁用状态：

| 功能 | 对象 | 状态 |
| --- | --- | --- |
| 导入状态 | Source数据流 | 草稿 |
| 导入状态 | 历程 | 草稿 |
| 统一轮廓 | 数据集 | 已禁用统一配置文件 |
| 支持 | 数据治理策略 | 已禁用 |

### Adobe Journey Optimizer对象 {#abobe-journey-optimizer-objects}

下表列出了当前支持沙盒工具的[!DNL Adobe Journey Optimizer]对象和限制。 有关最佳实践的完整列表，请参阅[Journey Optimizer一般最佳实践](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/connect-systems/sandbox/copy-objects-to-sandbox?#global)指南。

| 平台 | 对象 | 支持的依赖对象 | 详细信息 |
| --- | --- | --- | --- |
| [!DNL Adobe Journey Optimizer] | 受众 | | 受众可以复制为历程对象的依赖对象。 您可以选择创建新受众，也可以重复使用目标沙盒中的现有受众。 |
| [!DNL Adobe Journey Optimizer] | 架构 | | 历程中使用的架构可以作为依赖对象复制。 您可以选择创建新架构或重用目标沙盒中的现有架构。 |
| [!DNL Adobe Journey Optimizer] | 合并策略 | | 历程中使用的合并策略可以作为依赖对象复制。 在目标沙盒中，您&#x200B;**无法**&#x200B;创建新的合并策略，您只能使用现有的合并策略。 |
| [!DNL Adobe Journey Optimizer] | 历程 | 历程中使用的以下对象将作为依赖对象复制。 在导入工作流期间，您可以为每个选择&#x200B;**[!UICONTROL Create new]**&#x200B;或&#x200B;**[!UICONTROL Use existing]**： <ul><li>受众</li><li>画布详细信息</li><li>内容模板</li><li>自定义操作</li><li>数据源</li><li>事件</li><li>字段组</li><li>片段</li><li>架构</li></ul> | 当您在导入过程中选择&#x200B;**[!UICONTROL Use existing]**&#x200B;将历程复制到另一个沙盒时，您选择的现有自定义操作&#x200B;**必须**&#x200B;与源自定义操作完全匹配。 如果两者不匹配，新历程将生成无法解决的错误。<br>系统复制历程中使用的事件和事件详细信息，并在目标沙盒中创建新版本。 |
| [!DNL Adobe Journey Optimizer] | 操作 | | 历程中使用的电子邮件和推送消息可以作为依赖对象复制。 不检查消息中用于个性化的历程字段中使用的渠道操作活动的完整性。 不会复制内容块。<br><br>可以复制历程中使用的更新配置文件操作。 自定义操作可以单独添加到资源包中。 旅程中使用的操作详细信息也会被复制。 它始终会在目标沙盒中创建新版本。 |
| [!DNL Adobe Journey Optimizer] | 自定义操作 |  | 自定义操作可以单独添加到资源包中。 将自定义操作分配给历程后，便无法再编辑它。 要更新自定义操作，您应： <ul><li>在迁移历程之前移动自定义操作</li><li>在迁移后更新自定义操作的配置（如请求标头、查询参数和身份验证）</li><li>使用您在第一步中添加的自定义操作迁移历程对象</li></ul> |
| [!DNL Adobe Journey Optimizer] | 内容模板 | | 内容模板可以作为历程对象的依赖对象复制。 通过独立模板，可轻松地在Journey Optimizer营销活动和历程中重用自定义内容。 |
| [!DNL Adobe Journey Optimizer] | 片段 | 所有嵌套片段。 | 片段可以作为历程对象的依赖对象复制。 片段是可重用的组件，可以在各个Journey Optimizer营销活动和历程中的一个或多个电子邮件中引用。 |
| [!DNL Adobe Journey Optimizer] | 营销活动 | 促销活动中使用的以下对象将作为从属对象复制： <ul><li>营销活动</li><li>受众</li><li>架构</li><li>内容模板</li><li>片段</li><li>消息/内容</li><li>渠道配置</li><li>统一的决策对象</li><li>试验设置/变体</li></ul> | <ul><li>营销活动可与所有与用户档案、受众、架构、内联消息和依赖对象相关的项目一起复制。 不会复制某些项目，例如数据使用标签和语言设置。 有关无法复制的对象的完整列表，请参阅[将对象导出到另一个沙盒](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/configuration/copy-objects-to-sandbox)指南。</li><li>如果存在相同的配置，系统将自动检测并重新使用目标沙盒中的现有渠道配置对象。 如果未找到匹配的配置，则在导入期间跳过渠道配置，并且用户必须手动更新此历程的目标沙盒中的渠道设置。</li><li>用户可以重复使用目标沙盒中的现有试验和受众作为所选营销活动的依赖对象。</li></ul> |
| [!DNL Adobe Journey Optimizer] | 决策 | 在复制决策对象之前，目标沙盒中必须存在以下对象： <ul><li>在决策对象间使用的配置文件属性</li><li>自定义选件属性的字段组</li><li>用于跨规则、排名或上限的上下文属性的数据流架构。</li></ul> | <ul><li>当前不支持复制使用AI模型的排名公式。</li><li>决策项（优惠项）不会自动包含在内。 为确保它们已传输，请使用&#x200B;**添加到包**&#x200B;选项手动添加它们。</li><li>使用选择策略的策略要求在复制过程中手动添加关联的决策项。 使用手动或备用决策项目的策略会自动将这些项目作为直接依赖项包含在内。</li><li>必须先复制决策项目，然后再复制任何其他相关对象。</li><li>有关支持的对象的完整列表，请参阅[将对象导出到另一个沙盒](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/configuration/copy-objects-to-sandbox)指南。</li></ul> |

## 将对象导出到包中 {#export-objects}

>[!NOTE]
>
>所有导出操作都记录在审核日志中。

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_remove_object"
>title="移除对象"
>abstract="要从包中移除某个对象，请选择要移除的行，然后使用在选择后出现的删除选项。注意，无法从已发布的包中移除对象。"

>[!CONTEXTUALHELP]
>id="platform_sandbox_package_expiry"
>title="包过期设置"
>abstract="包被设置为在草稿状态下不活跃一段时间后过期。默认日期被设置为今天起 90 天后。此日期不断变化，直到发布包为止。如果您明天访问处于草稿状态下的包，则除非您手动设置此项，否则该日期前移 1 天。"

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_package_status"
>title="包状态"
>abstract="默认情况下，状态设置为草稿。发布包后，状态将更改为已发布。发布包后不能进行任何更改。"

>[!NOTE]
>
>只有在您有权访问对象时，才能导入资源包。

此示例记录了导出架构并将其添加到包的过程。 您可以使用相同的流程导出其他对象，例如数据集、历程等。

### 将对象添加到新包 {#add-object-to-new-package}

从左侧导航中选择&#x200B;**[!UICONTROL Schemas]**，然后选择&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡，其中列出了可用的架构。 接下来，选择选定架构旁边的省略号(`...`)，下拉菜单将显示控件。 从下拉列表中选择&#x200B;**[!UICONTROL Add to package]**。

![架构列表，显示突出显示[!UICONTROL Add to package]控件的下拉菜单。](../images/ui/sandbox-tooling/add-to-package.png)

从&#x200B;**[!UICONTROL Add to package]**&#x200B;对话框中，选择&#x200B;**[!UICONTROL Create new package]**&#x200B;选项。 为您的包提供一个[!UICONTROL Name]和一个可选的[!UICONTROL Description]，然后选择&#x200B;**[!UICONTROL Add]**。

![选定了[!UICONTROL Add to package]并突出显示[!UICONTROL Create new package]的[!UICONTROL Add]对话框。](../images/ui/sandbox-tooling/create-new-package.png)

您返回到&#x200B;**[!UICONTROL Schemas]**&#x200B;环境。 现在，您可以按照下面列出的后续步骤，将其他对象添加到您创建的资源包中。

### 将对象添加到现有包并发布 {#add-object-to-existing-package}

要查看可用架构的列表，请从左侧导航中选择&#x200B;**[!UICONTROL Schemas]**，然后选择&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡。 接下来，选择所选架构旁边的省略号(`...`)，在下拉菜单中查看控制选项。 从下拉列表中选择&#x200B;**[!UICONTROL Add to package]**。

![架构列表，显示突出显示[!UICONTROL Add to package]控件的下拉菜单。](../images/ui/sandbox-tooling/add-to-package.png)

出现&#x200B;**[!UICONTROL Add to package]**&#x200B;对话框。 选择&#x200B;**[!UICONTROL Existing package]**&#x200B;选项，然后选择&#x200B;**[!UICONTROL Package name]**&#x200B;下拉菜单并选择所需的包。 最后，选择&#x200B;**[!UICONTROL Add]**&#x200B;以确认您的选择。

![[!UICONTROL Add to package]对话框，显示从下拉列表中选定的包。](../images/ui/sandbox-tooling/add-to-existing-package.png)

将列出添加到包中的对象列表。 要发布包并使其可用于导入到沙盒中，请选择&#x200B;**[!UICONTROL Publish]**。

![包中的对象列表，突出显示[!UICONTROL Publish]选项。](../images/ui/sandbox-tooling/publish-package.png)

选择&#x200B;**[!UICONTROL Publish]**&#x200B;以确认发布包。

![发布包确认对话框，突出显示[!UICONTROL Publish]选项。](../images/ui/sandbox-tooling/publish-package-confirmation.png)

>[!NOTE]
>
>发布后，无法更改包的内容。 要避免出现兼容性问题，请确保已选择所有必要的资源。 如果必须进行更改，则需要创建新资源包。

您返回到&#x200B;**[!UICONTROL Packages]**&#x200B;环境中的[!UICONTROL Sandboxes]选项卡，您可以在其中查看新发布的包。

![突出显示新发布的包的沙盒包列表。](../images/ui/sandbox-tooling/published-packages.png)

## 将资源包导入目标沙盒 {#import-package-to-target-sandbox}

>[!NOTE]
>
>所有导入操作都记录在审核日志中。

要将包导入目标沙盒，请导航到沙盒&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡，然后选择沙盒名称旁边的加号(+)选项。

![沙盒&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡突出显示导入包选择。](../images/ui/sandbox-tooling/browse-sandboxes.png)

使用下拉菜单，选择要导入到目标沙盒的&#x200B;**[!UICONTROL Package name]**。 添加将用于未来监视的&#x200B;**[!UICONTROL Job name]**。 默认情况下，在导入包的架构时，将禁用统一配置文件。 切换&#x200B;**为配置文件**&#x200B;启用架构以启用它，然后选择&#x200B;**[!UICONTROL Next]**。

![导入详细信息页面显示[!UICONTROL Package name]下拉列表选择](../images/ui/sandbox-tooling/import-package-to-sandbox.png)

[!UICONTROL Package object and dependencies]页提供了此包中包含的所有资源的列表。 系统自动检测成功导入所选父对象所需的从属对象。 任何缺少的属性都会显示在页面顶部。 选择&#x200B;**[!UICONTROL View details]**&#x200B;以获取更详细的细分。

![[!UICONTROL Package object and dependencies]页面显示缺少的属性。](../images/ui/sandbox-tooling/missing-attributes.png)

>[!NOTE]
>
>依赖对象可以替换为目标沙盒中的现有对象，这允许您重用现有对象，而不是创建新版本。 例如，导入包含架构的包时，您可以在目标沙盒中重用现有的自定义字段组和身份命名空间。 或者，在导入包含历程的包时，您可以重复使用目标沙盒中的现有区段。
>
>沙盒工具当前不支持更新或覆盖现有对象。 您可以选择创建新对象，或继续使用现有对象而不进行修改。 如果检测到具有相同名称的现有对象，则沙盒工具将始终重用现有对象，即使您选择了[!UICONTROL Create new]选项以避免对象扩散。

要使用现有对象，请选择从属对象旁边的铅笔图标。

![[!UICONTROL Package object and dependencies]页面显示包中包含的资产列表。](../images/ui/sandbox-tooling/package-objects-and-dependencies.png)

此时会显示创建新或使用现有内容的选项。 选择 **[!UICONTROL Use existing]**。

![显示依赖对象选项[!UICONTROL Package object and dependencies]和[!UICONTROL Create new]的[!UICONTROL Use existing]页面。](../images/ui/sandbox-tooling/use-existing-object.png)

**[!UICONTROL Field group]**&#x200B;对话框显示该对象可用的字段组列表。 选择所需的字段组，然后选择&#x200B;**[!UICONTROL Save]**。

![显示在[!UICONTROL Field group]对话框上的字段列表，突出显示[!UICONTROL Save]选择。](../images/ui/sandbox-tooling/field-group-list.png)

返回到[!UICONTROL Package object and dependencies]页。 从此处选择&#x200B;**[!UICONTROL Finish]**&#x200B;以完成包导入。

![[!UICONTROL Package object and dependencies]页面显示包中包含的资产列表，突出显示[!UICONTROL Finish]。](../images/ui/sandbox-tooling/finish-object-dependencies.png)

## 导出和导入整个沙盒

>[!NOTE]
>
>目前，在导出或导入整个沙盒时仅支持Real-time Customer Data Platform对象。 目前不支持历程等Adobe Journey Optimizer对象。

您可以将所有受支持的对象类型导出到完整的沙盒包中，然后跨各种沙盒导入包以复制对象配置。 例如，此功能允许您：

- 如果需要重置沙盒，请重新导入沙盒以重现对象的所有配置
- 将包导入其他沙盒并将它用作Blueprint沙盒以加快开发过程。

### 导出整个沙盒 {#export-entire-sandbox}

要导出整个沙盒，请导航到[!UICONTROL Sandboxes] **[!UICONTROL Packages]**&#x200B;选项卡并选择&#x200B;**[!UICONTROL Create package]**。

![突出显示[!UICONTROL Sandboxes]的&#x200B;**[!UICONTROL Packages]** [!UICONTROL Create package]选项卡。](../images/ui/sandbox-tooling/create-sandbox-package.png)

在&#x200B;**[!UICONTROL Entire sandbox]**&#x200B;对话框中选择[!UICONTROL Type of package]的[!UICONTROL Create package]。 为您的新包提供[!UICONTROL Package name]，然后从下拉列表中选择&#x200B;**[!UICONTROL Sandbox]**。 最后，选择&#x200B;**[!UICONTROL Create]**&#x200B;以确认您的条目。

![显示已完成字段并突出显示[!UICONTROL Create package]的[!UICONTROL Create]对话框。](../images/ui/sandbox-tooling/create-package-dialog.png)

已成功创建包，请选择&#x200B;**[!UICONTROL Publish]**&#x200B;以发布包。

![突出显示新发布的包的沙盒包列表。](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

您返回到&#x200B;**[!UICONTROL Packages]**&#x200B;环境中的[!UICONTROL Sandboxes]选项卡，您可以在其中查看新发布的包。

### 导入整个沙盒包 {#import-entire-sandbox-package}

>[!NOTE]
>
>所有对象将作为新对象导入到目标沙盒中。 最佳实践是将完整的沙盒包导入空沙盒中。

要将包导入目标沙盒，请导航到[!UICONTROL Sandboxes] **[!UICONTROL Browse]**&#x200B;选项卡，然后选择沙盒名称旁边的加号(+)选项。

![沙盒&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡突出显示导入包选择。](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

使用下拉菜单，使用&#x200B;**[!UICONTROL Package name]**&#x200B;下拉菜单选择完整的沙盒。 添加将用于将来监视的&#x200B;**[!UICONTROL Job name]**&#x200B;和可选的&#x200B;**[!UICONTROL Job description]**，然后选择&#x200B;**[!UICONTROL Next]**。

![导入详细信息页面显示[!UICONTROL Package name]下拉列表选择](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>您必须对包中包含的所有对象具有完全权限。 如果您没有权限，导入操作将失败并显示错误消息。

您将转到[!UICONTROL Package object and dependencies]页面，在该页面中可以查看已导入和排除对象的对象和依赖项数量。 从此处选择&#x200B;**[!UICONTROL Import]**&#x200B;以完成包导入。

![[!UICONTROL Package object and dependencies]页面显示不受支持的对象类型的内联消息，突出显示[!UICONTROL Import]。](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)

留出一段时间以完成导入。 完成时间会因包中的对象数而异。 您可以从[!UICONTROL Sandboxes] **[!UICONTROL Jobs]**&#x200B;选项卡监视导入作业。

## 监控导入详细信息 {#view-import-details}

要查看导入的详细信息，请导航到[!UICONTROL Sandboxes] **[!UICONTROL Jobs]**&#x200B;选项卡，然后从列表中选择包。 或者，使用搜索栏搜索包。

![沙盒[!UICONTROL Jobs]选项卡突出显示导入包选择。](../images/ui/sandbox-tooling/imports-tab.png)

<!--### View imported objects {#view-imported-objects}

On the **[!UICONTROL Jobs]** tab in the [!UICONTROL Sandboxes] environment, select **[!UICONTROL View imported objects]** from the right details pane.

Select **[!UICONTROL View imported objects]** from the right details pane on the **[!UICONTROL Jobs]** tab in the [!UICONTROL Sandboxes] environment.

![The sandboxes [!UICONTROL Imports] tab highlights the [!UICONTROL View imported objects] selection in the right pane.](../images/ui/sandbox-tooling/view-imported-objects.png)

Use the arrows to expand objects to view the full list of fields that have been imported into the package.

![The sandboxes [!UICONTROL Imported objects] showing a list of objects imported into the package.](../images/ui/sandbox-tooling/expand-imported-objects.png)-->

在沙盒环境的&#x200B;**[!UICONTROL View import summary]**&#x200B;选项卡的右侧详细信息窗格中选择&#x200B;**[!UICONTROL Jobs]**。

![沙盒[!UICONTROL Imports]选项卡突出显示右侧窗格中的[!UICONTROL View import details]选择。](../images/ui/sandbox-tooling/view-import-details.png)

**[!UICONTROL Import summary]**&#x200B;对话框显示导入的细分，进度以百分比表示。

>[!NOTE]
>
>您可以通过导航到特定的清单页面来查看对象列表。

![显示导入详细划分的[!UICONTROL Import details]对话框。](../images/ui/sandbox-tooling/import-details.png)

导入完成后，将在Experience Platform UI中收到通知。 您可以通过警报图标访问这些通知。 如果作业不成功，您可以在此处导航到疑难解答。

## 通过沙盒工具跨沙盒传输迭代对象配置更新 {#move-configs}

您可以使用沙盒工具在不同沙盒之间传输对象配置。 以前，必须手动重新创建或重新导入对象（例如架构、字段组和数据类型）的配置更新才能传输到其他沙盒。 借助此功能，您可以使用沙盒工具通过在不同沙盒之间无缝传输配置更新来加快工作流并减少潜在错误。

![显示如何在沙盒之间移动更新的图表。](../images/ui/sandbox-tooling/move-updates-diagram.png)

>[!TIP]
>
> 在尝试在不同沙盒之间传输对象配置之前，请确保您满足以下先决条件。
>
>- 访问沙盒工具的相应权限。
>- 源沙盒中新创建或更新的对象（如架构）。

>[!BEGINSHADEBOX]

### 更新操作支持的对象类型

以下是支持更新的对象类型：

- 架构
- 字段组
- 数据类型

| 支持的更新 | 不支持的更新 |
| --- | --- |
| <ul><li>向资源中添加新字段/字段组。</li><li>将必填字段设为可选字段。</li><li>引入新的必填字段。</li><li>正在引入新的关系字段。</li><li>引入新的标识字段。</li><li>更改资源的显示名称和描述。</li></ul> | <ul><li>删除以前定义的字段。</li><li>为实时客户配置文件启用架构时，重新定义现有字段。</li><li>删除或限制以前支持的字段值。</li><li>将现有字段移动到架构树中的其他位置 — 这将在目标沙盒中创建一个新字段，但不会删除上一个字段。</li><li>启用或禁用架构以参与配置文件 — 比较时将跳过此操作。</li><li>访问控制标签。</li></ul> |

>[!ENDSHADEBOX]

请按照以下步骤了解如何使用沙盒工具在不同沙盒之间传输对象配置。

### 先前导入的对象

如果您的用例涉及源沙盒中要求在打包并导入到其他沙盒后进行配置更新的现有对象，请按照以下步骤操作。

首先，更新源沙盒中的对象。 例如，导航到&#x200B;**[!UICONTROL Schemas]**&#x200B;工作区，选择您的架构，然后添加新字段组。

![架构工作区具有更新的架构。](../images/ui/sandbox-tooling/update-schema.png)

更新架构后，导航到&#x200B;**[!UICONTROL Sandboxes]**，选择&#x200B;**[!UICONTROL Packages]**，然后找到现有包。

![已选定包的沙盒工具接口](../images/ui/sandbox-tooling/select-package.png)

使用包界面验证更改。 选择&#x200B;**[!UICONTROL Check for updates]**&#x200B;可查看对包中项目所做的任何更改。 接下来，选择&#x200B;**[!UICONTROL View diff]**&#x200B;以接收对项目执行的所有更改的详细摘要。

![选择了带有查看差异按钮的包接口。](../images/ui/sandbox-tooling/view-diff.png)

出现[!UICONTROL View diff]接口。 有关源工件和目标工件以及要应用于它们的更改的信息，请参阅此收费。

![更改摘要。](../images/ui/sandbox-tooling/summary-of-changes.png)

在此步骤中，您还可以选择[!UICONTROL Summarize with AI]以分步汇总所有更改。

![启用了AI的摘要。](../images/ui/sandbox-tooling/ai-summary.png)

准备就绪后，选择&#x200B;**[!UICONTROL Update package]**，然后在显示的弹出窗口中选择&#x200B;**[!UICONTROL Confirm]**。 作业完成后，您可以刷新页面并选择&#x200B;**[!UICONTROL View history]**&#x200B;以验证包的版本。

![确认窗口。](../images/ui/sandbox-tooling/confirm-changes.png)

要导入更改，请导航回[!UICONTROL Packages]目录并选择包旁边的省略号(`...`)，然后选择&#x200B;**[!UICONTROL Import package]**。 Experience Platform自动选择[!UICONTROL Update existing objects]。 验证更改，然后选择&#x200B;**[!UICONTROL Finish]**。

>[!NOTE]
>
>作为此工作流的一部分，所有依赖对象都会自动更新到目标沙盒中。

![导入目标接口。](../images/ui/sandbox-tooling/import-objective.png)

要进一步验证导入流程，请导航到目标沙盒，并手动从该沙盒中查看更新的对象。

### 在目标沙盒中手动创建的对象

如果您的用例涉及将配置更改应用到在单独的沙盒中手动创建的对象，请按照以下步骤操作。

首先，使用更新后的对象创建和发布新包。

接下来，将包导入包含要更新的对象的目标沙盒。 在导入过程中，选择&#x200B;**[!UICONTROL Update existing objects]**，然后使用对象导航器手动选择要应用更新的目标对象。

>[!NOTE]
>
>- 可以选择在不同的沙盒中为从属对象选择目标映射。 如果未选中任何项，则会创建一个新项。
>- 对于身份命名空间，如果需要在目标沙盒中重用现有身份，系统会自动检测是否需要创建新身份。

![要更新的目标对象的带占位符的导入目标接口。](../images/ui/sandbox-tooling/update-existing-objects.png)

标识要更新的目标对象后，请选择&#x200B;**[!UICONTROL Finish]**。

![选定的目标对象。](../images/ui/sandbox-tooling/add-updated-objects.png)

## 视频教程

以下视频旨在支持您了解沙盒工具，并概述如何创建新包、发布包和导入包。

>[!VIDEO](https://video.tv.adobe.com/v/3446099/?captions=chi_hans&learn=on)

## 后续步骤

本文档演示了如何在Experience Platform UI中使用沙盒工具功能。 有关沙盒的信息，请参阅[沙盒用户指南](../ui/user-guide.md)。

有关使用沙盒API执行不同操作的步骤，请参阅[沙盒开发人员指南](../api/getting-started.md)。 有关Experience Platform中沙盒的高级概述，请参阅[概述文档](../home.md)。
