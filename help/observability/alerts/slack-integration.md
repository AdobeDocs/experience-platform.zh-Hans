---
title: 面向客户的警报的Slack集成
description: 了解如何使用Adobe I/O Events App Builder将Adobe连接到Slack。
source-git-commit: c0fa0320b32e1bfe286d47a2e1af5ea1dcf74cb9
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 0%

---

# 面向客户的警报的Slack集成

Adobe Experience Platform允许您在[Adobe App Builder](https://developer.adobe.com/app-builder/docs/get_started/app_builder_get_started/first-app)上使用webhook代理在[中接收](https://developer.adobe.com/events/docs/guides/)Adobe I/O Events[!DNL Slack]。 代理处理Adobe的验证握手并将事件负载转换为[!DNL Slack]消息，以便您能够获取发送到工作区的面向客户的警报。

## 先决条件 {#prerequisites}

开始之前，请确保您满足以下条件：

* **Adobe Developer Console访问权限**：启用了App Builder的组织中的系统管理员或开发人员角色。
* **Node.js和npm**： Node.js（建议使用LTS），其中包含用于安装Adobe CLI和项目依赖项的npm。 有关详细信息，请参阅[下载Node.js](https://nodejs.org/)和[npm快速入门指南](https://docs.npmjs.com/getting-started)。
* **Adobe I/O CLI**：从终端安装Adobe I/O CLI： `npm install -g @adobe/aio-cli`。
* 带有传入Webhook的&#x200B;**Slack应用程序**：您的工作区中启用了&#x200B;**传入Webhook**&#x200B;的Slack应用程序。 请参阅[创建Slack应用程序](https://api.slack.com/apps)和[Slack传入Webhook指南](https://api.slack.com/messaging/webhooks)，以创建该应用程序并获取webhook URL（格式： `https://hooks.slack.com/...`）。

## 设置模板化项目 {#templated-project}

要设置模板化项目，请登录到Adobe Developer Console，然后从&#x200B;**[!UICONTROL Create project from template]**&#x200B;选项卡中选择&#x200B;**[!UICONTROL Home]**。

![Developer Console突出显示“主页”选项卡和“从模板创建项目”。](../images/alerts/slack-integration/developer-console-home.png)

选择&#x200B;**[!UICONTROL App Builder]**&#x200B;模板，然后输入&#x200B;**[!UICONTROL Project Title]**&#x200B;并选择&#x200B;**[!UICONTROL Add workspace]**。 最后，选择&#x200B;**[!UICONTROL Save]**。

![Developer Console高亮显示项目标题、添加Workspace并保存。](../images/alerts/slack-integration/developer-console-save.png)

您将收到项目已创建并移至&#x200B;**[!UICONTROL Project overview]**&#x200B;选项卡的确认。 从此处，您可以添加&#x200B;**[!UICONTROL Project description]**。

![显示项目详细信息的“项目概述”选项卡。](../images/alerts/slack-integration/developer-console-project.png)

## 初始化项目 {#initialize-project}

设置模板化项目后，初始化该项目。

1. 打开终端并输入以下命令以登录Adobe I/O。

   ```bash
   aio login
   ```

1. 初始化应用程序并提供名称。

   ```bash
   aio app init slack-webhook-proxy
   ```

1. 使用箭头键选择您的`Organization`，然后选择您之前在Developer Console中创建的`Project`。 选择要搜索的模板`Only Templates Supported By My Org`。

   ![终端，显示组织和项目选择，且仅显示我的组织支持的模板。](../images/alerts/slack-integration/terminal-organization-project.png)

1. 接下来，按&#x200B;**Enter**&#x200B;跳过模板并安装独立应用程序。

   ![终端，显示组织和项目选择，且仅显示我的组织支持的模板。](../images/alerts/slack-integration/terminal-skip-templates.png)

1. 指定要为此项目启用的Adobe I/O应用程序功能。 使用箭头键滚动并选择`Actions: Deploy Runtime actions`。

   ![终端显示具有下列操作的应用程序功能：已选择“部署运行时操作”。](../images/alerts/slack-integration/terminal-app-features.png)

1. 使用箭头键滚动并选择要创建的示例操作类型的`Adobe Experience Platform: Realtime Customer Profile`。

   ![终端显示Adobe Experience Platform的示例操作类型：已选择Realtime Customer Profile。](../images/alerts/slack-integration/terminal-sample-actions.png)

1. 为要添加到模板的UI滚动并选择`Pure HTML/JS`。 按&#x200B;**Enter**&#x200B;保留示例操作为默认值，然后再次按&#x200B;**Enter**&#x200B;保留该名称为默认值。

   ![终端显示选择了纯HTML/JS的UI选择。](../images/alerts/slack-integration/terminal-ui-template.png)

   您会收到应用程序初始化已完成的确认。

1. 导航到项目目录。

   ```bash
   cd slack-webhook-proxy
   ```

1. 添加Web操作。

   ```bash
   aio app add action
   ```

1. 选择 `Only Action Templates Supported By My Org`。此时将显示模板列表。

   ![显示操作模板列表的终端。](../images/alerts/slack-integration/terminal-action-templates.png)

1. 通过按空格键选择模板，然后使用您的`@adobe/generator-add-publish-events`向上&#x200B;**和**&#x200B;向下&#x200B;**箭头导航到**。 最后，按&#x200B;**空格键**&#x200B;并按&#x200B;**Enter**&#x200B;来选择模板。

   ![终端显示模板。](../images/alerts/slack-integration/terminal-action-select-template.png)

   将显示已安装`npm package @adobe/generator-add-publish-events`的确认。

1. 命名操作`webhook-proxy`。

   ![显示名为webhook-proxy的操作的终端。](../images/alerts/slack-integration/terminal-add-action-name.png)

   此时将显示模板已安装的确认消息。

## 创建文件操作并部署 {#create-file-actions}

添加代理代码，设置环境变量，然后部署。 该操作随后将在Developer Console中可用于注册。

### 实施运行时代理 {#runtime-proxy}

>[!NOTE]
>
>使用运行时操作注册时，签名验证和质询处理是自动进行的。

导航到项目文件夹并打开文件`actions/webhook-proxy/index.js`。 删除内容并替换为以下内容：

```
const fetch = require("node-fetch");
const { Core } = require("@adobe/aio-sdk");
 
/**
 * Adobe I/O Events to Slack Runtime Proxy
 *
 * Receives events from Adobe I/O Events and forwards them to Slack.
 * Signature verification and challenge handling are automatic when
 * using Runtime Action registration (non-web action).
 */
async function main(params) {
  const logger = Core.Logger("runtime-proxy", { level: params.LOG_LEVEL || "info" });
 
  try {
    logger.info(`Event received: ${JSON.stringify(params)}`);
 
    // Forward to Slack
    return forwardToSlack(params, params.SLACK_WEBHOOK_URL, logger);
 
  } catch (error) {
    logger.error(`Error: ${error.message}`);
    return { statusCode: 500, body: { error: "Internal server error" } };
  }
}
 
/**
 * Forwards the event payload to Slack
 */
async function forwardToSlack(payload, webhookUrl, logger) {
  if (!webhookUrl) {
    logger.error("SLACK_WEBHOOK_URL not configured");
    return { statusCode: 500, body: { error: "Server configuration error" } };
  }
 
  // Extract Adobe headers passed to runtime action
  const headers = {
    "x-adobe-event-code": payload["x-adobe-event-code"],
    "x-adobe-event-id": payload["x-adobe-event-id"],
    "x-adobe-provider": payload["x-adobe-provider"]
  };
 
  const slackMessage = buildSlackMessage(payload, headers);
 
  const response = await fetch(webhookUrl, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(slackMessage)
  });
 
  if (!response.ok) {
    const errorText = await response.text();
    logger.error(`Slack API error: ${response.status} - ${errorText}`);
    return { statusCode: response.status, body: { error: errorText } };
  }
 
  logger.info("Event forwarded to Slack");
  return { statusCode: 200, body: { success: true } };
}
 
/**
 * Builds a Slack Block Kit message from the event payload
 */
function buildSlackMessage(payload, headers) {
  // Adobe passes event code as x-adobe-event-code header (available in params for runtime actions)
  const eventType = headers["x-adobe-event-code"] ||
                    payload["x-adobe-event-code"] ||
                    payload.event_code ||
                    payload.type ||
                    payload.event_type ||
                    "Adobe Event";
  const eventId = headers["x-adobe-event-id"] || payload["x-adobe-event-id"] || payload.event_id || payload.id || "N/A";
  const eventData = payload.data || payload.event || payload;
 
  return {
    blocks: [
      {
        type: "header",
        text: { type: "plain_text", text: `Event: ${eventType}`, emoji: true }
      },
      {
        type: "section",
        fields: formatDataFields(eventData)
      },
      { type: "divider" },
      {
        type: "context",
        elements: [{
          type: "mrkdwn",
          text: `*Event ID:* ${eventId}  |  *Time:* ${new Date().toISOString()}`
        }]
      }
    ]
  };
}
 
/**
 * Formats event data as Slack mrkdwn fields
 */
function formatDataFields(data, maxFields = 10) {
  if (typeof data !== "object" || data === null) {
    return [{ type: "mrkdwn", text: `*Payload:*\n${String(data)}` }];
  }
 
  const entries = Object.entries(data);
  if (entries.length === 0) {
    return [{ type: "mrkdwn", text: "_No data provided_" }];
  }
 
  return entries.slice(0, maxFields).map(([key, value]) => ({
    type: "mrkdwn",
    text: `*${key}:*\n${typeof value === "object" ? `\`\`\`${JSON.stringify(value)}\`\`\`` : value}`
  }));
}
 
exports.main = main;
```

### 在app.config.yaml中配置操作 {#app-config}

>[!IMPORTANT]
>
>`app.config.yaml`中的操作配置是关键的。 您必须使用`web: no`创建可以在Developer Console中注册为运行时操作的非Web操作。

导航到项目文件夹并打开`app.config.yaml`。 将内容替换为以下内容：

```
application:
  runtimeManifest:
    packages:
      slack-webhook-proxy:
        license: Apache-2.0
        actions:
          webhook-proxy:
            function: actions/webhook-proxy/index.js
            web: no
            runtime: nodejs:22
            inputs:
              LOG_LEVEL: info
              SLACK_WEBHOOK_URL: $SLACK_WEBHOOK_URL
            annotations:
              require-adobe-auth: false
              final: true
```

### 环境变量 {#environment-variables}

>[!IMPORTANT]
>
>如果没有正确配置的.env文件，应用程序将无法运行。

要安全地管理凭据，请使用环境变量。 在项目的根目录中修改`.env`文件并添加：

```
SLACK_WEBHOOK_URL=https://hooks.slack.com/services/YOUR/WEBHOOK/URL
```

### 部署操作 {#deploy-action}

设置环境变量后，部署操作。 在终端中运行此命令时，请确保您位于项目的根目录下(`slack-webhook-proxy`)：

```bash
aio app deploy
```

将显示部署成功的确认。

>[!IMPORTANT]
>
>您的操作已部署到Adobe I/O Runtime。 该操作现在可在Developer Console中注册获得。

## 向Adobe I/O Events注册操作 {#register-events}

部署操作后，将其注册为Adobe I/O Events的目标。

在Developer Console中，打开您的App Builder项目，然后选择您的&#x200B;**[!UICONTROL Workspace]**。

在Workspace概述页面上，选择&#x200B;**[!UICONTROL Add service]**&#x200B;和&#x200B;**[!UICONTROL Event]**。

![Workspace概述页面，突出显示“添加服务和事件”。](../images/alerts/slack-integration/workspace-service-event.png)

在“添加事件”页面上，选择&#x200B;**[!UICONTROL Experience Platform]**&#x200B;和&#x200B;**[!UICONTROL Platform notifications]**，然后选择&#x200B;**[!UICONTROL Next]**。

![显示Experience Platform和Platform选定通知的“添加事件”页。](../images/alerts/slack-integration/add-events.png)

选择要接收通知的事件，然后选择&#x200B;**[!UICONTROL Next]**。

![显示要订阅的事件列表的“添加事件”页。](../images/alerts/slack-integration/select-events.png)

选择您的服务器到服务器身份验证凭据，然后选择&#x200B;**[!UICONTROL Next]**。

![显示服务器到服务器身份验证凭据选择的“添加事件”页。](../images/alerts/slack-integration/add-events-credentials.png)

为注册输入&#x200B;**[!UICONTROL Event registration name]**&#x200B;和清除&#x200B;**[!UICONTROL Event registration description]**，然后选择&#x200B;**[!UICONTROL Next]**。

![“添加事件”页显示事件注册名称和事件注册描述字段。](../images/alerts/slack-integration/add-events-registration.png)

选择&#x200B;**[!UICONTROL Runtime Action]**&#x200B;作为传递方式以及您创建的`slack-webhook-proxy/runtime-proxy`操作，然后选择&#x200B;**[!UICONTROL Save configured events]**。

![显示“运行时操作”传递方法和“保存配置的事件”的“添加事件”页。](../images/alerts/slack-integration/add-events-runtime.png)

webhook代理现已配置完成。 您将返回到Webhook代理页面。 您可以通过选择任何已配置事件旁边的&#x200B;**[!UICONTROL Send sample event]**&#x200B;图标，端到端地测试整个流。

![显示已配置事件和“发送示例事件”图标的webhook代理页面。](../images/alerts/slack-integration/send-sample.png)
