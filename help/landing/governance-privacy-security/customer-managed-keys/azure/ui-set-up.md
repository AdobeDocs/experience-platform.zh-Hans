---
title: 使用Experience Platform UI为Azure设置和配置客户管理的密钥
description: 了解如何使用您的Azure租户设置您的CMK应用并将您的加密密钥ID发送到Adobe Experience Platform。
role: Developer
feature: Privacy
exl-id: 5f38997a-66f3-4f9d-9c2f-fb70266ec0a6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 0%

---

# 使用Experience Platform UI为Azure设置和配置客户管理的密钥

本文档介绍了有关使用UI在Experience Platform中启用客户管理的密钥(CMK)功能的Azure特定说明。 有关特定于AWS的说明，请参阅[AWS安装指南](../aws/ui-set-up.md)。

有关如何使用API为Azure托管的Experience Platform实例完成此过程的说明，请参阅[API CMK设置文档](./api-set-up.md)。

## 先决条件

要查看和访问Adobe Experience Platform中的[!UICONTROL 加密]部分，您必须已创建一个角色，并为其分配了[!UICONTROL 管理客户管理的密钥]权限。 任何具有[!UICONTROL 管理客户管理的密钥]权限的用户都可以为其组织启用CMK。

有关在Experience Platform中分配角色和权限的详细信息，请参阅[配置权限文档](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html)。

若要启用CMK，必须使用以下设置配置您的[[!DNL Azure] 密钥保管库](./azure-key-vault-config.md)：

