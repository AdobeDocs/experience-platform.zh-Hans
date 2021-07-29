---
title: 为扩展创建Exchange列表
description: 了解如何在Adobe Experience Platform中将扩展添加到公共目录。
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 28%

---

# 为扩展创建Exchange列表

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，在产品文档中推出了一些术语更改。 有关术语更改的统一参考，请参阅以下[文档](../../term-updates.md)。

Adobe Experience Platform有一个统一的目录，用户可以在其中查看可用于安装的标记扩展。 此目录在产品中可用，其中包含三种类型的扩展：

1. **公共扩展**:这些是已完成的扩展，专为任何用户生产使用。
1. **专用扩展**:这些是为生产而设计的已完成扩展，但是由公司中的其他用户开发的，仅供公司中的用户使用。
1. **开发扩展**:这些扩展处于活动开发状态，且仅在您的公司内部以及专门指定为开发资产的资产上可用。

与产品目录中的扩展不同，某些扩展的[Experience CloudExchange Marketplace](https://exchange.adobe.com/experiencecloud.experience-platform-launch.html#product)中也有列表。

这些列表允许扩展开发人员发布功能描述，提供指向其他支持和文档的链接，以及向可能不了解您的公司或扩展功能的潜在用户营销扩展。 在此商城中，您的扩展将有一个公开列表，用户无需通过Platform身份验证即可查看该列表。  许多开发人员发现开发Exchange列表很有益，但这并非必要步骤。

如果您没有公司可以上传和测试扩展包，则应注册Exchange计划并开始列表。  这将触发公司帐户的创建（需要一些时间，完成此操作后您将收到一封电子邮件），您可以使用它上传和测试扩展。  你从来不必公开上市。

如果您已经拥有公司帐户，或者如果您不打算完成列表，则可以跳过此步骤的其余部分，继续[上传和测试扩展](./upload-and-test.md)。

## 创建列表

>[!NOTE]
>
>以下流程详细说明了如何在Adobe交换程序中创建应用程序列表。 这是用于Adobe Experience Platform中各种集成和扩展的术语。

![Experience Cloud应用程序管理器链接位置](../images/getting-started/app-mgr-link.png)

1. 登录到 [Exchange 合作伙伴网站](https://partners.adobe.com/exchangeprogram/experiencecloud)。登录后，选择您姓名旁边的&#x200B;**App Manager**&#x200B;链接。
1. 选择&#x200B;**创建新应用程序**&#x200B;选项卡，然后为自定义解决方案选择&#x200B;**创建新应用程序** ，或选择适用的模板。
1. 提供列表信息。有关应用程序管理器的详细信息，请参阅完整的[文章](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360024197931)。列出信息应当非常明确扩展的功能以及其用途。 列表可用作应用程序的营销空间。 在此处提升扩展，使用清晰的描述、指向网站登陆页面的链接、指向帮助文档的链接或支持电子邮件地址，等等。 尽管扩展视图的空间有限，但Exchange列表仍为您提供了推广扩展和提升公司的机会。 以下是改进扩展推广的建议：
   - **应用程序图标** - 确保用于 Exchange 列表的图标具有适当的尺寸，对于 png 图像，尺寸为 512 x 512；或者，对于 jpg 图像，长宽比为 1:1。

   >[!NOTE]
   >
   >这是与扩展代码中使用的文件格式不同。 扩展本身将包含 svg 文件作为[图标](../manifest.md)。

   - **特色图像**  — 使用可独立显示您的品牌并突出显示您的应用程序的图像，吸引关注。 特色图像是指当某人共享指向您的Exchange列表的链接或在社交媒体上发布有关该列表的信息时显示的图像。 因此，它必须是品牌的模型表示形式。
   - **应用程序发布者的徽标** - 这是您公司的徽标，请确保该图标具有适当的尺寸，即，1280 x 720 或 2560 x 1440 (16:9) 的 png 或 jpg 格式。
   - **配置说明**  — 告知客户如何配置您的Adobe Experience Platform扩展。当客户在资产中安装了您的扩展后，您的[配置视图](../configuration.md)会立即显示，请确保客户了解所有必需的设置和后续步骤。
   - **标记** - 在编辑列表的第一页，请确保在“自定义标记”字段中包含“Launch”一词。这样，您的列表便会显示在Exchange商城中标记的搜索中：
      ![](../images/getting-started/custom-tags.jpg)
   - **沙盒**  — 您对Adobe解决方案的访问是通过沙盒帐户进行的，您可以在该帐户中访问正常运行的Adobe Experience Platform版本。您可以在创建应用程序列表时申请这些沙盒帐户。在&#x200B;**连接**&#x200B;部分中，选择适用于您创建的应用程序（您的标记扩展）的特定连接，并点击&#x200B;**保存**&#x200B;时，将根据需要生成沙盒请求。
1. 提交列表。 Adobe Exchange 团队将审核您的应用程序，并在需要更新时向您提供反馈。如果您在提交列表时选中了&#x200B;**立即发布**&#x200B;复选框，则该列表将在获得批准后立即发布。 如果您希望稍后发布应用程序，请取消选中该复选框。当您的扩展列表获得批准后，该列表旁边会显示一个蓝色的&#x200B;**Publish**&#x200B;按钮，位于您的应用程序（扩展）列表页面上。

### 创建有效列表

请查看[应用程序提交指南](https://partners.adobe.com/exchangeprogram/experiencecloud/build/ec-exchange.html) ，以详细了解如何创建最引人注目的列表。

#### 提交 Exchange 列表后

提交列表后，Adobe Exchange 团队会审核相关应用程序，审核结果要么是批准该应用程序，要么是提出更改意见。应用程序提交指南详细介绍了此过程。

如果您未登录过 Exchange 网站，请按照[计划注册指南](https://partners.adobe.com/content/mcp/us/en/home/reg-guide.html)中的说明，确保注册您的电子邮件地址以加入 Exchange 计划。每个用户必须将其电子邮件与公司的合作伙伴帐户关联。 有关此过程的问题可通过电子邮件发送至<ExchangeHelpEC@adobe.com>。

#### 在获得初步批准后更新您的 Exchange 列表

当您更新扩展或者只是需要更新 Exchange 列表时，请登录到[合作伙伴门户](https://partners.adobe.com/exchangeprogram/experiencecloud)，然后选择您姓名旁边的“应用程序管理器”按钮。接下来，选择您的应用程序，并按照上面介绍的最初用于创建列表的流程来执行操作。重新提交后，Adobe Exchange 团队会审核更改情况，并将批准更改，或对更改情况提出意见。

## 将扩展包链接到列表

在您的列表获得批准并公开可用后，我们建议您在扩展包内`extension.json`文件的`exchange_url`字段中提供一个指向公共列表的链接。  这将在标记扩展目录中创建“更多信息”链接，以便产品中的用户能够找到您的列表及其附加信息。
