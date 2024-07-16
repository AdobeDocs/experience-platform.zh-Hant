---
title: Adobe Experience Platform Assurance 概觀
description: Adobe Experience Platform Assurance 讓您可以檢查、證明、模擬和驗證您在行動應用程式中收集資料或服務體驗的方式。
exl-id: e887f5f6-3db0-4521-be2d-20ef3d08e7d0
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 100%

---

# Adobe Experience Platform Assurance

Adobe Experience Platform Assurance 是 [Adobe Experience Cloud](https://www.adobe.com/experience-cloud.html) 所提供的產品，可協助您檢查、證明、模擬和驗證您在行動應用程式中收集資料或服務體驗的方式。

>[!IMPORTANT]
>
> Project Griffon 現在被稱為 **Assurance**！
>
> Project Griffon 現在以 Assurance 的名義正式推出，可供&#x200B;**所有** Adobe Experience Cloud 客戶使用。若要了解有關此轉變的詳細資訊，請閱讀[使用者存取指南](./user-access.md)。

>[!INFO]
>
>Assurance 公用 API 已可供使用！
>
>[Assurance API](https://developer.adobe.com/adobe-assurance-public-apis/) 是 API 的集合，可讓使用者在配備了 Adobe Assurance Mobile SDK 時，能夠測試自己的 Web 和行動應用程式並進行偵錯。

## 正式推出

從 2022 年 10 月 15 日開始，Assurance 即正式推出至所有 Adob&#x200B;&#x200B;e Experience Cloud。

### 有哪些變更？

10 月 15 日 - 對 Assurance 的存取權會透過 Admin Console 管理。請閱讀[使用者存取指南](./user-access.md)，以確保您的存取權持續不中斷。

我們預期對現有的 Assurance 整合、工作階段和事件並不會造成其他變更或中斷。若要持續存取 Assurance，您可透過 [https://griffon.adobe.com](https://griffon.adobe.com) **或者**&#x200B;可使用 (並加入書籤) [https://experience.adobe.com/assurance](https://experience.adobe.com/assurance)。

## Assurance 能為您提供什麼功能？

### 快速設定

只需幾行程式碼即可快速開始使用。對於行動應用程式，Assurance 會使用 Adob&#x200B;&#x200B;e Experience Platform Mobile SDK，協助您檢查、模擬和驗證應用程式事件、位置訊號、設定參數、SDK 記錄、裝置資訊等。

### 輕鬆連線

使用 Assurance 將您的應用程式和 Platform 連線既簡單又可靠。您不需要使用網路 Proxy、[MiTM](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)) 和其他複雜的網路操作 - 將您的應用程式連線至 Assurance 就像掃描 QR 碼或輕敲按鈕一樣容易。

![](./images/index/no-hassle-connection.png)

### 即時檢查、模擬和驗證

連線到 Assurance 後，您即可檢查直播串流應用程式的事件和活動，並進行篩選和搜尋以消除噪音。事件包含有關對您的行動應用程式實作進行驗證、偵錯和疑難排解的詳細資料。Assurance 還可以讓您即時取得螢幕擷圖、模擬位置訊號等。

![](./images/index/real-time-insepction.png)

### 和 Adobe Experience Cloud 的整合

用戶端資料和體驗的內容會透過使用者在我們以行銷人員為中心的使用者介面上設定報告規則、活動和行銷活動的方式提供。為了協助您連接兩者之間的點，我們正在和 Adob&#x200B;&#x200B;e Experience Cloud 解決方案整合，例如 Adob&#x200B;&#x200B;e Experience Platform、Adobe Analytics、Adobe Target、Places Service 等。

![](./images/index/integration.png)

## 功能

### Adobe Experience Platform Mobile SDK 事件、記錄等

Assurance 可協助您檢查 Adobe Experience Platform Mobile SDK 產生的原始 SDK 事件。SDK 收集的所有事件都可供檢查。SDK 事件會載入清單檢視，並依時間排序。每個事件都有一個可提供更多詳細資料的詳細檢視。還會提供用於瀏覽 SDK 設定、資料元素、共用狀態和 SDK 擴充功能版本的其他檢視。

### Adobe Analytics

Adobe Analytics > Analytics 事件檢視是一種聚焦式檢視，會顯示和 Adob&#x200B;&#x200B;e Analytics 行動實作相關的事件。清單檢視則會以特殊格式檢視顯示生命週期或動作/狀態事件、後續處理「狀態」以及必要的事件詳細資料。後續處理狀態會向您顯示對事件套用處理規則後 Adob&#x200B;&#x200B;e Analytics 會如何處理該事件。

### 適用於串流媒體的 Adobe Analytics

Adobe Analytics > Media Analytics 事件檢視會顯示您的音訊和影片分析實作的事件。事件詳細資料檢視則會顯示針對每個播放工作階段追蹤的標準和自訂中繼資料。此外，您還可以檢視後續處理狀態和後續處理的媒體分析資料，例如花費的媒體時間或總緩衝期間。

### 地點 (位置服務)

位置服務檢視是一種裝置上檢視，會顯示使用者位置的登入和退出事件以輕鬆進行驗證。這個易於使用的檢視可提供一個便利的介面，以檢視特定位置的資料點，以便在用戶端進行情境偵錯的檢查。

## Assurance 是否安全？

Assurance 已具備下列安全措施：

* Assurance 和 Assurance Web UI 的連線都使用有安全的 PIN 式握手。使用者必須明確地建立握手，這可防止一般使用者建立的「意外」Assurance 連線。
* 只會支援 Assurance 和屬於相同 Adob&#x200B;&#x200B;e Experience Cloud 組織 ID 的 Assurance Web UI 之間的連線。
* Adobe Experience Platform Mobile SDK 事件會經由 HTTPS 傳輸。
* Assurance 和 Adob&#x200B;&#x200B;e Experience Platform Mobile SDK 都會使用 TLS 1.2
* Assurance 工作階段會在 30 天刪除。
* 會將 Assurance 工作階段的待用資料加密，遵循儲存空間的最佳做法。

## 快速入門

若要設定 Assurance，您需要先在應用程式中安裝 Assurance 擴充功能。若要了解如何進行此步驟，請閱讀有關「[實作 Assurance 擴充功能](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app)」的教學課程。

將 Assurance 新增到您的應用程式後，您可以建立可連線至您的裝置的 Assurance 工作階段。若要了解如何使用 Assurance，請閱讀[有關如何使用 Assurance 的指南](./tutorials/using-assurance.md)。
