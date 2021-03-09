---
title: Adobe Experience Platform Web SDK 擴充功能 概述
description: 瞭解適用於Adobe Experience Platform Launch的Adobe Experience Platform網頁SDK擴充功能
translation-type: tm+mt
source-git-commit: b9fb71ac7eca95c65165d6780b681ada3f16325b
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 13%

---


# Adobe Experience Platform網頁SDK擴充功能概觀

Adobe Experience PlatformWeb SDK擴充功能會透過Adobe Experience Platform邊緣網路，從Web屬性傳送資料至Adobe Experience Cloud。 此擴充功能可讓您將資料串流至平台、同步身分、處理客戶同意訊號，並自動收集上下文資料。

本檔案說明如何在Adobe Experience Platform Launch使用者介面中設定擴充功能。

## 設定擴充功能

如果已為屬性安裝平台網頁SDK擴充功能，請在Platform launchUI中開啟屬性，然後選取「**[!UICONTROL 擴充功能]**」標籤。 在「平台網頁SDK」下，選取「**[!UICONTROL 設定]**」。

![](../images/extension/overview/configure.png)

如果尚未安裝擴展，請選擇&#x200B;**[!UICONTROL Catalog]**&#x200B;頁籤。 從可用擴充功能清單中，尋找平台網頁SDK擴充功能，並選取&#x200B;**[!UICONTROL Install]**。

![](../images/extension/overview/install.png)

在這兩種情況下，您都會到達平台網頁SDK的設定頁面。 以下各節說明擴充功能的設定選項。

![](../images/extension/overview/config-screen.png)

## 一般配置選項

頁面頂部的配置選項告訴Adobe Experience Platform資料路由的位置以及伺服器上要使用的配置。

### [!UICONTROL 名稱]

Adobe Experience Platform網頁SDK擴充功能支援頁面上的多個執行個體。 此名稱用於使用單一Platform launch配置向多個組織發送資料。

副檔名預設為&quot;[!DNL alloy]&quot;。 不過您可將例項名稱變更為任何有效的 JavaScript 物件名稱。

### **[!UICONTROL IMS 組織 ID]**

[!UICONTROL IMS組織ID]是您要在Adobe傳送資料的組織。 大部分時候，請使用自動填入的預設值。 當頁面上有多個例項時，請將您要傳送資料至的第二個組織的值填入此欄位。

### **[!UICONTROL 邊緣網域]**

[!UICONTROL Edge Domain]是Adobe Experience Platform分機發送和接收資料的域。 擴充功能會要求您為生產流量使用第一方 CNAME。預設的第三方網域適用於開發環境，但不適用於生產環境。若需設定第一方 CNAME 的相關說明，請參閱[此處](https://docs.adobe.com/content/help/zh-Hant/core-services/interface/ec-cookies/cookies-first-party.html)。

## [!UICONTROL Edge Configurations]

當請求傳送至Adobe Experience Platform邊緣網路時，會使用邊緣組態ID來參考伺服器端組態。 您可以更新設定，而不需在網站上變更程式碼。

如需詳細資訊，請參閱[edge configurations](../fundamentals/edge-configuration.md)上的指南。

## [!UICONTROL 隱私]

[!UICONTROL 隱私]區段可讓您設定SDK如何處理您網站的使用者同意訊號。 具體來說，它允許您選擇在未提供其他明確同意偏好的情況下假定用戶的預設同意級別。 預設同意層級不會儲存至使用者的設定檔。 下表列出每個選項所包含的內容：

| [!UICONTROL 預設許可級別] | 說明 |
| --- | --- |
| [!UICONTROL 在] | 收集在使用者提供同意偏好設定之前發生的事件。 |
| [!UICONTROL Out] | 捨棄在使用者提供同意偏好設定之前發生的事件。 |
| [!UICONTROL 待定] | 在使用者提供同意偏好設定之前發生的佇列事件。 當提供許可偏好時，會根據提供的偏好收集或捨棄事件。 |
| [!UICONTROL 由資料元素提供] | 預設同意層級由您定義的個別資料元素決定。 使用此選項時，您必須使用提供的下拉式功能表指定資料元素。 |

如果您需要明確的使用者同意才能進行業務運作，請使用「退出」或「待定」。