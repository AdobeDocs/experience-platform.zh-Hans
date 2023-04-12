---
keywords: Experience Platform；零售销售方法；Data Science Workspace；热门主题；方法
solution: Experience Platform
title: 创建零售销售架构和数据集
type: Tutorial
description: 本教程为您提供所有其他Adobe Experience Platform Data Science Workspace教程所需的先决条件和资产。 完成后，您和组织成员将可以使用零售销售架构和数据集进行Experience Platform。
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---


# 创建零售销售架构和数据集

本教程将为您提供所有其他 [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] 教程。 完成后，您和贵组织的成员将可以在 [!DNL Experience Platform].

## 快速入门

在启动本教程之前，您必须满足以下先决条件：
- 访问 [!DNL Adobe Experience Platform]. 如果您在 [!DNL Experience Platform]，请在继续操作之前与系统管理员联系。
- 授权 [!DNL Experience Platform] API调用。 完成 [验证和访问Adobe Experience Platform API](https://www.adobe.com/go/platform-api-authentication-en) 教程以获取以下值以成功完成本教程：
   - Authorization: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{ORG_ID}`
   - 客户端密钥： `{CLIENT_SECRET}`
   - 客户端证书： `{PRIVATE_KEY}`
- 示例数据和源文件 [零售销售方法](../pre-built-recipes/retail-sales.md). 下载此资产和其他资产所需的资产 [!DNL Data Science Workspace] 教程 [Adobe公共Git存储库](https://github.com/adobe/experience-platform-dsw-reference/).
- [派森>= 2.7](https://www.python.org/downloads/) 以下 [!DNL Python] 包：
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [诊断器](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- 对本教程中使用的以下概念有了良好的了解：
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [架构组合的基础知识](../../xdm/schema/field-dictionary.md)

## 创建零售销售架构和数据集

零售销售架构和数据集是使用提供的引导脚本自动创建的。 请按照以下步骤操作：

### 配置文件

1. 内部 [!DNL Experience Platform] 教程资源包，导航到目录 `bootstrap`，然后打开 `config.yaml` 使用适当的文本编辑器。
2. 在 `Enterprise` ，请输入以下值：

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {ORG_ID}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. 编辑在 `Platform` 部分，示例如下所示：

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway`:API调用的基本路径。 请勿修改此值。
   - `ims_token`:您的 `{ACCESS_TOKEN}` 到这里。
   - `ingest_data`:在本教程中，请将此值设置为 `"True"` 以创建零售销售架构和数据集。 值 `"False"` 将仅创建架构。
   - `build_recipe_artifacts`:在本教程中，请将此值设置为 `"False"` 以防止脚本生成方法项目。
   - `kernel_type`:方法对象的执行类型。 将此值保留为 `Python` if `build_recipe_artifacts` 设置为 `"False"`，否则请指定正确的执行类型。

4. 在 `Titles` 部分，为零售销售示例数据正确提供以下信息，并在进行编辑后保存并关闭文件。 示例如下所示：

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

1. 打开您的终端应用程序并导航到 [!DNL Experience Platform] 教程资源目录。
2. 设置 `bootstrap` 目录作为当前工作路径并运行 `bootstrap.py` [!DNL Python] 脚本：

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >脚本可能需要几分钟才能完成。

## 后续步骤

成功完成引导脚本后，可以在上查看零售销售输入和输出架构以及数据集 [!DNL Experience Platform]. 请参阅 [预览模式数据教程](./preview-schema-data.md)
以了解更多信息。

您还已成功将零售销售示例数据摄取到 [!DNL Experience Platform] 使用提供的引导脚本。

要继续使用摄取的数据，请执行以下操作：
- [使用Jupyter Notebooks分析数据](../jupyterlab/analyze-your-data.md)
   - 使用Data Science Workspace中的Jupyter Notebooks访问、探索、可视化和了解您的数据。
- [将源文件打包到方法中](./package-source-files-recipe.md)
   - 请阅读本教程，了解如何将您自己的模型引入 [!DNL Data Science Workspace] 将源文件打包到可导入的方法文件中。
