---
title: Platform功能板的Power BI报表模板
description: 使用报表模板以使用Power BI浏览Experience Platform数据。
exl-id: fb98a79f-3d82-4e11-b08a-b7cb06414462
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 0%

---

# 功能板的Power BI报表模板

利用Power BI报表模板功能，可创建填充了来自Adobe Experience Platform的数据的引人注目的报表。 简化的安装过程会自动安装用于Real-time Customer Profile、细分和目标的标准构件。 该安装还会将Power BI连接到数据模型，以便您轻松自定义和扩展报表模板。 这些报告可以在整个组织内共享，而无需收件人在Platform上获取贵组织的凭据。

本文档提供了有关如何将Adobe Experience Platform与Power BI应用程序连接并使用报表模板与外部用户共享关键Platform数据见解的说明。

## 快速入门

在继续本教程之前，建议先充分了解 [模式组合](../../xdm/schema/composition.md) Experience Platform中，以及属性如何通过 [合并模式](../../xdm/schema/composition.md#union).

要安装Power BI应用程序集成，用户必须首先获得以下Platform权限：

- 管理查询
- 管理沙盒

要了解如何分配这些权限，请阅读 [访问控制](../../access-control/home.md) 文档。

此外，您还必须拥有Power BI帐户才能参加本教程。 要创建帐户，请导航到 [Power BI主页](https://powerbi.microsoft.com/en-us/) 并遵循注册流程。 此Power BI帐户的用户还必须启用 **创建工作区** 的Power BI设置中的设置。 此设置可在Power BI管理门户的租户设置中找到。 如果您的帐户由租户或雇主提供，请联系各自的管理员以启用此设置。

![Power BI管理门户创建工作区设置。](../images/power-bi/create-workspace-settings.png)

>[!NOTE]
>
>为了使“功能板”选项卡显示在Platform UI的左侧导航区域中，并使“功能板库存”视图可见，您必须有权访问作为平台许可证一部分的配置文件、区段或目标功能板中的任意一个。

## 安装Power BI应用程序集成

在Platform UI中，选择 **[!UICONTROL 仪表板]** 在左侧导航中打开 [!UICONTROL 仪表板] 工作区。 此 [!UICONTROL 浏览] 选项卡显示当前可用的仪表板视图的列表。 要了解有关查看可用功能板的更多信息，请参阅 [清单文档](../inventory.md).

接下来，选择 **[!UICONTROL 集成]** 选项卡。 此时将显示“Power BI应用程序集成”页。 从此处选择 **[!UICONTROL 安装]** 以开始安装。

>[!NOTE]
>
>此 [!UICONTROL 安装] 除非您同时具有“查询服务管理”和“管理沙盒”权限，否则按钮被禁用。

![Power BI详细信息屏幕，其中高亮显示“安装”按钮。](../images/power-bi/details-screen.png)

### 提供凭据

安装过程中的第一步是为Power BI应用程序集成提供不会过期的凭据。 有两个选项可用于提供这些内容： [[!UICONTROL 创建新凭据]](#create-new-credentials) 或 [[!UICONTROL 使用现有凭据]](#use-existing-credentials). 选择相应的切换以继续。

#### 创建新凭据 {#create-new-credentials}

生成新凭据时，有两个必填字段： [!UICONTROL 名称] 和 [!UICONTROL 分配给]. 此 [!UICONTROL 分配给] 字段与与您的Power BI帐户关联的电子邮件地址相关。

![Power BI生成新凭据屏幕。](../images/power-bi/generate-new-credentials.png)

>[!IMPORTANT]
>
>创建不会过期的凭据需要您分配特定的权限和角色。 必要的权限是管理沙盒和管理查询服务集成。 所需的角色是Adobe Experience Platform管理员和开发人员角色。 要了解如何分配这些权限，请阅读 [访问控制](../../access-control/home.md) 文档。

要了解有关生成不会过期的查询服务凭据的更多信息，请参阅 [未过期的凭据指南](../../query-service/ui/credentials.md#non-expiring-credentials).

在首次生成不会过期的凭据后，会将JSON文件下载到该计算机。 然后，可以将此JSON文件作为凭据与其他用户共享，以完成安装过程。

#### 使用现有凭据 {#use-existing-credentials}

也可以上传JSON凭据文件以通过验证。 创建未过期的凭据时，会将包含未过期的凭据值的这些JSON文件下载到正在使用的本地计算机。

>[!IMPORTANT]
>
>要使用现有的不会过期的凭据，必须已经为用户分配了凭据。 如果用户没有分配凭据，并且无法使用Adobe Admin Console创建新凭据，则用户无法继续安装过程。

选择 **[!UICONTROL 上载凭据文件]**，然后在显示的对话框中选择要上传的相应JSON文件。

![突出显示“上传凭据文件”按钮的“Power BI凭据”屏幕。](../images/power-bi/upload-credential-file.png)

在您提供不会过期的凭据后，这些凭据将由Platform自动验证。 一旦验证成功，将显示确认消息。 选择 **[!UICONTROL 下一个]** 查看Power BI应用程序的同意协议。

![“未过期的凭据”屏幕已成功验证，并突出显示了“下一步”按钮。](../images/power-bi/successfully-uploaded-credential-file.png)

### 提供同意

将显示同意显示。 选择 **[!UICONTROL 审查同意]** 打开一个新窗口，其中详述Power BI根据其服务条款和隐私声明访问和使用您的数据所需的权限。

![提供同意显示，并突出显示审核同意按钮。](../images/power-bi/provide-consent-display.png)

选择 **[!UICONTROL 接受]** 以授予Power BI访问和使用您的Platform数据的权限。

![Power BI应用程序的权限请求。](../images/power-bi/permissions.png)

>[!NOTE]
>
>如果您在同意之前在任何时候退出安装过程，则Power BI应用程序集成将不会安装到功能板清单中。

在征得同意后，会作为安装过程的一部分，自动在Power BI环境中安装报表模板。 然后，Power BI使用未过期的凭据访问Platform，按顺序执行所有SQL查询，并使用返回的数据填充报表模板。

选择 **[!UICONTROL 完成]** 以返回到功能板库存。

![“提供同意”显示时，会高亮显示“完成”按钮。](../images/power-bi/finish-consent-review.png)

现在，Power BI报告模板已安装，并显示在下的可用功能板列表中 [!UICONTROL 浏览] 选项卡。 选择 **[!UICONTROL Power BI]** 从列表中导航到Power BI环境。

![在功能板清单中列出的Power BI。](../images/power-bi/power-bi-dashboard-inventory.png)

>[!IMPORTANT]
>
>Power BI管理员需要确保用户具有相应的访问权限，才能在Power BI环境中查看这些功能板。

## Power BI工作区

登录后 [Power BI工作区](https://dxt.powerbi.com)，报表模板可用于您有权访问的每个服务。 报表模板包括用户档案、区段和目标功能板 **仅限** 是否具有相应的查看权限。

默认情况下，Power BI模板报表中提供了来自配置文件、区段和目标的标准构件。

>[!NOTE]
>
>您必须为给定功能板启用编辑权限，才能允许在Power BI环境中安装该功能板。

![使用标准Platform配置文件小组件的“Power BI配置文件模板”报表。](../images/power-bi/profile-report-template.png)

在Power BI中安装功能板后，默认情况下会向所有用户显示报表模板。 如果要限制对任何报告模板的访问，请确保禁用相关Power BI在模板环境中的访问权限。

## 自定义Power BI报表模板

通过使用自定义小组件，您可以将自定义属性添加到数据模型，以丰富Power BI提供的报表模板。

>[!NOTE]
>
>可用于自定义小部件的属性取决于合并架构中可用的属性。 要了解如何查看和探索合并架构以使您的自定义构件受益，请参阅 [合并架构UI指南](../../profile/ui/union-schema.md).

### 创建自定义构件

自定义构件通过构件库创建。 请参阅 [构件库概述](../customize/widget-library.md) 介绍该功能和 [有关创建自定义小部件的教程](../customize/custom-widgets.md) 以获取特定说明。

>[!IMPORTANT]
>
>新创建的自定义构件包括 **非** 在Adobe Experience Platform功能板和Power BI报表模板之间自动同步。 在Platform UI中创建的任何自定义构件都必须在Power BI环境中手动重新创建。

### 在Power BI环境中重新创建自定义构件

一旦您的功能板具有自定义小组件中包含的相应量度和属性，您便可以修改在Power BI环境中显示的报表模板。 请参阅 [Power BI文档](https://docs.microsoft.com/zh-cn/power-bi/) 有关如何通过用户界面编辑报告的信息。

## 删除Power BI应用程序集成

要删除功能板，请导航到功能板清单并选择删除图标(![](../images/power-bi/delete-icon.png))。

>[!NOTE]
>
>只有安装Power BI功能板的用户才能从Platform UI中删除集成。

![仪表板清单屏幕浏览选项卡显示，浏览按钮和删除图标突出显示。](../images/power-bi/delete-power-bi-dashboard.png)

将出现确认弹出窗口。 选择 **[!UICONTROL 删除]** 以确认流程。

>[!IMPORTANT]
>
>从Platform UI中删除Power BI仪表板会 **非** 删除Power BI环境中可用的报表模板。 如果要完全删除Power BI报表模板中保存的信息，您需要登录您的Power BI帐户，并从该环境中删除报表模板。 删除后，用户可以按照上述安装说明重新安装Power BI仪表板。

## 后续步骤

通过阅读本文档，您可以更好地了解Power BI报表模板如何集成到Platform中，以共享来自配置文件、区段或目标功能板的引人注目的数据洞察。 请参阅 [仪表板自定义概述](../customize/overview.md) 了解有关自定义功能板的更多信息。
