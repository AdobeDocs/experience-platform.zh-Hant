---
description: Adobe Experience Platform中的目的地服務使用數個元件的設定端點，這些元件會建置目的地功能。 瞭解這些元件如何組合讓Experience Platform可連結到目的地合作夥伴、傳送自訂訊息，並在整個數位生態系統中啟用設定檔資料。
title: Destination SDK中的設定選項
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: f652faac7d771b590b30f591616b53d0cd2ff1eb
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# Destination SDK中的設定選項

Adobe Experience Platform中的目的地服務使用數個元件的設定端點，這些元件會建置目的地功能。

結合，這些元件可讓Experience Platform連線至目的地平台、傳送自訂訊息、匯出自訂檔案，以及在整個數位生態系統中啟用設定檔資料。

下圖顯示您可以透過Destination SDK設定以建置您自己的目的地的元件概觀。 這些元件將於下文詳細說明。

>[!BEGINSHADEBOX]

![顯示Destination SDK元件、組態端點及其支援之作業的圖表。](../assets/functionality/destination-sdk-components-diagram.png){zoomable="yes"}

>[!ENDSHADEBOX]

## 伺服器設定 {#server-configuration}

目的地伺服器組態會將伺服器規格的相關資訊與Adobe用來將負載傳送至目的地的範本連結在一起。

例如，您可以在此處指定Experience Platform需要連線的API端點，以及Platform將進行API呼叫的標題和格式。

針對以檔案為基礎的目的地，此設定也包含支援的目的地檔案格式和壓縮格式。 您可以透過[destination-servers端點](../authoring-api/destination-server/create-destination-server.md)設定下列功能。

* [伺服器規格](destination-server/server-specs.md)：包含資料傳送目的地之儲存位置或HTTP端點相關資訊的設定範本。
* [範本規格](destination-server/templating-specs.md)：在此範本中，您可以定義如何建構端點的HTTP API要求，包括如何在XDM結構描述和平台支援的格式之間轉換設定檔屬性欄位。 將此資訊與[訊息格式](destination-server/message-format.md)檔案一起使用。
* [訊息格式](destination-server/message-format.md)：本節提供支援的範本語言、訊息格式及Adobe設定與平台整合所需資訊的深入資訊。 請將此資訊與[範本規格](destination-server/templating-specs.md)檔案搭配使用。
* [檔案規格](destination-server/file-formatting.md)：包含批次目的地之檔案格式與壓縮選項的設定範本。

## 目的地設定 {#destination-configuration}

此設定端點包含有關您目的地的基本和進階資訊。 例如，您可以在此處指定目的地可支援的身分型別、匯出檔案的所需格式（適用於檔案型目的地），以及Adobe Experience Platform使用者介面中目的地卡片的各種UI屬性。

如需每個目的地設定元件的詳細資訊，請參閱以下檔案。 您可以透過[目的地端點](../authoring-api/destination-configuration/create-destination-configuration.md)設定下列功能。

* [客戶驗證組態](destination-configuration/customer-authentication.md)：選取Experience Platform應該用來連線到目的地的驗證機制。 此設定會在Experience Platform使用者介面中產生[設定新目的地](../../ui/connect-destination.md)頁面，使用者可在此將Experience Platform連線至他們在您的目的地擁有的帳戶。
* [OAuth2授權](destination-configuration/oauth2-authorization.md)：瞭解Destination SDK支援的所有[!DNL OAuth2]驗證流程，並取得為目的地設定[!DNL OAuth2]驗證的指示。
* [客戶資料欄位](destination-configuration/customer-data-fields.md)：瞭解如何在Experience PlatformUI中建立輸入欄位，讓您的使用者指定與如何連線及匯出資料至目的地相關的各種資訊。
* [UI屬性](destination-configuration/ui-attributes.md)：瞭解如何為使用Destination SDK建置的目的地設定UI屬性，例如檔案連結、目的地卡類別以及目的地連線型別和頻率。
* [結構描述組態](destination-configuration/schema-configuration.md)：瞭解如何定義使用者可將設定檔屬性和身分對應到目的地的目標結構描述。
* [身分名稱空間設定](destination-configuration/identity-namespace-configuration.md)：瞭解如何設定目的地支援的身分。 此設定會在Experience Platform使用者介面的[對應步驟](../../ui/activate-segment-streaming-destinations.md#mapping)中填入目標身分，使用者會將身分和屬性從其XDM結構描述對應到您目的地中的結構描述。
* [目的地傳遞](destination-configuration/destination-delivery.md)：瞭解如何設定匯出資料的確切位置，以及在資料著陸位置使用什麼驗證規則。
* [對象中繼資料組態](destination-configuration/audience-metadata-configuration.md)：瞭解對象名稱或ID等對象中繼資料應如何在Experience Platform和您的目的地之間共用。
* [彙總原則](destination-configuration/aggregation-policy.md)：瞭解如何設定彙總原則，以決定應該如何分組和批次處理目的地的HTTP要求。
* [批次組態](destination-configuration/batch-configuration.md)：設定使用者在Experience Platform使用者介面中連線到您的目的地時，可用的各種檔案命名和匯出排程設定。
* [歷史設定檔資格](destination-configuration/historical-profile-qualifications.md)：瞭解以Destination SDK建置的目的地所支援的歷史設定檔資格。

## 對象中繼資料設定 {#audience-metadata-configuration}

此元件允許您設定在您的目的地以程式設計方式建立、更新或刪除對象的方式。 針對以檔案為基礎的目的地，它可讓您在檔案成功傳送至目的地時設定通知。 您可以透過[對象範本端點](../metadata-api/create-audience-template.md)設定此功能。

## 後續步驟 {#next-steps}

閱讀本文章，您現在已大致瞭解Destination SDK所提供的功能，以及需閱讀哪些頁面以取得特定設定的詳細資訊。 接下來，您可以閱讀指南內容，其中包含使用Destination SDK[設定串流](../guides/configure-destination-instructions.md)或[檔案型目的地](../guides/configure-file-based-destination-instructions.md)的所有步驟。
