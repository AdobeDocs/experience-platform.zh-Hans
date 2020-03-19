---
title: 管理概述
seo-title: 实时CDP管理概述
description: 描述
seo-description: seo描述
translation-type: tm+mt
source-git-commit: 33e187053790b98d2f1c36306b38c738833c4659

---


# 实时CDP管理概述

本文档概述了由Adobe Experience Platform提供支持的实时客户数据平台的管理功能。

Experience Platform允许管理员管理基于角色的用户访问控制，以及管理用于应用程序开发的虚拟沙箱。

以下各节介绍了Experience Platform管理功能的中心组件，并包括指向Experience Platform文档的链接，其中提供了更多详细信息。

## 访问控制

访问控制通过 [Adobe Admin Console进行管理](http://adminconsole.adobe.com)。 此功能利用Admin Console中的产品配置，允许您将用户与权限和沙箱关联。 使用此功能，管理员可以授予或限制对已定义用户集的特定实时CDP功能的访问权限。

要了解有关访问控制的更多信息，请参 [阅Experience Platform文档中的](https://www.adobe.io/apis/experienceplatform/home/permissions-and-sandboxes/permissions-and-sandboxes.html#!api-specification/markdown/narrative/technical_overview/access-control/access-control-overview.md) “访问控制”概述。

>[!IMPORTANT]
>有关授予对实时CDP功能的访问权限（包括启用UI中的可见性）的详细指南，请遵循 [access control user guide](https://www.adobe.io/apis/experienceplatform/home/permissions-and-sandboxes/permissions-and-sandboxes.html#!api-specification/markdown/narrative/technical_overview/access-control/access-control-user-guide.md)（特别是用于管理产品配置的详细信息和其他服务）中提供的步骤。

## 沙箱

Adobe Experience Platform(以及实时CDP（扩展）)旨在在全球范围内丰富数字体验应用程序。 公司通常并行运行多个数字体验应用程序，并且需要满足这些应用程序的开发、测试和部署的需要，同时确保操作合规性。

为满足这一需求，Adobe Experience Platform提供了“沙箱”，使您能够将单个Platform实例分区到单独的虚拟环境中，这些环境可用于开发和改进数字体验应用程序。

有关沙箱的详细信息，请参阅 [Experience Platform文档中](https://www.adobe.io/apis/experienceplatform/home/permissions-and-sandboxes/permissions-and-sandboxes.html#!api-specification/markdown/narrative/technical_overview/sandboxes/sandboxes-overview.md) 的沙箱概述。