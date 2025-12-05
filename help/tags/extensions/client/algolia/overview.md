---
title: Algoria標籤擴充功能概觀
description: 瞭解Adobe Experience Platform中的Algolia標籤擴充功能。
exl-id: 8409bf8b-fae2-44cc-8466-9942f7d92613
source-git-commit: 6eee26df3841a7829625361fc726bf59a278f867
workflow-type: tm+mt
source-wordcount: '1954'
ht-degree: 1%

---

# [!DNL Algolia]標籤擴充功能概觀

[!DNL Algolia]標籤擴充功能可讓行銷人員輕鬆設定規則，將使用者互動資料傳送至[!DNL Algolia]，協助您提供更個人化的AI搜尋和探索體驗。

此擴充功能由主要功能提供支援：

* **[!DNL Algolia]深入分析**：自動擷取使用者互動事件並傳送至[!DNL Algolia]，如此可啟用強大的分析、個人化體驗並改善搜尋關聯性。

## 先決條件 {#prerequisites}

您必須擁有有效的[!DNL Algolia]帳戶才能使用此擴充功能。 移至[[!DNL Algolia] 註冊頁面](https://dashboard.algolia.com/users/sign_up)以建立帳戶（如果尚未建立）。

### 收集必要的設定詳細資料 {#configuration-details}

若要將[!DNL Algolia]與Adobe Experience Platform連線，您需要下列資訊：

| 認證 | 說明 | 範例 |
| --- | --- | --- |
| 應用程式ID | 您可以在[儀表板的](https://www.algolia.com/account/api-keys/all)API金鑰[!DNL Algolia]區段中找到您的應用程式ID。 | 0ABCDEFG12 |
| 搜尋API金鑰 | 您可以在[儀表板的](https://www.algolia.com/account/api-keys/all)API金鑰[!DNL Algolia]區段中找到您的搜尋API金鑰。 | 1234a12345678901b1234567890c1ab1 |

## 安裝並設定[!DNL Algolia] Insights擴充功能 {#install-configure}

若要安裝[!DNL Algolia] Insights擴充功能，請導覽至[!UICONTROL Data Collection UI]並從左側導覽中選取&#x200B;**[!UICONTROL Tags]**。 從這裡，選取要新增擴充功能的屬性，或改為建立新屬性。

選取或建立所需的屬性後，在左側導覽中選取「**[!UICONTROL Extensions]**」，然後選取「**[!UICONTROL Catalog]**」標籤。 搜尋[!DNL Algolia]深入分析卡片，然後選取&#x200B;**[!UICONTROL Install]**。

![](../../../images/extensions/client/algolia/install.png)

在出現的組態檢視中，您必須提供下列詳細資訊：

| 屬性 | 說明 |
| --- | --- |
| [!UICONTROL Application ID] | 輸入您先前在[!UICONTROL Application Id]組態詳細資料[區段中收集的](#configuration-details)。 |
| [!UICONTROL Search API Key] | 輸入您先前在[!UICONTROL Search API Key]組態詳細資料[區段中收集的](#configuration-details)。 |
| [!UICONTROL Index Name] | [!UICONTROL Index Name]包含產品或內容。  此索引將用作預設值。 |
| [!UICONTROL User Token Data Element] | 將傳回使用者權杖的資料元素。 |
| [!UICONTROL Authenticated User Token Data Element] | 設定將傳回已驗證使用者權杖的資料元素。 |
| [!UICONTROL Currency Code] | 以ISO-4217格式輸入貨幣代碼，例如USD或EUR。 此欄位支援資料元素。 |

![](../../../images/extensions/client/algolia/configure.png)

## [!DNL Algolia]個Insights延伸動作型別 {#action-types}

[!DNL Algolia]支援一組預先定義的標準事件，每個事件都有特定的內容和屬性。 [!DNL Algolia]擴充功能中可用的動作符合這些事件型別，可讓您根據事件型別輕鬆分類及設定您傳送給[!DNL Algolia]的事件。

### 載入Insights {#load-insights}

>[!NOTE]
>
>在大多數情況下，建議您在網站的每個頁面載入[!DNL Algolia]深入分析。

將&#x200B;**[!UICONTROL Load Insights]**&#x200B;動作新增至您的標籤規則，只要是根據您規則的內容載入[!DNL Algolia]深入分析最合理。 此動作會將`search-insights.js`程式庫載入頁面上。

建立新標籤規則或開啟現有標籤規則。 根據您的需求定義條件，然後選取&#x200B;**[!UICONTROL Algolia]**&#x200B;作為[!UICONTROL Extension]，並選取&#x200B;**[!UICONTROL Load Insights]**&#x200B;作為[!UICONTROL Action Type]。

| 屬性 | 說明 |
| --- | --- |
| [!UICONTROL Insight Library Version] | [!DNL Algolia]深入分析版本。 預設值為 `2.17.3`。 |
| [!UICONTROL User Opt Out Data Element] | 擷取使用者追蹤偏好設定的資料元素。 |
| [!UICONTROL Use User Token Cookie] | 核取此方塊可允許[!DNL Algolia]產生使用者權杖Cookie。 依預設，此選項設定為`true`。 |

![](../../../images/extensions/client/algolia/load-insights.png)

### 已點按 {#clicked}

將&#x200B;**[!UICONTROL Click]**&#x200B;動作新增至您的標籤規則，以將點選事件傳送至[!DNL Algolia]。 建立新標籤規則或開啟現有標籤規則。 根據您的需求定義條件，然後選取&#x200B;**[!UICONTROL Algolia]**&#x200B;作為[!UICONTROL Extension]，並選取&#x200B;**[!UICONTROL Clicked]**&#x200B;作為[!UICONTROL Action Type]。

| 屬性 | 說明 |
| --- | --- |
| [!UICONTROL Event Name] | 事件名稱，可用來進一步調整此點按事件。 |
| [!UICONTROL Event Details Data Element] | 資料元素會傳回JSON格式的事件詳細資料，包括： <ul><li>`indexName`</li><li>`objectIDs`</li><li>`queryID` （選擇性）</li><li>`positions` （選擇性）</li><li>`price` （選擇性）</li><li>`quantity` （選擇性）</li><li>`discount` （選擇性）</li><li>`objectData` （選擇性）</li><li>`currency` （選擇性）</li></ul> |


>[!NOTE]
>
>如果同時包含`queryID`和`positions`，則事件在搜尋&#x200B;**後會分類為**&#x200B;已點按物件ID。 否則，它被分類為&#x200B;**點選物件識別碼**&#x200B;事件。
><br>
>如果資料元素未提供`indexName`，則會在傳送事件時使用&#x200B;**預設索引名稱**。

![](../../../images/extensions/client/algolia/clicked.png)

如需事件類別的詳細資訊，請參閱搜尋後的[點選物件識別碼](https://www.algolia.com/doc/api-reference/api-methods/clicked-object-ids-after-search/)
和[已點按物件識別碼](https://www.algolia.com/doc/api-reference/api-methods/clicked-object-ids/)參考線。

### 已轉換 {#converted}

將&#x200B;**[!UICONTROL Converted]**&#x200B;動作新增至您的標籤規則，以將轉換的事件傳送至[!DNL Algolia]。 建立新標籤規則或開啟現有標籤規則。 根據您的需求定義條件，然後選取&#x200B;**[!UICONTROL Algolia]**&#x200B;作為[!UICONTROL Extension]，並選取&#x200B;**[!UICONTROL Converted]**&#x200B;作為[!UICONTROL Action Type]。

| 屬性 | 說明 |
| --- | --- |
| [!UICONTROL Event Name] | 將用於進一步調整此&#x200B;**轉換**&#x200B;事件的事件名稱。 |
| [!UICONTROL Event Details Data Element] | 資料元素會傳回事件詳細資料，包括： <ul><li>`indexName`</li><li>`objectIDs`</li><li>`queryID` （選擇性）</li><li>`recordID` （選擇性）</li></ul> |

>[!NOTE]
>
>如果資料元素包含`queryId`，則事件在搜尋後會分類為&#x200B;**已轉換**。 否則，它將被分類為&#x200B;**已轉換**&#x200B;事件。
><br>
>如果資料元素未提供`indexName`，則會在傳送事件時使用&#x200B;**預設索引名稱**。

![](../../../images/extensions/client/algolia/converted.png)

如需事件類別的詳細資訊，請參閱搜尋後的[轉換的物件識別碼](https://www.algolia.com/doc/api-reference/api-methods/converted-object-ids-after-search/)和[轉換的物件識別碼](https://www.algolia.com/doc/api-reference/api-methods/converted-object-ids/)指南。

### 已新增至購物車 {#added-to-cart}

將&#x200B;**[!UICONTROL Added to Cart]**&#x200B;動作新增至您的標籤規則，以將新增至購物車事件的動作傳送至[!DNL Algolia]。 建立新標籤規則或開啟現有標籤規則。 根據您的需求定義條件，然後選取&#x200B;**[!UICONTROL Algolia]**&#x200B;作為[!UICONTROL Extension]，並選取&#x200B;**[!UICONTROL Added to cart]**&#x200B;作為[!UICONTROL Action Type]。

| 屬性 | 說明 |
| --- | --- |
| [!UICONTROL Event Name] | 將用於進一步調整此&#x200B;**加入購物車**&#x200B;事件的事件名稱。 |
| [!UICONTROL Event Details Data Element] | 資料元素會傳回JSON格式的事件詳細資料，包括： <ul><li>`indexName`</li><li>`objectIDs`</li><li>`objectData`</li><li>`price`</li><li>`quantity`</li><li>`discount` （選擇性）</li><li>`queryID` （選擇性）</li><li>`currency` （選擇性）</li></ul>。 |

>[!NOTE]
>
>如果資料元素包含`queryId`，則事件將會分類為&#x200B;**，在搜尋**&#x200B;後新增到購物車物件ID。 否則，它將分類為&#x200B;**新增到購物車物件識別碼**&#x200B;事件。
><br>
>如果資料元素未提供`indexName`，則會在傳送事件時使用&#x200B;**預設索引名稱**。
><br>
>如果預設資料元素不符合您的需求，可以建立自訂的單一資料元素以傳回所需的事件詳細資訊。

![](../../../images/extensions/client/algolia/added-to-cart.png)

如需事件類別的詳細資訊，請參閱[搜尋後新增到購物車物件ID](https://www.algolia.com/doc/api-reference/api-methods/added-to-cart-object-ids-after-search/)和[新增到購物車物件ID](https://www.algolia.com/doc/api-reference/api-methods/added-to-cart-object-ids/)指南。

### 已購買 {#purchased}

將&#x200B;**[!UICONTROL Purchased]**&#x200B;動作新增至您的標籤規則，以將已購買的事件傳送至[!DNL Algolia]。 建立新標籤規則或開啟現有標籤規則。 根據您的需求定義條件，然後選取&#x200B;**[!UICONTROL Algolia]**&#x200B;作為[!UICONTROL Extension]，並選取&#x200B;**[!UICONTROL Purchased]**&#x200B;作為[!UICONTROL Action Type]。

| 屬性 | 說明 |
| --- | --- |
| [!UICONTROL Event Name] | 將用於進一步調整此&#x200B;**購買**&#x200B;事件的事件名稱。 |
| [!UICONTROL Event Details Data Element] | 資料元素會傳回JSON格式的事件詳細資料，包括： <ul><li>`indexName`</li><li>`objectIDs`</li><li>`objectData`</li><li>`price`</li><li>`quantity`</li><li>`discount` （選擇性）</li><li>`queryID` （選擇性）</li><li>`currency` （選擇性）</li></ul>。 |

>[!NOTE]
>
>「已購買」動作會根據已購買的專案ID從瀏覽器儲存空間中擷取事件資料。 如果任何購買的專案在其儲存的資料中包含`queryID`，則搜尋後&#x200B;**事件將被分類為**&#x200B;購買物件ID。 否則，將被分類為&#x200B;**已購買物件識別碼**&#x200B;事件。
><br>
>此方法可讓購買事件自動包含使用者先前與專案互動的所有相關內容（查詢ID、索引名稱、價格、數量、折扣）。

![](../../../images/extensions/client/algolia/purchased.png)

如需事件類別的詳細資訊，請參閱搜尋後的[購買物件ID](https://www.algolia.com/doc/api-reference/api-methods/purchased-object-ids-after-search/)
和[已購買的物件識別碼](https://www.algolia.com/doc/api-reference/api-methods/purchased-object-ids/)參考線。

### 已檢視 {#viewed}

將&#x200B;**[!UICONTROL Viewed]**&#x200B;動作新增至您的標籤規則，以將已購買的事件傳送至[!DNL Algolia]。 建立新標籤規則或開啟現有標籤規則。 根據您的需求定義條件，然後選取&#x200B;**[!UICONTROL Algolia]**&#x200B;作為[!UICONTROL Extension]，並選取&#x200B;**[!UICONTROL Viewed]**&#x200B;作為[!UICONTROL Action Type]。

| 屬性 | 說明 |
| --- | --- |
| [!UICONTROL Event Name] | 將用於進一步調整此&#x200B;**檢視**&#x200B;事件的事件名稱。 |
| [!UICONTROL Event Details Data Element] | 資料元素會傳回JSON格式的事件詳細資料，包括： <ul><li>`indexName`</li><li>`objectIDs`</li></ul> |

>[!NOTE]
>
>如果資料元素未提供`indexName`，則在傳送事件時將使用&#x200B;**預設索引名稱**。

![](../../../images/extensions/client/algolia/viewed.png)

如需檢視事件的詳細資訊，請參閱[已檢視物件識別碼](https://www.algolia.com/doc/api-reference/api-methods/viewed-object-ids/)指南。

## [!DNL Algolia]個Insights延伸資料元素 {#data-elements}

[!DNL Algolia]支援一組預先定義的資料元素，每個元素都有特定的內容和屬性。 以下章節說明[!DNL Algolia] Insights擴充功能中可用的資料元素。

### 資料集 {#dataset}

DataSet Data Element會擷取與HTML元素相關聯的資料，這些資料隨後用於[!DNL Algolia]動作。 此資料元素會自動將擷取的事件資料儲存在瀏覽器儲存空間中以供稍後使用（例如轉換或購買事件）。

**一般組態：**

| 屬性 | 說明 |
| --- | --- |
| [!UICONTROL Hit Element Div/Class Name] | 包含資料集屬性的HTML元素名稱和/或CSS類別名稱，包括HTML元素上的`data-insights-object-id`以及選擇性的`data-insights-query-id`和`data-insights-position`。 |
| [!UICONTROL Index Name Element Div/Class Name] | 在HTML元素上具有資料集屬性(`data-indexname`)的HTML元素名稱和/或CSS類別名稱。 |

**Commerce設定（選擇性）：**

| 屬性 | 說明 |
| --- | --- |
| [!UICONTROL Price Data Element] | 傳回專案價格的資料元素。 若提供，這會包含在商務事件的已儲存事件資料中。 |
| [!UICONTROL Quantity Data Element] | 傳回專案數量的資料元素。 若未提供，則預設為1。 |
| [!UICONTROL Discount Data Element] | 傳回專案折扣小數值的資料元素。 |
| [!UICONTROL Currency Code] | ISO-4217格式的貨幣代碼。 若未指定貨幣代碼，則會使用擴充功能設定的預設貨幣。 |

**覆寫（選擇性）：**

這些欄位可讓您覆寫從HTML資料集屬性擷取資料的預設行為。

| 屬性 | 說明 |
| --- | --- |
| [!UICONTROL Record ID Data Element] | 覆寫使用頁面URL作為記錄ID的預設方法。 記錄ID可用來儲存及查詢資料，以傳送至此產品/頁面的[!DNL Algolia]。 |
| [!UICONTROL Query ID Data Element] | 查詢ID會從HTML元素的資料集中擷取。 若要覆寫此行為，請使用此屬性來提供將查詢ID傳回為字串的資料元素。 |
| [!UICONTROL Object IDs Data Element] | 物件ID會從HTML元素的資料集中擷取。 若要覆寫此行為，請使用此屬性來提供將物件ID傳回為陣列的資料元素。 |
| [!UICONTROL Positions Data Element] | 系統會從HTML元素的資料集中擷取位置。 若要覆寫此行為，請使用此屬性來提供資料元素，該資料元素會以陣列形式傳回Positions。 |
| [!UICONTROL Index Name Data Element] | 索引名稱會從HTML元素的資料集中擷取。 若要覆寫此行為，請使用此屬性來提供將傳回索引名稱作為字串的資料元素。 |

![](../../../images/extensions/client/algolia/dataset.png)

此資料元素會傳回：

```javascript
{
  timestamp,
  queryID,
  indexName,
  objectIDs,
  positions,
  objectData,  // Optional: commerce data if price is provided
  currency,    // Optional: if provided
  recordID
}
```

包含資料集的HTML範例：

```html
<div data-indexname="acme_master_default_products" class="instant-search-comp__hits">
  <div class="hit-card"
    data-insights-object-id="${hit.objectID}"
    data-insights-position="${hit.__position}"
    data-insights-query-id="${hit.__queryID}">
    <h4 class="hit-name">...</h4>   
  </div>
</div>
```

### 查詢字串 {#query-string}

查詢字串資料元素會從URL查詢字串擷取資料，以用於[!DNL Algolia]動作。

| 屬性 | 說明 |
| --- | --- |
| [!UICONTROL Object ID Param Name] | 包含物件ID的查詢引數名稱。 |
| [!UICONTROL Index Name Param Name] | 包含索引名稱的查詢引數名稱。 |
| [!UICONTROL Query ID Param Name] | 包含查詢ID的查詢引數名稱。 |
| [!UICONTROL Position Param Name] | 包含「位置」的查詢引數名稱。 |

![](../../../images/extensions/client/algolia/query-string.png)

此資料元素會傳回：

```javascript
{
  timestamp,
  queryID,
  indexName,
  objectIDs,
  positions
}
```

包含查詢引數的HTML範例：

```html
<a href="product.html?objectID=${hit.objectID}&queryID=${hit.__queryID}&indexName=${indexName}&position=${hit.position}">Read More</a>
```

### 儲存空間 {#storage}

存放裝置資料元素會從瀏覽器工作階段存放裝置擷取資料，以用於[!DNL Algolia]動作。 此資料元素也可用來以其他商業資訊來增強已儲存的資料。

此資料元素會擷取先前儲存在工作階段存放區中的事件詳細資料（通常是由點選事件期間的DataSet資料元素所儲存）。 除非明確停用移除，否則資料會在轉換事件期間自動移除。

**覆寫（選擇性）：**

| 屬性 | 說明 |
| --- | --- |
| [!UICONTROL Record ID Data Element] | 記錄ID會作為索引鍵，用於查閱儲存在瀏覽器儲存體中的事件資料。 頁面URL是預設的記錄ID。 若要覆寫此行為，請使用此屬性來提供將記錄ID傳回為字串的資料元素。 |
| [!UICONTROL Price Data Element] | 傳回專案價格的資料元素。 如果提供，這將會以價格資訊更新儲存的事件資料。 |
| [!UICONTROL Quantity Data Element] | 傳回專案數量的資料元素。 如果提供，這將會以數量資訊更新儲存的事件資料。 |
| [!UICONTROL Discount Data Element] | 傳回專案折扣小數值的資料元素。 如果提供，這將會以折扣資訊更新儲存的事件資料。 |
| [!UICONTROL Currency Code] | 以ISO-4217格式輸入貨幣代碼。 如果提供，這將會以貨幣資訊更新儲存的事件資料。 |

![](../../../images/extensions/client/algolia/storage.png)

此資料元素會傳回工作階段存放區中儲存的內容，包括任何增強的商務資料：

```javascript
{
  timestamp,
  queryID,
  indexName,
  objectIDs,
  positions,      // If available from original event
  objectData,     // Optional: commerce data if price is provided
  currency,       // Optional: if provided
  recordID
}
```

## 搜尋後點選或轉換 {#clicked-converted-after-search}

搜尋&#x200B;*後按的*&#x200B;或&#x200B;*搜尋後轉換的*&#x200B;事件需要`queryID`，搜尋後按的`positions`也需要&#x200B;**。 在InstantSearch和/或Autocomplete查詢引數中啟用`insights`旗標時，這些屬性即可使用。 請參閱下列資源，瞭解如何設定網站的Insights：

* [在自動完成時設定深入分析](https://www.algolia.com/doc/ui-libraries/autocomplete/api-reference/autocomplete-js/autocomplete/#param-insights)
* [在InstantSearch.js上設定深入分析](https://www.algolia.com/doc/guides/building-search-ui/events/js/#set-the-insights-option-to-true)
* [開始使用點按和轉換事件](https://www.algolia.com/doc/guides/sending-events/implementing/how-to/sending-events-backend/)
* [傳送 [!DNL Algolia] 深入分析事件](https://www.algolia.com/doc/ui-libraries/autocomplete/guides/sending-algolia-insights-events/)
* [[!DNL Algolia] 啟動擴充功能GitHub存放庫](https://github.com/algolia/algolia-launch-extension)
* [InstantSearch.js檔案](https://www.algolia.com/doc/guides/building-search-ui/what-is-instantsearch/js/)
* [[!DNL Algolia] 深入分析API檔案](https://www.algolia.com/doc/rest-api/insights/)
* [Algoria Launch擴充功能程式碼存放庫](https://github.com/algolia/algolia-launch-extension)

## 後續步驟 {#next-steps}

本指南說明如何使用[!DNL Algolia]標籤延伸將資料傳送至[!DNL Algolia Insights]。 如果您也打算將伺服器端事件傳送至[!DNL Algolia]，您現在可以繼續安裝並設定[[!DNL Conversions API] 事件轉送擴充功能](../../server/algolia/overview.md)。

如需Experience Platform標籤的詳細資訊，請參閱[標籤總覽](../../../home.md)。