* [启用清除保护](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [启用软删除](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [使用基于 [!DNL Azure] 角色的访问控制配置访问](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [配置 [!DNL Azure] 密钥保管库](./azure-key-vault-config.md)

## 设置CMK应用程序 {#register-app}

配置密钥保管库后，下一步是注册将链接到[!DNL Azure]租户的CMK应用程序。

### 快速入门

要查看[!UICONTROL 加密配置]仪表板，请在左侧导航侧边栏的[!UICONTROL 管理]标题下选择&#x200B;**[!UICONTROL 加密]**。

![加密配置仪表板和客户管理的密钥卡突出显示。](../../../images/governance-privacy-security/customer-managed-keys/encryption-configraion.png)

选择&#x200B;**[!UICONTROL 配置]**&#x200B;以打开[!UICONTROL 客户托管密钥配置]视图。 此工作区包含完成下述步骤并执行与Azure Key保管库集成所需的所有值。

### 复制身份验证URL {#copy-authentication-url}

要开始注册过程，请从[!UICONTROL 客户托管密钥配置]视图中复制您组织的应用程序身份验证URL，并将其粘贴到您的[!DNL Azure]环境&#x200B;**[!DNL Key Vault Crypto Service Encryption User]**&#x200B;中。 下一节提供了有关如何[分配角色](#assign-to-role)的详细信息。

选择复制图标(![复制图标。](../../../../images/icons/copy.png))通过[!UICONTROL 应用程序身份验证URL]。

![突出显示应用程序身份验证URL部分的[!UICONTROL 客户托管密钥配置]视图。](../../../images/governance-privacy-security/customer-managed-keys/application-authentication-url.png)

将[!UICONTROL 应用程序身份验证URL]复制并粘贴到浏览器中以打开身份验证对话框。 选择&#x200B;**[!DNL Accept]**&#x200B;以将CMK应用服务主体添加到您的[!DNL Azure]租户。 确认身份验证会将您重定向到Experience Cloud登录页面。

![突出显示带有[!UICONTROL 接受]的Microsoft权限请求对话框。](../../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

>[!IMPORTANT]
>
>如果您有多个[!DNL Microsoft Azure]订阅，则可能会将您的Experience Platform实例连接到错误的密钥保管库。 在此情况下，您必须将应用程序身份验证URL名称的`common`部分交换为CMK目录ID。<br>从[!DNL Microsoft Azure]应用程序的门户设置、目录和订阅页面复制CMK目录ID<br>![突出显示目录ID的[!DNL Microsoft Azure]应用程序门户设置、目录和订阅页面。](../../../images/governance-privacy-security/customer-managed-keys/directory-id.png)<br>接下来，将其粘贴到浏览器地址栏中。<br>![突出显示应用程序身份验证URL的“common”部分的Google浏览器页面。](../../../images/governance-privacy-security/customer-managed-keys/common-url-section.png)

### 将CMK应用程序分配给角色 {#assign-to-role}

完成身份验证过程后，导航回您的[!DNL Azure]密钥库，并在左侧导航中选择&#x200B;**[!DNL Access control]**。 从此处依次选择&#x200B;**[!DNL Add]**&#x200B;和&#x200B;**[!DNL Add role assignment]**。

![突出显示了[!DNL Add]和[!DNL Add role assignment]的[!DNL Microsoft Azure]仪表板。](../../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

下一个屏幕提示您为此分配选择一个角色。 选择&#x200B;**[!DNL Key Vault Crypto Service Encryption User]**&#x200B;再选择&#x200B;**[!DNL Next]**&#x200B;以继续。

>[!NOTE]
>
>如果您有[!DNL Managed-HSM Key Vault]层，则必须选择&#x200B;**[!DNL Managed HSM Crypto Service Encryption User]**&#x200B;用户角色。

![突出显示了[!DNL Key Vault Crypto Service Encryption User]的[!DNL Microsoft Azure]仪表板。](../../../images/governance-privacy-security/customer-managed-keys/select-role.png)

在下一个屏幕上，选择&#x200B;**[!DNL Select members]**&#x200B;以在右边栏中打开一个对话框。 使用搜索栏查找CMK应用程序的服务主体，并从列表中选择它。 完成后，选择&#x200B;**[!DNL Save]**。

>[!NOTE]
>
>如果在列表中找不到您的应用程序，则表示您的服务主体尚未被租户接受。 为确保您拥有正确的权限，请与[!DNL Azure]管理员或代表合作。

您可以通过将[!UICONTROL 客户托管密钥配置]视图上提供的[!UICONTROL 应用程序ID]与[!DNL Microsoft Azure]应用程序概述上提供的[!DNL Application ID]进行比较，来验证应用程序。

![突出显示[!UICONTROL 应用程序ID]的[!UICONTROL 客户托管密钥配置]视图。](../../../images/governance-privacy-security/customer-managed-keys/application-id.png)

验证Azure Tools所需的所有详细信息都包含在Experience Platform UI中。 提供了此级别的粒度，因为许多用户希望使用其他Azure工具来增强其监视和记录这些应用程序对其密钥保管库的访问的能力。 了解这些标识符对于实现此目标以及帮助Adobe服务访问密钥至关重要。

## 在Experience Platform上启用加密密钥配置 {#send-to-adobe}

在[!DNL Azure]上安装CMK应用后，可以将加密密钥标识符发送到Adobe。 在左侧导航中选择&#x200B;**[!DNL Keys]**，然后选择要发送的密钥的名称。

![突出显示了[!DNL Keys]对象和键名称的Microsoft Azure仪表板。](../../../images/governance-privacy-security/customer-managed-keys/select-key.png)

选择键的最新版本，此时将显示其详细信息页面。 在此处，您可以选择为密钥配置允许的操作。

>[!IMPORTANT]
>
>允许对该键执行的最小所需操作是&#x200B;**[!DNL Wrap Key]**&#x200B;和&#x200B;**[!DNL Unwrap Key]**&#x200B;权限。 您可以根据需要包含[!DNL Encrypt]、[!DNL Decrypt]、[!DNL Sign]和[!DNL Verify]。

**[!UICONTROL 密钥标识符]**&#x200B;字段显示密钥的URI标识符。 复制此URI值以供在下一步中使用。

![Microsoft Azure功能板密钥详细信息中突出显示[!DNL Permitted operations]和复制密钥URL部分。](../../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

获得[!DNL Key vault URI]后，请返回[!UICONTROL 客户托管密钥配置]视图，并输入描述性&#x200B;**[!UICONTROL 配置名称]**。 接下来，将从Azure密钥详细信息页面获取的[!DNL Key Identifier]添加到&#x200B;**[!UICONTROL 密钥保管库密钥标识符]**&#x200B;中，并选择&#x200B;**[!UICONTROL 保存]**。

![具有[!UICONTROL 配置名称]和[!UICONTROL 密钥保管库密钥标识符]部分的[!UICONTROL 客户托管密钥配置]视图已突出显示。](../../../images/governance-privacy-security/customer-managed-keys/configuration-name.png)

您返回到[!UICONTROL 加密配置仪表板]。 [!UICONTROL 客户托管密钥]配置的状态显示为[!UICONTROL 正在处理]。

![在[!UICONTROL 客户托管密钥]卡上突出显示了[!UICONTROL 正在处理]的[!UICONTROL 加密配置]仪表板。](../../../images/governance-privacy-security/customer-managed-keys/processing.png)

## 验证配置的状态 {#check-status}

留出大量的处理时间。 要检查配置状态，请返回[!UICONTROL 客户托管密钥配置]视图，然后向下滚动到[!UICONTROL 配置状态]。 进度条已前进到第三步的第一步，并说明了系统正在验证Experience Platform是否有权访问密钥和密钥保管库。

CMK配置有四种潜在状态。 具体如下：

* 步骤1：验证Experience Platform是否能够访问密钥和密钥保管库。
* 步骤2：正在将密钥保管库和密钥名称添加到组织中的所有数据存储中。
* 步骤3：已成功将密钥保管库和密钥名称添加到数据存储。
* `FAILED`：出现问题，主要与密钥、密钥保管库或多租户应用设置有关。

## 后续步骤

通过完成上述步骤，您已成功为Azure托管的组织启用CMK。 现在，将使用[!DNL Azure]密钥保管库中的密钥对摄取到主数据存储中的数据加密和解密。

在为Azure托管组织启用CMK后，监视密钥使用情况，实施密钥轮换策略以增强安全性，并确保遵守组织的策略。
