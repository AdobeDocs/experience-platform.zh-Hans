---
title: Adobe Experience Platform中的数据加密
description: 了解如何在Adobe Experience Platform中加密传输数据和静态数据。
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: 4f67df5d3667218c79504535534de57f871b0650
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---

# Adobe Experience Platform中的数据加密

Adobe Experience Platform是一款功能强大且可扩展的系统，可跨企业解决方案集中化和标准化客户体验数据。 Platform使用的所有数据在传输和静止时都经过加密，以确保您的数据安全。 本文档从较高层面介绍了Platform的加密过程。

以下流程图说明了Experience Platform如何摄取、加密和保留数据：

![一个图表，说明如何通过Experience Platform摄取、加密和保留数据。](../images/governance-privacy-security/encryption/flow.png)

## 正在传输的数据 {#in-transit}

Platform与任何外部组件之间传输的所有数据都是使用HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246)通过安全的加密连接传输的。

通常，数据可通过三种方式引入Platform：

- [数据收集](../../collection/home.md)功能允许网站和移动应用程序将数据发送到PlatformEdge Network以进行暂存和摄取准备。
- [Source连接器](../../sources/home.md)从Adobe Experience Cloud应用程序和其他企业数据源直接将数据流式传输到Platform。
- 非AdobeETL （提取、转换、加载）工具将数据发送到[批处理摄取API](../../ingestion/batch-ingestion/overview.md)以供使用。

将数据导入系统并[静态加密](#at-rest)后，Platform服务通过以下方式扩充和导出数据：

- [目标](../../destinations/home.md)允许您激活数据以Adobe应用程序和合作伙伴应用程序。
- 本机平台应用程序(如[Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=zh-Hans)和[Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/ajo-home))也可以使用数据。

### mTLS协议支持 {#mtls-protocol-support}

您现在可以使用相互传输层安全性(mTLS)来确保到[HTTP API目标](../../destinations/catalog/streaming/http-destination.md)和Adobe Journey Optimizer [自定义操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions)的出站连接中的增强安全性。 mTLS是一种用于相互身份验证的端到端安全方法，可确保共享信息的双方在数据共享之前都是声称的身份。 与TLS相比，mTLS还包括一个附加步骤，在该步骤中，服务器还会请求客户端的证书并在其末尾验证它。

如果要[将mTLS与Adobe Journey Optimizer自定义操作](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/configuration/configure-journeys/action-journeys/about-custom-action-configuration)和Experience PlatformHTTP API目标工作流一起使用，则置入Adobe Journey Optimizer客户操作UI或目标UI的服务器地址必须禁用TLS协议，并且仅启用mTLS。 如果该端点上仍启用TLS 1.2协议，则不会为客户端身份验证发送证书。 这意味着，要将mTLS与这些工作流一起使用，您的“接收”服务器终结点必须是mTLS **仅限**&#x200B;启用的连接终结点。

>[!IMPORTANT]
>
>在激活mTLS的Adobe Journey Optimizer自定义操作或HTTP API目标中不需要任何其他配置；当检测到启用了mTLS的端点时，此过程会自动发生。 每个证书的通用名称(CN)和使用者可选名称(SAN)都作为证书的一部分在文档中提供，并且您可以根据需要用作所有权验证的附加层。
>
>2000年5月发布的RFC 2818不再使用HTTPS证书中的公用名(CN)字段进行使用者名称验证。 它建议改用“dns名称”类型的“使用者可选名称”扩展(SAN)。

### 下载证书 {#download-certificates}

>[!NOTE]
>
>您有责任使公共证书保持最新。 请确保您定期查看证书，尤其是在证书到期日期临近时。 您应该将此页面加入书签，以便在环境中保留最新副本。

如果要检查CN或SAN进行其他第三方验证，可以在此处下载相关证书：

- [Adobe Journey Optimizer公共证书](../images/governance-privacy-security/encryption/AJO-public-certificate.pem)
- [目标服务公共证书](../images/governance-privacy-security/encryption/destinations-public-cert.pem)。

## 静态数据 {#at-rest}

Platform摄取和使用的数据存储在数据湖中，这是一个高度精细化的数据存储，包含由系统管理的所有数据，而不管原始数据或文件格式如何。 数据湖中保留的所有数据都将在您的组织独有的独立[[!DNL Microsoft Azure Data Lake] 存储](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction)实例中进行加密、存储和管理。

有关如何在Azure Data Lake Storage中加密静态数据的详细信息，请参阅[Azure官方文档](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption)。

## 后续步骤

本文档提供了如何在Platform中加密数据的高级概述。 有关Platform中安全程序的更多信息，请参阅Experience League上的[治理、隐私和安全性](./overview.md)概述，或查看[Platform安全白皮书](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf)。
