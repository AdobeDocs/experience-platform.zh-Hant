---
title: (Beta 版) 使用計算欄位匯出平面方案檔案中的陣列
type: Tutorial
description: 瞭解如何使用計算欄位，將平面結構描述檔案中的陣列從Real-Time CDP匯出至雲端儲存空間目的地。
badge: Beta
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: b6bdfef8b9ac5ef03ea726d668477b8629b70b6c
workflow-type: tm+mt
source-wordcount: '1481'
ht-degree: 5%

---

# (Beta 版) 使用計算欄位匯出平面方案檔案中的陣列 {#use-calculated-fields-to-export-arrays-in-flat-schema-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="(Beta 版) 匯出陣列支援"
>abstract="使用&#x200B;**新增計算欄位**&#x200B;控制項，將簡單的整數、字串或布林值陣列從 Experience Platform 匯出到您想要的雲端儲存空間目的地。存在一些限制。檢視文件了解大量範例和支援的功能。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=zh-Hant#examples" text="範例"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=zh-Hant#known-limitations" text="已知限制"

>[!AVAILABILITY]
>
>* 透過計算欄位匯出陣列的功能目前在Beta版中。 文件和功能可能會有所變更。

瞭解如何透過平面結構描述檔案中Real-Time CDP的計算欄位將陣列匯出至 [雲端儲存空間目的地](/help/destinations/catalog/cloud-storage/overview.md). 請參閱本檔案以瞭解此功能啟用的使用案例。

取得有關計算欄位的廣泛資訊 — 這些是什麼以及它們為什麼重要。 請閱讀以下連結的頁面，瞭解「資料準備」中的計算欄位，以及有關所有可用函式的詳細資訊：

