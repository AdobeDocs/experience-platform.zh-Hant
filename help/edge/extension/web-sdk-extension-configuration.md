---
title: 配置Adobe Experience PlatformWeb SDK擴展
description: 如何在UI中配置Adobe Experience PlatformWeb SDK標籤擴展。
exl-id: 96d32db8-0c9a-49f0-91f3-0244522d66df
source-git-commit: ce2e80a7ea7385be98bbcda6a0704cd0814c62b2
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 6%

---

# 配置Adobe Experience PlatformWeb SDK擴展

Adobe Experience PlatformWeb SDK標籤擴展通過Adobe Experience Platform邊緣網路從Web屬性向Adobe Experience Cloud發送資料。 擴展允許您將資料流入平台、同步身份、處理客戶同意信號並自動收集上下文資料。

本文檔介紹如何在UI中配置擴展。

## 快速入門

如果已為屬性安裝了平台Web SDK擴展，請開啟UI中的屬性，然後選擇 **[!UICONTROL 擴展]** 頁籤。 在平台Web SDK下，選擇 **[!UICONTROL 配置]**。

![](../assets/extension/overview/configure.png)

如果尚未安裝擴展，請選擇 **[!UICONTROL 目錄]** 頁籤。 從可用擴展的清單中，查找平台Web SDK擴展，然後選擇 **[!UICONTROL 安裝]**。

![](../assets/extension/overview/install.png)

在這兩種情況下，您都會到達平台Web SDK的配置頁。 以下各節說明了擴展的配置選項。

![](../assets/extension/overview/config-screen.png)

## 常規配置選項

頁面頂部的配置選項告訴Adobe Experience Platform資料的路由位置以及伺服器上要使用的配置。

### [!UICONTROL 名稱]

Adobe Experience PlatformWeb SDK擴展支援頁面上的多個實例。 該名稱用於向具有標籤配置的多個組織發送資料。

副檔名的名稱預設為「[!DNL alloy]。 不過您可將例項名稱變更為任何有效的 JavaScript 物件名稱。

### **[!UICONTROL IMS 組織 ID]**

的 [!UICONTROL IMS組織ID] 是您希望在Adobe發送資料的組織。 大多數情況下，使用自動填充的預設值。 在頁上具有多個實例時，使用要向其發送資料的第二個組織的值填充此欄位。

### **[!UICONTROL 邊緣網域]**

的 [!UICONTROL 邊緣域] 是Adobe Experience Platform分機發送和接收資料的域。 Adobe建議對此擴展使用第1方域(CNAME)。 預設的第三方網域適用於開發環境，但不適用於生產環境。若需設定第一方 CNAME 的相關說明，請參閱[此處](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=zh-Hant)。

## [!UICONTROL 資料串流]

當請求發送到Adobe Experience Platform邊緣網路時，資料流ID用於引用伺服器端配置。 您無需在網站上更改代碼即可更新配置。

請參閱上的指南 [資料流](../datastreams/overview.md) 的子菜單。


## [!UICONTROL 隱私]

![](../assets/extension/overview/privacy.png)

的 [!UICONTROL 隱私] 部分允許您配置SDK如何處理來自您網站的用戶同意信號。 具體來說，它允許您選擇在未提供其他明確的同意首選項時假定用戶的預設同意級別。 預設同意級別未保存到用戶的配置檔案。 下表分析了每個選項所包含的內容：

| [!UICONTROL 預設同意級別] | 說明 |
| --- | --- |
| [!UICONTROL 在] | 收集在用戶提供同意首選項之前發生的事件。 |
| [!UICONTROL 出] | 放棄在用戶提供同意首選項之前發生的事件。 |
| [!UICONTROL 待定] | 在用戶提供同意首選項之前發生的隊列事件。 當提供同意偏好時，將根據提供的偏好收集或丟棄事件。 |
| [!UICONTROL 由資料元素提供] | 預設同意級別由您定義的單獨資料元素確定。 使用此選項時，必須使用提供的下拉菜單指定資料元素。 |

