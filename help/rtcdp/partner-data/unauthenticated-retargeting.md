---
title: 未驗證的伺服器端重新目標定位
description: 瞭解如何使用ECID重新鎖定未經驗證的使用者
feature: Use Cases, Customer Acquisition
exl-id: 008f4534-29e7-49b9-b0be-9e0c3962ee21
source-git-commit: ba2154e84f24ddf4ec270121bdcbb6dd5d3dff42
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# 未驗證的伺服器端重新目標定位 {#unauthenticated-retargeting}

由於第三方Cookie失效，企業正轉為使用無Cookie解決方案進行個人化參與和重新鎖定目標。 異地重新鎖定目標可讓企業根據先前的互動觸及高意圖使用者，而不需依賴使用者端JavaScript。

## 為何要考慮重新鎖定未經驗證的訪客 {#why-use-case}

透過整合Adobe Experience Platform的Web SDK和伺服器端事件轉送，您可以簡化事件串流和資料轉送。 這可讓您順暢地使用ECID (Experience Cloud ID)重新鎖定未經驗證的使用者，確保各平台間的持續參與。 使用此解決方案，您可以根據未經驗證的使用者過去的互動，有效重新鎖定他們的目標，以增加轉換機會。

## 必要條件和規劃 {#prerequisites-and-planning}

在繼續部署Web SDK和事件轉送設定之前，請確定以下事項：

1. **具有Web SDK設定的Adobe**：必須實作Adobe Web SDK，以便利事件收集和資料轉送。

2. **Adobe Experience Platform Edge Network設定**：請確定Edge Network已設定為支援即時事件轉送，以進行站外重新目標定位。

3. **ECID同步**：請確定ECID已跨平台同步，以啟用順暢的對象比對。

## 如何達成異地重新目標定位 {#achieve-offsite-retargeting}

1. **部署Web SDK**：在您的網站上實作Adobe Web SDK以擷取即時事件資料，包括頁面檢視、點按和其他行為等使用者互動。

2. **啟用事件轉送**：設定Platform中的事件轉送以傳送收集的使用者資料，確保有效傳輸資料以啟用對象。

3. **設定伺服器端啟用**：使用Adobe的伺服器端功能，啟用根據ECID重新鎖定受眾，確保各平台間的受眾目標定位準確無誤。

4. **建立重新定位的對象**：利用Platform的對象細分工具，根據使用者行為（例如檢視、互動或放棄的購物車）來定義重點對象。

5. **啟用對象**：在您重新定位的對象建立後，請啟用這些對象以提供個人化內容，確保使用者能根據其先前與您網站的互動重新參與。

## 使用運算屬性建立對象 {#create-audience}

若要有效地重新鎖定高意圖使用者，請根據他們過去與您的網站的互動來建立對象。 使用Platform透過計算屬性來劃分使用者。

1. **識別關鍵行為**：選取要追蹤的使用者動作，例如頁面檢視或點按。

2. **建立對象**：使用對象細分工具，根據行為將使用者分組。

3. **同步ECID**：確保ECID跨平台同步處理，以精確比對對象。

## 啟用您的對象 {#activate-audience}

建立受眾後，請跨平台啟用受眾，以吸引使用者。

1. **檢閱對象**：確定對象區段反映正確行為。

2. **建立啟用規則**：根據動作設定使用者何時及如何參與的條件。

3. **推播至平台**：啟用對象。

4. **監視效能**：追蹤對象效能並視需要調整。

## 設定離站重新目標定位擴充功能 {#configure-extension}

### 部署Web SDK

請確定Adobe Web SDK已正確整合至您的網站。 此SDK可讓您收集即時事件資料，這對有效率的重新目標定位至關重要。

### 啟用事件轉送

在Platform內設定事件轉送，將收集的使用者行為資料傳送至重新定位平台。 事件轉送可確保有效率地傳輸資料，讓企業能夠在不依賴Cookie的情況下鎖定高意圖使用者。

### 附加至重新定位規則

請確定Adobe Experience Platform資料收集中的站外重新目標定位擴充功能已附加至有效的事件規則。 一般而言，應建立全域規則以觸發關鍵動作，例如`page load`或特定使用者互動。

若要深入瞭解如何設定擴充功能，請閱讀[事件轉送](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started)檔案。

## 其他使用案例 {#other-use-cases}

本檔案提供成功開發及使用Web SDK和事件轉送設定的主要使用案例和技術考量事項概觀。 透過遵循概述的程式並確保滿足必要的先決條件，您可以顯著改善其資料追蹤和分析功能。

您可以透過Real-Time CDP中的合作夥伴資料支援，進一步探索啟用的使用案例：

- [使用合作夥伴資料與新客戶互動並取得客戶](./prospecting.md)。
- [利用合作夥伴協助的訪客辨識功能，個人化現場體驗](./offsite-retargeting.md)。
- [使用合作夥伴提供的屬性補充第一方設定檔](./supplement-first-party-profiles.md)。
