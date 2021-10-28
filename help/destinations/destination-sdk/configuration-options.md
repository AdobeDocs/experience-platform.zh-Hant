---
description: Adobe Experience Platform中的目的地服務使用多個元件的設定範本，以建立目的地功能。 這些元件結合後，Experience Platform便能連線至目的地合作夥伴、傳送自訂訊息，以及在數位生態系統中啟用設定檔資料。
seo-description: The destinations service in Adobe Experience Platform uses configuration templates for several components that build up the destinations functionality. Combined, these components allow Experience Platform to connect to destination partners, send custom messages, and activate profile data across the digital ecosystem.
seo-title: Configuration options in Destination SDK
title: 目標SDK中的設定選項
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: 0bd57e226155ee68758466146b5d873dc4fdca29
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 2%

---

# 目標SDK中的設定選項

## 總覽 {#overview}

Adobe Experience Platform中的目的地服務使用多個元件的設定範本，以建立目的地功能。 這些元件結合後，Experience Platform便能連線至目的地合作夥伴、傳送自訂訊息，以及在數位生態系統中啟用設定檔資料。 Adobe Experience Platform中使用的範本為：

* **目標配置**:包含目的地的基本資訊。 此設定包含您的目的地可支援的身分類型，以及Adobe Experience Platform使用者介面中目的地卡片的各種UI屬性。
* **伺服器和模板規格**:將伺服器規格的相關資訊和Adobe用於將裝載交付到目的地的模板聯繫起來。
   * **伺服器規格**:儲存端點詳細資訊的範本。
   * **模板規格**:在此範本中，您可以定義如何在XDM架構與您的平台支援的格式之間轉換設定檔屬性欄位。 如需支援的範本語言、訊息格式，以及Adobe設定與平台整合所需的資訊，請參閱 [訊息格式](./message-format.md).
* **驗證配置**:這些設定可定義Adobe Experience Platform使用者連線至您目的地的方式。
* **對象中繼資料設定**:此範本可讓您設定對象/區段以程式設計方式在您的目的地建立、更新或刪除的方式。

![目的地SDK範本和設定](./assets/self-service-configuration.png)

## 相關連結 {#related-links}

以下頁面提供Destination SDK中可用功能和設定選項，以及您可執行之對應API操作的詳細資訊。

| 功能說明 | API 參考資料 |
|--- |--- |
| [目標配置](./destination-configuration.md) | [目的地API端點作業](./destination-configuration-api.md) |
| [伺服器和模板規格](./server-and-template-configuration.md) | [目標伺服器API端點操作](./destination-server-api.md) |
| [驗證配置](./authentication-configuration.md) | [憑證端點API操作](./credentials-configuration-api.md) |
| [對象中繼資料管理](./audience-metadata-management.md) | [對象中繼資料端點API操作](./audience-metadata-api.md) |
| [OAuth 2設定](./oauth2-authentication.md) | 使用 `customerAuthenticationConfigurations` 參數 [/destinations API端點](./destination-configuration-api.md). |
| [訊息格式](./message-format.md) | - |
| [目的地測試](./test-destination.md) | [目的地測試API操作](./destination-testing-api.md) |
| [目的地發佈](./configure-destination-instructions.md#publish-destination) | [目的地發佈API作業](./destination-publish-api.md) |

{style=&quot;table-layout:auto&quot;}
