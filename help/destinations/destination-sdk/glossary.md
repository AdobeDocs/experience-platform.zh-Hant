---
solution: Experience Platform
title: Adobe Experience Platform Destination SDK字彙表
description: 瞭解使用Experience PlatformDestination SDK製作目的地時的重要術語。
exl-id: d65f390a-a980-49b8-9570-840f03534553
source-git-commit: a11f469cb54421e0ca30c7c5878128e216470f7f
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 1%

---

# Adobe Experience Platform Destination SDK字彙表

如需Destination SDK中所用辭彙的定義，請參閱本辭彙表。 如需其他Adobe Experience Platform術語，請參閱[Experience Platform字彙表](/help/landing/glossary.md)。

## A

**彙總原則**：在設定如何將資料匯出至您的即時串流目的地時，您可以定義在傳送至目的地平台之前，如何彙總設定檔資料。 這有助於最佳化資料傳送，方法是根據特定條件將資料記錄分組、降低API呼叫的頻率，並改善整體效率。 您可以設定不同的原則來滿足各種目的地需求，確保以最有效的方式封裝和傳送資料。 [閱讀全文](/help/destinations/destination-sdk/functionality/destination-configuration/aggregation-policy.md)。

**對象中繼資料組態**：對象中繼資料組態參考Adobe Experience Platform中定義的結構化設定和引數，可讓您以程式設計方式在指定目的地建立、更新和刪除對象區段。 此設定使用對象中繼資料範本，以符合目的地平台之行銷API的規格。 深入瞭解[對象中繼資料組態](/help/destinations/destination-sdk/functionality/audience-metadata-management.md)和[可用的巨集](/help/destinations/destination-sdk/functionality/audience-metadata-management.md#macros)。

## D

**目的地設定端點**： Adobe Experience Platform中的目的地設定端點（尤其是`/authoring/destinations` API端點）用於建立、擷取、更新和刪除目的地的設定。 這些設定會定義如何將來自Adobe Experience Platform的資料傳遞至各種外部系統或目的地，例如行銷平台、雲端儲存服務或其他資料處理端點。 深入瞭解[可用的組態選項](/help/destinations/destination-sdk/functionality/configuration-options.md#destination-configuration)，並檢視[參考檔案](/help/destinations/destination-sdk/authoring-api/destination-configuration/create-destination-configuration.md)。

**目的地執行個體**： Adobe Experience Platform中目的地組態的特定設定，透過Experience PlatformUI建立及管理。 其中包含連線及傳送資料至目的地所需的所有引數和認證。 建立與目的地的連線後，您可以在[瀏覽與目的地的連線](/help/destinations/ui/destination-details-page.md)時取得目的地執行個體識別碼。

![UI影像如何取得目的地執行個體識別碼](/help/destinations/destination-sdk/assets/testing-api/get-destination-instance-id.png)

## P

**[!DNL Pebble]範本**： [!DNL Pebble]範本用於將從Adobe Experience Platform匯出的資料轉換為目的地平台所需的格式。 它採用[!DNL Pebble]範本化語言，允許透過`filter`、`for`、`if`和`set`等功能進行動態資料轉換。 Adobe Experience Platform包含其他自訂函式，例如`addedSegments`和`removedSegments`。 這些範本有助於將資料元素（例如時間戳記和對象會籍）格式化，以符合目的地的規格。 在[這裡](/help/destinations/destination-sdk/functionality/destination-server/message-format.md)和[這裡](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md)瞭解更多資訊。

**私人目的地**：個別Adobe Experience Platform客戶建立的自訂整合。 這些模組是專為滿足特定業務需求而量身打造，只能在客戶組織記憶體取，提供資料匯出設定的彈性。 私人目的地僅供Real-Time CDP Ultimate客戶使用。 [閱讀全文](/help/destinations/destination-sdk/overview.md#productized-custom-integrations)。

**公開目的地**： Adobe Experience Platform目錄中的公開可用整合。 這些目的地會標準化、加上品牌，並提供預先設定的引數來簡化客戶設定。 所有使用Adobe Experience Platform的客戶都可存取。 [閱讀全文](/help/destinations/destination-sdk/overview.md#productized-custom-integrations)。

## S

**自助檔案範本**：自助檔案範本提供結構化格式，可供您記錄目的地。 其中包含概觀、使用案例、先決條件、支援的身分、對象、匯出型別和頻率的章節，以及連線至目的地、啟用對象和對應屬性的步驟。 使用此範本確保檔案完整一致，讓客戶快速開始使用您的目的地，並瞭解提供的使用案例。 深入瞭解[如何記錄您的目的地](/help/destinations/destination-sdk/docs-framework/documentation-instructions.md)、[下載最新的自助服務檔案範本](/help/destinations/destination-sdk/assets/docs-framework/yourdestination-template.zip)，以及[檢視其呈現方式](/help/destinations/destination-sdk/docs-framework/self-service-template.md)。

## T

**範本規格和範本化策略**：範本規格是用來格式化從Adobe Experience Platform傳送至目的地的HTTP要求的組態。 他們將XDM結構描述中的設定檔屬性欄位轉換為目的地平台支援的格式。 使用類似於[!DNL Jinja]的範本化語言，這些規格允許根據特定規則和輸入資料進行動態資料轉換。 [了解更多](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md)。

**測試API**：測試API可讓您在提交發佈要求之前驗證目的地組態。 它提供工具來產生範例設定檔和測試資料流程，確保設定符合目的地的需求。 此API支援串流和檔案型（批次）目的地，提供一種方法來模擬資料並疑難排解設定流程中的潛在問題。 深入瞭解[串流](/help/destinations/destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md)和[檔案型目的地](/help/destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md)的測試API。

**轉換範本**：轉換範本會自訂資料格式，從AdobeXDM結構描述轉換成目的地的預期格式。 [了解更多](/help/destinations/destination-sdk/functionality/destination-server/message-format.md)。
