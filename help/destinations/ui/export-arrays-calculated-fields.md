---
title: (Beta 版) 使用計算欄位匯出平面方案檔案中的陣列
type: Tutorial
description: 瞭解如何使用計算欄位，將平面結構描述檔案中的陣列從Real-Time CDP匯出至雲端儲存空間目的地。
badge: Beta
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: 787aaef26fab5ca3acff8303f928efa299cafa93
workflow-type: tm+mt
source-wordcount: '1477'
ht-degree: 5%

---

# (Beta 版) 使用計算欄位匯出平面方案檔案中的陣列 {#use-calculated-fields-to-export-arrays-in-flat-schema-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="(Beta 版) 匯出陣列支援"
>abstract="使用&#x200B;**新增計算欄位**&#x200B;控制項，將簡單的整數、字串或布林值陣列從 Experience Platform 匯出到您想要的雲端儲存空間目的地。存在一些限制。檢視文件了解大量範例和支援的功能。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#examples" text="範例"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#known-limitations" text="已知限制"

>[!AVAILABILITY]
>
>* 透過計算欄位匯出陣列的功能目前在Beta中。 文件和功能可能會有所變更。

瞭解如何透過計算欄位，將平面結構描述檔案中的Real-Time CDP陣列匯出至[雲端儲存空間目的地](/help/destinations/catalog/cloud-storage/overview.md)。 請參閱本檔案以瞭解此功能啟用的使用案例。

取得有關計算欄位的廣泛資訊 — 這些是什麼以及它們為什麼重要。 請閱讀以下連結的頁面，瞭解「資料準備」中的計算欄位，以及有關所有可用函式的詳細資訊：

* [UI指南和概觀](/help/data-prep/ui/mapping.md#calculated-fields)
* [資料準備函式](/help/data-prep/functions.md)

<!--

>[!IMPORTANT]
>
>Not all functions listed above are supported *when exporting fields to cloud storage destinations* using the calculated fields functionality. See the [supported functions section](#supported-functions) further below for more information.

-->

## Platform中的陣列和其他物件型別 {#arrays-strings-other-objects}

在Experience Platform中，您可以使用[XDM結構描述](/help/xdm/home.md)來管理不同的欄位型別。 之前，您可以將簡單的機碼值組型別欄位(例如不Experience Platform的字串)匯出至您想要的目的地。 先前支援匯出的欄位範例為`personalEmail.address`：`johndoe@acme.org`。

Experience Platform中的其他欄位型別包含陣列欄位。 深入瞭解[如何在Experience PlatformUI](/help/xdm/ui/fields/array.md)中管理陣列欄位。 除了先前支援的欄位型別之外，您現在可以匯出陣列物件，例如： `organizations:[marketing, sales, engineering]`。 請參閱以下的[大量範例](#examples)，瞭解如何使用各種函式來存取陣列元素、將陣列元素加入字串等。

## 已知限制 {#known-limitations}

請注意此功能Beta版的下列已知限制：

* 目前不支援匯出至具有階層式結構描述的JSON或Parquet檔案。 您只能將陣列匯出為平面結構描述CSV、JSON和Parquet檔案。
* 此時，*您只能將簡單陣列（或基本值陣列）匯出至雲端儲存目的地*。 這表示您可以匯出包含字串、int或布林值的陣列物件。 您無法匯出地圖或地圖或物件的陣列。計算欄位模型視窗只會顯示您可以匯出的陣列。

## 先決條件 {#prerequisites}

[連線](/help/destinations/ui/connect-destination.md)至所需的雲端儲存空間目的地，完成雲端儲存空間目的地的[啟動步驟](/help/destinations/ui/activate-batch-profile-destinations.md)並到達[對應](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)步驟。

## 如何匯出計算欄位 {#how-to-export-calculated-fields}

在雲端儲存空間目的地的啟動工作流程對應步驟中，選取&#x200B;**[!UICONTROL (Beta) 「新增計算欄位」]**。

![新增批次啟動工作流程對應步驟中反白顯示的計算欄位。](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

這會開啟一個模型視窗，您可在其中選取可用來將屬性匯出到Experience Platform之外的屬性。

>[!IMPORTANT]
>
>**[!UICONTROL 欄位]**&#x200B;檢視中只提供XDM結構描述中的部分欄位。 您可以看到字串值以及字串、int和布林值的陣列。 例如，不會顯示`segmentMembership`陣列，因為它包含其他陣列值。

![計算欄位功能的模型視窗，尚未選取函式。](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

例如，在`loyaltyID`欄位中使用`join`函式，如下所示，將熟客ID陣列匯出為CSV檔案中與底線串連的字串。 檢視[更多關於此專案及下方](#join-function-export-arrays)其他範例的資訊。

![已選取聯結函式之計算欄位功能的模型視窗。](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以保留計算欄位並返回對應步驟。

![已選取聯結函式且已反白儲存控制項之計算欄位功能的模型視窗。](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

回到工作流程的對應步驟，在匯出的檔案中，以您要用於此欄位的欄標題值填入&#x200B;**[!UICONTROL 目標欄位]**。

![目標欄位反白顯示的對應步驟。](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![選取目標欄位2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

準備就緒後，選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以繼續執行啟動工作流程的下一步。

![目標欄位反白且目標值已填入的對映步驟。](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## 支援的函式 {#supported-functions}

將資料啟用至以檔案為基礎的目的地時，支援所有記錄的[資料準備函式](/help/data-prep/functions.md)。

但是請注意，目前以下函式僅在Beta版的計算欄位中提供廣泛的使用案例說明和範例輸出資訊，並且支援目標的陣列：

* `join`
* `coalesce`
* `size_of`
* `iif`
* `index-based array access`
* `add_to_array`
* `to_array`
* `first`
* `last`
* `sha256`
* `md5`

## 用於匯出陣列的函式範例 {#examples}

如需上述部分函式，請參閱以下章節中的範例和進一步資訊。 如需列出的其餘函式，請參閱「資料準備」區段](/help/data-prep/functions.md)中的[一般函式檔案。

### `join`函式以匯出陣列 {#join-function-export-arrays}

使用`join`函式，使用所需的分隔符號（例如`_`或`|`）將陣列元素串連到字串中。

例如，您可以使用`join('_',loyalty.loyaltyID)`語法來結合下列XDM欄位，如對應熒幕擷圖中所示：

* `"organizations": ["Marketing","Sales,"Finance"]`陣列
* `person.name.firstName`字串
* `person.name.lastName`字串
* `personalEmail.address`字串

![包含聯結函式的對應範例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-join-function.png)

在此情況下，您的輸出檔案看起來如下所示。 請注意如何使用`_`字元將陣列的三個元素串連成單一字串。

```
`First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "Marketing_Sales_Finance"
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

使用`add_to_array`函式將元素加入至匯出的陣列。 您可以將此函式與上面進一步說明的`join`函式結合。

繼續使用上方的`organizations`陣列物件，您可以撰寫類似`source: join('_', add_to_array(organizations,"2023"))`的函式，傳回人員在2023年所屬的組織。

![包括add_to_array函式的對應範例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

在此情況下，您的輸出檔案看起來如下所示。 請注意陣列中的三個元素如何使用`_`字元串連成單一字串，而2023也會附加在字串的結尾。

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

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

除了專用於從陣列匯出陣列或元素的函式之外，您還可以使用雜湊函式在匯出的檔案中雜湊屬性。 例如，如果您在屬性中有任何個人識別資訊，可在匯出這些欄位時將其雜湊化。

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