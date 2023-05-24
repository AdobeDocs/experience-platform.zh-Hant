---
description: Adobe Experience Platform的目標服務使用配置端點來構建目標功能的多個元件。 瞭解這些元件組合如何使Experience Platform能夠連接到目標合作夥伴、發送自定義消息以及激活整個數字生態系統中的配置檔案資料。
title: 配置選項在Destination SDK
source-git-commit: 65a658208b48a50184e55a6d64cdf7ad6de0f04f
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---


# 配置選項在Destination SDK

Adobe Experience Platform的目標服務使用配置端點來構建目標功能的多個元件。

這些元件結合起來，使Experience Platform能夠連接到目標平台、發送自定義消息、導出自定義檔案並激活整個數字生態系統中的配置檔案資料。

下圖顯示了通過Destination SDK可配置以構建您自己的目標的元件的高級概述。 這些元件在下文中作進一步說明。

![顯示Destination SDK元件、配置端點及其支援的操作的圖。](../assets/functionality/destination-sdk-components-diagram.png)

## 伺服器設定 {#server-configuration}

目標伺服器配置將有關伺服器規格的資訊和Adobe用於將負載傳遞到目標的模板聯繫起來。

例如，在此處指定Experience Platform需要連接到的一方的API端點，以及平台將進行的API調用的標頭和格式。

對於基於檔案的目標，此配置還包括目標支援的檔案格式和壓縮格式。 您可以通過 [目標伺服器端點](../authoring-api/destination-server/create-destination-server.md)。

* [伺服器規格](destination-server/server-specs.md):一個配置模板，包含有關資料發送到的儲存位置或HTTP終結點的資訊。
* [模板規格](destination-server/templating-specs.md):在此模板中，可以定義如何將HTTP API請求結構化到終結點，包括如何在XDM架構和平台支援的格式之間轉換配置檔案屬性欄位。 將此資訊與 [消息格式](destination-server/message-format.md) 文檔。
* [消息格式](destination-server/message-format.md):本部分介紹有關支援的模板語言、消息格式以及Adobe設定與平台整合所需的資訊的詳細資訊。 將此資訊與 [模板規格](destination-server/templating-specs.md) 文檔。
* [檔案規格](destination-server/file-formatting.md):包含批處理目標的檔案格式和壓縮選項的配置模板。

## 目標配置 {#destination-configuration}

此配置終結點包含有關目標的基本和高級資訊。 例如，您可以在其中指定目標可以支援的標識類型、導出檔案的所需格式（對於基於檔案的目標）以及Adobe Experience Platform用戶介面中目標卡的各種UI屬性。

有關每個目標配置元件的詳細資訊，請參閱下面的文檔。 您可以通過 [目標終結點](../authoring-api/destination-configuration/create-destination-configuration.md)。

* [客戶身份驗證配置](destination-configuration/customer-authentication.md):選擇Experience Platform應用於連接到目標的身份驗證機制。 此配置將生成 [配置新目標](../../ui/connect-destination.md) Experience Platform用戶介面中的「Experience Platform」頁，其中用戶將連接到他們與目標的帳戶。
* [OAuth2身份驗證](destination-configuration/oauth2-authentication.md):瞭解所有 [!DNL OAuth2] 驗證流受Destination SDK支援，並獲取設定說明 [!DNL OAuth2] 目標的身份驗證……
* [客戶資料欄位](destination-configuration/customer-data-fields.md):瞭解如何在Experience PlatformUI中建立輸入欄位，以便用戶指定與如何連接資料並將資料導出到目標相關的各種資訊。
* [UI屬性](destination-configuration/ui-attributes.md):瞭解如何為使用Destination SDK構建的目標配置UI屬性，如文檔連結、目標卡類別以及目標連接類型和頻率。
* [架構配置](destination-configuration/schema-configuration.md):瞭解如何定義目標的目標架構，用戶可以將配置檔案屬性和標識映射到該架構。
* [標識命名空間配置](destination-configuration/identity-namespace-configuration.md):瞭解如何配置目標支援的身份。 此配置將填充 [映射步驟](../../ui/activate-segment-streaming-destinations.md#mapping) Experience Platform用戶介面中，用戶將標識和屬性從其XDM架構映射到目標中的架構。
* [目標傳遞](destination-configuration/destination-delivery.md):瞭解如何配置導出的資料到達的位置以及資料到達的位置使用哪些身份驗證規則。
* [受眾元資料配置](destination-configuration/audience-metadata-configuration.md):瞭解段元資料（如段名稱或ID）在Experience Platform和目標之間應如何共用。
* [聚合策略](destination-configuration/aggregation-policy.md):瞭解如何設定聚合策略以確定對目標的HTTP請求應如何分組和批處理。
* [批配置](destination-configuration/batch-configuration.md):在Experience Platform用戶介面中設定連接到目標時用戶可使用的各種檔案命名和導出計畫設定。
* [歷史配置檔案資格](destination-configuration/historical-profile-qualifications.md):瞭解使用Destination SDK構建的目標支援的歷史配置檔案資格。

## 受眾元資料配置 {#audience-metadata-configuration}

此元件允許您配置在目標中以寫程式方式建立、更新或刪除受眾/網段的方式。 對於基於檔案的目標，它允許您在檔案成功傳送到目標時設定通知。 您可以通過 [觀眾模板端點](../metadata-api/create-audience-template.md)。

## 後續步驟 {#next-steps}

通過閱讀本文，您現在概括瞭解了Destination SDK提供的功能，以及要閱讀哪些頁，以瞭解有關特定配置的詳細資訊。 接下來，您可以閱讀包含所有步驟的指南 [配置流](../guides/configure-destination-instructions.md) 或 [基於檔案的目標](../guides/configure-file-based-destination-instructions.md) 用Destination SDK。
