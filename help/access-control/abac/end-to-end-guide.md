---
keywords: Experience Platform；首頁；熱門主題；存取控制；屬性型存取控制；
title: 屬性型存取控制端對端指南
description: 本檔案提供Adobe Experience Platform中屬性型存取控制的端對端指南
exl-id: 7e363adc-628c-4a66-a3bd-b5b898292394
source-git-commit: 004f6183f597132629481e3792b5523317b7fb2f
workflow-type: tm+mt
source-wordcount: '1726'
ht-degree: 19%

---

# 屬性型存取控制端對端指南

以屬性為基礎的存取控制是Adobe Experience Platform的一項功能，可讓重視隱私權的多品牌客戶在管理使用者存取許可權時擁有更大的彈性。 根據物件的屬性和角色，可以使用原則來授予/拒絕對個別物件（例如結構描述欄位和區段）的存取權。 此功能可讓您為貴組織中的特定Platform使用者授予或撤銷個別物件的存取權。

此功能可讓您使用定義組織或資料使用範圍的標籤，將結構描述欄位、區段等分類。 您可以將這些相同的標籤套用至Adobe Journey Optimizer中的歷程、選件和其他物件。 同時，管理員可以定義有關Experience Data Model (XDM)結構描述欄位的存取原則，並更好地管理哪些使用者或群組（內部、外部或第三方使用者）可以存取這些欄位。

>[!NOTE]
>
>本檔案著重於存取控制原則的使用案例。 如果您嘗試設定原則來控管 **use** 而不是哪些Platform使用者有權存取這些資料，請參閱的端對端指南： [資料控管](../../data-governance/e2e.md) 而非。

## 快速入门

本教學課程需要您深入瞭解下列平台元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合基本概念](../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md)：內的分段引擎 [!DNL Platform] 用於根據客戶行為和屬性，從您的客戶設定檔建立受眾區段。

### 使用案例概觀

您將透過以屬性為基礎的存取控制工作流程範例，在此範例中，您將建立並指派角色、標籤和原則，以設定使用者是否可以存取組織中的特定資源。 本指南以限制存取敏感資料為例來示範工作流程。 此使用案例概述如下：

您是醫療保健提供者，且想要設定對組織中資源的存取權。

* 您的內部行銷團隊應能存取 **[!UICONTROL PHI/規範健康資料]** 資料。
* 您的外部機構應該無法存取 **[!UICONTROL PHI/規範健康資料]** 資料。

為此，您必須設定角色、資源和原則。

您將會：

