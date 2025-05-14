---
title: Adobe Experience Platform中的数据加密
description: 了解如何在Adobe Experience Platform中加密传输数据和静态数据。
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: f6eaba4c0622318ba713c562ba0a4c20bba02338
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# Adobe Experience Platform中的数据加密

Adobe Experience Platform是一款功能强大且可扩展的系统，可跨企业解决方案集中化和标准化客户体验数据。 Experience Platform使用的所有数据在传输和静止时都经过加密，以确保您的数据安全。 本文档从较高层面介绍了Experience Platform的加密过程。

以下流程图说明了Experience Platform如何摄取、加密和保留数据：

![一个图表，说明如何通过Experience Platform摄取、加密和保留数据。](../images/governance-privacy-security/encryption/flow.png)

## 正在传输的数据 {#in-transit}

Experience Platform与任何外部组件之间传输的所有数据均使用HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246)通过安全的加密连接进行。

通常，数据可通过三种方式引入Experience Platform：

- [数据收集](../../collection/home.md)功能允许网站和移动应用程序将数据发送到Experience Platform Edge Network以进行暂存和摄取准备。
- [Source连接器](../../sources/home.md)从Adobe Experience Cloud应用程序和其他企业数据源直接将数据流式传输到Experience Platform。
- 非Adobe ETL（提取、转换、加载）工具将数据发送到[批量摄取API](../../ingestion/batch-ingestion/overview.md)以供使用。

将数据导入系统并[静态加密](#at-rest)后，Experience Platform服务通过以下方式扩充和导出数据：

- [目标](../../destinations/home.md)允许您向Adobe应用程序和合作伙伴应用程序激活数据。
- 本机Experience Platform应用程序(如[Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=zh-Hans)和[Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/ajo-home))也可以使用数据。

### mTLS协议支持 {#mtls-protocol-support}

您现在可以使用相互传输层安全性(mTLS)来确保到[HTTP API目标](../../destinations/catalog/streaming/http-destination.md)和Adobe Journey Optimizer [自定义操作](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions)的出站连接中的增强安全性。 mTLS是一种用于相互身份验证的端到端安全方法，可确保共享信息的双方在数据共享之前都是声称的身份。 与TLS相比，mTLS还包括一个附加步骤，在该步骤中，服务器还会请求客户端的证书并在其末尾验证它。

如果要[将mTLS与Adobe Journey Optimizer自定义操作](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/configuration/configure-journeys/action-journeys/about-custom-action-configuration)和Experience Platform HTTP API目标工作流一起使用，则置入Adobe Journey Optimizer客户操作UI或目标UI的服务器地址必须禁用TLS协议，并且仅启用mTLS。 如果该端点上仍启用TLS 1.2协议，则不会为客户端身份验证发送证书。 这意味着，要将mTLS与这些工作流一起使用，您的“接收”服务器终结点必须是mTLS **仅限**&#x200B;启用的连接终结点。

>[!IMPORTANT]
>
>在激活mTLS的Adobe Journey Optimizer自定义操作或HTTP API目标中不需要任何其他配置；当检测到启用了mTLS的端点时，此过程会自动发生。 每个证书的通用名称(CN)和使用者可选名称(SAN)都作为证书的一部分在文档中提供，并且您可以根据需要用作所有权验证的附加层。
>
>2000年5月发布的RFC 2818不再使用HTTPS证书中的公用名(CN)字段进行使用者名称验证。 它建议改用“dns名称”类型的“使用者可选名称”扩展(SAN)。

### 下载证书 {#download-certificates}

>[!NOTE]
>
>您有责任确保您的系统使用有效的公共证书。 定期检查您的证书，尤其是在过期日期临近时。 使用API在证书过期之前检索和更新证书。

不再提供公共mTLS证书的直接下载链接。 请改用[公共证书终结点](../../data-governance/mtls-api/public-certificate-endpoint.md)来检索证书。 这是访问当前公共证书时唯一支持的方法。 它可确保您始终收到适用于集成的最新有效证书。

依赖基于证书的加密的集成必须更新其工作流，以支持使用API的自动证书检索。 依赖静态链接或手动更新可能会导致使用已过期或已吊销的证书，进而导致集成失败。

#### 证书生命周期自动化 {#certificate-lifecycle-automation}

Adobe现在可以自动化mTLS集成的证书生命周期，以提高可靠性并防止服务中断。 公共证书包括：

- 已重新发布60天后过期。
- 过期前30天撤销。

这些间隔将继续缩短，以符合[不断演变的CA/B论坛准则](https://www.digicert.com/blog/tls-certificate-lifetimes-will-officially-reduce-to-47-days)，该准则旨在将证书生命周期减少到最多47天。

如果您之前使用此页面上的链接来下载证书，请更新您的流程，以通过API专门检索它们。

## 静态数据 {#at-rest}

Experience Platform摄取和使用的数据存储在数据湖中，这是一个高度精细化的数据存储，包含由系统管理的所有数据，而不管是源数据还是文件格式。 数据湖中保留的所有数据都将在您的组织独有的独立[[!DNL Microsoft Azure Data Lake] 存储](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction)实例中进行加密、存储和管理。

有关如何在Azure Data Lake Storage中加密静态数据的详细信息，请参阅[Azure官方文档](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption)。

## 后续步骤

本文档提供了如何在Experience Platform中加密数据的高级概述。 有关Experience Platform中安全程序的更多信息，请参阅Experience League上的[治理、隐私和安全性](./overview.md)概述，或查看[Experience Platform安全白皮书](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf)。
