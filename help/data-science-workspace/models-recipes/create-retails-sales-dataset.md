---
keywords: Experience Platform；零售銷售方式； Data Science Workspace；熱門主題；方式
solution: Experience Platform
title: 建立零售銷售結構和資料集
type: Tutorial
description: 本教學課程提供其他Adobe Experience Platform Data Science Workspace教學課程所需的必要條件和資產。 完成後，您和IMS組織成員即可Experience Platform使用零售銷售結構和資料集。
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---


# 建立零售銷售結構和資料集

本教學課程提供所有其他必要條件和資產 [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] 教學課程。 完成後，您和IMS組織成員即可使用零售銷售結構和資料集 [!DNL Experience Platform].

## 快速入門

開始本教學課程之前，您必須具備下列必要條件：
- 存取 [!DNL Adobe Experience Platform]. 如果您無權存取 [!DNL Experience Platform]，請在繼續操作之前與系統管理員聯繫。
- 授權 [!DNL Experience Platform] API呼叫。 完成 [驗證及存取Adobe Experience Platform API](https://www.adobe.com/go/platform-api-authentication-en) 若要成功完成本教學課程，請取得下列值的教學課程：
   - Authorization: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{ORG_ID}`
   - 用戶端密碼： `{CLIENT_SECRET}`
   - 客戶端證書： `{PRIVATE_KEY}`
- 的範例資料和來源檔案 [零售銷售方式](../pre-built-recipes/retail-sales.md). 下載此及其他項目所需的資產 [!DNL Data Science Workspace] 教學課程 [Adobe公用Git存放庫](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2.7](https://www.python.org/downloads/) 和下列 [!DNL Python] 包：
   - [pi](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [字典](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- 深入了解本教學課程中使用的下列概念：
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [結構構成基本概念](../../xdm/schema/field-dictionary.md)

## 建立零售銷售結構和資料集

使用提供的引導指令碼自動建立零售銷售結構和資料集。 請依照下列步驟操作：

### 配置檔案

1. 內 [!DNL Experience Platform] 教程資源包，導航到目錄 `bootstrap`，開啟 `config.yaml` 使用適當的文字編輯器。
2. 在 `Enterprise` ，請輸入以下值：

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {ORG_ID}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. 編輯 `Platform` 區段，範例如下所示：

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway`:API呼叫的基本路徑。 請勿修改此值。
   - `ims_token`:您的 `{ACCESS_TOKEN}` 來這裡。
   - `ingest_data`:在本教學課程中，請將此值設為 `"True"` 以建立零售銷售結構和資料集。 值 `"False"` 只會建立結構。
   - `build_recipe_artifacts`:在本教學課程中，請將此值設為 `"False"` 來防止指令碼生成方式對象。
   - `kernel_type`:方式對象的執行類型。 將此值保留為 `Python` if `build_recipe_artifacts` 設為 `"False"`，否則請指定正確的執行類型。

4. 在 `Titles` 節中，為零售銷售示例資料適當提供以下資訊，在編輯完成後保存並關閉檔案。 以下範例所示：

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

### 運行引導指令碼

1. 開啟您的終端機應用程式，並導覽至 [!DNL Experience Platform] 教程資源目錄。
2. 設定 `bootstrap` 目錄作為當前工作路徑，並運行 `bootstrap.py` [!DNL Python] 指令碼，方法是輸入下列命令：

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >指令碼可能需要幾分鐘才能完成。

## 後續步驟

引導指令碼成功完成後，可以在上查看零售銷售的輸入和輸出結構和資料集 [!DNL Experience Platform]. 請參閱 [預覽架構資料教學課程](./preview-schema-data.md)
以取得更多資訊。

您也已成功將零售銷售範例資料內嵌至 [!DNL Experience Platform] 使用提供的引導指令碼。

若要繼續使用擷取的資料：
- [使用Jupyter Notebooks分析資料](../jupyterlab/analyze-your-data.md)
   - 使用Data Science Workspace中的Jupyter Notebooks來存取、探索、視覺化和了解您的資料。
- [將源檔案打包到配方中](./package-source-files-recipe.md)
   - 請依照本教學課程，了解如何將您自己的模型帶入 [!DNL Data Science Workspace] 將源檔案打包成可導入的方式檔案。
