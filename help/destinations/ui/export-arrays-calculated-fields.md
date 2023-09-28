---
title: （Beta版）使用計算欄位匯出平面檔案中的陣列
type: Tutorial
description: 瞭解如何從Real-Time CDP將陣列和計算欄位匯出到批次設定檔型目的地。
badge: "Beta"
source-git-commit: 79924b9a7d5114c94a004f99fb194102845b2127
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 2%

---


# （測試版）使用計算欄位匯出平面結構描述檔案中的陣列 {#use-calculated-fields-to-export-arrays-in-flat-schema-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="(Beta)匯出陣列支援"
>abstract="從Experience Platform將簡單的int、字串或布林值陣列匯出至您所需的雲端儲存空間目的地。 部分限制適用。 檢視檔案以取得廣泛的範例和支援的函式。"

<!--

additional links for contextualhelp:

>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#examples" text="Examples"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#known-limitations" text="Known limitations"

-->

>[!AVAILABILITY]
>
>* 透過計算欄位匯出陣列的功能目前在Beta版中。 文件和功能可能會有所變更。

瞭解如何透過計算欄位，將平面結構描述檔案中的Real-Time CDP陣列匯出至雲端儲存目標。 請參閱本檔案以瞭解此功能啟用的使用案例。

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

進度 [雲端儲存空間的啟用步驟](/help/destinations/ui/activate-batch-profile-destinations.md) 並前往 [對應](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 步驟。

## 如何匯出計算欄位 {#how-to-export-calculated-fields}

在雲端儲存空間目的地的啟用工作流程對應步驟中，選取 **[!UICONTROL （測試版）新增計算欄位]**.

![新增要匯出的計算欄位](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

這會開啟一個模型視窗，您可在其中選取可用來將屬性匯出到Experience Platform之外的屬性。

>[!IMPORTANT]
>
>您的XDM結構描述中只有一些欄位可用於 **[!UICONTROL 欄位]** 檢視。 您可以看到字串值以及字串、int和布林值的陣列。 例如， `segmentMembership` 陣列不會顯示，因為它包含其他陣列值。

![強制回應視窗1](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

例如，使用 `join` 函式於 `loyaltyID` 欄位，可將熟客ID陣列匯出為CSV檔案中串連底線的字串。 檢視 [有關本專案的更多資訊，以及下面其他範例](#join-function-export-arrays).

![強制回應視窗2](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

選取 **[!UICONTROL 儲存]** 以保留計算欄位並返回對應步驟。

![強制回應視窗3](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

回到工作流程的對應步驟，填寫 **[!UICONTROL 目標欄位]** 在匯出的檔案中，為此欄位使用您想要的欄標題值。

![選取目標欄位1](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![選取目標欄位2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

準備就緒後，選擇 **[!UICONTROL 下一個]** 以繼續進行啟動工作流程的下一步。

![選取「下一步」以繼續](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

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

![對應熒幕擷圖](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-join-function.png)

在此情況下，您的輸出檔案看起來如下所示。 請注意如何使用將陣列的三個元素串連到單一字串中 `_` 字元。

```
`First_Name,Last_Name,Organization
John,Doe,"Marketing_Sales_Finance"
```

### `coalesce` 匯出陣列的函式 {#coalesce-function-export-arrays}

使用 `coalesce` 函式，可存取陣列中的第一個非null元素並將其匯出至字串。

例如，您可以使用來組合下列XDM欄位，如對應熒幕擷圖所示 `coalesce(subscriptions.hasPromotion)` 語法以傳回陣列中false值的第一個true：

* `"subscriptions.hasPromotion": [null, true, null, false, true]` 陣列
* `person.name.firstName` 字串
* `person.name.lastName` 字串
* `personalEmail.address` 字串

![對應Coalesce函式的熒幕擷圖](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

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

![對應size_of函式的熒幕擷取畫面](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

在此情況下，您的輸出檔案看起來如下所示。 請注意第二欄如何指出陣列中的元素數量，對應於客戶進行的個別購買數量。

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### 索引型陣列存取 {#index-based-array-access}

您可以存取陣列的索引，以從陣列匯出單一專案。 例如，和以上範例類似， `size_of` 功能，如果您只想在客戶首次購買特定產品時存取和匯出，則可以使用 `purchaseTime[0]` 若要匯出時間戳記的第一個元素， `purchaseTime[1]` 若要匯出時間戳記的第二個元素， `purchaseTime[2]` 匯出時間戳記的第三個元素，依此類推。

![對應用於存取索引的熒幕擷取畫面](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

在此案例中，您的輸出檔案看起來像這樣：

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first` 和 `last` 匯出陣列的函式 {#first-and-last-functions-export-arrays}

使用 `first` 和 `last` 函式匯出陣列中的第一個或最後一個元素。 例如，繼續使用 `purchaseTime` 具有前述範例中多個時間戳記的陣列物件，您可以使用這些至函式，匯出個人進行的首次或上次購買時間。

![對應第一個和最後一個函式的熒幕擷圖](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

在此案例中，您的輸出檔案看起來像這樣：

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

<!--

### `iif` function to export arrays {#iif-function-export-arrays}

Here are some examples of how you could use the `iif` function to access and export arrays and other fields: (STILL TO DO)

-->

### `md5` 和 `sha256` 雜湊函式 {#hashing-functions}

除了專用於從陣列匯出陣列或元素的函式之外，您還可以使用雜湊函式來雜湊屬性。 例如，如果您在屬性中有任何個人識別資訊，可在匯出這些欄位時將其雜湊化。

例如，您可以直接雜湊字串值 `md5(personalEmail.address)`. 如有需要，您也可以將陣列欄位的個別元素進行雜湊處理，如下所示： `md5(purchaseTime[0])`



