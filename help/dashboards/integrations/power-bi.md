---
title: 平台功能板的Power BI报表模板
description: 使用报表模板来探索使用Experience Platform的Power BI。
exl-id: fb98a79f-3d82-4e11-b08a-b7cb06414462
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 0%

---

# Power BI功能板报表模板

利用Power BI报表模板功能，可创建填充了Adobe Experience Platform数据的引人入胜的报表。 简化的安装过程会自动安装用于实时客户配置文件、分段和目标的标准小组件。 安装过程还会将Power BI与数据模型相关联，以便您可以轻松自定义和扩展报表模板。 这些报表可以在您的整个组织之间共享，而无需在Platform上为您的IMS组织提供凭据的收件人。

本文档提供了有关如何将Adobe Experience Platform与Power BI应用程序连接以及使用报表模板与外部用户共享关键平台数据分析的说明。

## 快速入门

在继续本教程之前，建议您对 [模式组合](../../xdm/schema/composition.md) Experience Platform中，以及如何通过 [合并模式](../../xdm/schema/composition.md#union).

要安装Power BI应用程序集成，用户必须首先获得以下平台权限：

- 管理查询
- 管理沙箱

要了解如何分配这些权限，请阅读 [访问控制](../../access-control/home.md) 文档。

您还必须拥有Power BI帐户才能阅读本教程。 要创建帐户，请导航到 [Power BI主页](https://powerbi.microsoft.com/en-us/) 跟踪注册流程。 此Power BI帐户的用户还必须启用 **创建工作区** 设置Power BI。 此设置可在Power BI管理门户的租户设置中找到。 如果您的帐户由租户或雇主提供，请联系您各自的管理员以启用此设置。

![Power BI管理门户创建工作区设置。](../images/power-bi/create-workspace-settings.png)

>[!NOTE]
>
>为了在Platform UI的左侧导航中显示功能板选项卡，并且显示功能板清单视图，您必须有权访问作为Platform许可证一部分的任何配置文件、区段或目标功能板。

## 安装Power BI应用程序集成

在平台UI中，选择 **[!UICONTROL 功能板]** 在左侧导航中打开 [!UICONTROL 功能板] 工作区。 的 [!UICONTROL 浏览] 选项卡会显示当前可用的功能板视图列表。 要了解有关查看可用功能板的更多信息，请参阅 [库存文档](../inventory.md).

接下来，选择 **[!UICONTROL 集成]** 选项卡。 此时将显示Power BI应用程序集成页面。 从此处选择 **[!UICONTROL 安装]** 以开始安装。

>[!NOTE]
>
>的 [!UICONTROL 安装] 按钮被禁用，除非您同时具有“查询服务管理”和“管理沙箱”权限。

![Power BI详细信息屏幕中突出显示了安装按钮。](../images/power-bi/details-screen.png)

### 提供凭据

安装过程的第一步是为Power BI应用程序集成提供未过期的凭据。 有两个选项可用于提供以下功能： [[!UICONTROL 创建新凭据]](#create-new-credentials) 或 [[!UICONTROL 使用现有凭据]](#use-existing-credentials). 选择相应的切换开关以继续。

#### 创建新凭据 {#create-new-credentials}

生成新凭据时有两个必填字段： [!UICONTROL 名称] 和 [!UICONTROL 已分配给]. 的 [!UICONTROL 已分配给] 字段与与您的Power BI帐户关联的电子邮件地址相关联。

![Power BI生成新凭据屏幕。](../images/power-bi/generate-new-credentials.png)

>[!IMPORTANT]
>
>创建未过期的凭据需要您分配特定权限和角色。 必需的权限包括管理沙箱和管理查询服务集成。 所需的角色包括Adobe Experience Platform管理员和开发人员角色。 要了解如何分配这些权限，请阅读 [访问控制](../../access-control/home.md) 文档。

要了解有关生成未过期的查询服务凭据的更多信息，请参阅 [未过期的凭据指南](../../query-service/ui/credentials.md#non-expiring-credentials).

首次生成未过期的凭据后，会将一个JSON文件下载到该计算机。 然后，可以将此JSON文件作为凭据与其他用户共享，以完成安装过程。

#### 使用现有凭据 {#use-existing-credentials}

还可以上传JSON凭据文件以通过验证。 这些包含未过期凭据值的JSON文件将下载到创建未过期凭据时所使用的本地计算机。

>[!IMPORTANT]
>
>要使用现有的未过期凭据，必须已为用户分配了凭据。 如果用户未分配凭据，并且无法使用Adobe Admin Console创建新凭据，则用户将无法继续安装过程。

选择 **[!UICONTROL 上载凭据文件]**，然后在显示的对话框中选择要上传的相应JSON文件。

![Power BI凭据屏幕中，“上传凭据文件”按钮突出显示。](../images/power-bi/upload-credential-file.png)

在您提供未过期的凭据后，Platform会自动验证这些凭据。 验证成功后，将显示确认消息。 选择 **[!UICONTROL 下一个]** 查看Power BI应用程序的同意协议。

![未过期的凭据已成功验证屏幕，且“Next（下一步）”按钮已高亮显示。](../images/power-bi/successfully-uploaded-credential-file.png)

### 提供同意

将显示同意显示。 选择 **[!UICONTROL 审核同意]** 打开一个新窗口，详细介绍根据Power BI的服务条款和隐私声明访问和使用数据所需的权限。

![提供同意显示时，会突出显示“审阅同意”按钮。](../images/power-bi/provide-consent-display.png)

选择 **[!UICONTROL 接受]** 授予Power BI访问和使用Platform数据的权限。

![Power BI应用程序的权限请求。](../images/power-bi/permissions.png)

>[!NOTE]
>
>如果您在征得同意之前随时退出安装过程，则Power BI应用程序集成将不会安装到功能板清单中。

获得同意后，报告模板将作为安装过程的一部分自动安装在Power BI环境中。 然后，Power BI使用未过期的凭据访问Platform，按顺序执行所有SQL查询，并使用返回的数据填充报表模板。

选择 **[!UICONTROL 完成]** 返回到功能板库。

![提供同意显示，并突出显示“完成”按钮。](../images/power-bi/finish-consent-review.png)

安装Power BI报表模板后，该模板会显示在 [!UICONTROL 浏览] 选项卡。 选择 **[!UICONTROL Power BI]** 从列表中导航到Power BI环境。

![功能板清单中列出的Power BI。](../images/power-bi/power-bi-dashboard-inventory.png)

>[!IMPORTANT]
>
>Power BI管理员需要确保用户具有相应的访问权限，才能在Power BI环境中查看这些功能板。

## Power BI工作区

登录后 [Power BI工作区](https://dxt.powerbi.com)，则报表模板可用于您有权访问的每项服务。 报表模板包括用户档案、区段和目标功能板 **仅** 是否具有相应的查看权限。

默认情况下，用户档案、区段和目标中的标准小组件在Power BI模板报表中可用。

>[!NOTE]
>
>您必须为给定的功能板启用编辑权限，才能在Power BI环境中安装该功能板。

![Power BI配置文件模板报表。](../images/power-bi/profile-report-template.png)

在Power BI中安装功能板后，默认情况下会向所有用户显示报表模板。 如果要限制对任何报表模板的访问，请确保从Power BI环境中禁用有关用户的访问权限。

## 自定义Power BI报表模板

通过使用自定义小组件，您可以向数据模型添加自定义属性，以扩充由Power BI提供的报表模板。

>[!NOTE]
>
>可用于自定义小组件的属性取决于并集架构中的可用内容。 要了解如何查看和探索联合模式以使自定义小组件受益，请参阅 [并集架构UI指南](../../profile/ui/union-schema.md).

### 创建自定义小组件

自定义小组件通过小组件库创建。 请参阅 [小组件库概述](../customize/widget-library.md) 有关功能和 [创建自定义小组件的教程](../customize/custom-widgets.md) 以了解具体说明。

>[!IMPORTANT]
>
>新创建的自定义小组件包括 **not** 在Adobe Experience Platform功能板和Power BI报表模板之间自动同步。 必须在Platform UI中手动重新创建在该环境中创建的任何自定义小组件。

### 在Power BI环境中重新创建自定义小组件

当您的功能板具有自定义小组件中包含的相应量度和属性后，您便可以修改从Power BI环境中显示的报表模板。 请参阅 [Power BI文档](https://docs.microsoft.com/zh-cn/power-bi/) 有关如何通过其用户界面编辑报表的信息。

## 删除Power BI应用程序集成

要删除功能板，请导航到功能板库，然后选择删除图标(![](../images/power-bi/delete-icon.png))。

>[!NOTE]
>
>只有安装了Power BI功能板的用户才能从Platform UI中删除集成。

![功能板清单屏幕浏览选项卡显示了“浏览”按钮，并突出显示了“删除”图标。](../images/power-bi/delete-power-bi-dashboard.png)

此时会出现确认弹出窗口。 选择 **[!UICONTROL 删除]** 以确认该过程。

>[!IMPORTANT]
>
>从Platform UI中删除Power BI功能板时，会执行以下操作 **not** 删除Power BI环境中可用的报表模板。 如果要完全删除Power BI报表模板中保留的信息，您需要登录Power BI帐户并从该环境中删除报表模板。 删除后，用户可以按照与上面所述相同的安装说明重新安装Power BI仪表板。

## 后续步骤

通过阅读本文档，您可以更好地了解如何将Power BI报表模板集成到Platform中，以从用户档案、区段或目标功能板共享引人入胜的数据分析。 请参阅 [功能板自定义概述](../customize/overview.md) 以了解有关自定义功能板的更多信息。
