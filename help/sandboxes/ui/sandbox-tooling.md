---
title: 沙盒工具
description: 在沙盒之间无缝导出和导入沙盒配置。
exl-id: f1199ab7-11bf-43d9-ab86-15974687d182
source-git-commit: 58fcf3cbff242f65969193fd2e3d6eea0e6539aa
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 7%

---

# 沙盒工具

>[!NOTE]
>
>沙盒工具是支持两者的基本功能 [!DNL Real-Time Customer Data Platform] 和 [!DNL Journey Optimizer] 提高了开发周期效率和配置准确性。<br><br>您需要具有以下两个基于角色的访问控制权限，才能使用沙盒工具功能：<br>- `manage-sandbox` 或 `view-sandbox`<br>- `manage-package`

提高沙盒之间的配置准确性，并通过沙盒工具功能在沙盒之间无缝导出和导入沙盒配置。 使用沙盒工具缩短实现实施过程的价值时间，并在沙盒之间移动成功的配置。

您可以使用沙盒工具功能选择不同的对象并将它们导出到包中。 软件包可以包含单个对象或多个对象。 <!--or an entire sandbox.-->包中包含的任何对象必须来自同一沙盒。

## 沙盒工具支持的对象 {#supported-objects}

沙盒工具功能使您能够导出 [!DNL Adobe Real-Time Customer Data Platform] 和 [!DNL Adobe Journey Optimizer] 对象放入包中。

### Real-time Customer Data Platform对象 {#real-time-cdp-objects}

下表列出了 [!DNL Adobe Real-Time Customer Data Platform] 当前支持沙盒工具处理的对象：

| 平台 | 对象 | 详细信息 |
| --- | --- | --- |
| 客户数据平台 | 源 | 出于安全原因，源帐户凭据未复制到目标沙盒中，需要手动更新。 默认情况下，源数据流将以草稿状态复制。 |
| 客户数据平台 | 受众 | 仅 **[!UICONTROL 客户受众]** type **[!UICONTROL 分段服务]** 受支持。 用于同意和管理的现有标签将复制到同一导入作业中。 |
| 客户数据平台 | 标识 | 在Adobe沙盒中创建时，系统将自动删除重复的目标标准身份命名空间。 仅当在合并架构中启用受众规则中的所有属性时，才能复制受众。 必须先为统一配置文件移动和启用必要的架构。 |
| 客户数据平台 | 架构 | 用于同意和管理的现有标签将复制到同一导入作业中。 架构统一配置文件状态将从源沙盒中按原样复制。 如果为源沙盒中的统一配置文件启用了架构，则所有属性都将移至合并架构。 架构关系边缘用例未包含在包中。 |
| 客户数据平台 | 数据集 | 在复制数据集时，默认情况下将禁用统一配置文件设置。 |

以下对象已导入，但处于草稿或已禁用状态：

| 功能 | 对象 | 状态 |
| --- | --- | --- |
| 导入状态 | 源数据流 | 草稿 |
| 导入状态 | 历程 | 草稿 |
| 统一个人资料 | 数据集 | 已禁用统一配置文件 |
| 支持 | 数据治理策略 | 已禁用 |

### Adobe Journey Optimizer对象 {#abobe-journey-optimizer-objects}

下表列出了 [!DNL Adobe Journey Optimizer] 当前支持沙盒工具处理的对象和限制：

| 平台 | 对象 | 详细信息 |
| --- | --- | --- |
| [!DNL Adobe Journey Optimizer] | 受众 | 受众可以复制为历程对象的依赖对象。 您可以选择创建新受众，也可以重复使用目标沙盒中的现有受众。 |
| [!DNL Adobe Journey Optimizer] | 架构 | 历程中使用的架构可以作为依赖对象复制。 您可以选择创建新架构或重用目标沙盒中的现有架构。 |
| [!DNL Adobe Journey Optimizer] | 历程 — 画布详细信息 | 画布上的历程表示形式包括历程中的对象，如复制的条件、操作、事件、读取受众等。 跳转活动将从副本中排除。 |
| [!DNL Adobe Journey Optimizer] | 活动 | 旅程中使用的事件和事件详细信息已复制。 它始终会在目标沙盒中创建新版本。 |
| [!DNL Adobe Journey Optimizer] | 操作 | 历程中使用的电子邮件和推送消息可以作为依赖对象复制。 不检查消息中用于个性化的历程字段中使用的渠道操作活动的完整性。 不会复制内容块。<br><br>可以复制历程中使用的更新配置文件操作。 历程中使用的自定义操作和操作详细信息也会被复制。 它始终会在目标沙盒中创建新版本。 |

