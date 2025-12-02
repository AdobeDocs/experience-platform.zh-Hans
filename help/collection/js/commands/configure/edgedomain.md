---
title: edgeDomain
description: 确定要将数据发送到的根域。
exl-id: 6beb5116-cd23-42fd-934c-5cf84d1d7153
source-git-commit: 09799847c61d82ed5b7cd372d92aa436697d54f3
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 3%

---

# `edgeDomain`

`edgeDomain`属性允许您更改Web SDK发送数据的域。 此属性经常由使用[第一方Cookie](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=zh-Hans)的组织使用。 数据会发送到组织自己的域，然后CNAME记录会将该数据转发到Adobe。

您为`edgeDomain`使用的值取决于您对[Adobe管理的证书计划](https://experienceleague.adobe.com/zh-hans/docs/core-services/interface/data-collection/adobe-managed-cert)的参与情况：

**如果您的组织参与了Adobe管理的证书计划**，请将该值设置为设置证书时选择的第一方域。 通常此值是您的组织拥有的子域。 例如：`data.example.com`。贵组织中的CNAME记录将该数据重定向到Adobe。

**如果不参与证书计划**，则将该值设置为`data.adobedc.net`的子域。 Adobe建议使用贵组织的公司ID来保持一致性。 例如：`example.data.adobedc.net`。使用以下步骤可确定您的公司ID：

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 在Experience Cloud界面中的任意位置，按`[Cmd]` + `[I]` (iOS)或`[Ctrl]` + `[I]` (Windows)。
1. 出现&#x200B;**[!UICONTROL User data debugger]**。 选择 **[!UICONTROL Assigned orgs]** 选项卡。
1. 展开所需的IMS组织。
1. 找到&#x200B;**[!UICONTROL Tenant]**&#x200B;字段。 建议使用`data.adobedc.net`的子域使用此值。

运行`edgeDomain`命令时设置`configure`字符串。 如果在配置SDK时省略此属性，则默认设置为`edge.adobedc.net`。 虽然默认值是可接受的，但Adobe认为最佳实践是设置特定于组织的值。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeDomain: "data.example.com"
});
```

## 使用Web SDK标记扩展的Edge域

与此属性等效的标记扩展是配置扩展时&#x200B;**[!UICONTROL Edge domain]** SDK实例配置设置[下的](/help/tags/extensions/client/web-sdk/configure/general.md)字段。