* [為您的使用者加上標籤](#label-roles)：以醫療保健提供者（ACME業務群組）為例，其行銷群組與外部代理合作。
* [為資源加上標籤（結構描述欄位和區段）](#label-resources)：指派 **[!UICONTROL PHI/規範健康資料]** 結構描述資源和區段的標籤。
* 
   * [啟用將連結它們的原則： ](#policy)：啟用預設原則，將資源上的標籤連結至角色中的標籤，以防止存取結構描述欄位和區段。 之後，具有相符標籤的使用者將獲得架構欄位的存取權，以及所有沙箱中的區段。

## 权限

[!UICONTROL 許可權] 是Experience Cloud區域，管理員可在此定義使用者角色和原則，以管理產品應用程式內功能和物件的許可權。

到 [!UICONTROL 許可權]，您可以建立和管理角色，並為這些角色指派所需的資源許可權。 [!UICONTROL 权限还允许您管理与特定角色关联的标签、沙盒和用户。]

如果您沒有管理員許可權，請聯絡您的系統管理員以獲得存取權。

取得管理員許可權後，請前往 [Adobe Experience Cloud](https://experience.adobe.com/) 並使用您的Adobe憑證登入。 登入後， **[!UICONTROL 概觀]** 頁面會針對您擁有管理員許可權的組織顯示。 此頁面顯示貴組織訂閱的產品，以及新增使用者和管理員至組織的其他控制項。 選取 **[!UICONTROL 許可權]** 以開啟您的平台整合工作區。

![此影像顯示正在Adobe Experience Cloud中選取的許可權產品](../images/flac-ui/flac-select-product.png)

Platform UI的許可權工作區隨即顯示，並開啟於 **[!UICONTROL 角色]** 頁面。

## 將標籤套用至角色 {#label-roles}

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about"
>title="标签是什么？"
>abstract="通过标签，可根据适用于数据的使用策略将数据集和字段分类。Platform 提供若干由 Adobe 定义的“核心”数据使用标签，这些标签涵盖适用于数据治理的多种常见限制。例如，通过 RHD（受监管的健康数据）等敏感的“S”标签，可将涉及受保护的健康信息 (PHI) 的数据分类。还可自行定义适合组织需求的自定义标签。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=zh-Hans#understanding-data-usage-labels" text="数据使用标签概述"

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="创建新标签"
>abstract="可自行创建自定义标签以适合组织需求。自定义标签可用于将数据治理和访问控制配置应用于您的数据。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=zh-Hans#manage-labels" text="管理自定义标签"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about"
>title="角色是什么？"
>abstract="角色是将与您的 Platform 实例交互的用户的类型分类的方法，还是访问控制策略的构建块。一个角色具有一组给定的权限，可将您组织的成员分配给一个或多个角色，具体取决于他们需要的查看或写入访问权限的范围。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=zh-Hans" text="管理角色"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="创建新角色"
>abstract="可创建新角色以更好地将访问您的 Platform 实例的用户分类。例如，可为内部营销团队创建一个角色，并将 RHD 标签应用于该角色，使您的内部营销团队可访问受保护的健康信息 (PHI)。或者，还可为外部机构创建一个角色，并通过不将 RHD 标签应用于该角色而拒绝该角色访问 PHI 数据。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=zh-Hans#create-a-new-role" text="创建新角色"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_details"
>title="角色概述"
>abstract="角色概述对话框显示允许给定角色访问的资源和沙盒。"

角色是分類與您的Platform執行個體互動的使用者型別的方法，也是存取控制原則的建置組塊。 角色具有一組指定的許可權，而您組織的成員可以根據他們需要的存取範圍指派給一或多個角色。

若要開始使用，請選取 **[!UICONTROL ACME Business Group]** 從的 **[!UICONTROL 角色]** 頁面。

![顯示要在角色中選取的ACME企業角色的影像](../images/abac-end-to-end-user-guide/abac-select-role.png)

接下來，選取 **[!UICONTROL 標籤]** 然後選取 **[!UICONTROL 新增標籤]**.

![影像顯示「新增標籤」標籤上正在選取的標籤](../images/abac-end-to-end-user-guide/abac-select-add-labels.png)

您的組織中的所有標籤清單隨即顯示。 選取 **[!UICONTROL RHD]** 新增標籤 **[!UICONTROL PHI/規範健康資料]**. 請稍候片刻，讓標籤旁邊出現一個藍色勾號，然後選取 **[!UICONTROL 儲存]**.

![顯示正在選取和儲存之RHD標籤的影像](../images/abac-end-to-end-user-guide/abac-select-role-label.png)

>[!NOTE]
>
>將組織群組新增至角色時，該群組中的所有使用者都會新增至角色。 對組織群組所做的任何變更（移除或新增的使用者）都會在角色中自動更新。

## 將標籤套用至結構描述欄位 {#label-resources}

現在您已使用設定使用者角色 [!UICONTROL RHD] 標籤，下一步是將相同的標籤新增至您要為該角色控制的資源。

選取 **[!UICONTROL 結構描述]** 從左側導覽列中，然後選取 **[!UICONTROL ACME醫療保健]** 從出現的結構描述清單中。

![此影像顯示從「結構」標籤選取的ACME Healthcare結構](../images/abac-end-to-end-user-guide/abac-select-schema.png)

接下來，選取 **[!UICONTROL 標籤]** 檢視顯示與您的結構描述關聯欄位的清單。 從這裡，您可以一次將標籤指派給一個或多個欄位。 選取 **[!UICONTROL 血糖]** 和 **[!UICONTROL 胰島素水準]** 欄位，然後選取 **[!UICONTROL 套用存取權和資料治理標籤]**.

![顯示正在選取的BloodGlucose和InsulinLevel的影像，並套用正在選取的存取權和資料治理標籤](../images/abac-end-to-end-user-guide/abac-select-schema-labels-tab.png)

此 **[!UICONTROL 編輯標籤]** 對話方塊隨即顯示，供您選擇要套用至結構描述欄位的標籤。 對於此使用案例，請選取 **[!UICONTROL PHI/規範健康資料]** 標籤，然後選取 **[!UICONTROL 儲存]**.

![顯示正在選取和儲存之RHD標籤的影像](../images/abac-end-to-end-user-guide/abac-select-schema-labels.png)

>[!NOTE]
>
>將標籤新增至欄位時，該標籤會套用至該欄位的父項資源（類別或欄位群組）。 如果父類別或欄位群組被其他結構描述使用，這些結構描述將繼承相同的標籤。

## 將標籤套用至區段

完成標示結構描述欄位後，您現在可以開始標示區段。

選取 **[!UICONTROL 區段]** 從左側導覽列中。 隨即顯示貴組織中可用的區段清單。 在此範例中，下列兩個區段會加上標籤，因為它們包含敏感的健康情況資料：

* 血糖>100
* 胰島素&lt;50

選取 **[!UICONTROL 血糖>100]** 以開始標籤區段。

![顯示從「區段」索引標籤中選取「血糖> 100」的影像](../images/abac-end-to-end-user-guide/abac-select-segment.png)

區段 **[!UICONTROL 詳細資料]** 畫面隨即顯示。 選取 **[!UICONTROL 管理存取權]**.

![顯示「管理存取」選取範圍的影像](../images/abac-end-to-end-user-guide/abac-segment-fields-manage-access.png)

此 **[!UICONTROL 編輯標籤]** 對話方塊隨即顯示，供您選擇要套用至區段的標籤。 對於此使用案例，請選取 **[!UICONTROL PHI/規範健康資料]** 標籤，然後選取 **[!UICONTROL 儲存]**.

![顯示RHD標籤選取範圍並儲存選取專案的影像](../images/abac-end-to-end-user-guide/abac-select-segment-labels.png)

重複上述步驟，使用 **[!UICONTROL 胰島素&lt;50]**.

## 啟用存取控制原則 {#policy}

預設存取控制策略將利用標籤來定義哪些使用者角色有權存取特定Platform資源。 在此範例中，如果使用者不在結構欄位中具有對應標籤的角色中，其所有沙箱中的結構欄位和區段存取權將會遭到拒絕。

若要啟用存取控制原則，請選取 [!UICONTROL 許可權] 從左側導覽列中，然後選取 **[!UICONTROL 原則]**.

![顯示的原則清單](../images/abac-end-to-end-user-guide/abac-policies-page.png)

接著，選取省略符號(`...`)，下拉式清單則會顯示可編輯、啟動、刪除或複製角色的控制項。 選取 **[!UICONTROL 啟動]** 下拉式清單中的。

![啟動原則的下拉式清單](../images/abac-end-to-end-user-guide/abac-policies-activate.png)

啟動原則對話方塊會出現，提示您確認啟動。 選取 **[!UICONTROL 確認]**.

![啟用原則對話方塊](../images/abac-end-to-end-user-guide/abac-activate-policies-dialog.png)

已收到啟用原則的確認，您會返回 [!UICONTROL 原則] 頁面。

![啟用原則確認](../images/abac-end-to-end-user-guide/abac-policies-confirm-activate.png)

<!-- ## Create an access control policy {#policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="What are policies?"
>abstract="Policies are statements that bring attributes together to establish permissible and impermissible actions. Every organization comes with a default policy that you must activate to define rules for resources like segments and schema fields. Default policies can neither be edited nor deleted. However, default policies can be activated or deactivated."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en" text="Manage policies"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about_create"
>title="Create a policy"
>abstract="Create a policy to define the actions that your users can and cannot take against your segments and schema fields."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#create-a-new-policy" text="Create a policy"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_permitdeny"
>title="Configure permissible and impermissible actions for a policy"
>abstract="A <b>deny access to</b> policy will deny users access when the criteria is met. Combined with <b>The following being false</b> - all users will be denied access unless they meet the matching criteria set. This type of policy allows you to protect a sensitive resource and only allow access to users with matching labels. <br>A <b>permit access to</b> policy will permit users access when the criteria are met. When combined with <b>The following being true</b> - users will be given access if they meet the matching criteria set. This does not explicitly deny access to users, but adds a permit access. This type of policy allows you to give additional access to resource and in addition to those users who might already have access through role permissions."</br>
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#edit-a-policy" text="Edit a policy"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_resource"
>title="Configure permissions for a resource"
>abstract="A resource is the asset or object that a user can or cannot access. Resources can be segments or schemas fields. You can configure write, read, or delete permissions for segments and schema fields."

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_condition"
>title="Edit conditions"
>abstract="Apply conditional statements to your policy to configure user access to certain resources. Select match all to require users to have roles with the same labels as a resource to be permitted access. Select match any to require users to have a role with just one label matching a label on a resource. Labels can either be defined as core or custom labels, with core labels representing labels created and provided by Adobe and custom labels representing labels that you created for your organization."

Access control policies leverage labels to define which user roles have access to specific Platform resources. Policies can either be local or global and can override other policies. In this example, access to schema fields and segments will be denied in all sandboxes for users who don't have the corresponding labels in the schema field.

>[!NOTE]
>
>A "deny policy" is created to grant access to sensitive resources because the role grants permission to the subjects. The written policy in this example **denies** you access if you are missing the required labels.

To create an access control policy, select **[!UICONTROL Permissions]** from the left navigation and then select **[!UICONTROL Policies]**. Next, select **[!UICONTROL Create policy]**.

![Image showing Create policy being selected in the Permissions](../images/abac-end-to-end-user-guide/abac-create-policy.png)

The **[!UICONTROL Create new policy]** dialog appears, prompting you to enter a name and an optional description. Select **[!UICONTROL Confirm]** when finished.

![Image showing the Create new policy dialog and selecting Confirm](../images/abac-end-to-end-user-guide/abac-create-policy-details.png)

To deny access to the schema fields, use the dropdown arrow and select **[!UICONTROL Deny access to]** and then select **[!UICONTROL No resource selected]**. Next, select **[!UICONTROL Schema Field]** and then select **[!UICONTROL All]**.

![Image showing Deny access and resources selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema.png)

The table below shows the conditions available when creating a policy:

| Conditions | Description |
| --- | --- |
| The following being false| When 'Deny access to' is set, access will be restricted if the user does not meet the criteria selected. |
| The following being true| When 'Permit access to' is set, access will be permitted if the user meets the selected criteria. |
| Matches any| The user has a label that matches any label applied to a resource. |
| Matches all| The user has all labels that matches all labels applied to a resource. |
| Core label| A core label is an Adobe-defined label that is available in all Platform instances.|
| Custom label| A custom label is a label that has been created by your organization.|

Select **[!UICONTROL The following being false]** and then select **[!UICONTROL No attribute selected]**. Next, select the user **[!UICONTROL Core label]**, then select **[!UICONTROL Matches all]**. Select the resource **[!UICONTROL Core label]** and finally select **[!UICONTROL Add resource]**.

![Image showing the conditions being selected and Add resource being selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema-expression.png)

>[!TIP]
>
>A resource is the asset or object that a subject can or cannot access. Resources can be segments or schemas.

To deny access to the segments, use the dropdown arrow and select **[!UICONTROL Deny access to]** and then select **[!UICONTROL No resource selected]**. Next, select **[!UICONTROL Segment]** and then select **[!UICONTROL All]**.

Select **[!UICONTROL The following being false]** and then select **[!UICONTROL No attribute selected]**. Next, select the user **[!UICONTROL Core label]**, then select **[!UICONTROL Matches all]**. Select the resource **[!UICONTROL Core label]** and finally select **[!UICONTROL Save]**.

![Image showing conditions selected and Save being selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-segment.png)

Select **[!UICONTROL Activate]** to activate the policy, and a dialog appears which prompts you to confirm activation. Select **[!UICONTROL Confirm]** and then select **[!UICONTROL Close]**.

![Image showing the Policy being activated ](../images/abac-end-to-end-user-guide/abac-create-policy-activation.png) -->

## 后续步骤

您已完成將標籤套用至角色、結構描述欄位和區段。 指派給這些角色的外部機構無法檢視這些標籤及其在結構描述、資料集和設定檔檢視中的值。 使用「區段產生器」時，這些欄位也不能用於區段定義。

如需以屬性為基礎的存取控制的詳細資訊，請參閱 [屬性型存取控制概觀](./overview.md).
