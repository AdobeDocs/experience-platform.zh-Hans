---
title: 为扩展创建Exchange列表
description: 了解如何将扩展添加到Adobe Experience Platform中的公共目录。
exl-id: 0395fc99-5e2b-46d6-a067-f8f167733e02
source-git-commit: 0d98183838125fac66768b94bc1993bde9a374b5
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 24%

---

# 为扩展创建Exchange列表

>[!NOTE]
>
>经过品牌重塑，Adobe Experience Platform Launch 已变为 Adobe Experience Platform 中的一套数据收集技术。因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

Adobe Experience Platform具有单个统一的目录，用户可以在其中查看可用于安装的标记扩展。 此目录在产品中提供，并包含三种类型的扩展：

1. **公共扩展**：这些扩展是专为任何用户生产使用而设计的完整扩展。
1. **私有扩展**：这些是专为生产而设计的完整扩展，但由公司中的其他用户开发，仅对公司内的用户可用。
1. **开发扩展**：这些扩展正在开发中，仅在公司内可用，并且仅在特别指定为开发资产的资产上可用。

除了产品目录中的扩展之外，公共扩展在[Experience Cloud Exchange应用程序市场](https://exchange.adobe.com/apps/browse/ec)中也有列表。

利用这些列表，扩展开发人员可以发布功能描述，提供指向其他支持和文档的链接，并向可能不知道您的公司或扩展功能的潜在用户营销扩展。 在该商城中，您的扩展将有一个可供查看的公开列表，用户无需进行Platform身份验证即可查看。 对于公共扩展，创建此Exchange列表是必需步骤。

>[!TIP]
>
>发布Exchange列表后，将自动向列表内容添加一个链接，通过该链接，您的客户和潜在客户可以单击和`Connect with publisher`，以了解有关您的产品和服务的更多信息。 不会显示您的联系电子邮件地址，因为这些邮件将由Exchange系统转发给您。

如果您没有公司可以上传和测试扩展包，则您应该注册Exchange计划并开始列表。 这将触发公司帐户的创建（需要一些时间，完成后，您将收到一封电子邮件），您可以将其用于上传和测试扩展。 同样，Exchange列表仅对公共扩展是必需的。

如果您已经拥有公司帐户，或者您不需要Exchange列表（仅限私有扩展），则可以跳过此步骤的其余部分，继续进行[上载和测试扩展](./upload-and-test.md)。

## 创建列表

>[!NOTE]
>
>以下流程详细介绍了如何在Adobe Exchange程序中创建应用程序列表。 这是用于Adobe Experience Platform中各种集成和扩展的术语。

![Experience Cloud App Manager链接位置](../images/getting-started/app-mgr-link.png)

1. 登录到 [Exchange 合作伙伴网站](https://partners.adobe.com/exchangeprogram/experiencecloud)。登录后，选择您姓名旁边的&#x200B;**应用程序管理器**&#x200B;链接。
1. 选择&#x200B;**新建应用程序**&#x200B;选项卡，然后为自定义解决方案选择&#x200B;**新建应用程序**，或者选择适用的模板。
1. 提供列表信息。有关应用程序管理器的详细信息，请查看完整的[文章](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360024197931)。 列表信息应非常清楚扩展的功能及其用途。 列表可用作应用程序的营销空间。 通过清晰的描述、指向网站上登陆页面的链接、指向帮助文档的链接或支持电子邮件地址等，在此处推广您的扩展。 尽管扩展视图中的空间有限，但Exchange列表提供了同时推广您的扩展和您的公司的机会。 以下是有关改进扩展促销活动的建议：
   - **应用程序图标** — 确保用于Exchange列表的图标具有适当的尺寸，对于png图像，尺寸为512 x 512；或者，对于jpg图像，长宽比为1:1。

     >[!NOTE]
     >
     >这与扩展代码中使用的文件格式不同。 扩展本身将包含 svg 文件作为[图标](../manifest.md)。

   - **精选图像** — 使用可单独显示您的品牌并突出显示您的应用程序的图像来吸引关注。 特色图像是人们在共享您的Exchange列表链接或在社交媒体上发布有关该列表的帖子时显示的图像。 因此，它需要成为您品牌的模型表示形式。
   - **应用程序发布者的徽标** - 这是您公司的徽标，请确保该图标具有适当的尺寸，即，1280 x 720 或 2560 x 1440 (16:9) 的 png 或 jpg 格式。
   - **配置说明** — 告知客户如何配置Adobe Experience Platform扩展。 当客户在资产中安装了您的扩展后立即显示[配置视图](../configuration.md)时，请确保客户了解所有必需的设置和后续步骤。
   - **标记** - 在编辑列表的第一页，请确保在“自定义标记”字段中包含“Launch”一词。这将使您的列表显示在Exchange Marketplace的标记搜索中：
     ![](../images/getting-started/custom-tags.jpg)
   - **沙盒** — 您对Adobe解决方案的访问是通过沙盒帐户进行的，您可以在其中访问功能齐全的Adobe Experience Platform版本。 您可以在创建应用程序列表时申请这些沙盒帐户。在&#x200B;**连接**&#x200B;部分选择适用于您创建的应用程序（标记扩展）的特定连接，当您点击&#x200B;**保存**&#x200B;时，将根据需要生成沙盒请求。
1. 提交列表。 Adobe Exchange 团队将审核您的应用程序，并在需要更新时向您提供反馈。如果您在提交列表时选中了&#x200B;**立即发布**&#x200B;复选框，则该列表会在获得批准后立即发布。 如果您希望稍后发布应用程序，请取消选中该复选框。 扩展列表获得批准后，您的应用程序（扩展）列表页面上会在该列表旁边显示一个蓝色的&#x200B;**发布**&#x200B;按钮。

### 创建有效列表

请查看[应用程序提交指南](https://partners.adobe.com/exchangeprogram/experiencecloud/build/ec-exchange.html)，详细了解如何创建最引人注目的列表。

#### 提交 Exchange 列表后

提交列表后，Adobe Exchange 团队会审核相关应用程序，审核结果要么是批准该应用程序，要么是提出更改意见。应用程序提交指南详细介绍了此过程。

如果您未登录过 Exchange 网站，请按照[计划注册指南](https://partners.adobe.com/content/mcp/us/en/home/reg-guide.html)中的说明，确保注册您的电子邮件地址以加入 Exchange 计划。每个用户都必须将其电子邮件与公司的合作伙伴帐户关联。 有关此进程的问题可通过电子邮件发送至<ExchangeHelpEC@adobe.com>。

#### 在获得初步批准后更新您的 Exchange 列表

当您更新扩展或者只是需要更新 Exchange 列表时，请登录到[合作伙伴门户](https://partners.adobe.com/exchangeprogram/experiencecloud)，然后选择您姓名旁边的“应用程序管理器”按钮。接下来，选择您的应用程序，并按照上面介绍的最初用于创建列表的流程来执行操作。重新提交后，Adobe Exchange 团队会审核更改情况，并将批准更改，或对更改情况提出意见。

## 将扩展包链接到列表

您的列表获得批准并公开后，我们建议您在扩展包中的`extension.json`文件的`exchange_url`字段中提供指向公开列表的链接。  这将在标记扩展目录中创建一个“更多信息”链接，以便产品中的用户能够找到您的列表及其中的额外信息。
