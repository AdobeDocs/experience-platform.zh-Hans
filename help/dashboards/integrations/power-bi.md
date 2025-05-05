---
title: 适用于Experience Platform功能板的Power BI报表模板
description: 使用报表模板，通过Power BI浏览Experience Platform数据。
exl-id: fb98a79f-3d82-4e11-b08a-b7cb06414462
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 0%

---

# 用于功能板的Power BI报表模板

Power BI报表模板功能允许您从Adobe Experience Platform创建填充了数据的引人注目的报表。 简化的安装过程会自动安装用于Real-time Customer Profile、细分和目标的标准构件。 该安装还将Power BI连接到您的数据模型，以便您轻松自定义和扩展报表模板。 这些报告可以在整个组织内共享，并且收件人不需要Experience Platform上贵组织的凭据。

本文档提供了有关如何将Adobe Experience Platform与Power BI应用程序连接并使用报表模板与外部用户共享关键Experience Platform数据见解的说明。

## 快速入门

在继续本教程之前，建议很好地了解Experience Platform中的[架构组合](../../xdm/schema/composition.md)，以及如何通过[合并架构](../../xdm/schema/composition.md#union)将属性包含在实时客户配置文件中。

要安装Power BI应用程序集成，用户必须首先获得以下Experience Platform权限：

- 管理查询
- 管理沙盒

要了解如何分配这些权限，请阅读[访问控制](../../access-control/home.md)文档。

此外，您还必须拥有Power BI帐户才能学习本教程。 要创建帐户，请导航到[Power BI主页](https://powerbi.microsoft.com/en-us/)，然后按照注册过程操作。 此Power BI帐户的用户还必须在其Power BI设置中启用&#x200B;**创建工作区**&#x200B;设置。 此设置可在Power BI管理门户的租户设置中找到。 如果您的帐户由租户或雇主提供，请联系各自的管理员以启用此设置。

![Power BI管理门户创建工作区设置。](../images/power-bi/create-workspace-settings.png)

>[!NOTE]
>
>为了使“功能板”选项卡显示在Experience Platform UI的左侧导航中，并且“功能板库存”视图可见，您必须有权访问作为Experience Platform许可证一部分的配置文件、区段或目标功能板中的任意一个。

## 安装Power BI应用程序集成

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 功能板]**&#x200B;以打开[!UICONTROL 功能板]工作区。 [!UICONTROL 浏览]选项卡显示当前可用的仪表板视图列表。 要了解有关查看可用功能板的详细信息，请参阅[清单文档](../inventory.md)。

接下来，选择&#x200B;**[!UICONTROL 集成]**&#x200B;选项卡。 此时将显示Power BI应用程序集成页面。 从此处选择&#x200B;**[!UICONTROL 安装]**&#x200B;开始安装。

>[!NOTE]
>
>[!UICONTROL 安装]按钮已禁用，除非您同时具有“查询服务管理”和“管理沙盒”权限。

![Power BI详细信息屏幕中突出显示“安装”按钮。](../images/power-bi/details-screen.png)

### 提供凭据

安装过程中的第一步是为Power BI应用程序集成提供不会过期的凭据。 有两个选项可供提供： [[!UICONTROL 创建新凭据]](#create-new-credentials)或[[!UICONTROL 使用现有凭据]](#use-existing-credentials)。 选择相应的切换以继续。

#### 新建凭据 {#create-new-credentials}

生成新凭据时有两个必填字段：[!UICONTROL 名称]和[!UICONTROL 分配给]。 [!UICONTROL 分配给]字段与您的Power BI帐户关联的电子邮件地址相关。

![Power BI生成新凭据屏幕。](../images/power-bi/generate-new-credentials.png)

>[!IMPORTANT]
>
>创建不会过期的凭据需要您分配特定的权限和角色。 必要的权限是管理沙盒和管理查询服务集成。 所需的角色是Adobe Experience Platform管理员和开发人员角色。 要了解如何分配这些权限，请阅读[访问控制](../../access-control/home.md)文档。

若要了解有关生成不会过期的查询服务凭据的更多信息，请参阅[不会过期的凭据指南](../../query-service/ui/credentials.md#non-expiring-credentials)。

在首次生成不会过期的凭据后，会将JSON文件下载到该计算机。 然后，可以将此JSON文件作为凭据与其他用户共享，以完成安装过程。

#### 使用现有凭据 {#use-existing-credentials}

也可以上传JSON凭据文件以通过验证。 创建未过期的凭据时，会将包含未过期的凭据值的这些JSON文件下载到正在使用的本地计算机。

>[!IMPORTANT]
>
>要使用现有的未过期的凭据，必须已为该用户分配了凭据。 如果用户未分配凭据，并且无法使用Adobe Admin Console创建新凭据，则用户无法继续安装过程。

选择&#x200B;**[!UICONTROL 上载凭据文件]**，然后在显示的对话框中选择要上载的相应JSON文件。

![Power BI凭据屏幕突出显示“上载凭据文件”按钮。](../images/power-bi/upload-credential-file.png)

在您提供不会过期的凭据后，Experience Platform会自动验证这些凭据。 一旦验证成功，将显示一条确认消息。 选择&#x200B;**[!UICONTROL 下一步]**&#x200B;查看Power BI应用程序的同意协议。

![已成功验证未过期的凭据，并突出显示了“下一步”按钮。](../images/power-bi/successfully-uploaded-credential-file.png)

### 提供同意

此时会显示同意显示。 选择&#x200B;**[!UICONTROL 查看同意]**&#x200B;以打开一个新窗口，详述Power BI根据其服务条款和隐私声明访问和使用您的数据所需的权限。

![显示了“提供同意”并突出显示了“审核同意”按钮。](../images/power-bi/provide-consent-display.png)

选择&#x200B;**[!UICONTROL 接受]**&#x200B;以授予Power BI访问和使用您的Experience Platform数据的权限。

Power BI应用程序的![权限请求。](../images/power-bi/permissions.png)

>[!NOTE]
>
>如果您在同意之前在任何时候退出安装过程，Power BI应用程序集成将不会安装到功能板清单中。

在同意之后，作为安装过程的一部分，报表模板会自动安装在Power BI环境中。 然后，Power BI会使用不会过期的凭据访问Experience Platform，依次执行所有SQL查询，并使用返回的数据填充报表模板。

选择&#x200B;**[!UICONTROL 完成]**&#x200B;以返回到仪表板清单。

![显示“提供同意”并突出显示“完成”按钮。](../images/power-bi/finish-consent-review.png)

现在已安装Power BI报告模板，它出现在[!UICONTROL 浏览]选项卡下的可用功能板列表中。 从列表中选择&#x200B;**[!UICONTROL Power BI]**&#x200B;以导航到Power BI环境。

![Power BI在功能板清单中列出。](../images/power-bi/power-bi-dashboard-inventory.png)

>[!IMPORTANT]
>
>Power BI管理员需要确保用户具有相应的访问权限，才能在Power BI环境中查看这些功能板。

## Power BI工作区

登录[Power BI工作区](https://dxt.powerbi.com)后，报表模板可用于您有权访问的每个服务。 报表模板仅包含用户档案、区段和目标功能板&#x200B;**&#x200B;**（如果他们具有相应的查看权限）。

默认情况下，Power BI模板报表中提供了来自配置文件、区段和目标的标准构件。

>[!NOTE]
>
>您必须为给定功能板启用编辑权限，才能允许在Power BI环境中安装该功能板。

![使用标准Power BI配置文件小组件的Experience Platform配置文件模板报告。](../images/power-bi/profile-report-template.png)

在Power BI中安装功能板后，默认情况下会向所有用户显示报表模板。 如果要限制对任何报表模板的访问，请确保从Power BI环境中禁用相关用户的访问权限。

## 自定义Power BI报表模板

通过使用自定义构件，您可以将自定义属性添加到数据模型，以丰富Power BI提供的报表模板。

>[!NOTE]
>
>可用于自定义构件的属性取决于合并架构中可用的属性。 要了解如何查看和探索合并架构以受益于您的自定义小组件，请参阅[合并架构UI指南](../../profile/ui/union-schema.md)。

### 创建自定义构件

自定义构件通过构件库创建。 有关该功能的介绍，请参阅[构件库概述](../customize/widget-library.md)；有关具体说明，请参阅[有关创建自定义构件的教程](../customize/custom-widgets.md)。

>[!IMPORTANT]
>
>新创建的自定义小组件在Adobe Experience Platform功能板和Power BI报表模板之间&#x200B;**不**&#x200B;自动同步。 在Experience Platform UI中创建的任何自定义构件都必须在Power BI环境中手动重新创建。

### 在Power BI环境中重新创建自定义构件

一旦您的功能板具有自定义小组件中包含的相应量度和属性，您就可以随时从Power BI环境中修改显示的报表模板了。 有关如何通过用户界面编辑报告的信息，请参阅[Power BI文档](https://docs.microsoft.com/en-us/power-bi/)。

## 删除Power BI应用程序集成

要删除仪表板，请导航到仪表板清单，然后选择仪表板名称旁边的删除图标（![删除图标](/help/images/icons/delete.png)）。

>[!NOTE]
>
>只有安装Power BI功能板的用户才能从Experience Platform UI中删除集成。

![仪表板清单屏幕浏览选项卡显示，浏览按钮和删除图标突出显示。](../images/power-bi/delete-power-bi-dashboard.png)

此时将显示确认弹出框。 选择&#x200B;**[!UICONTROL 删除]**&#x200B;以确认该进程。

>[!IMPORTANT]
>
>从Experience Platform UI中删除Power BI功能板&#x200B;**不会**&#x200B;删除Power BI环境中可用的报表模板。 如果要完全删除Power BI报表模板中包含的信息，您需要登录Power BI帐户，并从该环境中删除报表模板。 删除后，用户可以按照上述相同的安装说明重新安装Power BI功能板。

## 后续步骤

通过阅读本文档，您可以更好地了解Power BI报表模板如何集成到Experience Platform中，以便从配置文件、区段或目标功能板共享引人注目的数据洞察。 请参阅[仪表板自定义概述](../customize/overview.md)，了解有关自定义仪表板的更多信息。
