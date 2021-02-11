---
title: Adobe Experience Platform Web SDK 擴充功能
seo-title: Adobe Experience Platform Launch 中的 Adobe Experience Platform Web SDK 擴充功能
description: Adobe Experience Platform Launch 中的 Adobe Experience Platform Web SDK 擴充功能
seo-description: Adobe Experience Platform Web SDK 擴充功能 Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 473cc1f7617f1d65cdb70ff0e758178ea0174f00
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 58%

---


# Adobe Experience Platform Web SDK Extension for Platform Launch

Adobe Experience Platform Web SDK Extension會透過Adobe Experience Platform Edge Network，從Web屬性將資料傳送至Adobe Experience Cloud。 Adobe Experience Platform Web SDK 擴充功能可將資料串流至平台、同步身分資料、啟用加入宣告功能，並自動收集內容資料。

## 設定 AEP Web SDK 擴充功能

本節提供設定 Adobe Experience Platform Web SDK 擴充功能時可用選項的參考資料。

如果尚未安裝Adobe Experience Platform Web SDK擴充功能，請開啟您的屬性，然後選取「**[!UICONTROL 擴充功能>目錄]**」，將滑鼠指標暫留在Adobe Experience Platform Web SDK擴充功能上，然後選取「**[!UICONTROL 安裝]**」。

若要設定擴充功能，請開啟&#x200B;**[!UICONTROL 擴充功能]**&#x200B;標籤，將滑鼠指標暫留在擴充功能上，然後選取&#x200B;**[!UICONTROL 設定]**。

![](./assets/ext-aep-config.png)

### 例項名稱

Adobe Experience Platform Web SDK擴充功能支援頁面上的多個例項。 只要藉由單一 Adobe Experience Platform Launch 設定，即可將資料傳送至多個組織。**[!UICONTROL 名稱]**&#x200B;預設為合金。 不過您可將例項名稱變更為任何有效的 JavaScript 物件名稱。Adobe Experience Platform擴充功能要求每個例項都有不同的&#x200B;**[!UICONTROL 組態ID]**&#x200B;和不同的&#x200B;**[!UICONTROL 組織ID]**。

## **[!UICONTROL 設定ID]**

**[!UICONTROL Config ID]**&#x200B;會告訴Adobe Experience Platform資料應路由的位置以及伺服器應使用哪些組態。 這是 Adobe Experience Platform 擴充功能運作的必要條件。您可以連絡客戶服務，取得設定 ID。


### **[!UICONTROL 組織 ID]**

**[!UICONTROL 組織ID]**&#x200B;是您要在Adobe傳送資料的組織。 大多數案例中，您都應該使用自動填入的預設值。頁面上有多個例項時，請找到您要傳送資料的第二個組織，以該組織的值填入此例項。

### **[!UICONTROL 邊緣網域]**

**[!UICONTROL Edge Domain]**&#x200B;是Adobe Experience Platform擴充功能傳送及接收資料的網域。 擴充功能會要求您為生產流量使用第一方 CNAME。預設的第三方網域適用於開發環境，但不適用於生產環境。若需設定第一方 CNAME 的相關說明，請參閱[此處](https://docs.adobe.com/content/help/zh-Hant/core-services/interface/ec-cookies/cookies-first-party.html)。

### **[!UICONTROL 啟用錯誤]**

根據預設，如果擴充功能發生錯誤，系統會將錯誤記錄至主控台。如果要隱藏生產環境中的錯誤，可以取消選中&#x200B;**[!UICONTROL 啟用錯誤]**&#x200B;複選框。 在 Platform Launch 中開啟偵錯功能後，系統仍會列印出錯誤。

### **[!UICONTROL 啟用選擇加入]**

如果&#x200B;**[!UICONTROL 啟用選擇加入]**&#x200B;已啟用，AEP Web SDK擴充功能可保留點擊，直到收到選擇加入為止。 此擴充功能會顯示設定加入宣告偏好設定的動作。

### **[!UICONTROL 啟用移轉ECID]**

AEP Web SDK 擴充功能會使用新的 Cookie 來儲存 ECID。此設定可讓新 Cookie 與舊 Cookie 相容，以利移轉。Adobe 強烈建議您啟用此設定，除非您沒有具 ECID 的現有訪客，則另當別論。

### **[!UICONTROL 使用第三方Cookie]**

Adobe Experience Platform 會一律將 Cookie 儲存在第一方網域中。透過此選項，除了第一方網域中的 Cookie 之外，您還能使用在 demdex.net 上設定的第三方 Cookie。如果您的使用者需要在多個網域之間移動，此功能會相當實用。這會停用對 demdex.net 的呼叫。

### **[!UICONTROL 內容]**

擴充功能會自動收集要求內容的資訊 (例如 URL 和瀏覽器的詳細資訊)。取消選取特定內容即可停用此功能。

- **[!UICONTROL web]** -網頁的詳細資訊，例如url、反向連結等。
- **[!UICONTROL device]** -裝置的詳細資訊，例如螢幕方向、螢幕高度和螢幕寬度。
- **[!UICONTROL 環境]** -有關計算環境的資訊（瀏覽器、連接等）
- **[!UICONTROL 位置]** -使用者位置的有限資訊

## 下一步

1. 設定[操作類型](action-types.md)。
2. 設定[資料元素類型](data-element-types.md)。
