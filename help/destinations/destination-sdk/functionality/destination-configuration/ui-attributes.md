---
description: 瞭解如何為使用Destination SDK構建的目標配置UI屬性，如文檔連結、目標卡類別以及目標連接類型和頻率。
title: UI屬性
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---


# UI屬性

UI屬性定義了Adobe在Adobe Experience Platform用戶介面中為目標卡顯示的可視元素，如目標平台徽標、指向文檔頁的連結、目標說明及其類別和類型。

要瞭解此元件在與Destination SDK建立的整合中的位置，請參閱 [配置選項](../configuration-options.md) 文檔，或參閱以下目標配置概述頁：

* [使用Destination SDK配置流目標](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [使用Destination SDK配置基於檔案的目標](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

當 [建立目標](../../authoring-api/destination-configuration/create-destination-configuration.md) 通過Destination SDK, `uiAttributes` 部分定義目標卡的以下可視屬性：

* 目標文檔頁的URL [目標目錄](../../../catalog/overview.md)。
* 承載要顯示在目標目錄卡中的表徵圖的URL。
* 在平台UI中顯示目標的類別。
* 目標的資料導出頻率。
* 目標連接類型，如AmazonS3、Azure Blob等。

您可以通過 `/authoring/destinations` 端點。 有關詳細的API調用示例，請參閱以下API參考頁，在這些示例中可以配置此頁中顯示的元件。

* [建立目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目標配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文介紹可用於目標的所有支援的UI屬性，並顯示客戶將在Experience PlatformUI中看到的內容。

![顯示Experience Platform介面中UI屬性的UI螢幕快照](../../assets/functionality/destination-configuration/ui-attributes.png)

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 支援的整合類型 {#supported-integration-types}

有關哪些類型的整合支援本頁所述功能的詳細資訊，請參閱下表。

| 整合類型 | 支援功能 |
|---|---|
| 即時（流）整合 | 是 |
| 基於檔案（批處理）的整合 | 是 |

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

`documentationLink` 是一個字串參數，它引用了 [目標目錄](../../../catalog/overview.md) 你的目的地。 Adobe Experience Platform的每個已生產目的地都必須有相應的文檔頁面。 [瞭解如何建立目標文檔頁面](../../docs-framework/documentation-instructions.md) 你的目的地。 請注意，對於專用/自定義目標，不需要此功能。

使用以下格式： `http://www.adobe.com/go/destinations-YOURDESTINATION-en`，也請參見Wiki頁。 `YOURDESTINATION` 是目標的名稱。 對於名為Moviestar的目標，您將使用 `http://www.adobe.com/go/destinations-moviestar-en`。

用戶可以從UI的目標目錄頁面查看和訪問文檔連結。 他們需要瀏覽到您的目標卡，然後選擇 **[!UICONTROL 更多操作]**，然後 **[!UICONTROL 查看文檔]**，如下圖所示。

![顯示文檔連結位置的UI影像。](../../assets/functionality/destination-configuration/ui-attributes-doc-link.png)

>[!NOTE]
>
>此連結僅在Adobe設定目標即時並發佈文檔後才起作用。

### `category` {#category}

`category` 是一個字串參數，它引用分配給您在Adobe Experience Platform的目標的類別。 有關詳細資訊，請閱讀 [目標類別](../../../destination-types.md)。 使用以下值之一： `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`。

用戶可以在目標目錄中查看螢幕左側的目標類別清單，如下圖所示。

![顯示目標類別位置的UI影像。](../../assets/functionality/destination-configuration/ui-attributes-category.png)

<!-- ### `iconUrl` {#icon-url}

`iconUrl` is a string parameter that refers to the URL where you hosted the icon to be displayed in the destinations catalog card. For private custom integrations, this is not required. For productized configurations, you need to share an icon with the Adobe team when you [submit the destination for review](../../guides/submit-destination.md#logo).

Users can see the icon on your destination card, as shown in the image below.

![UI image showing the icon location.](../../assets/functionality/destination-configuration/ui-attributes-icon.png) -->

### `connectionType` {#connection-type}

`connectionType` 是一個字串參數，它引用連接類型，具體取決於目標。 支援的值： <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul>

用戶可以在 [瀏覽](../../../ui/destinations-workspace.md#browse) 頁籤。

![顯示UI中連接類型位置的UI影像。](../../assets/functionality/destination-configuration/ui-attributes-connection.png)

### `frequency` {#frequency}

`frequency` 是一個字串參數，它引用目標支援的資料導出類型。 設定為 `Streaming` 用於基於API的整合，或 `Batch` 將檔案導出到目標。

用戶可以在 **[!UICONTROL 資料流運行]** 每個目標連接的頁面。

![顯示UI中頻率類型位置的UI影像。](../../assets/functionality/destination-configuration/ui-attributes-frequency.png)

### `isBeta` {#isbeta}

如果您使用Destination SDK建立的目標將對數量有限的客戶可用，則您可能希望將目標目錄中的目標卡標籤為beta。

要執行此操作，可使用 `isBeta: "true"` 目標配置的UI屬性部分中的參數，以適當標籤目標卡。

![顯示標籤為beta的目標卡的UI影像。](../../assets/functionality/destination-configuration/ui-attributes-isbeta.png)

## 後續步驟 {#next-steps}

閱讀本文後，您應該更清楚地瞭解您可以為目標配置哪些UI屬性，以及用戶在平台UI中將在何處看到這些屬性。

要瞭解有關其他目標元件的詳細資訊，請參閱以下文章：

* [客戶驗證](customer-authentication.md)
* [OAuth2身份驗證](oauth2-authentication.md)
* [客戶資料欄位](customer-data-fields.md)
* [架構配置](schema-configuration.md)
* [標識命名空間配置](identity-namespace-configuration.md)
* [目標傳遞](destination-delivery.md)
* [受眾元資料配置](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批配置](batch-configuration.md)
* [歷史配置檔案資格](historical-profile-qualifications.md)