---
description: 了解如何針對使用Destination SDK建置的目的地，設定UI屬性，例如說明檔案連結、目的地卡類別，以及目的地連線類型和頻率。
title: UI屬性
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---


# UI屬性

UI屬性會定義Adobe在Adobe Experience Platform使用者介面中應針對您的目的地卡片顯示的視覺元素，例如目的地平台標誌、檔案頁面的連結、目的地說明及其類別和類型。

若要了解此元件在透過Destination SDK建立的整合中的插入位置，請參閱 [配置選項](../configuration-options.md) 檔案或請參閱下列目的地組態概觀頁面：

* [使用Destination SDK來設定串流目的地](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [使用Destination SDK配置基於檔案的目標](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

當 [建立目的地](../../authoring-api/destination-configuration/create-destination-configuration.md) 透過Destination SDK, `uiAttributes` 區段會定義目的地卡片的下列視覺屬性：

* 目的地檔案頁面的URL，位於 [目的地目錄](../../../catalog/overview.md).
* 托管圖示以顯示在目的地目錄卡片中的URL。
* Platform UI中將顯示目的地的類別。
* 目的地的資料匯出頻率。
* 目的地連線類型，例如Amazon S3、Azure Blob等。

您可以透過 `/authoring/destinations` 端點。 如需詳細API呼叫範例，請參閱下列API參考頁面，您可在其中設定本頁面所示的元件。

* [建立目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目標配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文說明您可用於目的地的所有支援UI屬性，並顯示Experience PlatformUI中會顯示哪些內容。

![顯示Experience Platform介面中UI屬性的UI螢幕擷圖](../../assets/functionality/destination-configuration/ui-attributes.png)

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名稱和值均為 **區分大小寫**. 為避免區分大小寫錯誤，請使用參數名稱和值，如說明檔案所示。

## 支援的整合類型 {#supported-integration-types}

如需詳細資訊，請參閱下表以了解哪些類型的整合支援本頁面所述的功能。

| 整合類型 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 是 |

## 支援的參數 {#supported-parameters}

```json
"uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"cloudStorage",
      "connectionType":"S3",
      "frequency":"batch",
      "isBeta":"true"
   }
```

### `documentationLink` {#documentation-link}

`documentationLink` 是字串參數，會參考 [目的地目錄](../../../catalog/overview.md) 你的目的地。 Adobe Experience Platform中每個已分類的目的地都必須有對應的檔案頁面。 [了解如何建立目的地檔案頁面](../../docs-framework/documentation-instructions.md) 你的目的地。 請注意，私人/自訂目的地並非必要項目。

使用下列格式： `http://www.adobe.com/go/destinations-YOURDESTINATION-en`，其中 `YOURDESTINATION` 是您目的地的名稱。 對於名為Moviestar的目的地，您將使用 `http://www.adobe.com/go/destinations-moviestar-en`.

使用者可以從UI的目的地目錄頁面查看並造訪您的檔案連結。 他們需要瀏覽至您的目的地卡片，然後選取 **[!UICONTROL 更多動作]**，然後 **[!UICONTROL 檢視檔案]**，如下圖所示。

![顯示檔案連結位置的UI影像。](../../assets/functionality/destination-configuration/ui-attributes-doc-link.png)

>[!NOTE]
>
>此連結僅在Adobe將您的目的地設為即時且檔案已發佈後才有效。

### `category` {#category}

`category` 是字串參數，會參照指派給Adobe Experience Platform中目的地的類別。 如需詳細資訊，請閱讀 [目標類別](../../../destination-types.md). 使用下列其中一個值： `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`.

使用者可以在目的地目錄的畫面左側看到目的地類別清單，如下圖所示。

![顯示目標類別位置的UI影像。](../../assets/functionality/destination-configuration/ui-attributes-category.png)

<!-- ### `iconUrl` {#icon-url}

`iconUrl` is a string parameter that refers to the URL where you hosted the icon to be displayed in the destinations catalog card. For private custom integrations, this is not required. For productized configurations, you need to share an icon with the Adobe team when you [submit the destination for review](../../guides/submit-destination.md#logo).

Users can see the icon on your destination card, as shown in the image below.

![UI image showing the icon location.](../../assets/functionality/destination-configuration/ui-attributes-icon.png) -->

### `connectionType` {#connection-type}

`connectionType` 是參照連線類型的字串參數，視目的地而定。 支援的值： <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul>

使用者可以在 [瀏覽](../../../ui/destinations-workspace.md#browse) 目標工作區的標籤。

![顯示UI中連線類型位置的UI影像。](../../assets/functionality/destination-configuration/ui-attributes-connection.png)

### `frequency` {#frequency}

`frequency` 是字串參數，會參照您的目的地所支援的資料匯出類型。 設為 `Streaming` （適用於API型整合），或 `Batch` 將檔案匯出至目的地時。

使用者可以在 **[!UICONTROL 資料流運行]** 每個目的地連線的頁面。

![顯示UI中頻率類型位置的UI影像。](../../assets/functionality/destination-configuration/ui-attributes-frequency.png)

### `isBeta` {#isbeta}

如果您透過Destination SDK建立的目的地將可供有限數量的客戶使用，您可能會想要將目的地目錄中的目的地卡片標示為測試版。

若要這麼做，您可以使用 `isBeta: "true"` 參數（位於目的地設定的UI屬性區段中），以適當標示目的地卡片。

![顯示標示為測試版的目的地卡片的UI影像。](../../assets/functionality/destination-configuration/ui-attributes-isbeta.png)

## 後續步驟 {#next-steps}

閱讀本文後，您應該更清楚了解您可以為目的地設定的UI屬性，以及使用者在Platform UI中的哪些位置會看到這些屬性。

若要進一步了解其他目的地元件，請參閱下列文章：

* [客戶驗證](customer-authentication.md)
* [OAuth2驗證](oauth2-authentication.md)
* [客戶資料欄位](customer-data-fields.md)
* [結構配置](schema-configuration.md)
* [身分命名空間設定](identity-namespace-configuration.md)
* [目的地傳送](destination-delivery.md)
* [對象中繼資料設定](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批次設定](batch-configuration.md)
* [歷史設定檔資格](historical-profile-qualifications.md)