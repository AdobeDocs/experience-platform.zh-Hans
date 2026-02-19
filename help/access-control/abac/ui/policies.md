---
keywords: Experience Platform；主页；热门主题；访问控制；基于属性的访问控制；ABAC
title: 管理访问控制策略
description: 通过Adobe Experience Cloud中的“权限”界面管理访问控制策略。
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: b0094920720c54990953f79de32ab95c2a5c7e1c
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 10%

---

# 管理访问控制策略

访问控制策略是将属性集合在一起以建立允许和不允许的操作的语句。 Adobe提供了一个默认策略，可立即激活该策略，或者在您的组织准备好开始根据[标签](./labels.md){target="_blank"}控制对特定对象的访问时激活该策略。 默认策略&#x200B;**[!UICONTROL Default-Label-Based-Access-Control-Policy]**&#x200B;利用应用于资源的标签来拒绝访问，除非用户处于具有匹配标签的角色中。

>[!IMPORTANT]
>
>不应将访问控制策略与数据使用策略混淆，数据使用策略控制数据在Adobe Experience Platform中的使用方式。 有关详细信息，请参阅有关创建[数据使用策略](../../../data-governance/policies/create.md){target="_blank"}的指南。

## 为沙盒配置策略 {#configure-policy}

>[!NOTE]
>
>**[!UICONTROL Default-Label-Based-Access-Control-Policy]**&#x200B;策略当前是唯一可用于配置的策略。

要开始配置策略，请在&#x200B;**[!UICONTROL Permissions]** Adobe Experience Cloud[中导航到](https://experience.adobe.com/){target="_blank"}。 从左侧面板中选择&#x200B;**[!UICONTROL Policies]**。 从列表中选择&#x200B;**[!UICONTROL Default-Label-Based-Access-Control-Policy]**。

![显示现有策略列表的策略工作区。](../../images/ui/policies/policies-home.png){zoomable="yes"}

将显示策略详细信息工作区。 选择 **[!UICONTROL Sandboxes]**。将显示与策略关联的沙盒列表。

![策略的沙盒工作区显示关联沙盒的列表。](../../images/ui/policies/policy-sandbox.png){zoomable="yes"}

### 将策略添加到所有沙盒 {#add-policy-to-all}

>[!IMPORTANT]
>
>默认情况下，**[!UICONTROL Auto-include]**&#x200B;处于打开状态，这意味着所有当前和未来的沙盒都会自动添加到策略中。

关闭&#x200B;**[!UICONTROL Auto-include]**&#x200B;功能以阻止将来自动将沙盒添加到策略中。 关闭功能&#x200B;**将不会**&#x200B;从策略中删除任何沙盒。

![策略的“沙盒”选项卡，自动包含切换突出显示，且处于“关闭”状态。](../../images/ui/policies/policy-auto-include.png){zoomable="yes"}

如果&#x200B;**[!UICONTROL Auto-include]**&#x200B;在策略中处于非活动状态，则可以使用切换开关将其重新打开。 出现&#x200B;**[!UICONTROL Enable Auto-include]**&#x200B;对话框，提示您确认选择。 选择&#x200B;**[!UICONTROL Enable]**&#x200B;以完成配置设置。

>[!NOTE]
>
>关闭&#x200B;**[!UICONTROL Auto-include]**&#x200B;时您从策略中删除的任何沙盒都将重新添加。

![突出显示了“启用”选项的“启用自动包含”对话框。](../../images/ui/policies/policy-enable-auto-include.png){zoomable="yes"}

### 为策略手动选择沙盒 {#manually-select-sandboxes}

若要手动向策略添加沙盒或从中删除沙盒，**[!UICONTROL Auto-include]**&#x200B;切换&#x200B;**必须**&#x200B;关闭。

#### 添加沙盒

要将沙盒添加到策略，请选择&#x200B;**[!UICONTROL Add Sandboxes]**。

![突出显示了“添加沙盒”选项的策略工作区。](../../images/ui/policies/policy-add-sandboxes.png){zoomable="yes"}

出现&#x200B;**[!UICONTROL Add Sandboxes]**&#x200B;对话框。 选择要添加到策略的沙盒，然后选择&#x200B;**[!UICONTROL Save]**。

![选中了沙盒并突出显示“保存”选项的“添加沙盒”对话框。](../../images/ui/policies/policy-add-sandboxes-select.png){zoomable="yes"}

>[!NOTE]
>
>如果所有可用的沙盒都已添加到策略中，您将在对话框中看到“库中没有任何内容”消息。

#### 删除沙盒

要从策略中删除沙盒，请找到要从列表中删除的沙盒，然后选择&#x200B;**X**&#x200B;图标。

