---
title: 结束对Internet Explorer 10和11中的标记的支持
description: Adobe Experience Platform不再为Internet Explorer 10和11中的标记提供更新支持。
exl-id: 35491c80-2a8a-4e07-baa7-a5db373b6852
source-git-commit: 44e056407f5089c927752f00cc6bf173d7640b83
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# 结束对Internet Explorer 10和11中的标记的支持

随着在线数字体验环境的不断发展，Adobe不再投资资源来支持Adobe Experience Platform标记的Internet Explorer 10 (IE10)和Internet Explorer 11 (IE11)。 虽然Adobe没有主动取消对IE10和IE11的支持，但未来更新中将不再考虑这些浏览器对新功能的影响。

## 为什么不再支持IE10和IE11？

标记不再支持IE10和IE11的原因有四个：

* **Microsoft将停止对IE10和IE11的支持**：自2020年1月起， [Microsoft已停止支持IE10](https://docs.microsoft.com/en-us/lifecycle/announcements/internet-explorer-10-end-of-support) 进行安全性更新和非安全性更新。 截至2022年6月， [Microsoft已停止支持IE11](https://docs.microsoft.com/en-us/lifecycle/announcements/internet-explorer-11-end-of-support) 在特定版本的Windows上。
* **更广泛的行业正在停止对IE10和IE11的支持**：随着更广泛的行业停止支持IE10和IE11，标记与这些技术保持向后兼容性的能力日益受到阻碍。
* **现代技术不支持IE10和IE11**：要使标记继续支持最现代的技术，它必须终止对IE10和IE11的支持，因为这些现代技术与这些Web浏览器不兼容。
* **支持IE10和IE11会减慢总体功能开发的速度**：为标记发布的许多新功能需要仔细考虑IE10和IE11。 这种考量导致需要花费数小时的额外工作来获取可与IE10和IE11配合使用的难以找到的测试工具，添加额外的代码以使功能可与没有本机支持的IE10和IE11配合使用，并进行研究以确保功能按预期工作。 通过停止对IE10和IE11的支持，Adobe可以更快地提供新功能。

## IE10和IE11弃用的影响

弃用支持后，将发生以下影响：

* 新功能可能不支持IE10和IE11。
* 将停止测试使用IE10和IE11的当前功能支持和新功能支持。
* 以前支持IE10和IE11的功能可能不再支持这些浏览器。