如果您需要明確的用戶同意才能進行業務操作，請使用「退出」或「待定」。

## [!UICONTROL 身分]

![](../assets/extension/overview/identity.png)

### [!UICONTROL 從VisitorAPI遷移ECID]

此選項已預設啟用。啟用此功能後，SDK可以讀取AMCV和s_ecid Cookie，並設定Visitor.js使用的AMCV Cookie。 此功能在遷移到Adobe Experience PlatformWeb SDK時非常重要，因為某些頁面可能仍在使用Visitor.js。 它允許SDK繼續使用相同的ECID，以便用戶不被標識為兩個單獨的用戶。

### [!UICONTROL 使用第三方Cookie]

此選項使SDK能夠嘗試將用戶標識符儲存在第三方Cookie中。 如果成功，則當用戶在多個域中導航時，該用戶被標識為單個用戶，而不是被標識為每個域上的單獨用戶。 如果啟用此選項，則如果瀏覽器不支援第三方Cookie或用戶已配置為不允許第三方Cookie，則SDK可能仍無法將用戶標識符儲存在第三方Cookie中。 在這種情況下，SDK僅將標識符儲存在第一方域中。

## [!UICONTROL 個人化]

![](../assets/extension/overview/personalization.png)

如果在載入個性化內容時要隱藏某些部件，則可以在預隱藏樣式編輯器中指定要隱藏的元素。 然後，您可以複製提供給您的預設預隱藏代碼段，並將其貼上到 `<head>`HTML站點的元素。

## [!UICONTROL 資料收集]

![](../assets/extension/overview/data-collection.png)

### [!UICONTROL 回調函式]

擴展中提供的回調函式也稱為 [`onBeforeEventSend` 函式](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=zh-Hant) 的下界。 此函式允許您在事件發送到Adobe Edge網路之前全局修改事件。 有關如何使用此函式的詳細資訊，請參閱 [這裡](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#modifying-events-globally)。

### [!UICONTROL 按一下資料收集]

SDK可以自動收集您的連結點擊資訊。 預設情況下，此功能已啟用，但可以使用此選項禁用。 如果連結包含在 [!UICONTROL 下載連結限定符] 的子菜單。 Adobe為您提供了一些預設下載連結限定符，但可以隨時編輯這些限定符。

### [!UICONTROL 自動收集的上下文資料]

預設情況下，SDK會收集與設備、Web、環境和放置上下文相關的某些上下文資料。 如果您想看到Adobe收集的資訊清單，可以找到 [這裡](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=en)。 如果您不想收集此資料或只想收集某些類別的資料，則可以更改這些選項。

## [!UICONTROL 資料流配置覆蓋]

資料流覆蓋允許您為資料流定義其他配置，這些配置通過Web SDK傳遞到邊緣網路。

這有助於您觸發與預設資料流行為不同的資料流行為，而無需建立新資料流或修改現有設定。

資料流配置覆蓋是兩個步驟：

1. 首先，必須在 [資料流配置頁](../datastreams/configure.md)。
2. 然後，您必須通過Web SDK命令或使用Web SDK標籤擴展將覆蓋發送到邊緣網路。

查看資料流 [配置覆蓋文檔](../datastreams/overrides.md) 有關如何覆蓋資料流配置的詳細說明。

作為通過Web SDK命令傳遞替代的替代方法，您可以在下面顯示的標籤擴展螢幕中配置替代。

![顯示Web SDK標籤擴展頁中資料流配置覆蓋的影像。](../assets/extension/overview/datastream-overrides.png)

## [!UICONTROL 進階設定]

![](../assets/extension/overview/advanced-settings.png)

### [!UICONTROL 邊基路徑]

如果需要更改用於與Adobe Edge網路交互的基本路徑，請使用此欄位。 這不應需要更新，但是，如果您參與測試版或Alpha,Adobe可能會要求您更改此欄位。