曲面（例如预设）不会被复制。 系统根据消息类型和表面名称，自动选择目标沙盒上最接近的匹配项。 如果在目标沙盒上未找到表面，则表面复制将失败，导致消息复制失败，因为消息需要表面才可供设置。 在这种情况下，需要为消息的正确渠道至少创建一个表面，以便副本正常工作。

导出历程时，不支持将自定义身份类型作为依赖对象。

## 将对象导出到资源包中 {#export-objects}

>[!NOTE]
>
>所有导出操作都记录在审核日志中。

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_exit_package"
>title="保存并退出包"
>abstract="要退出包并保存，用户只需使用后退选项即可。"

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_remove_object"
>title="移除对象"
>abstract="用户必须选择行，然后使用删除选项（选择后可用）来移除该行。"

>[!CONTEXTUALHELP]
>id="platform_sandbox_package_expiry"
>title="包有效期设置"
>abstract="该日期设为从今天起 90 天。该日期会持续更改，直到包发布为止。如果用户明天访问处于草稿状态的包，则日期会移动 +1 天（除非用户设置）。"

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_package_status"
>title="包状态"
>abstract="默认情况下，状态设置为草稿。发布包后，状态将更改为已发布。发布包后不能进行任何更改。"

>[!NOTE]
>
>只有在您有权访问对象时，才能导入资源包。

此示例记录了导出架构并将其添加到包的过程。 您可以使用相同的流程导出其他对象，例如数据集、历程等。

### 将对象添加到新包 {#add-object-to-new-package}

选择 **[!UICONTROL 架构]** 从左侧导航中，然后选择 **[!UICONTROL 浏览]** 选项卡，其中列出了可用的架构。 接下来，选择省略号(`...`)，此时下拉菜单中显示控件。 选择 **[!UICONTROL 添加到包]** 从下拉菜单中查找。

![架构列表，其中显示了突出显示 [!UICONTROL 添加到包] 控制。](../images/ui/sandbox-tooling/add-to-package.png)

从 **[!UICONTROL 添加到包]** 对话框，选择 **[!UICONTROL 创建新包]** 选项。 提供 [!UICONTROL 名称] 适用于您的包和可选 [!UICONTROL 描述]，然后选择 **[!UICONTROL 添加]**.

![此 [!UICONTROL 添加到包] 对话框 [!UICONTROL 创建新包] 选定并突出显示 [!UICONTROL 添加].](../images/ui/sandbox-tooling/create-new-package.png)

您将返回 **[!UICONTROL 架构]** 环境。 现在，您可以按照下面列出的后续步骤，将其他对象添加到您创建的资源包中。

### 将对象添加到现有包并发布 {#add-object-to-existing-package}

要查看可用架构的列表，请选择 **[!UICONTROL 架构]** 从左侧导航中，然后选择 **[!UICONTROL 浏览]** 选项卡。 接下来，选择省略号(`...`)，以查看下拉菜单中的控制选项。 选择 **[!UICONTROL 添加到包]** 从下拉菜单中查找。

![架构列表，其中显示了突出显示 [!UICONTROL 添加到包] 控制。](../images/ui/sandbox-tooling/add-to-package.png)

此 **[!UICONTROL 添加到包]** 出现对话框。 选择 **[!UICONTROL 现有包]** 选项，然后选择 **[!UICONTROL 包名称]** 下拉列表并选择所需的包。 最后，选择 **[!UICONTROL 添加]** 确认您的选择。

![[!UICONTROL 添加到包] 对话框，从下拉列表中显示选定的包。](../images/ui/sandbox-tooling/add-to-existing-package.png)

将列出添加到包中的对象列表。 要发布包并使其可用于导入到沙盒中，请选择 **[!UICONTROL Publish]**.

