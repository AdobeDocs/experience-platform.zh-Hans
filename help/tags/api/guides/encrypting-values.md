---
title: 加密值
description: 了解如何在使用Reactor API时加密敏感值。
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---

# 加密值

在Adobe Experience Platform中使用标记时，某些工作流需要提供敏感值（例如，在通过主机将库交付到环境时提供私钥）。 这些全权证书的敏感性质需要
安全传输和存储。

本文档介绍如何使用[GnuPG加密](https://www.gnupg.org/gph/en/manual/x110.html)（也称为GPG）加密敏感值，以便只有标签系统可以读取这些值。

## 获取公共GPG密钥和校验和

在[下载](https://gnupg.org/download/)并安装最新版本的GPG后，必须获取标记生产环境的公共GPG密钥：

* [GPG密钥](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg)
* [校验和](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg.sum)

## 将密钥导入密钥链

将密钥保存到计算机后，下一步是将其添加到GPG密钥链。

**语法**

```shell
gpg --import {KEY_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{KEY_NAME}` | 公钥文件的名称。 |

{style=&quot;table-layout:auto&quot;}

**示例**

```shell
gpg --import launch@adobe.com_pub.gpg
```

## 加密值

将密钥添加到密钥链后，可以使用`--encrypt`标记开始加密值。 以下脚本演示了此命令的工作方式：

```shell
echo -n 'Example value' | gpg --armor --encrypt -r "Tags Data Encryption <launch@adobe.com>"
```

此命令可按如下方式划分：

* 输入内容被提供给`gpg`命令。
* `--armor` 创建ASCII装甲输出，而不是二进制。这简化了通过JSON传输值的过程。
* `--encrypt` 指示GPG加密数据。
* `-r` 设置数据的收件人。只有收件人（与公钥对应的私钥的持有者）才能解密数据。 通过检查`gpg --list-keys`的输出，可以找到所需密钥的收件人名称。

以上命令使用`Tags Data Encryption <launch@adobe.com>`的公钥以ASCII装甲格式加密值`Example value`。

该命令的输出将类似于以下内容：

```shell
-----BEGIN PGP MESSAGE-----

hQIMAxJHCI6fydT/ARAAwQ0Y0k7eSAbd0T9seoaWX75G70O2gxAF20KY5FWiZ9/m
/RkgJwhJusZyEdazC/CmAdfXi9bsVxQT0i06ErUxXfQF0VtweRlcyRBsxzLz6Hr+
BpYGnq+cCCzGAT73Gg1CM4UWmaPKLLyWKGkXtDBAqVBRAIQT/8JhnkbyWIohHkWV
I/Uf7NrPXuaSmrqZ1SZQgwjIM3qNMR02qtqg59dncKoCQBji8Oeb8lqRLskRT0Jq
gVgbJYwSe2n6KpJkELJ6QtF9lCRl1+yU4mvM4jBHgkM1+vb1WmbFRIR40dDpg85N
0J9hVj4bg//eLRDfAdEC9kgq9Atph0WqJ5EpehdS7yVO9lO8mpbpqZ4BCGjTi/VS
isEPr6eZ2mxRbk8f9Z4csRZnkErY8ep5+cqC5CZVdmguWvC9PKzXqEsPFd0PSYk3
Qp3UIW2/JMf16E5CKmntm+gKdl6kggZOOvNQuyJYa9yNbzySPerHXsknTOxV+QP/
WXwrAL52g5+gpMib7Ve/KBz5/OViDhDqkmHzlGad73W74d+CYjf0AnuXuWRRlUMT
s8ORw1eplInldhXk2mgkGPZS/gWDs3zpKUu4GSO9AaeWldynLG/Bgh78XhumQ58h
ekGD+p3PyyvxjfS5G/wf9HQZ085+mnjpKFa7fuFBQPbg4WpBadhWrhobthC+hN3S
SAE9yWU11Y3xpoxqg4y7iYZ6rnX+qP2oUNYxC2/hdhsFbbZtUh4s51qaoLbe0iWB
OUoIPf4KxTaboHZOEy32ZBng5heVrn4i9w==
=jrfE
-----END PGP MESSAGE-----
```

此输出只能由具有私钥的系统解密
对应于`Tags Data Encryption <launch@adobe.com>`公钥。

此输出是向Reactor API发送数据时应在中提供的值。 系统存储此加密输出，并根据需要临时解密。 例如，系统解密足够长的主机凭据以启动与服务器的连接，然后立即删除解密值的所有迹线。

>[!NOTE]
>
>装甲、加密值的格式很重要。 确保在请求中提供的值中正确转义行返回。
