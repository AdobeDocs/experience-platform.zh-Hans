---
keywords: Experience Platform；主页；热门主题；访问控制；基于属性的访问控制；ABAC
title: 基于属性的访问控制创建策略
description: 本文档提供了有关Adobe Experience Platform中基于属性的访问控制的信息
hide: true
hidefromtoc: true
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 19f1e8df8cd8b55ed6b03f80e42810aefd211474
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# 管理策略

>[!IMPORTANT]
>
>目前，基于属性的访问控制在面向美国医疗保健客户的有限版本中提供。 此功能在完全发布后将可供所有Real-time Customer Data Platform客户使用。

政策是将属性集合在一起以确立允许和不允许的行动的声明。 策略可以是本地策略，也可以是全局策略，并且可以覆盖其他策略。

## 创建新策略

要创建新策略，请选择 **[!UICONTROL 策略]** ，然后选择 **[!UICONTROL 创建策略]**.

![flac-new-policy](../../images/flac-ui/flac-new-policy.png)

的 **[!UICONTROL 创建新策略]** 对话框，提示您输入名称和可选描述。 完成后，选择 **[!UICONTROL 确认]**.

![flac-create-new-policy](../../images/flac-ui/flac-create-new-policy.png)

使用下拉箭头选择是否要 **允许访问** (![flac-permit-access-to](../../images/flac-ui/flac-permit-access-to.png))资源或 **拒绝访问** (![flac-deny-access-to](../../images/flac-ui/flac-deny-access-to.png))资源。

接下来，使用下拉菜单和搜索访问类型（读取或写入）选择要包含在策略中的资源。

![flac-flac-policy-resource-dropdon](../../images/flac-ui/flac-policy-resource-dropdown.png)

接下来，使用下拉箭头选择要应用于此策略的条件， **以下是true** (![flac-policy-true](../../images/flac-ui/flac-policy-true.png))或 **以下内容为false** (![flac-policy-false](../../images/flac-ui/flac-policy-false.png))。

选择加号图标以 **添加匹配表达式** 或 **添加表达式组** 的值。

![flac-policy-expression](../../images/flac-ui/flac-policy-expression.png)

使用下拉菜单，选择 **资源**.

![flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown.png)

接下来，使用下拉菜单选择 **匹配**.

![flac-policy-matches-dropdown](../../images/flac-ui/flac-policy-matches-dropdown.png)

接下来，使用下拉菜单，选择 **用户**.

![flac-policy-user-dopdown](../../images/flac-ui/flac-policy-user-dropdown.png)

最后，选择 **沙盒** 您希望策略条件应用到的规则集。

![flac-policy-sandboxes-dropdown](../../images/flac-ui/flac-policy-sandboxes-dropdown.png)

选择 **添加资源** 添加更多资源。 完成后，选择 **[!UICONTROL 保存并退出]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

新策略已成功创建，您将被重定向到 **[!UICONTROL 策略]** 选项卡中，您将看到新创建的策略显示在列表中。

![flac-policy-saved](../../images/flac-ui/flac-policy-saved.png)

## 编辑策略

要编辑现有策略，请从 **[!UICONTROL 策略]** 选项卡。 或者，使用筛选器选项筛选结果以查找要编辑的策略。

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

接下来，选择省略号(`…`)，并且下拉列表会显示用于编辑、停用、删除或复制角色的控件。 从下拉菜单中选择编辑。

![flac-policy-edit](../../images/flac-ui/flac-policy-edit.png)

将显示策略权限屏幕。 进行更新，然后选择 **[!UICONTROL 保存并退出]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

策略已成功更新，您将被重定向到 **[!UICONTROL 策略]** 选项卡。

## 复制策略

要复制现有策略，请从 **[!UICONTROL 策略]** 选项卡。 或者，使用筛选器选项筛选结果以查找要编辑的策略。

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

接下来，选择省略号(`…`)，并且下拉列表会显示用于编辑、停用、删除或复制角色的控件。 从下拉菜单中选择“复制”。

![flac-policy-duplicate](../../images/flac-ui/flac-policy-duplicate.png)

的 **[!UICONTROL 复制策略]** 对话框，提示您确认复制。

![flac-policy-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

新策略将作为原始策略的副本显示在 **[!UICONTROL 策略]** 选项卡。

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## 删除策略

要删除现有策略，请从 **[!UICONTROL 策略]** 选项卡。 或者，使用筛选器选项筛选结果以查找要删除的策略。

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

接下来，选择省略号(`…`)，并且下拉列表会显示用于编辑、停用、删除或复制角色的控件。 从下拉菜单中选择删除。

![flac-policy-delete](../../images/flac-ui/flac-policy-delete.png)

的 **[!UICONTROL 删除用户策略]** 对话框，提示您确认删除。

![flac-policy-delete-confirm](../../images/flac-ui/flac-policy-delete-confirm.png)

您将返回到 **[!UICONTROL 策略]** ，此时会出现确认删除弹出窗口。

![flac-policy-delete-confirmation](../../images/flac-ui/flac-policy-delete-confirmation.png)

## 激活策略

要激活现有策略，请从 **[!UICONTROL 策略]** 选项卡。 或者，使用筛选器选项筛选结果以查找要删除的策略。

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

接下来，选择省略号(`…`)，并且下拉列表会显示用于编辑、激活、删除或复制角色的控件。 从下拉菜单中选择激活。

![flac-policy-activate](../../images/flac-ui/flac-policy-delete.png)

的 **[!UICONTROL 激活用户策略]** 对话框，提示您确认激活。

![flac-policy-activate-confirm](../../images/flac-ui/flac-policy-activate-confirm.png)

您将返回到 **[!UICONTROL 策略]** 选项卡，此时会显示激活确认弹出窗口。 策略状态显示为活动状态。

![flac-policy-activated](../../images/flac-ui/flac-policy-activated.png)

## 后续步骤

创建新策略后，您可以继续执行 [管理角色的权限](permissions.md).