![包中的对象列表，突出显示 [!UICONTROL Publish] 选项。](../images/ui/sandbox-tooling/publish-package.png)

选择 **[!UICONTROL Publish]** 以确认发布包。

![发布包确认对话框，突出显示 [!UICONTROL Publish] 选项。](../images/ui/sandbox-tooling/publish-package-confirmation.png)

>[!NOTE]
>
>发布后，无法更改包的内容。 要避免出现兼容性问题，请确保已选择所有必要的资源。 如果必须进行更改，则需要创建新资源包。

您将返回 **[!UICONTROL 包]** 选项卡 [!UICONTROL 沙盒] 环境，您可以在其中查看新发布的包。

![突出显示新发布的包的沙盒包列表。](../images/ui/sandbox-tooling/published-packages.png)

## 将资源包导入目标沙盒 {#import-package-to-target-sandbox}

>[!NOTE]
>
>所有导入操作都记录在审核日志中。

要将包导入目标沙盒，请导航到沙盒 **[!UICONTROL 浏览]** 选项卡，然后选择沙盒名称旁边的加号(+)选项。

![沙箱 **[!UICONTROL 浏览]** 选项卡中突出显示了导入包选择。](../images/ui/sandbox-tooling/browse-sandboxes.png)

使用下拉菜单，选择 **[!UICONTROL 包名称]** 您希望导入到目标沙盒。 添加可选 **[!UICONTROL 作业名称]**，以用于未来监控，然后选择 **[!UICONTROL 下一个]**.

![导入详细信息页面显示 [!UICONTROL 包名称] 下拉菜单选择](../images/ui/sandbox-tooling/import-package-to-sandbox.png)

此 [!UICONTROL 程序包对象和依赖项] 页面提供了此包中包含的所有资源的列表。 系统自动检测成功导入所选父对象所需的从属对象。

![此 [!UICONTROL 程序包对象和依赖项] 页面显示包中包含的资产列表。](../images/ui/sandbox-tooling/package-objects-and-dependencies.png)

>[!NOTE]
>
>依赖对象可以替换为目标沙盒中的现有对象，这允许您重用现有对象，而不是创建新版本。 例如，导入包含架构的包时，您可以在目标沙盒中重用现有的自定义字段组和身份命名空间。 或者，在导入包含历程的包时，您可以重复使用目标沙盒中的现有区段。

要使用现有对象，请选择从属对象旁边的铅笔图标。 此时会显示创建新或使用现有内容的选项。 选择 **[!UICONTROL 使用现有]**.

![此 [!UICONTROL 程序包对象和依赖项] 显示依赖对象选项的页面 [!UICONTROL 新建] 和 [!UICONTROL 使用现有].](../images/ui/sandbox-tooling/use-existing-object.png)

此 **[!UICONTROL 字段组]** 对话框显示对象可用的字段组列表。 选择所需的字段组，然后选择 **[!UICONTROL 保存]**.

![上显示的字段列表 [!UICONTROL 字段组] 对话框，突出显示 [!UICONTROL 保存] 选择。 ](../images/ui/sandbox-tooling/field-group-list.png)

您将返回 [!UICONTROL 程序包对象和依赖项] 页面。 从此处选择 **[!UICONTROL 完成]** 以完成资源包导入。

![此 [!UICONTROL 程序包对象和依赖项] 页面显示包中包含的资产列表，突出显示 [!UICONTROL 完成].](../images/ui/sandbox-tooling/finish-object-dependencies.png)

<!--
## Export and import an entire sandbox 

>[!NOTE]
>
>All export and import actions are recorded in the audit logs.

### Export an entire sandbox {#export-entire-sandbox}

To export an entire sandbox, navigate to the [!UICONTROL Sandboxes] **[!UICONTROL Packages]** tab and select **[!UICONTROL Create package]**.

![The [!UICONTROL Sandboxes] **[!UICONTROL Packages]** tab highlighting [!UICONTROL Create package].](../images/ui/sandbox-tooling/create-sandbox-package.png)

Select **[!UICONTROL Entire sandbox]** for the Type of package in the [!UICONTROL Create package] dialog. Provide a [!UICONTROL Package name] for your package and select the **[!UICONTROL Sandbox]** from the dropdown. Finally, select **[!UICONTROL Create]** to confirm your entries.

