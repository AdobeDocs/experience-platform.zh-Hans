---
keywords: Experience Platform；主页；热门主题；访问控制；基于属性的访问控制；ABAC
title: 管理访问控制策略
description: 本文档提供了有关通过Adobe Experience Cloud中的“权限”界面管理访问控制策略的信息。
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 7cafe1f7e9dd6789db4199631cb605be666ce48a
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 0%

---

# 管理访问控制策略

访问控制策略是将属性集合在一起以建立允许和不允许的操作的语句。 访问策略可以是本地策略或全局策略，也可以覆盖其他策略。 Adobe提供了一个默认策略，可立即激活该策略，或者在您的组织准备好开始根据标签控制对特定对象的访问时激活该策略。 默认策略利用应用于资源的标签来拒绝访问，除非用户处于具有匹配标签的角色中。

>[!IMPORTANT]
>
>不要将访问策略与数据使用策略混淆，数据使用策略控制数据在Adobe Experience Platform中的使用方式，而不是贵组织中的哪些用户有权访问数据。 请参阅有关创建的指南 [数据使用策略](../../../data-governance/policies/create.md) 以了解更多信息。

<!-- ## Create a new policy

To create a new policy, select the **[!UICONTROL Policies]** tab in the sidebar and select **[!UICONTROL Create Policy]**.

![flac-new-policy](../../images/flac-ui/flac-new-policy.png)

The **[!UICONTROL Create a new policy]** dialog appears, prompting you to enter a name, and an optional description. When finished, select **[!UICONTROL Confirm]**.

![flac-create-new-policy](../../images/flac-ui/flac-create-new-policy.png)

Using the dropdown arrow select if you would like to **Permit access to** (![flac-permit-access-to](../../images/flac-ui/flac-permit-access-to.png)) a resource or **Deny access to** (![flac-deny-access-to](../../images/flac-ui/flac-deny-access-to.png)) a resource.

Next, select the resource that you would like to include in the policy using the dropdown menu and search access type, read or write.

![flac-flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown.png)

Next, using the dropdown arrow select the condition you would like to apply to this policy, **The following being true** (![flac-policy-true](../../images/flac-ui/flac-policy-true.png)) or **The following being false** (![flac-policy-false](../../images/flac-ui/flac-policy-false.png)).

Select the plus icon to **Add matches expression** or **Add expression group** for the resource. 

![flac-policy-expression](../../images/flac-ui/flac-policy-expression.png)

Using the dropdown, select the **Resource**.

![flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown-1.png)

Next, using the dropdown select the **Matches**.

![flac-policy-matches-dropdown](../../images/flac-ui/flac-policy-matches-dropdown.png)

Next, using the dropdown, select the type of label (**[!UICONTROL Core label]** or **[!UICONTROL Custom label]**) to match the label assigned to the User in roles.

![flac-policy-user-dropdown](../../images/flac-ui/flac-policy-user-dropdown.png)

Finally, select the **Sandbox** that you would like the policy conditions to apply to, using the dropdown menu.

![flac-policy-sandboxes-dropdown](../../images/flac-ui/flac-policy-sandboxes-dropdown.png)

Select **Add resource** to add more resources. Once finished, select **[!UICONTROL Save and exit]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

The new policy is successfully created, and you are redirected to the **[!UICONTROL Policies]** tab, where you will see the newly created policy appear in the list. 

![flac-policy-saved](../../images/flac-ui/flac-policy-saved.png)

## Edit a policy

To edit an existing policy, select the policy from the **[!UICONTROL Policies]** tab. Alternatively, use the filter option to filter the results to find the policy you want to edit.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Next, select the ellipsis (`…`) next to the policies name, and a dropdown displays controls to edit, deactivate, delete, or duplicate the role. Select edit from the dropdown.

![flac-policy-edit](../../images/flac-ui/flac-policy-edit.png)

The policy permissions screen appears. Make the updates then select **[!UICONTROL Save and exit]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

The policy is successfully updated, and you are redirected to the **[!UICONTROL Policies]** tab.

## Duplicate a policy

To duplicate an existing policy, select the policy from the **[!UICONTROL Policies]** tab. Alternatively, use the filter option to filter the results to find the policy you want to edit.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Next, select the ellipsis (`…`) next to a policies name, and a dropdown displays controls to edit, deactivate, delete, or duplicate the role. Select duplicate from the dropdown.

![flac-policy-duplicate](../../images/flac-ui/flac-policy-duplicate.png)

The **[!UICONTROL Duplicate policy]** dialog appears, prompting you to confirm the duplication. 

