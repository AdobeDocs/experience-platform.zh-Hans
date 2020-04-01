---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 订阅隐私事件
topic: privacy events
translation-type: tm+mt
source-git-commit: e4cd042722e13dafc32b059d75fca2dab828df60

---


# 订阅隐私事件

隐私事件是Adobe Experience Platform Privacy Service提供的消息，该服务利用发送到已配置网络挂接的Adobe I/O事件来促进高效的作业请求自动化。 他们减少或消除了轮询Privacy Service API的需求，以便检查作业是否完成或是否已到达工作流中的特定里程碑。

当前有四种类型的通知与隐私作业请求生命周期相关：

| 类型 | 描述 |
--- | ---
| 作业完成 | 所有Experience Cloud解决方案均已报告回来，作业的整体或全局状态已标记为完成。 |
| 作业错误 | 一个或多个解决方案在处理请求时报告了错误。 |
| 产品完成 | 与此作业相关的解决方案之一已完成其工作。 |
| 产品错误 | 其中一个解决方案在处理请求时报告了错误。 |

本文档提供了在Adobe I/O中设置隐私服务通知集成的步骤。有关隐私服务及其功能的高级概述，请参阅隐私 [服务概述](home.md)。

## 入门指南

本教程使用 **Ngrok**（一种通过安全隧道将本地服务器公开到公共Internet的软件产品）。 请先 [安装网卡](https://ngrok.com/download) ，然后再开始本教程，以便继续学习并创建到本地机器的网卡。 本指南还要求您下载一个GIT存储库，其中包含一个以 [Node.js编写的简单服务器](https://nodejs.org/)。

## 创建本地服务器

您的Node.js服务器必须返 `challenge` 回由请求发送到根(`/`)端点的参数。 使用以 `index.js` 下JavaScript设置文件以实现此目的：

```js
var express = require('express')
var app = express()

app.set('port', (process.env.PORT || 3000))
app.use(express.static(__dirname + '/public'))

app.get('/', function(request, response) {
  response.send(request.originalUrl.split('?challenge=')[1]);
})

app.listen(app.get('port'), function() {
  console.log("Node app is running at localhost:" + app.get('port'))
})
```

使用命令行，导航到Node.js服务器的根目录。 然后，键入以下命令：

1. `npm install`
1. `npm start`

这些命令安装所有依赖关系并初始化服务器。 如果成功，您可以在http://localhost:3000/上找到正在运行的服务器。

## 使用ngrok创建网页挂接

在同一目录内和新命令行窗口中，键入以下命令：

```shell
ngrok http -bind-tls=true 3000
```

成功的输出如下所示：

![ngrok输出](images/privacy-events/ngrok-output.png)

请注意 `Forwarding` URL(`https://e142b577.ngrok.io`)，因为下一步将使用它识别您的Webhook。

## 使用Adobe I/O控制台创建新集成

登录到 [Adobe I/O Console](https://console.adobe.io) ，然后单击“集 **成** ”选项卡。 出现 _“Integrations_ （集成）”窗口。 在此处，单击“ **新建集成”**。

![Adobe I/O控制台中的视图集成](images/privacy-events/integrations.png)

将显 *示“创建新集成* ”窗口。 选择 **接收近实时事件**，然后单击 **继续**。

![创建新集成](images/privacy-events/new-integration.png)

下一个屏幕提供选项，用于根据您的事件、授权和权限创建与组织可用的不同订阅、产品和服务的集成。 对于此集成，选择“隐 **私服务事件**”，然后单击 **继续**。

![选择隐私事件](images/privacy-events/privacy-events.png)

此时 *会显示“集成详细信息* ”(Integration Details)表单，要求您提供集成的名称和说明以及公钥证书。

![集成详细信息](images/privacy-events/integration-details.png)

如果您没有公共证书，则可以使用以下终端命令生成一个证书：

```shell
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub
```

生成证书后，将文件拖放到 **Public keys certificates框中** ，或单击 **Select a File** （选择文件）浏览文件目录并直接选择证书。

添加证书后，将显示“ *事件注册* ”选项。 单击“ **添加事件注册**”。

![添加事件注册](images/privacy-events/add-event-registration.png)

此时将展开对话框以显示其他控件。 您可以在此选择所需的事件类型并注册Webhook。 输入事件注册的名称、Webhook URL(最初创建Webhook `Forwarding` 时返回的 [地址](#create-a-webhook-using-ngrok))以及简短说明。 最后，选择要订阅的事件类型，然后单击“保 **存”**。

![事件注册表单](images/privacy-events/event-registration-form.png)

完成事件注册表单后，单击 **创建集成** ,I/O集成将完成。

![创建集成](images/privacy-events/create-integration.png)

## 视图事件数据

创建I/O集成和隐私作业后，您可以视图收到的该集成通知。 从I/ **O控制台的** “集成”选项卡中，导航到您的集成，然后单击“ **视图”**。

![视图集成](images/privacy-events/view-integration.png)

此时会显示集成的详细信息页面。 单击 **事件** ，以视图集成的事件注册。 找到隐私事件注册，然后单击 **视图**。

![视图事件注册](images/privacy-events/view-registration.png)

出现 *“事件详细信息* ”窗口，您可以视图有关注册的更多信息，编辑其配置，或视图自激活网络挂接后收到的实际事件。 您可以视图事件详细信息，也可以导航到“调试跟 **踪”选项** 。

![调试跟踪](images/privacy-events/debug-tracing.png)

“有 **效负荷** ”部分提供有关选定事件的详细信息，包括其事件类型(`"com.adobe.platform.gdpr.productcomplete"`)，如上例中所述。

## 后续步骤

您可以重复上述步骤，根据需要为不同的Webhook地址添加新集成。