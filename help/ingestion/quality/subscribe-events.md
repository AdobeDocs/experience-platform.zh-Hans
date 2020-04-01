---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 订阅数据获取事件
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# 数据摄取通知

将数据引入Adobe Experience Platform的过程由多个步骤组成。 在您确定需要摄取到平台中的数据文件后，摄取过程开始，每个步骤都会连续进行，直到数据被成功摄取或失败。 可以使用 [Adobe Experience Platform Data Ingestion API或Experience Platform用户界面启动摄取过程](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) 。

加载到平台中的数据必须经过多个步骤才能到达其目标、数据湖或实时客户用户档案数据存储。 每个步骤都涉及处理数据、验证数据，然后在将数据传递到下一步之前存储数据。 根据摄取的数据量，这可能会成为一个耗时的过程，并且始终有可能由于验证、语义或处理错误而导致该过程失败。 在出现故障的事件中，需要修复数据问题，然后必须使用更正的数据文件重新启动整个摄取过程。

为了帮助监视摄取过程，Experience Platform允许订阅在该过程的每个步骤发布的一组事件，通知您所摄取数据的状态和任何可能的故障。

## 可用状态通知事件

以下是可订阅的可用数据摄取状态通知的列表。

>[!NOTE] 只为所有数据获取通知提供一个事件主题。 为了区分不同的状态，可以使用事件代码。

| 平台服务 | 状态 | 事件说明 | 事件代码 |
| ---------------- | ------ | ----------------- | ---------- |
| 数据登陆 | success | 摄取——批处理成功 | ing_load_success |
| 数据登陆 | 失败 | 摄取——批处理失败 | ing_load_failure |
| 实时客户资料 | success | 用户档案服务——数据加载批成功 | ps_load_success |
| 实时客户资料 | 失败 | 用户档案服务——数据加载批处理失败 | ps_load_failure |
| 标识图 | success | 标识图——数据加载批成功 | ig_load_success |
| 标识图 | 失败 | 标识图——数据加载批处理失败 | ig_load_failure |

## 通知有效负荷模式

数据摄取通知事件模式是一个体验数据模型(XDM)模式，其中包含提供有关所摄取数据状态的详细信息的字段和值。 请访问公共XDM GitHub存储库以视图最新的通知有效负 [载模式](https://github.com/adobe/xdm/blob/master/schemas/common/notifications/ingestion.schema.json)。

## 订阅数据摄取状态通知

通过 [Adobe I/O事件](https://www.adobe.io/apis/experienceplatform/events.html)，您可以使用Webhook订阅多种通知类型。 要了解有关网络挂钩的更多信息以及如何使用网络挂钩订阅Adobe I/O事件，请参 [阅Adobe I/O事件网络挂钩指南的介绍](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) 。

### 使用Adobe I/O控制台创建新集成

登录到 [Adobe I/O Console](https://console.adobe.io/home) ，单击“集成”选项卡，或单击“快速开始”下的“创建集成”(Create integration ****** )。 当出现“ *集成* ”屏幕时，单 **击“新建集成** ”以创建新集成。

![创建新集成](../images/quality/subscribe-events/create_integration_start.png)

将出 *现“创建新集成* ”屏幕。 选择 **接收近实时事件**，然后单击 **继续**。

![接收近乎实时的事件](../images/quality/subscribe-events/create_integration_receive_events.png)

下一个屏幕提供选项，用于根据您的事件、授权和权限创建与组织可用的不同订阅、产品和服务的集成。 对于此集成，在Experience Platform下选择 **Platform通知** ，然后单击 **继续**。

![选择事件提供者](../images/quality/subscribe-events/create_integration_select_provider.png)

此时 *会显示“集成详细信息* ”(Integration Details)表单，要求您提供集成的名称和说明以及公钥证书。

如果您没有公共证书，则可以使用以下命令在终端中生成一个证书：

```shell
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub
```

生成证书后，将文件拖放到 **Public keys certificates框中** ，或单击 **Select a File** （选择文件）浏览文件目录并直接选择证书。

添加证书后，将显示“ *事件注册* ”选项。 单击“ **添加事件注册**”。

![集成详细信息](../images/quality/subscribe-events/create_integration_details.png)

事件注 *册详细信息对话框* ，将展开以显示其他控件。 您可以在此选择所需的事件类型并注册Webhook。 输入事件注册的名称、Webhook URL *（可选）*，以及简短说明。 最后，选择要订阅的事件类型（数据摄取通知），然后单击保 **存**。

![选择事件](../images/quality/subscribe-events/create_integration_select_event.png)

## 后续步骤

创建I/O集成后，您可以视图收到的该集成通知。 有关如何跟 [踪您的事件的详细说明](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) ，请参阅跟踪Adobe I/O事件指南。
