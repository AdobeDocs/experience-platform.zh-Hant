---
title: Adobe Experience Platform保證概述
description: Adobe Experience Platform保證可讓您檢查、校樣、模擬及驗證您在行動應用程式中收集資料或提供體驗的方式。
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 1%

---


# Adobe Experience Platform保障

Adobe Experience Platform保障是 [Adobe Experience Cloud](https://www.adobe.com/experience-cloud.html) 協助您檢查、校樣、模擬及驗證如何收集資料或提供行動應用程式中的體驗。

>[!IMPORTANT]
>
> Griffon項目現在稱為 **保證**!
>
> Griffon專案現已可供 **all** Adobe Experience Cloud客戶作為保證。 若要進一步了解此轉變，請閱讀 [使用者存取指南](./user-access.md).

>[!INFO]
>
>可使用保證公用API!
>
>[保證API](https://developer.adobe.com/adobe-assurance-public-apis/) 是API的集合，當使用者配合Adobe保證行動SDK時，可讓使用者測試其網頁和行動應用程式並除錯。

## 全面發佈

自2022年10月15日起，所有Adobe Experience Cloud皆可一般使用「保證」。

### 有什麼改變？

10月15日 — 存取保障將透過Admin Console管理。 請閱讀 [使用者存取指南](./user-access.md) 以確保您能持續存取。

現有的「保證」整合、工作階段和事件預期不會有其他變更或中斷情形。 可繼續透過 [https://griffon.adobe.com](https://griffon.adobe.com) **或** 您可以使用（和書籤） [https://experience.adobe.com/assurance](https://experience.adobe.com/assurance).

## Assurance能為您做什麼？

### 快速設定

用幾行代碼快速開始。 針對行動應用程式，Assurance會與Adobe Experience Platform Mobile SDK搭配使用，協助您檢查、模擬及驗證應用程式事件、位置訊號、設定參數、SDK記錄檔、裝置資訊等。

### 無障礙連線

透過「保證」，將您的應用程式與Platform連線既簡單又可靠。 您不需要使用網路代理， [MiTM](https://en.wikipedia.org/wiki/Man-in-the-middle_attack))，以及其他網路體操 — 將應用程式連接到「保障」就像掃描QR碼或點擊按鈕一樣簡單。

![](./images/index/no-hassle-connection.png)

### 即時檢查、模擬和驗證

連線至「保證」後，您可以檢查即時串流應用程式事件和活動，並篩選和搜尋以消除雜訊。 事件包含驗證、除錯和疑難排解行動應用程式實作的詳細資訊。 保證也可讓您即時擷取、模擬位置訊號等。

![](./images/index/real-time-insepction.png)

### 與Adobe Experience Cloud整合

用戶端資料和體驗的提供內容，是透過使用者在以行銷人員為中心的使用者介面上設定報表規則、活動和促銷活動的方式。 為協助您將兩者結合，我們整合了Adobe Experience Cloud解決方案，例如Adobe Experience Platform、Adobe Analytics、Adobe Target、Places Service等。

![](./images/index/integration.png)

## 功能

### Adobe Experience Platform Mobile SDK事件、記錄檔等

保證可協助您檢查由Adobe Experience Platform Mobile SDK產生的原始SDK事件。 SDK收集的所有事件都可供檢查。 SDK事件會以清單檢視載入，並依時間排序。 每個事件都有詳細的檢視，可提供更詳細的資訊。 此外，也提供瀏覽SDK設定、資料元素、共用狀態和SDK擴充功能版本的其他檢視。

### Adobe Analytics

「Adobe Analytics > Analytics事件」檢視是重點明確的檢視，可顯示與您的Adobe Analytics行動實作相關的事件。 清單檢視會以特殊格式化的檢視顯示生命週期或動作/狀態事件、處理後的「狀態」，以及必要的事件詳細資料。 「處理後」狀態會顯示在事件上套用處理規則後，Adobe Analytics如何處理事件。

### 適用於串流媒體的 Adobe Analytics

「Adobe Analytics > Media Analytics事件」檢視會顯示您音訊與視訊分析實作的事件。 事件詳細資料檢視會顯示每個播放工作階段所追蹤的標準和自訂中繼資料。 此外，您也可以檢視處理後狀態和後處理的媒體分析資料，例如媒體逗留時間或總緩衝期間。

### Places(Location Services)

「Location Services」檢視是裝置上的檢視，可顯示使用者位置登入和退出事件，以方便驗證。 這個方便的視圖提供了一個方便的介面，用於查看特定位置的資料點，以便在客戶端上進行檢查以進行上下文調試。

## 保證安全嗎？

保證有下列安全措施：

* 保證和保證Web UI都具有一個連接的安全、基於PIN的握手。 用戶必須顯式建立握手，這樣就防止最終用戶建立「意外」保證連接。
* 僅支援Assurance與屬於相同Adobe Experience Cloud組織ID之Assurance Web UI之間的連線。
* Adobe Experience Platform Mobile SDK事件是透過HTTPS傳輸。
* 保證和Adobe Experience Platform Mobile SDK使用TLS 1.2
* 30天後會刪除保證工作階段。
* 遵循儲存最佳實務，保證工作階段資料會在閒置時加密。

## 快速入門

若要設定保證，您必須先在您的應用程式中安裝保證擴充功能。 若要了解如何執行此作業，請閱讀 [實作保證延伸](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

將保證新增至應用程式後，您可以建立可連線至裝置的保證工作階段。 若要了解如何使用Assurance，請閱讀 [使用保證指南](./tutorials/using-assurance.md).
