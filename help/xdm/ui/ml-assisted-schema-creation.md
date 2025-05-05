---
title: 機器學習輔助結構描述建立
description: 瞭解如何在Experience Platform使用者介面中建立方案。
badgeBeta: label="Beta" type="Informative"
exl-id: 6b14caed-a3ad-4834-8fa8-8d67dce6290e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 2%

---

# 機器學習輔助的結構描述建立

>[!AVAILABILITY]
>
>* 機器學習輔助的結構描述建立目前處於Beta版。 文件和功能可能會有所變更。

使用ML演演算法從範例資料產生結構。 為大型複雜資料集定義結構、欄位和資料型別時，此程式可節省時間並提高準確性。

產生ML結構描述後，您可以快速整合新的資料來源，並減少手動建立的錯誤。 非技術使用者可以使用此外掛程式來產生結構描述或管理大型和複雜的資料集，而不需要額外的工作。 此協助可加快從取得資料到獲得見解的流程，因為可讓您更輕鬆地合併新資料來源及執行資料分析。

## 快速入門

本教學課程需要您實際瞭解架構建立的需求。 繼續本指南之前，您應該先閱讀[建立和編輯結構描述的UI指南](./resources/schemas.md)。

本指南說明如何使用機器學習(ML)演演算法建立結構描述，以從範例資料產生結構描述。 請參閱[手動結構描述建立工作流程手冊](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/ui/resources/schemas#add-field-groups)，以取得有關在結構描述編輯器中的[欄位式工作流程](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/ui/field-based-workflows)上建立結構描述或檔案的資訊，以增進您對結構描述建立程式的瞭解。

>[!NOTE]
>
>您也可以使用[!DNL Schema Registry] API來撰寫結構描述。 若要使用API手動建立結構描述，請先閱讀[[!DNL Schema Registry] 開發人員指南](../api/getting-started.md)，再嘗試進行有關[使用API建立結構描述](../tutorials/create-schema-api.md)的教學課程。

## 導覽至建立結構描述工作流程 {#navigate-to-schema-creation-workflow}

從Experience Platform UI的左側導覽中，選取&#x200B;**[!UICONTROL 結構描述]**&#x200B;工作區。 **[!UICONTROL 結構描述]**&#x200B;工作區隨即顯示。 選取&#x200B;**[!UICONTROL 建立結構描述]**&#x200B;以新增結構描述，以啟動結構描述建立工作流程。

![結構描述工作區在左側導覽和建立結構描述突出顯示。](../images/ui/ml-schema-creation/schemas-workspace-create-schema.png)

## 建立結構描述 {#create-a-schema}

[!UICONTROL 建立結構描述]對話方塊就會顯示。 選取&#x200B;**[ML輔助]**&#x200B;結構描述建立選項，接著選取&#x200B;**[!UICONTROL 選取]**&#x200B;以確認您的選擇。

![ [!UICONTROL 建立結構描述]對話方塊，並反白顯示[!UICONTROL ML — 輔助]。](../images/ui/ml-schema-creation/use-sample-csv.png)

### 選取基底類別 {#select-base-class}

[!UICONTROL 建立結構描述]工作流程隨即顯示。 選取結構描述的基底類別，接著選取&#x200B;**[!UICONTROL 下一步]**。

![結構描述詳細資料工作區，其中包含類別和下一個反白顯示專案。](../images/ui/ml-schema-creation/select-base-class.png)

### 上傳 CSV 檔案 {#upload-csv}

建立工作流程的&#x200B;**[!UICONTROL 選取資料]**&#x200B;階段即會出現。 從&#x200B;**[!UICONTROL 上傳檔案]**&#x200B;區段中，選取&#x200B;**[!UICONTROL 選擇檔案]**&#x200B;或&#x200B;**[!UICONTROL 拖放檔案]**&#x200B;區段。 從電腦中選取.csv檔案以產生結構描述。

![「建立結構描述」工作流程的「選取資料」階段中，「上傳檔案」區段會反白顯示。](../images/ui/ml-schema-creation/upload-files.png)

### 預覽資料 {#preview-data}

[!UICONTROL 上傳檔案]區段會顯示您匯入的CSV檔案名稱，而&#x200B;**[!UICONTROL 預覽]**&#x200B;區段會顯示您上傳之檔案中的範例資料列。 選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以繼續工作流程。

![預覽區段中反白顯示的範例資料列，以及[下一步]反白顯示的資料列。](../images/ui/ml-schema-creation/preview-data.png)

### 檢閱和編輯結構描述 {#review-schema}

建立工作流程的&#x200B;**[!UICONTROL 檢閱和編輯]**&#x200B;階段現在會出現，在表格檢視中顯示機器學習輔助的&#x200B;**[!UICONTROL 結構描述建議]**。 在這個階段，您可以從機器學習模型產生的建議結構描述中編輯、新增或移除欄位。 此表格包含下列欄位：

| 欄位名稱 | 說明 |
|------------------|---------------------------------------------------------|
| [!UICONTROL 資料表] | 欄位起源的資料集或資料庫。 |
| [!UICONTROL Source欄位] | 來源系統的原始欄位名稱。 |
| [!UICONTROL 目標欄位] | 將對應資料的目標系統中的欄位名稱。 |
| [!UICONTROL 顯示名稱] | 用來在使用者介面中顯示欄位的名稱。 此名稱應該更易懂或描述性。 |
| [!UICONTROL 資料型別] | 儲存在欄位中的資料型別（例如，`String`、`Date`）。 |
| [!UICONTROL 欄位群組] | 根據欄位使用或內容的分類(例如，[!UICONTROL 人口統計詳細資料]、[!UICONTROL Commerce詳細資料])。 |

![結構描述建立工作流程的檢閱和編輯階段。](../images/ui/ml-schema-creation/schema-recommendation.png)

#### 新增欄位 {#add-field}

若要將欄位新增至結構描述，請選取&#x200B;**[!UICONTROL 新增欄位]**。

![反白顯示[新增欄位]的結構描述建立工作流程的[檢閱和編輯]階段。](../images/ui/ml-schema-creation/add-new-field.png)

[!UICONTROL 選取欄位]對話方塊就會顯示。 此對話方塊包含目前存在的結構描述圖表。 選取所要的欄位並選取&#x200B;**[選取]**&#x200B;以新增欄位到結構描述。 視需要選取&#x200B;**[取消]**&#x200B;以關閉對話方塊。

![[選取欄位]對話方塊中選取了欄位，且[選取]反白顯示。](../images/ui/ml-schema-creation/select-field-dialog.png)

新列會出現在您建議的結構描述中。 您現在可以編輯欄位。

#### 編輯欄位 {#edit-field}

若要編輯欄位，請選取要編輯之列的鉛筆圖示。 右側會出現一個詳細資訊面板，您可以在其中編輯自訂欄位對應。 詳細資料面板包含[!UICONTROL 目標欄位]、[!UICONTROL 顯示名稱]、[!UICONTROL 資料型別]和[!UICONTROL 欄位群組]。 進行任何必要的變更，並選取&#x200B;**[!UICONTROL 套用]**&#x200B;以確認。 再次選取鉛筆圖示以關閉詳細資料面板。

![結構描述建立工作流程的「檢閱和編輯」階段中，鉛筆圖示和詳細資訊面板會反白顯示。](../images/ui/ml-schema-creation/edit-field.png)

#### 移除欄位 {#remove-field}

若要移除欄位，請選取要刪除之列上的減號圖示。

>[!CAUTION]
>
>移除此專案時，不會顯示確認對話方塊。

![結構描述建立工作流程的檢閱和編輯階段中，反白顯示減號圖示。](../images/ui/ml-schema-creation/remove-field.png)

#### 核准您建議的結構描述 {#approve}

若要核准您建議的結構描述並繼續&#x200B;**[!UICONTROL 建立結構描述]**&#x200B;工作流程，請選取&#x200B;**[下一步]**。

![結構描述建立工作流程的[檢閱和編輯]階段中，[下一步]會反白顯示。](../images/ui/ml-schema-creation/next.png)

### 命名並儲存結構描述 {#name-and-save}

建立工作流程的&#x200B;**[!UICONTROL 名稱及儲存]**&#x200B;階段隨即顯示。 輸入&#x200B;**[結構描述顯示名稱]**&#x200B;和選用的說明。 **[產生的結構描述]**&#x200B;區段提供ML產生的結構描述圖表。 選取&#x200B;**[完成]**&#x200B;以完成結構描述建立工作流程。

![結構描述建立工作流程的「名稱」和「儲存結構描述」階段中反白顯示「完成」。](../images/ui/ml-schema-creation/name-and-save.png)

### 在架構編輯器中檢視 {#view-in-editor}

結構編輯器出現，您新建立的結構顯示在畫布中。 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以返回[!UICONTROL 結構描述]工作區。

![結構描述編輯器顯示您命名的ML產生的結構描述。](../images/ui/ml-schema-creation/schema-editor.png)

## 後續步驟

建立結構描述後，您可以視需要使用結構描述編輯器來進行進一步的修改。 您的新結構描述現在已準備好與您的資料來源整合，並用於資料分析。

如需使用結構描述編輯器的詳細資訊，請參閱[編輯現有結構描述指南](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/xdm/ui/resources/schemas#edit)。
