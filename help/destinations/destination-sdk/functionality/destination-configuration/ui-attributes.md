---
description: 瞭解如何為使用Destination SDK建立的目的地設定UI屬性，例如檔案連結、目的地卡片類別以及目的地連線型別和頻率。
title: UI屬性
exl-id: aed8d868-c516-45da-b224-c7e99e4bfaf1
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---

# UI屬性

UI屬性會定義Adobe應該在Adobe Experience Platform使用者介面中為目的地卡片顯示的視覺元素，例如標誌、檔案頁面的連結、目的地說明及其類別和型別。

若要瞭解此元件在何處適合使用Destination SDK建立的整合，請參閱[設定選項](../configuration-options.md)檔案中的圖表，或檢視以下目的地設定概觀頁面：

* [使用Destination SDK設定串流目的地](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [使用Destination SDK設定以檔案為基礎的目的地](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

透過Destination SDK建立[目的地](../../authoring-api/destination-configuration/create-destination-configuration.md)時，`uiAttributes`區段會定義目的地卡片的下列視覺屬性：

* [目的地目錄](../../../catalog/overview.md)中目的地檔案頁面的URL。
* Experience Platform UI中顯示您目的地的類別。
* 您目的地的資料匯出頻率。
* 目的地連線型別，例如Amazon S3、Azure Blob等。
* 您託管要在目的地目錄卡片中顯示之圖示的URL。

您可以透過`/authoring/destinations`端點設定UI屬性。 請參閱下列API參考頁面，以取得詳細的API呼叫範例，您可在此範例設定本頁面中顯示的元件。

* [建立目的地設定](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目的地設定](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文說明可用於目的地的所有受支援UI屬性，並顯示客戶將在Experience Platform UI中看到的內容。

![顯示Experience Platform介面中UI屬性的UI熒幕擷圖](../../assets/functionality/destination-configuration/ui-attributes.png)

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值都會區分大小寫&#x200B;****。 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 支援的整合型別 {#supported-integration-types}

如需瞭解哪些型別的整合支援本頁面所述功能的詳細資訊，請參閱下表。

| 整合型別 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 是 |

## 支援的引數 {#supported-parameters}

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

`documentationLink`是字串引數，參照到您目的地的[目的地目錄](../../../catalog/overview.md)中的檔案頁面。 Adobe Experience Platform中每個產品化的目的地都必須有對應的檔案頁面。 [瞭解如何為您的目的地建立目的地檔案頁面](../../docs-framework/documentation-instructions.md)。 請注意，私人/自訂目的地不需要此資訊。

使用以下格式： `http://www.adobe.com/go/destinations-YOURDESTINATION-en`，其中`YOURDESTINATION`是您目的地的名稱。 對於名為Moviestar的目的地，您可以使用`http://www.adobe.com/go/destinations-moviestar-en`。

使用者可以從UI中的目的地目錄頁面檢視和瀏覽您的檔案連結。 他們需要瀏覽到您的目的地卡片，然後選取&#x200B;**[!UICONTROL 其他動作]**，然後選取&#x200B;**[!UICONTROL 檢視檔案]**，如下圖所示。

![顯示檔案連結位置的UI影像。](../../assets/functionality/destination-configuration/ui-attributes-doc-link.png)

>[!NOTE]
>
>只有在Adobe將您的目的地設定為上線並發佈檔案後，此連結才能運作。

### `category` {#category}

`category`是字串引數，會參照指派給您Adobe Experience Platform中目的地的類別。 如需詳細資訊，請閱讀[目的地類別](../../../destination-types.md)。 使用下列其中一個值： `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`。

使用者可在目的地目錄的畫面左側看到目的地類別清單，如下圖所示。

![顯示目的地類別位置的UI影像。](../../assets/functionality/destination-configuration/ui-attributes-category.png)

### `connectionType` {#connection-type}

`connectionType`是參照連線型別的字串引數，視目的地而定。 支援的值： <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul>

使用者可在目的地工作區的[瀏覽](../../../ui/destinations-workspace.md#browse)索引標籤中看到目的地連線型別。

![UI影像顯示UI中的連線型別位置。](../../assets/functionality/destination-configuration/ui-attributes-connection.png)

### `frequency` {#frequency}

`frequency`是字串引數，參考目的地支援的資料匯出型別。 針對以API為基礎的整合設定為`Streaming`，或當您匯出檔案至目的地時設定為`Batch`。

使用者可以在每個目的地連線的&#x200B;**[!UICONTROL 資料流執行]**&#x200B;頁面中看到頻率型別。

![UI影像顯示UI中的頻率型別位置。](../../assets/functionality/destination-configuration/ui-attributes-frequency.png)

### `isBeta` {#isbeta}

如果您使用Destination SDK建立的目的地可供有限數量的客戶使用，您可能會想要將目的地目錄中的目的地卡片標示為測試版。

若要這麼做，您可以使用目的地設定之UI屬性區段中的`isBeta: "true"`引數，以適當地標示目的地卡片。

![UI影像顯示標示為Beta的目的地卡片。](../../assets/functionality/destination-configuration/ui-attributes-isbeta.png)

### `icon` {#icon}

您可以新增標誌圖示至您的目的地，如下圖所示。

![顯示圖示位置的UI影像。](../../assets/functionality/destination-configuration/ui-attributes-icon.png)

若要新增標誌至您的目的地卡片，您必須在[提交目的地以供檢閱時](../../guides/submit-destination.md#logo)，與Adobe團隊共用想要的影像。

## 後續步驟 {#next-steps}

閱讀本文後，您應該更加瞭解您可以為目的地設定哪些UI屬性，以及使用者將在Experience Platform UI中的何處看到這些屬性。

若要深入瞭解其他目的地元件，請參閱下列文章：

* [客戶驗證](customer-authentication.md)
* [OAuth2授權](oauth2-authorization.md)
* [客戶資料欄位](customer-data-fields.md)
* [結構描述設定](schema-configuration.md)
* [身分名稱空間設定](identity-namespace-configuration.md)
* [目的地傳遞](destination-delivery.md)
* [對象中繼資料設定](audience-metadata-configuration.md)
* [彙總原則](aggregation-policy.md)
* [批次設定](batch-configuration.md)
* [歷史設定檔資格](historical-profile-qualifications.md)