* [UI指南和概觀](/help/data-prep/ui/mapping.md#calculated-fields)
* [資料準備函式](/help/data-prep/functions.md)

>[!IMPORTANT]
>
>並非上方列出的所有函式都受支援 *將欄位匯出至雲端儲存空間目的地時* 使用計算欄位功能。 請參閱 [支援的函式區段](#supported-functions) 如需詳細資訊，請參閱以下內容。

## Platform中的陣列和其他物件型別 {#arrays-strings-other-objects}

在Experience Platform中，您可以使用 [XDM結構描述](/help/xdm/home.md) 以管理不同的欄位型別。 之前，您可以將簡單的機碼值組型別欄位(例如不Experience Platform的字串)匯出至您想要的目的地。 先前支援匯出的此類欄位範例為 `personalEmail.address`：`johndoe@acme.org`.

Experience Platform中的其他欄位型別包含陣列欄位。 深入瞭解 [管理Experience PlatformUI中的陣列欄位](/help/xdm/ui/fields/array.md). 除了先前支援的欄位型別之外，您現在可以匯出陣列物件，例如： `organizations:[marketing, sales, engineering]`. 請參閱下文 [廣泛的範例](#examples) 有關如何使用各種函式來存取陣列元素、將陣列元素加入字串等。

## 已知限制 {#known-limitations}

請注意此功能Beta版的下列已知限制：

* 目前不支援匯出至具有階層式結構描述的JSON或Parquet檔案。 您只能將陣列匯出為平面結構描述CSV、JSON和Parquet檔案。
* 此時， *您只能將簡單陣列（或基本值陣列）匯出至雲端儲存目的地*. 這表示您可以匯出包含字串、int或布林值的陣列物件。 您無法匯出地圖或地圖或物件的陣列。計算欄位模型視窗只會顯示您可以匯出的陣列。

## 先決條件 {#prerequisites}

[連線](/help/destinations/ui/connect-destination.md) 前往所需的雲端儲存空間目的地，前往 [雲端儲存空間的啟用步驟](/help/destinations/ui/activate-batch-profile-destinations.md) 並前往 [對應](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 步驟。

## 如何匯出計算欄位 {#how-to-export-calculated-fields}

在雲端儲存空間目的地的啟用工作流程對應步驟中，選取 **[!UICONTROL （測試版）新增計算欄位]**.

![新增批次啟動工作流程對應步驟中反白顯示的計算欄位。](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

這會開啟一個模型視窗，您可在其中選取可用來將屬性匯出到Experience Platform之外的屬性。

>[!IMPORTANT]
>
>您的XDM結構描述中只有一些欄位可用於 **[!UICONTROL 欄位]** 檢視。 您可以看到字串值以及字串、int和布林值的陣列。 例如， `segmentMembership` 陣列不會顯示，因為它包含其他陣列值。

![尚未選取任何函式的計算欄位功能的模型視窗。](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

例如，使用 `join` 函式於 `loyaltyID` 欄位，可將熟客ID陣列匯出為CSV檔案中串連底線的字串。 檢視 [有關本專案的更多資訊，以及下面其他範例](#join-function-export-arrays).

![已選取聯結函式之計算欄位功能的模型視窗。](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

選取 **[!UICONTROL 儲存]** 以保留計算欄位並返回對應步驟。

![已選取聯結函式，且「儲存」控制項反白顯示的計算欄位功能的模型視窗。](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

回到工作流程的對應步驟，填寫 **[!UICONTROL 目標欄位]** 在匯出的檔案中，為此欄位使用您想要的欄標題值。

![反白顯示目標欄位的對應步驟。](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![選取目標欄位2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

準備就緒後，選擇 **[!UICONTROL 下一個]** 以繼續進行啟動工作流程的下一步。

![反白目標欄位並填入目標值的對應步驟。](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## 支援的函數 {#supported-functions}

請注意，測試版的計算欄位僅支援以下函式，且目的地的陣列支援：

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

如需上述部分函式，請參閱以下章節中的範例和進一步資訊。 對於列出的其餘函式，請參閱 [「資料準備」一節中的一般函式檔案](/help/data-prep/functions.md).

### `join` 匯出陣列的函式 {#join-function-export-arrays}

使用 `join` 使用所需的分隔符號（例如）將陣列元素串連到字串中的函式 `_` 或 `|`.

例如，您可以使用來組合下列XDM欄位，如對應熒幕擷圖所示 `join('_',loyalty.loyaltyID)` 語法：

* `"organizations": ["Marketing","Sales,"Finance"]` 陣列
* `person.name.firstName` 字串
* `person.name.lastName` 字串
* `personalEmail.address` 字串

![包含連線函式的對應範例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-join-function.png)

在此情況下，您的輸出檔案看起來如下所示。 請注意如何使用將陣列的三個元素串連到單一字串中 `_` 字元。

```
`First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "Marketing_Sales_Finance"
```

### `iif` 匯出陣列的函式 {#iif-function-export-arrays}

使用 `iif` 函式以匯出特定條件下的陣列元素。 例如，繼續使用 `organizations` 陣列物件，您可以撰寫簡單的條件式函式，例如 `iif(organizations[0].equals("Marketing"), "isMarketing", "isNotMarketing")`.

![包括iif函式的對應範例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-iif-function.png)

在此情況下，您的輸出檔案看起來如下所示。 在此案例中，陣列的第一個元素為行銷，因此該人員為行銷部門的成員。

```
`First_Name,Last_Name, Personal_Email, Is_Member_Of_Marketing_Dept
John,Doe, johndoe@acme.org, "isMarketing"
```

### `add_to_array` 匯出陣列的函式 {#add-to-array-function-export-arrays}

使用 `add_to_array` 將元素新增至匯出陣列的函式。 您可以將此函式與 `join` 函式中，進一步說明。

繼續使用 `organizations` 陣列物件，您可以編寫函式，如 `source: join('_', add_to_array(organizations,"2023"))`，傳回2023年個人所屬的組織。

![包括add_to_array函式的對應範例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

在此情況下，您的輸出檔案看起來如下所示。 請注意如何使用將陣列的三個元素串連到單一字串中 `_` 字元和2023也會附加在字串的末端。

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

### `coalesce` 匯出陣列的函式 {#coalesce-function-export-arrays}

使用 `coalesce` 函式，可存取陣列中的第一個非null元素並將其匯出至字串。

例如，您可以使用來組合下列XDM欄位，如對應熒幕擷圖所示 `coalesce(subscriptions.hasPromotion)` 傳回第一個 `true` 之 `false` 陣列中的值：

* `"subscriptions.hasPromotion": [null, true, null, false, true]` 陣列
* `person.name.firstName` 字串
* `person.name.lastName` 字串
* `personalEmail.address` 字串

![包括coalesce函式的對應範例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

在此情況下，您的輸出檔案看起來如下所示。 請注意第一個非空值的方式 `true` 陣列中的值會匯出至檔案中。

```
First_Name,Last_Name,hasPromotion
John,Doe,true
```

### `size_of` 匯出陣列的函式 {#sizeof-function-export-arrays}

使用 `size_of` 表示陣列中有多少元素的函式。 例如，如果您擁有 `purchaseTime` 具有多個時間戳記的陣列物件，您可以使用 `size_of` 函式，可指出某個人已進行多少次個別購買。

例如，您可以合併下列XDM欄位，如對應熒幕擷圖所示。

* `"purchaseTime": ["1538097126","1569633126,"1601255526","1632791526","1664327526"]` 陣列，指出客戶分別購買五次
* `personalEmail.address` 字串

![包括size_of函式的對應範例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

在此情況下，您的輸出檔案看起來如下所示。 請注意第二欄如何指出陣列中的元素數量，對應於客戶進行的個別購買數量。

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### 索引型陣列存取 {#index-based-array-access}

您可以存取陣列的索引，以從陣列匯出單一專案。 例如，和以上範例類似， `size_of` 功能，如果您只想在客戶首次購買特定產品時存取和匯出，則可以使用 `purchaseTime[0]` 若要匯出時間戳記的第一個元素， `purchaseTime[1]` 若要匯出時間戳記的第二個元素， `purchaseTime[2]` 匯出時間戳記的第三個元素，依此類推。

![顯示如何存取陣列元素的對應範例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

在此情況下，您的輸出檔案看起來如下所示，會在客戶首次購買時匯出：

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first` 和 `last` 匯出陣列的函式 {#first-and-last-functions-export-arrays}

使用 `first` 和 `last` 函式匯出陣列中的第一個或最後一個元素。 例如，繼續使用 `purchaseTime` 具有前述範例中多個時間戳記的陣列物件，您可以使用這些至函式，匯出個人進行的首次或上次購買時間。

![包含第一個和最後一個函式的對應範例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

在此情況下，您的輸出檔案看起來如下所示，匯出客戶第一次和最後一次購買的時間：

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

### 雜湊函式 {#hashing-functions}

除了專用於從陣列匯出陣列或元素的函式之外，您還可以使用雜湊函式在匯出的檔案中雜湊屬性。 例如，如果您在屬性中有任何個人識別資訊，可在匯出這些欄位時將其雜湊化。

例如，您可以直接雜湊字串值 `md5(personalEmail.address)`. 如有需要，您也可以雜湊陣列欄位的個別元素，假設陣列中的元素是字串，如下所示： `md5(purchaseTime[0])`

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