---
title: Adobe Experience Platform Web SDK擴充功能概述
description: 了解適用於Adobe Experience Platform Launch的Adobe Experience Platform Web SDK擴充功能
exl-id: 96d32db8-0c9a-49f0-91f3-0244522d66df
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 12%

---

# Adobe Experience Platform Web SDK擴充功能概述

Adobe Experience Platform Web SDK擴充功能會透過Adobe Experience Platform邊緣網路，將資料從Web屬性傳送至Adobe Experience Cloud。 擴充功能可讓您將資料串流至Platform、同步身分、處理客戶同意訊號，以及自動收集內容資料。

本檔案說明如何在Adobe Experience Platform Launch使用者介面中設定擴充功能。

## 設定擴充功能

如果已為屬性安裝Platform Web SDK擴充功能，請開啟Platform launchUI中的屬性，然後選取&#x200B;**[!UICONTROL Extensions]**&#x200B;標籤。 在「平台Web SDK」下，選擇「**[!UICONTROL 配置]**」。

![](../images/extension/overview/configure.png)

如果您尚未安裝擴充功能，請選取「**[!UICONTROL 目錄]**」標籤。 從可用擴充功能清單中，尋找Platform Web SDK擴充功能，然後選取&#x200B;**[!UICONTROL 安裝]**。

![](../images/extension/overview/install.png)

在這兩種情況下，您都會到達Platform Web SDK的設定頁面。 以下各節說明擴充功能的設定選項。

![](../images/extension/overview/config-screen.png)

## 一般配置選項

頁面頂端的設定選項會告訴Adobe Experience Platform要在何處路由資料，以及要在伺服器上使用哪些設定。

### [!UICONTROL 名稱]

Adobe Experience Platform Web SDK擴充功能支援頁面上的多個執行個體。 名稱可用來透過單一Platform launch設定將資料傳送至多個組織。

擴充功能的名稱預設為「[!DNL alloy]」。 不過您可將例項名稱變更為任何有效的 JavaScript 物件名稱。

### **[!UICONTROL IMS 組織 ID]**

[!UICONTROL IMS組織ID]是您希望在Adobe傳送資料的組織。 大部分時候，請使用自動填入的預設值。 頁面上有多個執行個體時，請以您要傳送資料的第二個組織的值填入此欄位。

### **[!UICONTROL 邊緣網域]**

[!UICONTROL Edge Domain]是Adobe Experience Platform擴充功能傳送及接收資料的網域。 擴充功能會要求您為生產流量使用第一方 CNAME。預設的第三方網域適用於開發環境，但不適用於生產環境。若需設定第一方 CNAME 的相關說明，請參閱[此處](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=zh-Hant)。

## [!UICONTROL 資料流]

當請求傳送至Adobe Experience Platform邊緣網路時，資料流ID會用來參考伺服器端設定。 您不必在網站上變更程式碼，即可更新設定。

如需詳細資訊，請參閱[datastreams](../fundamentals/datastreams.md)上的指南。


## [!UICONTROL 隱私]

[!UICONTROL Privacy]區段可讓您設定SDK如何處理來自您網站的使用者同意訊號。 具體來說，它可讓您在未提供其他明確同意偏好設定時，選取使用者所假設的預設同意等級。 預設同意層級不會儲存至使用者的設定檔。 下表列出每個選項的要求：

| [!UICONTROL 預設同意層級] | 說明 |
| --- | --- |
| [!UICONTROL 在] | 收集在使用者提供同意偏好設定之前發生的事件。 |
| [!UICONTROL 退出] | 捨棄在使用者提供同意偏好設定之前發生的事件。 |
| [!UICONTROL 待定] | 在使用者提供同意偏好設定之前，將發生的事件排入佇列。 提供同意偏好設定時，系統會根據提供的偏好設定，收集或捨棄事件。 |
| [!UICONTROL 由資料元素提供] | 預設同意層級由您定義的個別資料元素決定。 使用此選項時，您必須使用提供的下拉式選單來指定資料元素。 |

如果您的業務操作需要明確的用戶同意，請使用「取消」或「待定」。