![The [!UICONTROL Create package] dialog showing completed fields and highlighting [!UICONTROL Create].](../images/ui/sandbox-tooling/create-package-dialog.png)

The package is created successfully, select **[!UICONTROL Publish]** to publish the package.

![List of sandbox packages highlighting the new published package.](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

You are returned to the **[!UICONTROL Packages]** tab in the [!UICONTROL Sandboxes] environment, where you can see the new published package.

### Import the entire sandbox package {#import-entire-sandbox-package}

To import the package into a target sandbox, navigate to the [!UICONTROL Sandboxes] **[!UICONTROL Browse]** tab and select the plus (+) option beside the sandbox name.

![The sandboxes **[!UICONTROL Browse]** tab highlighting the import package selection.](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

Using the dropdown menu, select the full sandbox using the **[!UICONTROL Package name]** dropdown. Add an optional **[!UICONTROL Job name]**, which will be used for future monitoring, then select **[!UICONTROL Next]**.

![The import details page showing the [!UICONTROL Package name] dropdown selection](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>All objects are created as new from the package when importing an entire sandbox. The objects are not listed in the [!UICONTROL Package object and dependencies] page, as there can be multiples. An inline message is displayed, advising of object types that are not supported.

You are taken to the [!UICONTROL Package object and dependencies] page where you can see the number of objects and dependencies that are imported and excluded objects. From here, select **[!UICONTROL Import]** to complete the package import.

 ![The [!UICONTROL Package object and dependencies] page shows the inline message of object types not supported, highlighting [!UICONTROL Import].](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)
-->

## 监视导入作业并查看导入对象详细信息

要查看导入的对象和导入的详细信息，请导航至 [!UICONTROL 沙盒] **[!UICONTROL 导入]** 选项卡并从列表中选择包。 或者，使用搜索栏搜索包。

![沙箱 [!UICONTROL 导入] 选项卡高亮显示导入资源包选项。](../images/ui/sandbox-tooling/imports-tab.png)

### 查看导入的对象 {#view-imported-objects}

在 **[!UICONTROL 导入]** 选项卡 [!UICONTROL 沙盒] 环境，选择 **[!UICONTROL 查看导入的对象]** 从右侧详细信息窗格中。

选择 **[!UICONTROL 查看导入的对象]** 从右侧详细信息窗格中的 **[!UICONTROL 导入]** 选项卡 [!UICONTROL 沙盒] 环境。

![沙箱 [!UICONTROL 导入] 选项卡高亮显示 [!UICONTROL 查看导入的对象] 在右窗格中选择。](../images/ui/sandbox-tooling/view-imported-objects.png)

使用箭头可展开对象以查看已导入到文件包中的字段的完整列表。

![沙箱 [!UICONTROL 导入的对象] 显示导入到资源包中的对象列表。](../images/ui/sandbox-tooling/expand-imported-objects.png)

### 查看导入详细信息 {#view-import-details}

选择 **[!UICONTROL 查看导入详细信息]** 从右侧详细信息窗格中的 **[!UICONTROL 导入]** 选项卡。

![沙箱 [!UICONTROL 导入] 选项卡高亮显示 [!UICONTROL 查看导入详细信息] 在右窗格中选择。](../images/ui/sandbox-tooling/view-import-details.png)

此 **[!UICONTROL 导入详细信息]** 对话框显示导入的详细细分。

![此 [!UICONTROL 导入详细信息] 显示导入详细划分的对话框。](../images/ui/sandbox-tooling/import-details.png)

>[!NOTE]
>
>导入完成后，您将在Platform UI中收到通知。 您可以通过警报图标访问这些通知。 如果作业不成功，您可以在此处导航到疑难解答。

## 后续步骤

本文档演示了如何在Experience PlatformUI中使用沙盒工具功能。 有关沙箱的信息，请参见 [沙盒用户指南](../ui/user-guide.md).

有关使用沙盒API执行不同操作的步骤，请参阅 [沙盒开发人员指南](../api/getting-started.md). 有关Experience Platform中沙盒的高级概述，请参阅 [概述文档](../home.md).
