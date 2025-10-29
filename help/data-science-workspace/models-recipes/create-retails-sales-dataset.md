---
keywords: Experience Platform；零售指导方针；数据科学Workspace；热门主题；指导方针
solution: Experience Platform
title: 创建零售架构和数据集
type: Tutorial
description: 本教程提供了所有其他Adobe Experience Platform数据科学Workspace教程所需的先决条件和资源。 完成后，您和您的组织成员将可以在Experience Platform上使用零售架构和数据集。
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 2%

---


# 创建零售架构和数据集

>[!NOTE]
>
>数据科学Workspace不再可供购买。
>
>本文档面向之前有权访问数据科学Workspace的现有客户。

本教程提供了所有其他[!DNL Adobe Experience Platform] [!DNL Data Science Workspace]教程所需的先决条件和资源。 完成后，零售架构和数据集将在[!DNL Experience Platform]上为您和您的组织成员提供。

## 快速入门

在开始本教程之前，您必须满足以下先决条件：

- 访问[!DNL Adobe Experience Platform]。 如果您无权访问[!DNL Experience Platform]中的组织，请在继续之前与系统管理员交谈。
- 授权进行[!DNL Experience Platform] API调用。 要成功完成本教程，请完成[身份验证和访问Adobe Experience Platform API](https://www.adobe.com/go/platform-api-authentication-en)教程以获取以下值：
   - 授权： `{ACCESS_TOKEN}`
   - x-api-key： `{API_KEY}`
   - x-gw-ims-org-id： `{ORG_ID}`
   - 客户端密码： `{CLIENT_SECRET}`
   - 客户端证书： `{PRIVATE_KEY}`
- [零售销售方法](../pre-built-recipes/retail-sales.md)的示例数据和源文件。 从[!DNL Data Science Workspace]Adobe公共Git存储库[下载此教程和其他](https://github.com/adobe/experience-platform-dsw-reference/)教程所需的资源。
- [Python >= 2.7](https://www.python.org/downloads/)和以下[!DNL Python]包：
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [听写器](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- 对本教程中使用的以下概念的实用了解：
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [架构构成基础](../../xdm/schema/field-dictionary.md)

## 创建零售架构和数据集

使用提供的引导脚本自动创建零售架构和数据集。 请按顺序执行以下步骤：

### 配置文件

1. 在[!DNL Experience Platform]教程资源包中，导航到目录`bootstrap`，然后使用适当的文本编辑器打开`config.yaml`。
2. 在`Enterprise`部分下，输入以下值：

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {ORG_ID}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. 编辑在`Platform`部分下找到的值，如下所示：

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway`： API调用的基本路径。 请勿修改此值。
   - `ims_token`：您的`{ACCESS_TOKEN}`转到此处。
   - `ingest_data`：在本教程中，请将此值设置为`"True"`以创建零售架构和数据集。 值为`"False"`将仅创建架构。
   - `build_recipe_artifacts`：在本教程中，请将此值设置为`"False"`以防止脚本生成方法构件。
   - `kernel_type`：方法工件的执行类型。 如果`Python`设置为`build_recipe_artifacts`，则将此值保留为`"False"`，否则请指定正确的执行类型。

4. 在`Titles`部分下，为零售样本数据适当提供以下信息，并在进行编辑后保存并关闭文件。 示例如下所示：

   ```yaml
   Titles:
       input_class_title: retail_sales_input_class
       input_mixin_title: retail_sales_input_mixin
       input_mixin_definition_title: retail_sales_input_mixin_definition
       input_schema_title: retail_sales_input_schema
       input_dataset_title: retail_sales_input_dataset
       file_replace_tenant_id: DSWRetailSalesForXDM0.9.9.9.json
       file_with_tenant_id: DSWRetailSales_with_tenant_id.json
       is_output_schema_different: "True"
       output_mixin_title: retail_sales_output_mixin
       output_mixin_definition_title: retail_sales_output_mixin_definition
       output_schema_title: retail_sales_output_title
       output_dataset_title: retail_sales_output_dataset
   ```

### 运行引导脚本

1. 打开您的终端应用程序并导航到[!DNL Experience Platform]教程资源目录。
2. 将`bootstrap`目录设置为当前工作路径，并通过输入以下命令运行`bootstrap.py` [!DNL Python]脚本：

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >脚本可能需要几分钟才能完成。

## 后续步骤

成功完成bootstrap脚本后，可以在[!DNL Experience Platform]上查看Retail Sales输入输出架构和数据集。 请参阅[预览架构数据教程](./preview-schema-data.md)
以了解更多信息。

您还已成功使用提供的引导脚本将零售业样本数据摄取到[!DNL Experience Platform]。

要继续使用摄取的数据，请执行以下操作：

- [使用 Jupyter Notebooks 分析数据](../jupyterlab/analyze-your-data.md)
   - 使用数据科学Workspace中的Jupyter Notebooks访问、浏览、可视化和了解您的数据。
- [将源文件打包到方法中](./package-source-files-recipe.md)
   - 按照本教程了解如何通过将源文件打包到可导入的方法文件中来将您自己的模型导入[!DNL Data Science Workspace]。
