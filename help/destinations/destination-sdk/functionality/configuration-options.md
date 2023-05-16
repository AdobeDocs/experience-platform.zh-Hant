---
description: Adobe Experience Platform中的目的地服務使用多個元件的設定端點來建立目的地功能。 了解這些元件結合後，Experience Platform可如何連線至目的地合作夥伴、傳送自訂訊息，以及在數位生態系統中啟用設定檔資料。
title: 配置Destination SDK
source-git-commit: 65a658208b48a50184e55a6d64cdf7ad6de0f04f
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---


# 配置Destination SDK

Adobe Experience Platform中的目的地服務使用多個元件的設定端點來建立目的地功能。

這些元件結合後，Experience Platform便能連線至目的地平台、傳送自訂訊息、匯出自訂檔案，以及在數位生態系統中啟用設定檔資料。

下圖顯示可透過Destination SDK設定，以建立您自己目的地的元件概觀。 以下將進一步說明這些元件。

![圖表顯示Destination SDK元件、配置端點及其支援的操作。](../assets/functionality/destination-sdk-components-diagram.png)

## 伺服器設定 {#server-configuration}

目標伺服器配置將伺服器規格和Adobe用於將裝載交付到目標的模板的相關資訊聯繫起來。

例如，您可以在此處指定Experience Platform需要連線的API端點，以及Platform將進行之API呼叫的標題和格式。

針對以檔案為基礎的目的地，此設定也包含支援的目的地檔案格式和壓縮格式。 您可以透過 [destination-servers端點](../authoring-api/destination-server/create-destination-server.md).

* [伺服器規格](destination-server/server-specs.md):包含資料被發送到的儲存位置或HTTP端點資訊的配置模板。
* [模板規格](destination-server/templating-specs.md):在此範本中，您可以定義如何向端點建構HTTP API請求，包括如何在XDM架構與平台支援的格式之間轉換設定檔屬性欄位。 將此資訊與 [訊息格式](destination-server/message-format.md) 檔案。
* [訊息格式](destination-server/message-format.md):本節深入說明支援的範本語言、訊息格式，以及Adobe設定與平台整合所需的資訊。 將此資訊與 [模板規格](destination-server/templating-specs.md) 檔案。
* [檔案規格](destination-server/file-formatting.md):配置模板，包含批處理目標的檔案格式和壓縮選項。

## 目標配置 {#destination-configuration}

此設定端點包含有關您目的地的基本和進階資訊。 例如，您可以在此為Adobe Experience Platform使用者介面中的目的地卡片指定目的地可支援的身分類型、所需的匯出檔案格式（針對檔案式目的地），以及各種UI屬性。

如需每個目標設定元件的詳細資訊，請參閱下列檔案。 您可以透過 [目的地端點](../authoring-api/destination-configuration/create-destination-configuration.md).

* [客戶驗證配置](destination-configuration/customer-authentication.md):選取Experience Platform應用來連線至目的地的驗證機制。 此設定會產生 [配置新目標](../../ui/connect-destination.md) 頁面，使用者可在此將Experience Platform連線至其與您目的地的帳戶。
* [OAuth2驗證](destination-configuration/oauth2-authentication.md):了解所有 [!DNL OAuth2] Destination SDK支援的驗證流程，並取得設定指示 [!DNL OAuth2] 目的地的驗證……
* [客戶資料欄位](destination-configuration/customer-data-fields.md):了解如何在Experience PlatformUI中建立輸入欄位，讓使用者能指定與如何連線及將資料匯出至目的地相關的各種資訊。
* [UI屬性](destination-configuration/ui-attributes.md):了解如何針對使用Destination SDK建置的目的地，設定UI屬性，例如說明檔案連結、目的地卡類別，以及目的地連線類型和頻率。
* [結構配置](destination-configuration/schema-configuration.md):了解如何定義使用者可將設定檔屬性和身分對應至的目的地目標結構。
* [身分命名空間設定](destination-configuration/identity-namespace-configuration.md):了解如何設定您目的地支援的身分識別。 此設定會填入 [對應步驟](../../ui/activate-segment-streaming-destinations.md#mapping) Experience Platform使用者介面的，使用者可將身分和屬性從其XDM結構對應至目的地的結構。
* [目的地傳送](destination-configuration/destination-delivery.md):了解如何設定匯出資料的確切位置，以及資料著陸位置中使用的驗證規則。
* [對象中繼資料設定](destination-configuration/audience-metadata-configuration.md):了解區段中繼資料（例如區段名稱或ID）應如何在Experience Platform與目的地之間共用。
* [聚合策略](destination-configuration/aggregation-policy.md):了解如何設定匯總原則，以決定對您目的地的HTTP請求進行分組和批次處理的方式。
* [批次設定](destination-configuration/batch-configuration.md):在Experience Platform使用者介面中連線至您的目的地時，設定使用者可用的各種檔案命名和匯出排程設定。
* [歷史設定檔資格](destination-configuration/historical-profile-qualifications.md):了解透過Destination SDK建置的目的地所支援的歷史設定檔資格。

## 對象中繼資料設定 {#audience-metadata-configuration}

此元件可讓您設定對象/區段以程式設計方式在您的目的地建立、更新或刪除的方式。 對於檔案型目的地，可讓您在檔案成功傳送至目的地時設定通知。 您可以透過 [對象範本端點](../metadata-api/create-audience-template.md).

## 後續步驟 {#next-steps}

閱讀本文後，您現在可以概略了解Destination SDK所提供的功能，以及要閱讀哪些頁面以取得特定設定的詳細資訊。 接下來，您可以閱讀指南，其中包含 [設定串流](../guides/configure-destination-instructions.md) 或 [檔案型目的地](../guides/configure-file-based-destination-instructions.md) 使用Destination SDK。
