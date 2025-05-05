---
title: 使用計算欄位對匯出到雲端儲存目標的資料執行轉換
type: Tutorial
description: 瞭解如何使用計算欄位功能，對匯出至雲端儲存空間的資料執行轉換
exl-id: 1e14f964-4c03-4d0c-be8d-c3dcb48a335a
source-git-commit: 14c672ef57e0b0247020075552c782ed18db8484
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 8%

---

# 使用計算欄位對匯出到雲端儲存目標的資料執行轉換 {#data-transformation-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="新增計算欄位"
>abstract="<p>使用「**新增計算欄位**」控制項對匯出到雲端儲存目標的資料執行各種資料轉換。例如，您可以對資料進行雜湊、將陣列串連成字串等等。"

<!--

disable additional URLs for a while

>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-maps-objects.html?lang=zh-Hant#examples" text="Examples"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-maps-objects.html?lang=zh-Hant#known-limitations" text="Known limitations"

-->

>[!AVAILABILITY]
>
>對於匯出至雲端儲存空間目的地的資料，通常可在下列目的地使用執行轉換的功能： [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)、[[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)、[[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)、[[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md)、[[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md)、[[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md)，以及任何透過[Destination SDK](/help/destinations/destination-sdk/overview.md)撰寫的自訂合作夥伴編寫的雲端儲存空間目的地。

若要對匯出至雲端儲存空間的資料執行各種轉換，您必須在匯出工作流程的對應步驟中使用計算欄位功能。 如需有關計算欄位的詳細資訊，請瀏覽以下連結的頁面。 這些頁面包含「資料準備」中計算欄位的介紹，以及有關所有可用函式的更多資訊：

* [UI指南和概觀](/help/data-prep/ui/mapping.md#calculated-fields)
* [資料準備函式](/help/data-prep/functions.md)

## 先決條件 {#prerequisites}

若要使用計算欄位進行資料轉換：

1. [連線](/help/destinations/ui/connect-destination.md)至所需的雲端儲存空間目的地。 連線到所需的雲端目的地時，將&#x200B;**[!UICONTROL 匯出陣列、對應、物件]** [選項關閉](/help/destinations/ui/export-arrays-maps-objects.md##export-arrays-maps-objects-toggle)。
2. 進行雲端儲存空間目的地[&#128279;](/help/destinations/ui/activate-batch-profile-destinations.md)的啟動步驟，並前往[對應](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)步驟。

## 如何使用計算欄位 {#how-to-export-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_control"
>title="啟用階層式輸出結構描述"
>abstract="將此設定切換為開啟，便可以將陣列、對應及物件匯出至 JSON 或 Parquet 檔案。"

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_calculated_field_disabled"
>title="新增計算欄位已停用"
>abstract="此控制項已停用，因為您在設定此目標連線時，將「**匯出陣列、對應、物件**」切換為「*開啟*」。若要使用計算欄位和其中可用的函數，請將「**匯出陣列、對應、物件**」切換為「*關閉*」，再設定新的目標連線。"

在雲端儲存體目的地的啟動工作流程對應步驟中，選取&#x200B;**[!UICONTROL 新增計算欄位]**。

>[!TIP]
>
>已針對已關閉&#x200B;**[!UICONTROL 匯出陣列、對應及物件]**&#x200B;控制項的目的地連線，停用&#x200B;**[!UICONTROL 新增計算欄位]**&#x200B;控制項。 [閱讀全文](/help/destinations/ui/export-arrays-maps-objects.md#export-arrays-maps-objects-toggle)。

![新增批次啟動工作流程對應步驟中反白顯示的計算欄位。](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

這會開啟模型視窗，您可在其中選取要從Experience Platform匯出屬性的函式和欄位。

![計算欄位功能的模型視窗，尚未選取函式。](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

例如，在`organizations`欄位上使用`array_to_string`函式，如下所示，將組織陣列匯出為CSV檔案中的字串。 檢視[更多關於此專案及下方](#array-to-string-function-export-arrays)其他範例的資訊。

![已選取陣列至字串函式的計算欄位功能的模型視窗。](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以保留計算欄位並返回對應步驟。

![已選取陣列至字串函式，且[儲存]控制項反白顯示的計算欄位功能的模型視窗。](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

回到工作流程的對應步驟，在匯出的檔案中，以您要用於此欄位的欄標題值填入&#x200B;**[!UICONTROL 目標欄位]**。

![目標欄位反白顯示的對應步驟。](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![選取目標欄位2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

準備就緒後，選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以繼續執行啟動工作流程的下一步。

![目標欄位反白且目標值已填入的對映步驟。](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## 執行資料轉換的支援函式範例 {#supported-functions}

將資料啟用至以檔案為基礎的目的地時，支援所有記錄的[資料準備函式](/help/data-prep/functions.md)。

以下專用於處理陣列匯出或對欄位套用雜湊的函式與範例一起記錄。

* `array_to_string`
* `flattenArray`
* `filterArray`
* `transformArray`
* `coalesce`
* `size_of`
* `iif`
* `index-based array access`
* `add_to_array`
* `to_array`
* `first`
* `last`

## 用來執行資料轉換的函式範例 {#examples}

如需上述部分函式，請參閱以下章節中的範例和進一步資訊。 如需列出的其餘函式，請參閱「資料準備」區段[&#128279;](/help/data-prep/functions.md)中的一般函式檔案。

### `array_to_string`函式以匯出陣列 {#array-to-string-function-export-arrays}

使用`array_to_string`函式，使用所需的分隔符號（例如`_`或`|`）將陣列元素串連到字串中。 如果您想要將陣列的元素從Experience Platform匯出至CSV檔案，此函式十分實用。

例如，您可以使用`array_to_string('_',organizations)`語法來結合下列XDM欄位，如對應熒幕擷圖中所示：

* `organizations`陣列
* `person.name.firstName`字串
* `person.name.lastName`字串
* `personalEmail.address`字串

![包括array_to_string函式的對應範例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-array-to-string-function.png)

在此情況下，您的輸出檔案看起來如下所示。 請注意陣列元素如何使用`_`字元串連成單一字串。

```
First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':456,'orgName':'Superstar Inc','founded':2004,'latestInteraction':1692921600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### `filterArray`函式以匯出篩選的陣列 {#filter-array}

使用`filterArray`函式來篩選匯出陣列的元素。 您可以將此函式與上面進一步說明的`array_to_string`函式結合。

繼續使用上方的`organizations`陣列物件，您可以撰寫類似`array_to_string('_', filterArray(organizations, org -> org.founded > 2021))`的函式，這會傳回在2021年或之後具有`founded`值的組織。

![filterArray函式的範例。](/help/destinations/assets/ui/export-arrays-calculated-fields/filter-array-function.png)

在此情況下，您的輸出檔案看起來如下所示。 請注意陣列中符合條件的兩個元素如何使用`_`字元串連成單一字串。

```
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### `transformArray`函式以匯出轉換的陣列 {#transform-array}

使用`transformArray`函式轉換匯出陣列的元素。 您可以將此函式與上面進一步說明的`array_to_string`函式結合。

繼續使用上方的`organizations`陣列物件，您可以撰寫類似`array_to_string('_', transformArray(organizations, org -> ucase(org.orgName)))`的函式，傳回已轉換為全部大寫的組織名稱。

![TransformArray函式的範例。](/help/destinations/assets/ui/export-arrays-calculated-fields/transform-array-function.png)

在此情況下，您的輸出檔案看起來如下所示。 請注意如何使用`_`字元將陣列的三個元素轉換並串連為單一字串。

```
John,Doe,johndoe@acme.org,ACME INC_SUPERSTAR INC_ENERGY CORP
```

### `iif`函式以匯出陣列 {#iif-function-export-arrays}

在特定條件下，使用`iif`函式匯出陣列的元素。 例如，繼續使用上面的`organizations`陣列物件，您可以編寫簡單的條件函式，例如`iif(organizations[0].equals("Marketing"), "isMarketing", "isNotMarketing")`。

![包含iif函式的對應範例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-iif-function.png)

在此情況下，您的輸出檔案看起來如下所示。 在此案例中，陣列的第一個元素為行銷，因此該人員為行銷部門的成員。

```
`First_Name,Last_Name, Personal_Email, Is_Member_Of_Marketing_Dept
John,Doe, johndoe@acme.org, "isMarketing"
```

### `add_to_array`函式以匯出陣列 {#add-to-array-function-export-arrays}

使用`add_to_array`函式將元素加入至匯出的陣列。 您可以將此函式與上面進一步說明的`array_to_string`函式結合。

繼續使用上方的`organizations`陣列物件，您可以撰寫類似`source: array_to_string('_', add_to_array(organizations,"2023"))`的函式，傳回人員在2023年所屬的組織。

![包括add_to_array函式的對應範例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

在此情況下，您的輸出檔案看起來如下所示。 請注意陣列中的三個元素如何使用`_`字元串連成單一字串，而2023也會附加在字串的結尾。

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

### `flattenArray`函式以匯出平面化陣列 {#flatten-array}

使用`flattenArray`函式平面化匯出的多維陣列。 您可以將此函式與上面進一步說明的`array_to_string`函式結合。

繼續使用上方的`organizations`陣列物件，您可以編寫類似`array_to_string('_', flattenArray(organizations))`的函式。 請注意，`array_to_string`函式預設會將輸入陣列平面化為字串。

產生的輸出與上面進一步說明的`array_to_string`函式相同。

### `coalesce`函式以匯出陣列 {#coalesce-function-export-arrays}

使用`coalesce`函式來存取並將陣列中的第一個非null元素匯出至字串。

例如，您可以使用`coalesce(subscriptions.hasPromotion)`語法來傳回陣列中`false`值的前`true`個，以結合下列XDM欄位，如對應熒幕擷圖中所示：

* `"subscriptions.hasPromotion": [null, true, null, false, true]`陣列
* `person.name.firstName`字串
* `person.name.lastName`字串
* `personalEmail.address`字串

![包括coalesce函式的對應範例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

在此情況下，您的輸出檔案看起來如下所示。 請注意如何將陣列中的第一個非Null `true`值匯出到檔案中。

```
First_Name,Last_Name,hasPromotion
John,Doe,true
```

### `size_of`函式以匯出陣列 {#sizeof-function-export-arrays}

使用`size_of`函式指出陣列中有多少元素。 例如，如果您有具有多個時間戳記的`purchaseTime`陣列物件，則可以使用`size_of`函式來指出某人分別進行了多少次購買。

例如，您可以合併下列XDM欄位，如對應熒幕擷圖所示。

* `"purchaseTime": ["1538097126","1569633126,"1601255526","1632791526","1664327526"]`陣列，指出客戶分別購買五次
* `personalEmail.address`字串

![包括size_of函式的對應範例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

在此情況下，您的輸出檔案看起來如下所示。 請注意第二欄如何指出陣列中的元素數量，對應於客戶進行的個別購買數量。

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### 索引型陣列存取 {#index-based-array-access}

>[!IMPORTANT]
>
>不同於此頁面上說明的其他函式，若要匯出陣列的個別元素，您&#x200B;*不需要*&#x200B;在UI中使用&#x200B;**[!UICONTROL 計算欄位]**&#x200B;控制項。

您可以存取陣列的索引，以從陣列匯出單一專案。 例如，與上述的`size_of`函式範例類似，如果您只想在客戶第一次購買特定產品時存取和匯出，您可以使用`purchaseTime[0]`匯出時間戳記的第一個元素，`purchaseTime[1]`匯出時間戳記的第二個元素，`purchaseTime[2]`匯出時間戳記的第三個元素，依此類推。

![顯示如何存取陣列專案的對應範例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

在此情況下，您的輸出檔案看起來如下所示，會在客戶首次購買時匯出：

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first`和`last`函式以匯出陣列 {#first-and-last-functions-export-arrays}

使用`first`和`last`函式匯出陣列中的第一個或最後一個元素。 例如，繼續使用具有先前範例中多個時間戳記的`purchaseTime`陣列物件，您可以使用這些至函式，匯出人員進行的首次或上次購買時間。

![包含第一個和最後一個函式的對應範例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

在此情況下，您的輸出檔案看起來如下所示，匯出客戶第一次和最後一次購買的時間：

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

### 雜湊函式 {#hashing-functions}

其他可用的函式則專用於從陣列匯出陣列或元素。 您可以使用雜湊函式來雜湊匯出檔案中的屬性。 例如，如果您在屬性中有任何個人識別資訊，可在匯出這些欄位時將其雜湊化。

您可以直接雜湊字串值，例如`md5(personalEmail.address)`。 如有需要，您也可以雜湊陣列欄位的個別元素，假設陣列中的元素是字串，如下所示： `md5(purchaseTime[0])`

支援的雜湊函式有：

| 函數 | 範例運算式 |
|---------|----------|
| `sha1` | `sha1(organizations[0])` |
| `sha256` | `sha256(organizations[0])` |
| `sha512` | `sha512(organizations[0])` |
| `hash` | `hash("crc32", organizations[0], "UTF-8")` |
| `md5` | `md5(organizations[0], "UTF-8")` |
| `crc32` | `crc32(organizations[0])` |

{style="table-layout:auto"}
