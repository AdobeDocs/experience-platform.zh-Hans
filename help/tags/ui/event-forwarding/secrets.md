---
title: 在事件转发中配置密钥
description: 了解如何在UI中配置密钥，以对事件转发属性中使用的端点进行身份验证。
exl-id: eefd87d7-457f-422a-b159-5b428da54189
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '1633'
ht-degree: 0%

---

# 在事件转发中配置密钥

在事件转发中，密钥是表示其他系统的身份验证凭据的资源，允许安全地交换数据。 只能在事件转发属性中创建密钥。

当前支持三种密钥类型：

| 密钥类型 | 描述 |
| --- | --- |
| [!UICONTROL 令牌] | 一个字符串，表示两个系统已知和理解的身份验证令牌值。 |
| [!UICONTROL HTTP] | 包含用户名和密码的两个字符串属性。 |
| [!UICONTROL OAuth 2] | 包含多个属性以支持 [客户端凭据授予类型](https://datatracker.ietf.org/doc/html/rfc6749#section-1.3.4) 对于 [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) 验证规范。 系统会要求您提供所需信息，然后在指定的间隔内为您处理这些令牌的续订。 |
| [!UICONTROL Google OAuth 2] | 包含多个属性以支持 [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) 验证规范，用于 [Google Ads API](https://developers.google.com/google-ads/api/docs/oauth/overview) 和 [Pub/Sub API](https://cloud.google.com/pubsub/docs/reference/service_apis_overview). 系统会要求您提供所需信息，然后在指定的间隔内为您处理这些令牌的续订。 |

{style=&quot;table-layout:auto&quot;}

本指南简要概述了如何为事件转发配置密钥([!UICONTROL Edge])属性。

>[!NOTE]
>
>有关如何在Reactor API中管理密钥（包括密钥结构的示例JSON）的详细指南，请参阅 [Secrets API指南](../../api/guides/secrets.md).

## 先决条件

本指南假定您已经熟悉如何在UI中管理标记和事件转发的资源，包括如何创建数据元素和事件转发规则。 请参阅 [管理资源](../managing-resources/overview.md) 如果您需要介绍。

您还应该对标记和事件转发的发布流程有一定的了解，包括如何向库添加资源并将内部版本安装到您的网站上以进行测试。 请参阅 [发布概述](../publishing/overview.md) 以了解更多详细信息。

## 创建密钥 {#create}

要创建密钥，请选择 **[!UICONTROL 事件转发]** 在左侧导航中，打开要在下添加密钥的事件转发属性。 接下来，选择 **[!UICONTROL 秘密]** 在左侧导航中，然后是 **[!UICONTROL 创建新密钥]**.

![创建新密钥](../../images/ui/event-forwarding/secrets/create-new-secret.png)

下一个屏幕允许您配置密钥的详细信息。 为了让事件转发可用的密钥，必须将其分配到现有环境。 如果尚未为事件转发资产创建任何环境，请参阅 [环境](../publishing/environments.md) ，以了解如何在继续之前配置它们。

>[!NOTE]
>
>如果您仍想在将密钥添加到环境之前创建并保存该密钥，请禁用 **[!UICONTROL 将密钥附加到环境]** 在填写其余信息之前进行切换。 请注意，如果要使用密码，则必须稍后将其分配给环境。
>
>![禁用环境](../../images/ui/event-forwarding/secrets/env-disabled.png)

在 **[!UICONTROL Target环境]**，请使用下拉菜单选择要将密钥分配到的环境。 在 **[!UICONTROL 密钥名称]**，在环境上下文中提供密钥的名称。 该名称在事件转发属性下的所有密钥中必须唯一。

![环境和名称](../../images/ui/event-forwarding/secrets/env-and-name.png)

一次只能将一个密钥分配给一个环境，但您可以根据需要将相同的凭据分配给不同环境中的多个密钥。 选择 **[!UICONTROL 添加环境]** 向列表中添加另一行。

![添加环境](../../images/ui/event-forwarding/secrets/add-env.png)

对于您添加的每个环境，必须为关联的密钥提供另一个唯一名称。 如果您耗尽了所有可用环境， **[!UICONTROL 添加环境]** 按钮。

![添加环境不可用](../../images/ui/event-forwarding/secrets/add-env-greyed.png)

在此处，创建密钥的步骤因您创建的密钥类型而异。 有关详细信息，请参阅以下子部分：

* [[!UICONTROL 令牌]](#token)
* [[!UICONTROL HTTP]](#http)
* [[!UICONTROL OAuth 2]](#oauth2)
* [[!UICONTROL Google OAuth 2]](#google-oauth2)

### [!UICONTROL 令牌] {#token}

要创建令牌密钥，请选择 **[!UICONTROL 令牌]** 从 **[!UICONTROL 类型]** 下拉列表。 在 **[!UICONTROL 令牌]** 字段，请提供由您对其进行身份验证的系统所识别的凭据字符串。 选择 **[!UICONTROL 创建密钥]** 来保存秘密。

![令牌密钥](../../images/ui/event-forwarding/secrets/token-secret.png)

### [!UICONTROL HTTP] {#http}

要创建HTTP密钥，请选择 **[!UICONTROL 简单HTTP]** 从 **[!UICONTROL 类型]** 下拉列表。 在下面显示的字段中，提供凭据的用户名和密码，然后再选择 **[!UICONTROL 创建密钥]** 来保存秘密。

>[!NOTE]
>
>保存凭据后，将使用 [“基本”HTTP身份验证方案](https://www.rfc-editor.org/rfc/rfc7617.html).

![HTTP密钥](../../images/ui/event-forwarding/secrets/http-secret.png)

### [!UICONTROL OAuth 2] {#oauth2}

要创建OAuth 2密钥，请选择 **[!UICONTROL OAuth 2]** 从 **[!UICONTROL 类型]** 下拉列表。 在下面显示的字段中，提供 [[!UICONTROL 客户端ID] 和 [!UICONTROL 客户端密钥]](https://www.oauth.com/oauth2-servers/client-registration/client-id-secret/)，以及 [[!UICONTROL 令牌URL]](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) 的OAuth集成。 的 [!UICONTROL 令牌URL] UI中的字段是授权服务器主机和令牌路径之间的串联。

![OAuth 2密钥](../../images/ui/event-forwarding/secrets/oauth-secret-1.png)

在 **[!UICONTROL 凭据选项]**，则可以提供其他凭据选项，例如 `scope` 和 `audience` 键值对的形式。 要添加更多键值对，请选择 **[!UICONTROL 添加其他]**.

![凭据选项](../../images/ui/event-forwarding/secrets/oauth-secret-2.png)

最后，您可以配置 **[!UICONTROL 刷新偏移]** 值。 这表示在令牌到期前系统将执行自动刷新的秒数。 以小时和分钟为单位的等效时间显示在字段右侧，并在您键入内容时自动更新。

![刷新偏移](../../images/ui/event-forwarding/secrets/oauth-secret-3.png)

例如，如果刷新偏移设置为 `14400` （4小时），且访问令牌具有 `expires_in` 值 `86400` （24小时），系统将在20小时内自动刷新密码。

>[!IMPORTANT]
>
>OAuth密钥在刷新之间至少需要4小时，并且至少8小时内有效。 此限制允许您在生成的令牌出现问题时至少4小时进行干预。
>
>例如，如果将“偏移”设置为 `28800` （八小时），且访问令牌具有 `expires_in` of `36000` （10小时），因差异小于4小时而导致交换失败。

完成后，选择 **[!UICONTROL 创建密钥]** 来保存秘密。

![保存OAuth 2偏移](../../images/ui/event-forwarding/secrets/oauth-secret-4.png)

### [!UICONTROL Google OAuth 2] {#google-oauth2}

要创建Google OAuth 2密钥，请选择 **[!UICONTROL Google OAuth 2]** 从 **[!UICONTROL 类型]** 下拉列表。 在 **[!UICONTROL 范围]**，选择要使用此密钥授予访问权限的Google API。 当前支持以下产品：

* [Google Ads API](https://developers.google.com/google-ads/api/docs/oauth/overview)
* [Pub/Sub API](https://cloud.google.com/pubsub/docs/reference/service_apis_overview)

完成后，选择 **[!UICONTROL 创建密钥]**.

![Google OAuth 2密码](../../images/ui/event-forwarding/secrets/google-oauth.png)

此时会出现一个弹出窗口，通知您需要通过Google手动授权密钥。 选择 **[!UICONTROL 创建并授权]** 继续。

![Google授权弹出窗口](../../images/ui/event-forwarding/secrets/google-authorization.png)

此时会出现一个对话框，用于输入Google帐户的凭据。 按照提示授予在所选范围内对数据的事件转发访问权限。 授权过程完成后，将创建密钥。

## 编辑密钥

为资产创建密钥后，您可以在 **[!UICONTROL 秘密]** 工作区。 要编辑现有密钥的详细信息，请从列表中选择其名称。

![选择要编辑的密钥](../../images/ui/event-forwarding/secrets/edit-secret.png)

下一个屏幕允许您更改密钥的名称和凭据。

![编辑密钥](../../images/ui/event-forwarding/secrets/edit-secret-config.png)

>[!NOTE]
>
>如果密钥与现有环境关联，则无法将密钥重新分配给其他环境。 如果您希望在其他环境中使用相同的凭据，则必须 [创建新密码](#create) 中。 如果您从未事先将密钥分配给环境，或者您删除了将密钥附加到的环境，则从此屏幕重新分配环境的唯一方法是。

### 重试密码交换

您可以从编辑屏幕中重试或刷新密钥交换。 此过程因编辑的密码类型而异：

| 密钥类型 | 重试协议 |
| --- | --- |
| [!UICONTROL 令牌] | 选择 **[!UICONTROL 交换密钥]** 重试密钥交换。 此控件仅在有附加到该密钥的环境时可用。 |
| [!UICONTROL HTTP] | 如果没有附加到该密钥的环境，请选择 **[!UICONTROL 交换密钥]** 将凭据交换到base64。 如果附加了环境，请选择“选择” **[!UICONTROL 交换和部署密钥]** 交换基地64并部署秘密。 |
| [!UICONTROL OAuth 2] | 选择 **[!UICONTROL 生成令牌]** 用于交换凭据并返回来自身份验证提供程序的访问令牌。 |

## 删除密钥

删除  **[!UICONTROL 秘密]** 工作区中，选中其名称旁边的复选框，然后再选择 **[!UICONTROL 删除]**.

![删除密钥](../../images/ui/event-forwarding/secrets/delete.png)

## 在事件转发中使用密钥

要在事件转发中使用密钥，您必须先创建 [数据元素](../managing-resources/data-elements.md) 这个秘密本身。 保存数据元素后，可以将其包含在事件转发中 [规则](../managing-resources/rules.md) 并将这些规则添加到 [库](../publishing/libraries.md)，这些服务器又可以部署到Adobe服务器，作为 [构建](../publishing/builds.md).

创建数据元素时，选择 **[!UICONTROL 核心]** 扩展，然后选择 **[!UICONTROL 密码]** （对于数据元素类型）。 右侧面板会更新并提供下拉控件，用于向数据元素分配最多三个密钥：一个 [!UICONTROL 开发], [!UICONTROL 暂存]和 [!UICONTROL 生产] 分别进行。

![数据元素](../../images/ui/event-forwarding/secrets/data-element.png)

>[!NOTE]
>
>只有与开发、暂存和生产环境相关的密钥才会显示其各自的下拉菜单。

通过为单个数据元素分配多个密钥并将其包含在规则中，可以使数据元素的值根据容器库在 [发布流程](../publishing/publishing-flow.md).

![具有多个密钥的数据元素](../../images/ui/event-forwarding/secrets/multi-secret-data-element.png)

>[!NOTE]
>
>创建数据元素时，必须分配开发环境。 暂存和生产环境不需要密钥，但是，如果尝试迁移到这些环境的内部版本的密钥类型数据元素没有为相关环境选择密钥，则这些内部版本将失败。

## 后续步骤

本指南介绍了如何在UI中管理密钥。 有关如何使用Reactor API与密钥交互的信息，请参阅 [secrets endpoint指南](../../api/endpoints/secrets.md).
