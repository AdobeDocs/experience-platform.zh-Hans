---
description: Adobe Experience Platform中的目标服务对构建目标功能的多个组件使用配置端点。 了解这些组件如何组合使Experience Platform能够在数字生态系统中连接到目标合作伙伴、发送自定义消息并激活配置文件数据。
title: Destination SDK中的配置选项
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---

# Destination SDK中的配置选项

Adobe Experience Platform中的目标服务对构建目标功能的多个组件使用配置端点。

通过结合这些组件，Experience Platform可以连接到目标平台、发送自定义消息、导出自定义文件并在数字生态系统中激活配置文件数据。

下图显示您可以通过Destination SDK配置以构建您自己的目标的组件的高级概述。 这些组件将在下面进一步说明。

>[!BEGINSHADEBOX]

![显示Destination SDK组件、配置端点及其支持的操作的图表。](../assets/functionality/destination-sdk-components-diagram.png){zoomable="yes"}

>[!ENDSHADEBOX]

## 服务器配置 {#server-configuration}

目标服务器配置将有关服务器规范的信息与Adobe用于将负载交付到目标所使用的模板绑定在一起。

例如，您可以在此处指定Experience Platform需要连接到的API端点，以及Experience Platform将进行的API调用的标题和格式。

对于基于文件的目标，此配置还包括目标支持的文件格式和压缩格式。 您可以通过[destination-servers终结点](../authoring-api/destination-server/create-destination-server.md)配置下述功能。

* [服务器规范](destination-server/server-specs.md)：配置模板，其中包含有关数据发送到的存储位置或HTTP终结点的信息。
* [模板规范](destination-server/templating-specs.md)：在此模板中，您可以定义如何构造指向端点的HTTP API请求，包括如何在XDM架构和平台支持的格式之间转换配置文件属性字段。 将此信息与[消息格式](destination-server/message-format.md)文档一起使用。
* [消息格式](destination-server/message-format.md)：本节将深入介绍支持的模板语言、消息格式以及Adobe设置与您的平台集成所需的信息。 请将此信息与[模板规范](destination-server/templating-specs.md)文档一起使用。
* [文件规范](destination-server/file-formatting.md)：包含批处理目标文件格式和压缩选项的配置模板。

## 目标配置 {#destination-configuration}

此配置端点包含有关目标的基本和高级信息。 例如，您可以在此处指定目标可以支持的身份类型、所需的导出文件格式（适用于基于文件的目标）以及Adobe Experience Platform用户界面中目标卡的各种UI属性。

有关每个目标配置组件的详细信息，请参阅下面的文档。 您可以通过[目标终结点](../authoring-api/destination-configuration/create-destination-configuration.md)配置下述功能。

* [客户身份验证配置](destination-configuration/customer-authentication.md)：选择Experience Platform应用于连接到目标的身份验证机制。 此配置会在Experience Platform用户界面中生成[配置新目标](../../ui/connect-destination.md)页面，用户可在此页面中将Experience Platform连接到他们在您的目标中拥有的帐户。
* [OAuth2授权](destination-configuration/oauth2-authorization.md)：了解Destination SDK支持的所有[!DNL OAuth2]身份验证流程，并获取有关为您的目标设置[!DNL OAuth2]身份验证的说明。
* [客户数据字段](destination-configuration/customer-data-fields.md)：了解如何在Experience Platform UI中创建输入字段，以允许用户指定与如何连接数据并将其导出到目标相关的各种信息。
* [UI属性](destination-configuration/ui-attributes.md)：了解如何为使用Destination SDK构建的目标配置UI属性，如文档链接、目标卡类别以及目标连接类型和频率。
* [架构配置](destination-configuration/schema-configuration.md)：了解如何定义用户可将配置文件属性和身份映射到目标的目标架构。
* [身份命名空间配置](destination-configuration/identity-namespace-configuration.md)：了解如何配置目标支持的身份。 此配置填充Experience Platform用户界面的[映射步骤](../../ui/activate-segment-streaming-destinations.md#mapping)中的目标身份，在该步骤中，用户将其XDM架构中的身份和属性映射到目标中的架构。
* [目标投放](destination-configuration/destination-delivery.md)：了解如何配置导出数据的确切位置以及在数据登陆位置使用的身份验证规则。
* [受众元数据配置](destination-configuration/audience-metadata-configuration.md)：了解受众名称或ID等受众元数据应如何在Experience Platform与您的目标之间共享。
* [聚合策略](destination-configuration/aggregation-policy.md)：了解如何设置聚合策略，以确定应如何对发往目标的HTTP请求进行分组和批处理。
* [批处理配置](destination-configuration/batch-configuration.md)：在Experience Platform用户界面中设置用户可以使用的各种文件命名和导出计划设置。
* [历史配置文件资格](destination-configuration/historical-profile-qualifications.md)：了解使用Destination SDK构建的目标所支持的历史配置文件资格。

## 受众元数据配置 {#audience-metadata-configuration}

利用此组件，可配置在您的目标中以编程方式创建、更新或删除受众的方式。 对于基于文件的目标，它允许您在文件成功传送到目标时设置通知。 您可以通过[受众模板端点](../metadata-api/create-audience-template.md)配置此功能。

## 后续步骤 {#next-steps}

通过阅读本文，您现在可以概括了解Destination SDK提供的功能，以及要阅读哪些页面以了解有关特定配置的更多信息。 接下来，您可以阅读包含使用Destination SDK [配置流式传输](../guides/configure-destination-instructions.md)或[基于文件的目标](../guides/configure-file-based-destination-instructions.md)的所有步骤的指南。
