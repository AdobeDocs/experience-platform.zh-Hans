---
title: 双向传输层安全性(mTLS)概述
description: 了解如何使用mTLS安全地检索Adobe颁发的公共证书以进行事件转发。
exl-id: e8ee8655-213d-4d2a-93d4-d62824b53b1d
source-git-commit: ab16cc3f70ec54460c7c4834e665c828d75d4d9e
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 2%

---

# 相互传输层安全性([!DNL mTLS])概述

在[!UICONTROL 环境UI]中绑定相互传输层安全性([!DNL mTLS])证书，以控制扩展的安全性。 [!DNL mTLS]证书是数字凭据，用于证明安全通信中服务器或客户端的身份。 当您使用[!DNL mTLS]服务API时，这些证书可帮助您验证并加密与Adobe Experience Platform事件转发的交互。 此过程不仅可以保护您的数据，还可以确保每个连接都来自可信合作伙伴。

## 在新环境中实施[!DNL mTLS] {#implement-mtls}

设置事件转发环境，确保将库版本正确部署到边缘网络。 在设置过程中，您可以选择最适合您的部署需求的托管选项。 [!DNL mTLS]证书也将自动添加到您的新环境中以进行安全通信。

要创建新环境，请选择事件转发属性左侧面板中的&#x200B;**[!UICONTROL 环境]**&#x200B;选项卡，然后选择&#x200B;**[!UICONTROL 添加环境]**。

![事件转发属性显示现有环境，突出显示[!UICONTROL 添加环境]。](../../../images/extensions/server/cloud-connector/add-environment.png)

在下一个页面中，选择要用于此设置的环境。 提供了三个环境：

>[!NOTE]
>
>资产仅限于一个开发、一个暂存和一个生产环境。

| 环境 | 描述 |
| --- | --- |
| 开发 | 开发环境供团队成员测试事件转发中的库或更改。 |
| 暂存 | 暂存环境是可选的，它允许已批准的团队成员在发布库之前测试和批准库。 |
| 生产 | 生产环境用于实时生产数据。 |

![环境选择屏幕，突出显示[!UICONTROL 为开发选择]。](../../../images/extensions/server/cloud-connector/select-environment.png)

在&#x200B;**[!UICONTROL 创建环境]**&#x200B;页面上，输入&#x200B;**[!UICONTROL 名称]**，然后从&#x200B;**[!UICONTROL 选择主机]**&#x200B;下拉菜单中选择&#x200B;***Adobe Managed***。 **[!UICONTROL 证书]**&#x200B;是&#x200B;***自动添加的***。 最后，选择&#x200B;**[!UICONTROL 保存]**。

![创建开发环境页面，突出显示[!UICONTROL 名称]、[!UICONTROL 选择主机]和[!UICONTROL 保存]。](../../../images/extensions/server/cloud-connector/create-environment.png)

已成功创建环境，并且您返回到&#x200B;**[!UICONTROL 环境]**&#x200B;选项卡，该选项卡显示您的新环境。

![[!UICONTROL 环境]选项卡，突出显示开发环境。](../../../images/extensions/server/cloud-connector/new-environment-created.png)

## 查看环境证书详细信息 {#view-certificate}

要查看环境的证书详细信息，请选择事件转发属性左侧面板中的&#x200B;**[!UICONTROL 环境]**&#x200B;选项卡，然后选择环境以查看详细信息。

将显示以下证书详细信息：

| 字段名称 | 描述 |
| --- | --- |
| 证书 | 证书的详细信息，包括：<ul><li>**Name**：证书的名称。</li><li>**创建日期**：创建证书的日期。</li><li>**状态**：证书的当前状态：<ul><li>**当前**：证书正在使用中。</li><li>**已过时**：证书不在使用中，但尚未过期。 仍可将其选中以供使用。</li><li>**已过期**：证书已过期、灰显且不再可用。</li></ul></ul> |
| 过期 | 证书到期日期。 |
| Variable Name | 证书的变量名称。 |
| 状态 | 证书的当前状态：<ul><li>**已部署**：证书已成功部署且处于活动状态。</li><li>**正在部署**：正在部署证书。</li><li>**需要部署**：在选择了过时的证书时，将出现此状态。</li></ul> |

![编辑开发环境页面，突出显示[!UICONTROL 证书]详细信息。](../../../images/extensions/server/cloud-connector/certificate-details.png)

### 选择并部署过时的证书 {#deploy-obsolete-certificate}

要使用过时的证书，请导航到事件转发属性左侧面板中的&#x200B;**[!UICONTROL 环境]**&#x200B;选项卡，然后选择环境以查看其详细信息。

![[!UICONTROL 环境]选项卡，突出显示开发环境。](../../../images/extensions/server/cloud-connector/new-environment-created.png)

从&#x200B;**[!UICONTROL 证书]**&#x200B;下拉列表中，选择一个过时的证书，然后选择&#x200B;**[!UICONTROL 保存]**。

![编辑开发环境页面，突出显示[!UICONTROL 证书]下拉列表，其中已弃用证书并突出显示“保存”。](../../../images/extensions/server/cloud-connector/obsolete-certificate.png)

要部署证书，请在&#x200B;**[!UICONTROL 部署证书]**&#x200B;对话框中选择&#x200B;**[!UICONTROL 保存并部署]**。

![突出显示了“保存并部署”的“部署证书”对话框。](../../../images/extensions/server/cloud-connector/obsolete-certificate-deploy.png)


## 后续步骤 {#next-steps}

本文档演示了如何为事件转发属性创建环境、添加证书和使用过时的证书。 有关[!DNL mTLS]证书的详细信息，请参阅[[!DNL mTLS] 服务API概述](../../../../data-governance/mtls-api/overview.md)

要了解如何在事件转发规则中使用[!DNL mTLS]证书，请参阅[Cloud Connector扩展概述](../cloud-connector/overview.md/#mtls-rules)。