![策略的“沙盒”列表（高亮显示“x”）以删除沙盒。](../../images/ui/policies/policy-remove-sandbox.png){zoomable="yes"}

将出现一个确认对话框。 选择&#x200B;**[!UICONTROL Confirm]**&#x200B;完成从策略中删除沙盒。

![带有“确认”选项的沙盒的确认对话框突出显示。](../../images/ui/policies/policy-remove-sandbox-confirmation.png){zoomable="yes"}

## 激活一项策略 {#activate-policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="策略是什么？"
>abstract="策略是一些语句，它将若干属性组合在一起以确定允许执行和不允许执行的操作。每个组织都有一个默认策略，您必须激活该策略才能开始根据标签控制对特定对象的访问。除非用户被分配了具有匹配标签的角色，否则应用于资源的标签会拒绝访问。策略无法编辑或删除，但可以激活或停用。"
>additional-url="https://experienceleague.adobe.com/zh-hans/docs/experience-platform/access-control/abac/permissions-ui/labels" text="管理标签"

要激活现有策略，请从&#x200B;**[!UICONTROL Policies]**&#x200B;的&#x200B;**[!UICONTROL Permissions]**&#x200B;选项卡中选择策略。 策略的激活状态显示在&#x200B;**[!UICONTROL Status]**&#x200B;部分下。

![策略工作区中突出显示了策略状态。](../../images/ui/policies/policy-status.png){zoomable="yes"}

将会显示策略的详细信息工作区。 选择 **[!UICONTROL Activate]**。

![策略的“激活”选项突出显示的详细信息工作区。](../../images/ui/policies/policy-activate.png){zoomable="yes"}

出现&#x200B;**[!UICONTROL Activate Policy]**&#x200B;对话框。 选择&#x200B;**[!UICONTROL Confirm]**&#x200B;以完成激活策略。

![突出显示了“确认”选项的“激活策略”对话框。](../../images/ui/policies/policy-activate-confirm.png){zoomable="yes"}

## 后续步骤

激活策略后，您可以继续下一步以[管理角色](permissions.md)的权限。

<!--Policies are applied at the sandbox level to control which sandboxes enforce label-based access control. By default, the **[!UICONTROL Auto-include]** feature is turned on, which means all current and future sandboxes are automatically added to the policy. When **[!UICONTROL Auto-include]** is turned off, only the sandboxes you manually add will be subject to the policy's access control rules.

To begin configuring a policy's sandboxes, navigate to **[!UICONTROL Permissions]** in [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Select **[!UICONTROL Policies]** from the left panel, then select the **[!UICONTROL Default-Label-Based-Access-Control-Policy]** from the list.

The policy's details workspace appears. Select the **[!UICONTROL Sandboxes]** tab to view the list of sandboxes associated with the policy and access the sandbox configuration options.

### Manage Auto-include {#manage-auto-include}

To control which sandboxes are included in a policy, you can toggle the **[!UICONTROL Auto-include]** feature on or off. When you toggle off **[!UICONTROL Auto-include]**, future sandboxes will not be automatically added to the policy. However, toggling off the feature **will not** remove any sandboxes that are already included in the policy.

To re-enable **[!UICONTROL Auto-include]**, use the toggle to turn it back on. The **[!UICONTROL Enable Auto-include]** dialog appears prompting you to confirm your selection. Select **[!UICONTROL Enable]** to complete the configuration setting.

>[!NOTE]
>
>When you re-enable **[!UICONTROL Auto-include]**, any sandboxes you previously removed from the policy will be re-added.

### Manually manage sandboxes {#manually-manage-sandboxes}

When **[!UICONTROL Auto-include]**is turned off, you can manually add or remove specific sandboxes from the policy. This gives you precise control over which sandboxes enforce the policy's access control rules.

>[!NOTE]
>
>To manually add or remove sandboxes, the **[!UICONTROL Auto-include]** toggle **must** be off.

**To add sandboxes:**

Select **[!UICONTROL Add Sandboxes]** from the policy's sandbox workspace.

The **[!UICONTROL Add Sandboxes]** dialog appears, displaying your library of available sandboxes. Select the sandbox(es) you wish to add to the policy and then select **[!UICONTROL Save]**.

>[!NOTE]
>
>If all available sandboxes are already included in the policy, you will see a "You have nothing in your library" message within the dialog.

**To remove sandboxes:**

Find the sandbox you wish to remove from the list and select the **X** icon next to its name.

A confirmation dialog will appear. Select **[!UICONTROL Confirm]** to finish removing the sandbox from the policy.

-->