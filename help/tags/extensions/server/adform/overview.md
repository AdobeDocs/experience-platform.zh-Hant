---
keywords: adform整合； adform；
title: Adform整合以進行未經驗證的重新目標定位
description: 此Adobe Experience Platform整合可讓您根據ECID重新鎖定使用者。
last-substantial-update: 2025-03-26T00:00:00Z
source-git-commit: 23da6e12b1f5bdc37240d7aa11a44e040b29e3f7
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 2%

---

# [!DNL Adform]擴充功能概觀

[[!DNL Adform]](https://www.adformhelp.com/hc/en-us/articles/29635608709137-Use-the-Adform-S2S-Site-Tracking-Extension-With-Adobe-Experience-Cloud)擴充功能可在Adobe Experience Platform中啟用伺服器端事件轉送，讓廣告商、媒體代理及發佈者直接與Adform的ID Fusion系統同步資料。 此整合可讓企業跨多個管道吸引受眾、改善行銷活動績效，並提供量身打造的解決方案，以調整數位廣告策略及發揮最大的廣告支出效益。

與傳統使用者端追蹤不同，此擴充功能運用第一方ID (具體而言，就是與Adform同步的ECID (Experience Cloud ID))，消除了第三方Cookie的需求。 這可讓您順暢地重新鎖定受眾，而不需要使用者端JavaScript部署。

本指南說明如何安裝、設定和部署擴充功能，以透過Adobe的Edge Network，將事件從品牌的數位財產轉送至Adform，進而實現訪客的無縫重定目標。

## 異地重新目標定位

透過站外重新目標定位，您可以重新與造訪過您的網站但未轉換的潛在客戶互動。 Adform可協助您在各種平台上觸及這些對象，強化品牌知名度，並增加轉換機會。 使用此整合來：

* 不使用第三方Cookie重新與未知訪客互動。
* 直接在ECID上啟用受眾，而不使用第三方Cookie替代識別碼或數位屬性上的其他標籤。

Adform可協助您：

* 輕鬆將ECID上所代表的第一方對象轉換為數位廣告促銷活動的可定址ID。
* 將ECID連結至40多個可競標ID解決方案，以針對目標受眾最佳化您的觸及率、頻率和效能。

### 使用[!DNL Adform]的伺服器端對象啟用 {#server-side-activation}

與傳統使用者端ID部署不同，這項整合不需要您在數位財產上部署ID供應商的解決方案。 而是運用已與Adform同步的ECID，以啟用伺服器端對象啟用。 主要優點包括：

* **沒有使用者端JavaScript部署**：您不需要管理使用者端訪客辨識邏輯，或將使用者端ID解密為較長的穩定版本。
* **順暢的對象同步處理**： ECID會對應至Adform的內部ID圖表，以有效率地跨平台重新鎖定目標。
* **增強的觸及範圍和重複資料刪除**： ID Fusion圖表會將ECID連線到多個識別碼，以確保高品質的對象比對。

## 先決條件 {#prerequisites}

將Adform與Adobe整合之前，請確定符合下列必要條件：

1. **Adobe Web SDK設定**：必須實作Adobe Web SDK，以便利資料收集和事件轉送。

2. **CDP或連線SKU**：您必須擁有Adobe客戶資料平台(CDP) Prime、Ultimate SKU或連線SKU，才能啟用順暢的使用者端和伺服器端通訊。

3. **Adobe Experience Platform Edge Network設定**：
   * 確保已將Edge Network設定為支援即時事件轉送，以進行離站重新目標定位。 如需詳細資訊，請參閱Adobe的[事件轉送快速入門手冊](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started)。
   * 此步驟對於有效率地將資料傳輸至Adform的伺服器端端點至關重要。

這些先決條件設定完成之後，您就可以繼續設定和部署[!DNL Adform]擴充功能。

## 設定 [!DNL Adform] 擴充功能 {#configure-adform-extension}

若要設定[!DNL Adform]擴充功能，請遵循以下各節所述的步驟。

### 安裝並設定擴充功能

導覽至事件轉送UI中的[!DNL Adform extension]並輸入必要的值：

| 輸入 | 說明 |
| --- | --- |
| 追蹤設定ID | Adform為追蹤事件所提供的唯一識別碼。 |
| 全域網域 | 使用`a1.adform.net`最佳化效能並避免區域延遲問題。 |

輸入這些詳細資料後儲存設定。

<!-- ![Installing and configuring the Adform extension in Adobe Experience Platorm]() -->

### 定義追蹤引數

「追蹤」動作是主要事件規則。 它會根據預先定義的動作觸發，通常是`page load.`包括下列引數：

**必要的引數：**

| 參數 | 說明 |
| --- | --- |
| `Page Name` | 識別頁面或使用者動作。 |
| `User Agent` | 擷取對象比對的資訊。 |
| `IP Address` | 對於準確定位和重新定位至關重要。 |

**建議的引數：**

| 參數 | 說明 |
| --- | --- |
| `Page URL` | 識別頁面或使用者動作。 |
| `Referral URL` | 擷取對象比對的資訊。 |
| `ECID` | 對於準確定位和重新定位至關重要。 |
| `Source Domain` | 對於準確定位和重新定位至關重要。 |

<!-- ![Tracking parameters for Adform]() -->

### 附加規則

擴充功能必須附加至規則才能正常運作。 若未設定任何條件，請建立全域規則以確保其一律執行。

>[!NOTE]
>
>如果擴充功能未引發，請確認其已附加至Adobe Experience Platform資料收集中的有效規則。

<!-- ![Attach a rule to the Adform extension]() -->

## 驗證和部署

請確認擴充功能已安裝且設定正確，且已對應所有必要的資料元素，包括：
* [ECID](/help/identity-service/features/ecid.md)
* 頁面名稱
* 轉介URL
* 使用者代理
* IP位址

輸入所有必要欄位並完成測試後，請選取&#x200B;**建置**&#x200B;以部署擴充功能。

## 後續步驟

您現在應該瞭解Adform如何與Adobe的伺服器端功能整合，並且可評估整合在您現有基礎結構中的可行性。 如需詳細資訊，請參閱[Adform的正式檔案](https://www.adformhelp.com/hc/en-us/articles/29635608709137-Use-the-Adform-S2S-Site-Tracking-Extension-With-Adobe-Experience-Cloud)。