---
description: Adobe Experience Platform中的目的地服務使用多個元件的設定端點來建立目的地功能。 這些元件結合後，Experience Platform便能連線至目的地合作夥伴、傳送自訂訊息，以及在數位生態系統中啟用設定檔資料。
title: 配置Destination SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: 9b4c7da5aa02ae27608c2841b1d825445ac3015e
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# 配置Destination SDK

## 總覽 {#overview}

Adobe Experience Platform中的目的地服務使用多個元件的設定端點來建立目的地功能。 這些元件結合後，Experience Platform便能連線至目的地平台、傳送自訂訊息、匯出自訂檔案，以及在數位生態系統中啟用設定檔資料。 用於Adobe Experience Platform Destination SDK的設定包括：

* **目標配置**:包含目的地的基本資訊。 此設定包含您的目的地可支援的身分類型、所需的匯出檔案格式（針對檔案式目的地），以及Adobe Experience Platform使用者介面中目的地卡片的各種UI屬性。
* **伺服器、檔案和模板規格**:將伺服器規格的相關資訊和Adobe用於將裝載交付到目的地的模板聯繫起來。 針對以檔案為基礎的目的地，此設定也包含支援的目的地檔案格式和壓縮格式。
   * **伺服器規格**:包含資料被發送到的儲存位置或HTTP端點資訊的配置模板。
   * **檔案規格**:配置模板，包含批處理目標的檔案格式和壓縮選項。
   * **模板規格**:在此範本中，您可以定義如何在XDM架構與您的平台支援的格式之間轉換設定檔屬性欄位。 如需支援的範本語言、訊息格式，以及Adobe設定與平台整合所需的資訊，請參閱 [訊息格式](./message-format.md).
* **驗證配置**:這些設定可定義Adobe Experience Platform使用者連線至您目的地的方式。
* **對象中繼資料設定**:此設定端點可讓您設定對象/區段以程式設計方式在您的目的地建立、更新或刪除的方式。 對於批次目的地，可讓您在檔案成功傳送至目的地時設定通知。

![圖表顯示Destination SDK配置端點，以及它們如何一起使用。](./assets/self-service-configuration.png)

## 相關連結 {#related-links}

以下頁面提供更多詳細資訊，說明Destination SDK中可用的功能和設定選項，以及您可執行的對應API操作。

| 功能說明（串流目的地） | 功能說明（批次目的地） | API 參考資料 |
|--- |--- |--- |
| [目標配置選項](./destination-configuration.md) | [基於檔案的目標配置選項](/help/destinations/destination-sdk/file-based-destination-configuration.md) | [目的地API端點作業](./destination-configuration-api.md) |
| [伺服器和模板規格](./server-and-template-configuration.md) | [伺服器和檔案配置規格](/help/destinations/destination-sdk/server-and-file-configuration.md) | [目標伺服器API端點操作](./destination-server-api.md) |
| [驗證配置](./authentication-configuration.md) | 與串流目的地相同。 | 您可以透過 `customerAuthenticationConfigurations` 參數 `/destinations` 端點。 更多資訊 [串流](/help/destinations/destination-sdk/destination-configuration.md#customer-authentication-configurations) 和 [批次](/help/destinations/destination-sdk/file-based-destination-configuration.md#customer-authentication-configurations) 目的地。 |
| [對象中繼資料管理](./audience-metadata-management.md) | 和串流相同。 請參閱 [檔案型範例](/help/destinations/destination-sdk/audience-metadata-management.md#example-file-based) 了解如何在批次目的地內容中使用對象中繼資料。 | [對象中繼資料端點API操作](./audience-metadata-api.md) |
| [OAuth 2設定](./oauth2-authentication.md) | 與串流目的地相同 | 使用 `customerAuthenticationConfigurations` 參數 [/destinations API端點](./destination-configuration-api.md). |
| [訊息格式](./message-format.md) | - | - |
| [串流目的地的測試工具](./test-destination.md) | [檔案型目的地的測試工具](/help/destinations/destination-sdk/file-based-destination-testing-overview.md) | [目的地測試API操作](./destination-testing-api.md) |
| [目的地發佈](./configure-destination-instructions.md#publish-destination) | 與串流目的地相同 | [目的地發佈API作業](./destination-publish-api.md) |

{style="table-layout:auto"}

## 後續步驟 {#next-steps}

閱讀本文後，您現在可以概略了解Destination SDK所提供的功能，以及要閱讀哪些頁面以取得特定設定的詳細資訊。 接下來，您可以閱讀指南，其中包含 [設定串流](/help/destinations/destination-sdk/configure-destination-instructions.md) 或 [檔案型目的地](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md) 使用Destination SDK。
