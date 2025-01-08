---
title: Salesforce Source Connector概述
description: 了解如何使用API或用户界面将Salesforce连接到Adobe Experience Platform。
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: 258e54b969e7b392eec97459e0a51931f2109fe7
workflow-type: tm+mt
source-wordcount: '1483'
ht-degree: 0%

---

# [!DNL Salesforce]

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

Experience Platform支持从第三方CRM系统中摄取数据。 CRM提供商的支持包括[!DNL Salesforce]。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于区域的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 有关详细信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页。

## 从[!DNL Salesforce]到XDM的字段映射

要建立[!DNL Salesforce]与Platform之间的源连接，[!DNL Salesforce]源数据字段必须在被引入Platform之前映射到其相应的目标XDM字段。

有关[!DNL Salesforce]数据集与Platform之间的字段映射规则的详细信息，请参阅以下内容：

- [联系人](../adobe-applications/mapping/salesforce.md#contact)
- [潜在客户](../adobe-applications/mapping/salesforce.md#lead)
- [帐户](../adobe-applications/mapping/salesforce.md#account)
- [机会](../adobe-applications/mapping/salesforce.md#opportunity)
- [机会联系人角色](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [营销活动](../adobe-applications/mapping/salesforce.md#campaign)
- [营销活动成员](../adobe-applications/mapping/salesforce.md#campaign-member)
- [帐户联系人关系](../adobe-applications/mapping/salesforce.md#account-contact-relation)

## 设置[!DNL Salesforce]命名空间和架构自动生成实用程序

要将[!DNL Salesforce]源用作[!DNL B2B-CDP]的一部分，您必须首先设置[!DNL Postman]实用工具以自动生成您的[!DNL Salesforce]命名空间和架构。 以下文档提供了有关设置[!DNL Postman]实用工具的其他信息：

- 您可以从此[GitHub存储库](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility)下载命名空间和架构自动生成实用程序集合和环境。
- 有关如何使用Platform API的信息，包括有关如何收集所需标头的值和读取示例API调用的详细信息，请参阅[Platform API快速入门](../../../landing/api-guide.md)指南。
- 有关如何为平台API生成凭据的信息，请参阅有关[身份验证和访问Experience PlatformAPI](../../../landing/api-authentication.md)的教程。
- 有关如何为平台API设置[!DNL Postman]的信息，请参阅[设置开发人员控制台和 [!DNL Postman]](../../../landing/postman.md)上的教程。

通过平台开发人员控制台和[!DNL Postman]设置，您现在可以开始将相应的环境值应用到您的[!DNL Postman]环境。

下表包含示例值以及有关填充[!DNL Postman]环境的其他信息：

| Variable | 描述 | 示例 |
| --- | --- | --- |
| `CLIENT_SECRET` | 用于生成`{ACCESS_TOKEN}`的唯一标识符。 有关如何检索`{CLIENT_SECRET}`的信息，请参阅有关[身份验证和访问Experience PlatformAPI](../../../landing/api-authentication.md)的教程。 | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web令牌(JWT)是用于生成{ACCESS_TOKEN}的身份验证凭据。 有关如何生成`{JWT_TOKEN}`的信息，请参阅有关[身份验证和访问Experience PlatformAPI](../../../landing/api-authentication.md)的教程。 | `{JWT_TOKEN}` |
| `API_KEY` | 用于对调用Experience PlatformAPI进行身份验证的唯一标识符。 有关如何检索`{API_KEY}`的信息，请参阅有关[身份验证和访问Experience PlatformAPI](../../../landing/api-authentication.md)的教程。 | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | 完成对Experience PlatformAPI的调用所需的授权令牌。 有关如何检索`{ACCESS_TOKEN}`的信息，请参阅有关[身份验证和访问Experience PlatformAPI](../../../landing/api-authentication.md)的教程。 | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | 对于[!DNL Marketo]，此值是固定的，并且始终设置为： `ent_dataservices_sdk`。 | `ent_dataservices_sdk` |
| `CONTAINER_ID` | `global`容器包含所有标准Adobe和Experience Platform合作伙伴提供的类、架构字段组、数据类型和架构。 对于[!DNL Marketo]，此值是固定的，并且始终设置为`global`。 | `global` |
| `PRIVATE_KEY` | 用于向Experience PlatformAPI验证您的[!DNL Postman]实例的凭据。 有关如何检索{PRIVATE_KEY}的说明，请参阅有关设置开发人员控制台和[设置开发人员控制台和 [!DNL Postman]](../../../landing/postman.md)的教程。 | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | 用于集成到Adobe I/O的凭据。 | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management System (IMS)提供了对Adobe服务进行身份验证的框架。 对于[!DNL Marketo]，此值是固定的，并且始终设置为： `ims-na1.adobelogin.com`。 | `ims-na1.adobelogin.com` |
| `IMS_ORG` | 公司实体，可以拥有产品或服务，也可以为其授予产品和服务许可证，并允许其成员访问。 有关如何检索`{ORG_ID}`信息的说明，请参阅有关[设置开发人员控制台和 [!DNL Postman]](../../../landing/postman.md)的教程。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | 您正在使用的虚拟沙盒分区的名称。 | `prod` |
| `TENANT_ID` | 一个ID，用于确保您创建的资源被正确命名并包含在您的组织内。 | `b2bcdpproductiontest` |
| `PLATFORM_URL` | 您对其进行API调用的URL端点。 此值是固定的，并且始终设置为： `http://platform.adobe.io/`。 | `http://platform.adobe.io/` |
| `munchkinId` | [!DNL Marketo]帐户的唯一ID。 有关如何检索`munchkinId`的信息，请参阅[验证 [!DNL Marketo] 实例](../adobe-applications/marketo/marketo-auth.md)的教程。 | `123-ABC-456` |
| `sfdc_org_id` | 您的[!DNL Salesforce]帐户的组织ID。 有关获取[!DNL Salesforce]组织ID的更多信息，请参阅以下[[!DNL Salesforce] 指南](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1)。 | `00D4W000000FgYJUA0` |
| `has_abm` | 一个布尔值，指示您是否订阅了[!DNL Marketo Account-Based Marketing]。 | `false` |
| `has_msi` | 一个布尔值，指示您是否订阅了[!DNL Marketo Sales Insight]。 | `false` |

{style="table-layout:auto"}

### 运行脚本

设置了[!DNL Postman]收藏集和环境后，您现在可以通过[!DNL Postman]界面运行脚本。

在[!DNL Postman]界面中，选择自动生成器实用工具的根文件夹，然后从顶部标题中选择&#x200B;**[!DNL Run]**。

![根文件夹](../../images/tutorials/create/salesforce/root-folder.png)

出现[!DNL Runner]接口。 在此处，确保选中所有复选框，然后选择&#x200B;**[!DNL Run Namespaces and Schemas Autogeneration Utility]**。

![运行生成器](../../images/tutorials/create/salesforce/run-generator.png)

成功的请求将根据测试版规范创建B2B命名空间和架构。

## 设置您的[!DNL Salesforce]源以便在Amazon Web Services上Experience Platform {#aws}

>[!AVAILABILITY]
>
>本节适用于在Amazon Web Services (AWS)上运行的Experience Platform的实施。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform多云概述](../../../landing/multi-cloud.md)。

请按照以下步骤了解如何设置您的[!DNL Salesforce]帐户以在Amazon Web Services (AWS)上Experience Platform。

### 先决条件

要将您的[!DNL Salesforce]帐户连接到AWS地区的Experience Platform，您必须具备以下条件：

- 具有API访问权限的[!DNL Salesforce]帐户。
- 随后可用于启用JWT_BEARER OAuth流的[!DNL Salesforce Connected App]。
- [!DNL Salesforce]中访问数据所需的权限。

列入允许列表您还必须将以下IP地址添加到IP帐户，以将您的[!DNL Salesforce]帐户连接到Amazon Web Services (AWS)上的Experience Platform：

- `34.193.63.59`
- `44.217.93.240`
- `44.194.79.229`

### 创建[!DNL Salesforce Connected App]

首先，使用以下内容创建PEM文件的证书/密钥对。

```shell
openssl req -newkey rsa:4096 -new -nodes -x509 -days 3650 -keyout key.pem -out cert.pem  
```

1. 在[!DNL Salesforce]仪表板中，选择设置(![设置图标。](/help/images/icons/settings.png))，然后选择&#x200B;**[!DNL Setup]**。
2. 导航到[!DNL App Manager]，然后选择&#x200B;**[!DNL New Connection App]**。
3. 为应用程序提供一个名称，并允许自动填写其余字段。
4. 为[!DNL Enable OAuth Settings]启用该框。
5. 设置回调URL。 由于这不会用于JWT，因此您可以使用`https://localhost`。
6. 为[!DNL Use Digital Signatures]启用该框。
7. 上载先前创建的cert.perm文件。

#### 添加所需权限

添加以下权限：

1. 通过API (api)管理用户数据
2. 访问自定义权限(custom_permissions)
3. 访问身份URL服务（id、个人资料、电子邮件、地址、电话）
4. 访问唯一标识符(openid)
5. 随时执行请求(refresh_token、offline_access)

添加权限后，请确保为&#x200B;**[!DNL Issue JSON Web Token (JWT)-based access tokens for named user]**&#x200B;启用该框。

接下来，依次选择&#x200B;**[!DNL Save]**、**[!DNL Continue]**&#x200B;和&#x200B;**[!DNL Manage Customer Details]**。 使用使用者详细信息面板检索以下内容：

- **使用者密钥**：稍后在对要Experience Platform的[!DNL Salesforce]帐户进行身份验证时，您将使用此使用者密钥作为您的客户端ID。
- **使用者密码**：稍后在向Experience Platform验证您的[!DNL Salesforce]帐户时，您将使用此使用者密码作为您的客户端ID。

### 授权您的[!DNL Salesforce]用户访问连接的应用程序

请按照以下步骤获得使用连接的应用程序的授权：

1. 导航到&#x200B;**[!DNL Manage Connected Apps]**。
2. 选择 **[!DNL Edit]**。
3. 将&#x200B;**[!DNL Permitted Users]**&#x200B;配置为&#x200B;**[!DNL Admin approved users are pre-authorized]**，然后选择&#x200B;**[!DNL Save]**。
4. 导航到&#x200B;**[!DNL Settings]> [!DNL Manage Users] >[!DNL Profiles]**。
5. 编辑与用户关联的配置文件。
6. 导航到&#x200B;**[!DNL Connected App Access]**，然后选择在之前的步骤中创建的应用程序。

### 生成JWT持有者令牌

请按照以下步骤生成JWT持有者令牌。

#### 将密钥对转换为pkcs12

要生成JWT持有者令牌，您必须首先使用以下命令将证书/密钥对转换为pkcs12格式。 在此步骤中，您还必须在出现提示时&#x200B;**设置导出密码**。

```shell
openssl pkcs12 -export -in cert.pem -inkey key.pem -name jwtcert >jwtcert.p12
```

#### 基于pkcs12创建Java密钥库

接下来，使用以下命令基于刚刚生成的pkcs12创建Java密钥库。 在此步骤中，您还必须在出现提示时&#x200B;**设置目标密钥库密码**。 此外，您必须提供以前的导出密码作为源密钥库密码。

```shell
keytool -importkeystore -srckeystore jwtcert.p12 -destkeystore keystore.jks -srcstoretype pkcs12 -alias jwtcert
```

#### 确认您的keystroke.jks包含jwtcert别名

接下来，使用以下命令确认您的`keystroke.jks`包含`jwtcert`别名。 在此步骤中，系统将提示您提供上一步中生成的目标密钥库密码。

```shell
keytool -keystore keystore.jks -list
```

#### 生成签名令牌

最后，使用下面的java类JWTExample生成您的签名令牌。

```java
package org.example;
 
import org.apache.commons.codec.binary.Base64;
 
import java.io.*;
import java.security.*;
import java.text.MessageFormat;
 
public class Main {
 
    public static void main(String[] args) {
 
        String header = "{\"alg\":\"RS256\"}";
        String claimTemplate = "'{'\"iss\": \"{0}\", \"sub\": \"{1}\", \"aud\": \"{2}\", \"exp\": \"{3}\"'}'";
 
        try {
            StringBuffer token = new StringBuffer();
 
            //Encode the JWT Header and add it to our string to sign
            token.append(Base64.encodeBase64URLSafeString(header.getBytes("UTF-8")));
 
            //Separate with a period
            token.append(".");
 
            //Create the JWT Claims Object
            String[] claimArray = new String[5];
            claimArray[0] = "{CLIENT_ID}";
            claimArray[1] = "{AUTHORIZED_SALESFORCE_USERNAME}";
            claimArray[2] = "{SALESFORCE_LOGIN_URL}";
            claimArray[3] = Long.toString((System.currentTimeMillis() / 1000) + 2629746*4);
            MessageFormat claims;
            claims = new MessageFormat(claimTemplate);
            String payload = claims.format(claimArray);
 
            //Add the encoded claims object
            token.append(Base64.encodeBase64URLSafeString(payload.getBytes("UTF-8")));
 
            //Load the private key from a keystore
            KeyStore keystore = KeyStore.getInstance("JKS");
            keystore.load(new FileInputStream("path/to/keystore"), "keystorepassword".toCharArray());
            PrivateKey privateKey = (PrivateKey) keystore.getKey("jwtcert", "privatekeypassword".toCharArray());
 
            //Sign the JWT Header + "." + JWT Claims Object
            Signature signature = Signature.getInstance("SHA256withRSA");
            signature.initSign(privateKey);
            signature.update(token.toString().getBytes("UTF-8"));
            String signedPayload = Base64.encodeBase64URLSafeString(signature.sign());
 
            //Separate with a period
            token.append(".");
 
            //Add the encoded signature
            token.append(signedPayload);
 
            System.out.println(token.toString());
 
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

| 属性 | 配置 |
| --- | --- |
| `claimArray[0]` | 使用您的客户端ID更新`claimArray[0]`。 |
| `claimArray[1]` | 使用针对应用程序授权的[!DNL Salesforce]用户名更新`claimArray[1]`。 |
| `claimArray[2]` | 使用您的[!DNL Salesforce]登录URL更新`claimArray[2]`。 |
| `claimArray[3]` | 用自纪元以来毫秒的格式设置过期日期更新`claimArray[3]`。 例如，`3660624000000`为12-31-2085。 |
| `/path/to/keystore` | 将`/path/to/keystore`替换为您的keystore.jks的正确路径 |
| `keystorepassword` | 将`keystorepassword`替换为您的目标密钥库密码。 |
| `privatekeypassword` | 将`privatekeypassword`替换为您的源密钥库密码。 |

## 后续步骤

完成为[!DNL Salesforce]帐户设置的先决条件后，您可以继续连接[!DNL Salesforce]帐户以Experience Platform和摄取CRM数据。 有关详细信息，请阅读下面的文档：

### 使用API将[!DNL Salesforce]连接到平台

以下文档提供了有关如何使用API或用户界面将[!DNL Salesforce]连接到Platform的信息：

- [使用流服务API创建Salesforce基本连接](../../tutorials/api/create/crm/salesforce.md)
- [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
- [使用流服务API为CRM源创建数据流](../../tutorials/api/collect/crm.md)

### 使用UI将[!DNL Salesforce]连接到平台

- [在UI中创建Salesforce源连接](../../tutorials/ui/create/crm/salesforce.md)
- [在用户界面中为CRM连接创建数据流](../../tutorials/ui/dataflow/crm.md)