![flac-policy-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

The new policy appears in the list as a copy of the original on the **[!UICONTROL Policies]** tab.

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Delete a policy

To delete an existing policy, select the policy from the **[!UICONTROL Policies]** tab. Alternatively, use the filter option to filter the results to find the policy you want to delete.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Next, select the ellipsis (`…`) next to a policies name, and a dropdown displays controls to edit, deactivate, delete, or duplicate the role. Select delete from the dropdown.

![flac-policy-delete](../../images/flac-ui/flac-policy-delete.png)

The **[!UICONTROL Delete user policy]** dialog appears, prompting you to confirm the deletion. 

![flac-policy-delete-confirm](../../images/flac-ui/flac-policy-delete-confirm.png)

You are returned to the **[!UICONTROL policies]** tab and a confirmation of deletion pop over appears.

![flac-policy-delete-confirmation](../../images/flac-ui/flac-policy-delete-confirmation.png) -->

## 为沙盒配置策略

>[!IMPORTANT]
>
>默认情况下， [!UICONTROL 自动包含] 将为所有客户打开功能，这意味着所有沙盒都将添加到策略中。

>[!NOTE]
>
>此 **[!UICONTROL Default-Label-Based Access-Control-Policy]** 策略是目前唯一可用于配置的策略。

要查看与策略关联的沙盒，请从以下位置选择策略 **[!UICONTROL 策略]** 选项卡。

![显示现有可用策略列表的“策略”页。](../../images/abac-end-to-end-user-guide/abac-policies-page.png)

接下来，选择策略，然后选择 **[!UICONTROL 沙盒]** 选项卡。 将显示与策略关联的沙盒列表。

![显示现有可用策略列表的“策略”页。](../../images/flac-ui/abac-policies-sandboxes-tab.png)

### 将策略添加到所有沙盒

使用 **[!UICONTROL 自动包含]** 打开 **[!UICONTROL 沙盒]** 选项卡以激活所有沙盒的策略。

![此 [!UICONTROL 沙盒] 选项卡显示 [!UICONTROL 自动包含] 切换。](../../images/flac-ui/abac-policies-auto-include.png)

此 **[!UICONTROL 启用自动包含]** 出现对话框提示您确认选择。 选择 **[!UICONTROL 启用]** 以完成配置设置。

![此 [!UICONTROL 启用自动包含] 对话框突出显示 [!UICONTROL 启用].](../../images/flac-ui/abac-policies-auto-include-enable.png)

>[!SUCCESS]
>
>将为所有现有沙盒激活策略，并在任何新沙盒可用时自动将其添加到新沙盒。

### 添加策略以选择沙盒

>[!IMPORTANT]
>
>如果符合以下条件，则默认情况下不会将未来的沙盒包含在策略中 [!UICONTROL 自动包含] 切换功能已关闭。 您需要手动管理沙盒并将其添加到策略中。

使用 **[!UICONTROL 自动包含]** 打开 **[!UICONTROL 沙盒]** 选项卡禁用所有沙盒的策略。

![此 [!UICONTROL 沙盒] 选项卡显示 [!UICONTROL 自动包含] 切换。](../../images/flac-ui/abac-policies-auto-include.png)

从 **[!UICONTROL 沙盒]** 选项卡，选择 **[!UICONTROL 添加沙盒]** 以选择此策略将应用的沙盒。

![此 [!UICONTROL 沙盒] 选项卡，其中显示了添加到策略的沙盒列表。](../../images/flac-ui/abac-policies-sandboxes-tab-add.png)

此时将显示沙盒列表。 从列表中选择要添加的沙盒。 或者，使用搜索栏搜索沙盒。 选择&#x200B;**[!UICONTROL 保存]**。

![此 [!UICONTROL 添加沙盒] 显示可添加到策略的现有沙盒列表的页面。](../../images/flac-ui/abac-policies-sandboxes-list.png)

>[!SUCCESS]
>
>选定的沙盒已成功添加到策略中。

### 从策略中删除沙盒

要删除沙盒，请选择 **X** 沙盒名称旁边的图标。

![此 [!UICONTROL 沙盒] 选项卡显示沙盒列表，突出显示 [!UICONTROL X] 以删除。](../../images/flac-ui/abac-policies-remove-sandbox-x.png)

此 **[!UICONTROL 移除]** 出现对话框提示您确认选择。 选择 **[!UICONTROL 确认]** 以完成删除。

![此 [!UICONTROL 移除] 对话框突出显示 [!UICONTROL 确认].](../../images/flac-ui/abac-policies-remove-sandbox.png)

>[!SUCCESS]
>
>已成功从策略中删除选定的沙盒。

## 激活策略

要激活现有策略，请从 **[!UICONTROL 策略]** 选项卡。

![flac-policy-select](../../images/abac-end-to-end-user-guide/abac-policies-page.png)

接下来，选择省略号(`…`)，此时下拉菜单会显示用于编辑、激活、删除或复制角色的控件。 从下拉菜单中选择激活。

![flac-policy-activate](../../images/abac-end-to-end-user-guide/abac-policies-activate.png)

此 **[!UICONTROL 激活策略]** 出现对话框，提示您确认激活。

![flac-policy-activate-confirm](../../images/abac-end-to-end-user-guide/abac-activate-policies-dialog.png)


您将返回 **[!UICONTROL 策略]** 选项卡，此时会显示确认激活弹出窗口。 策略状态显示为活动。

![flac策略激活](../../images/abac-end-to-end-user-guide/abac-policies-confirm-activate.png)

## 后续步骤

激活策略后，您可以继续下一步以 [管理角色的权限](permissions.md).
