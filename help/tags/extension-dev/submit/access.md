---
title: 授予用户访问权限
description: 在Adobe Experience Platform中设置团队成员的标记用户帐户和权限。
exl-id: c7235e50-13b3-4487-b171-873063875621
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 24%

---

# 授予用户访问权限

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

开始使用 extension_package 之前，您需要为团队成员设置用户帐户和权限。此操作可以在 [Adobe Admin Console](https://adminconsole.adobe.com/) 中完成。

本文档提供了通过Admin Console授予对Adobe Experience Platform中标记的访问权限的步骤。

## 先决条件

本指南假定您是 Admin Console 指定的组织管理员。如果您需要有关 Admin Console 和分配角色的更多信息，请参阅以下资源：

* [管理用户指南](https://helpx.adobe.com/cn/enterprise/administering/user-guide.html?topic=/enterprise/administering/morehelp/introduction.ug.js)：有关 Admin Console 中所有内容的信息
* [企业管理角色](https://helpx.adobe.com/cn/enterprise/using/admin-roles.html)：有关不同类型的管理角色的更多信息。对于以下指南，我们假定您是组织管理员。

## 选择您的组织

您的 Adobe Experience Cloud 组织管理员应登录到 [Admin Console](https://adminconsole.adobe.com/)。第一个屏幕是概述。

![“管理控制台概述”选项卡](../images/getting-started/admin-console-overview.png)

您中的某些人可能有权访问多个组织（组织）。 要将标记功能添加到正确的组织，请选择屏幕右上角显示的组织名称。 接下来，从下拉列表中选择要在其中使用标记的组织。

![管理控制台组织选择下拉列表](../images/getting-started/admin-console-choose-org.png)

## 创建产品配置文件

产品配置文件是一个组。 单个权限将会分配给产品配置文件，然后配置文件中的所有用户都会继承这些权限。

选择 **[!UICONTROL 产品]** 链接，以及 **[!UICONTROL Experience Cloud]** 左边。 如果数据收集UI未列出，则客户应联系其客户团队，合作伙伴应发送电子邮件至 <ExchangeTechEC@adobe.com>.

![“管理控制台产品”选项卡](../images/getting-started/admin-console-products-launch.png)

上面的屏幕截图显示了一个示例配置文件，您可能还没有一个。 要创建一个报表包，请选择 **[!UICONTROL 新建用户档案]**. 在 **创建新用户档案** 屏幕，只需添加 **配置文件名称** （例如，数据收集测试），以及 **描述**，然后选择 **[!UICONTROL 保存]**:

![“新建配置文件”显示](../images/getting-started/admin-console-create-a-new-profile.png)

产品用户档案现已添加到组织。 接下来，将用户添加到产品配置文件。

## 将用户分配到产品配置文件

请注意，对于 **授权用户** 和 **管理员**. 选择您创建的产品配置文件的名称（在我们的示例中为数据收集测试）。

![产品配置文件显示](../images/getting-started/admin-console-profiles-add-user.png)

选择 **[!UICONTROL 用户]** 选项卡。 在此，您可以通过电子邮件搜索现有Adobe ID用户，或将新用户添加到此产品配置文件。 选择 **[!UICONTROL 添加用户链接]**.

![产品配置文件用户选项卡](../images/getting-started/admin-console-add-launch-user.png)

在相应的文本字段中输入名称、用户组或电子邮件地址。 建议尽可能包含名字和姓氏。 选择 **[!UICONTROL 保存]** 添加用户。

![将用户添加到“配置文件”显示](../images/getting-started/admin-console-add-user.png)

当您在此产品配置文件中拥有所有所需用户时，我们将为他们添加权限。 选择 **[!UICONTROL 权限]** 选项卡。 在权限屏幕上，您将看到 **[!UICONTROL 属性]**, **[!UICONTROL 公司权限]**&#x200B;和 **[!UICONTROL 资产权限]**. 选择 **[!UICONTROL 编辑]**.

![产品配置文件权限选项卡](../images/getting-started/admin-console-profile-permissions.png)

要创作扩展，您的团队必须至少具有以下权限：

* “管理资产”。
* 资产组中的“管理扩展”、“管理环境”和“开发”。

如果需要，您可以稍后创建权限更受限的其他产品配置文件，但现在只需选择 **[!UICONTROL +添加全部]** 同时用于 **公司权限** 和 **资产权限**. 确保选择 **[!UICONTROL 保存]** 每一个。

![管理资产权限](../images/getting-started/admin-console-add-all-property-rights.png)

![管理公司权限](../images/getting-started/admin-console-add-all-company-rights.png)

到目前为止，我们已选择了相应的组织、创建了产品配置文件、将用户添加到产品配置文件并分配了权限。

这可完成Admin Console中所需的设置。 您和已设置为用户的团队成员现在可以登录到 [数据收集UI](https://launch.adobe.com/).

## 确认配置

在按照如上所述为公司配置了对标记的访问权限并设置了用户后，您应该能够从 [数据收集UI](https://launch.adobe.com/). 如果您已经为标记配置并完成了上述Admin Console步骤，但仍无法登录到数据收集UI，请联系您的Adobe支持代表。
