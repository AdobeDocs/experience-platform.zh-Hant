---
title: 事件轉發概述
description: 了解 Adobe Experience Platform 中的事件轉送功能，它可讓您使用 Platform Edge Network 執行工作，而不變更標記實施。
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: 1ab1c269fd43368e059a76f96b3eb3ac4e7b8388
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 8%

---

# 事件轉發概述

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

Adobe Experience Platform的事件轉發允許您將收集的事件資料發送到目標進行伺服器端處理。 通過使用Adobe Experience Platform邊緣網路執行通常在客戶端上完成的任務，事件轉發降低了網頁和應用的權重。 以與標籤類似的方式實現，事件轉發規則可以轉換資料並將其發送到新目的地，但是，與其從客戶端應用程式（如Web瀏覽器）發送此資料，不如從Adobe的伺服器發送。

本文檔提供了平台中事件轉發的高級概述。

![資料收集生態系統中的事件轉發](../../../collection/images/home/event-forwarding.png)

>[!NOTE]
>
>有關事件轉發在平台中資料收集生態系統中的作用的資訊，請參見 [資料收集概述](../../../collection/home.md)。

事件轉發與Adobe Experience Platform [Web SDK](../../../edge/home.md) 和 [移動SDK](https://aep-sdks.gitbook.io/docs/) 提供了以下好處：

**效能**:

* 從包含資料負載的頁面進行單次呼叫，該資料負載隨後會在伺服器端進行聯合，以減少客戶端網路流量並為客戶提供更快的體驗。
* 減少網頁載入所花費的時間以提高站點效能。
* 減少所需的客戶端技術數量，以提供您的體驗並將資料發送到多個目標。

**資料治理**:

* 提高透明度，並控制在所有屬性之間發送資料的位置。

## 事件轉發和標籤之間的差異 {#differences-from-tags}

在配置方面，事件轉發使用許多與標籤相同的概念，如 [規則](../managing-resources/rules.md)。 [資料元素](../managing-resources/data-elements.md), [擴展](../managing-resources/extensions/overview.md)。 兩者的主要區別可歸納為：

* 標籤 **收集** 來自網站或本機移動應用程式的事件資料，並將其發送到平台邊緣網路。
* 事件轉發 **發送** 將事件資料從平台邊緣網路傳入到終結點，該終結點表示最終目標或終結點，該終結點提供您希望使用其豐富原始負載的資料。

當標籤使用平台Web和移動SDK直接從站點或本地移動應用程式收集事件資料時，事件轉發要求事件資料已通過平台邊緣網路發送，以便轉發到目標。 換句話說，您必須在數字屬性上（通過標籤或使用原始代碼）實現平台Web或移動SDK，才能使用事件轉發。

### 屬性 {#properties}

事件轉發維護其自己的屬性儲存，這些屬性與標籤分開，通過選擇 **[!UICONTROL 事件轉發]** 的子菜單。

![資料收集UI中的事件轉發屬性](../../images/ui/event-forwarding/overview/properties.png)

所有事件轉發屬性清單 **[!UICONTROL 邊緣]** 作為他們的平台。 它們不區分Web或移動，因為它們只處理從平台邊緣網路接收的資料，平台邊緣網路本身可以從Web和移動平台接收事件資料。

### 擴充功能 {#extensions}

事件轉發具有其自己的相容擴展目錄，如 [核心](../../extensions/web/core/event-forwarding.md) 擴展和 [Adobe雲連接器](../../extensions/web/cloud-connector/overview.md) 擴展。 通過選擇 **[!UICONTROL 擴展]** 在左側導航中，然後 **[!UICONTROL 目錄]**。

![資料收集UI中的事件轉發擴展](../../images/ui/event-forwarding/overview/extensions.png)

### 資料元素 {#data-elements}

在事件轉發中可用的資料元素的類型僅限於相容目錄 [擴展](#extensions) 提供它們。

雖然資料元素本身的建立和配置方式與標籤的轉發方式相同，但在如何引用平台邊緣網路中的資料方面，存在一些重要的語法差異。

#### 從平台邊緣網路引用資料 {#data-element-path}

要從平台邊緣網路引用資料，必須建立一個資料元素，該資料元素提供該資料的有效路徑。 在UI中建立資料元素時，選擇 **[!UICONTROL 核心]** 為延期和 **[!UICONTROL 路徑]** 的雙曲餘切值。

的 **[!UICONTROL 路徑]** 資料元素的值必須遵循模式 `arc.event.{ELEMENT}` (例如： `arc.event.xdm.web.webPageDetails.URL`)。 必須正確指定此路徑才能發送資料。

![用於事件轉發的路徑類型資料元素示例](../../images/ui/event-forwarding/overview/data-reference.png)

### 規則 {#rules}

在事件中建立規則轉發屬性的方式與標籤類似，關鍵區別在於不能選擇事件作為規則元件。 事件轉發規則會處理它從 [資料流](../../../edge/datastreams/overview.md) 如果滿足某些條件，則將這些事件轉發到目標。

![資料收集UI中的事件轉發規則](../../images/ui/event-forwarding/overview/rules.png)

#### 資料元素代碼化 {#tokenization}

在標籤規則中，資料元素與 `%` 在資料元素名稱的開頭和結尾處(例如： `%viewportHeight%`)。 在轉發規則時，資料元素會與 `{{` 於年初及 `}}` 在資料元素名稱的末尾(例如： `{{viewportHeight}}`)。

![用於事件轉發的路徑類型資料元素示例](../../images/ui/event-forwarding/overview/tokenization.png)

#### 規則動作順序 {#action-sequencing}

的 [!UICONTROL 操作] 事件轉發規則的部分始終按順序執行。 儲存規則時，請確認動作順序正確。此執行序列不能像對標籤執行時那樣非同步執行。

## 秘密 {#secrets}

事件轉發允許您建立、管理和儲存可用於向要向其發送資料的伺服器進行身份驗證的機密。 請參閱上的指南 [秘密](./secrets.md) 不同類型的可用密鑰類型以及它們在UI中的實現方式。

## 後續步驟

本文檔對事件轉發作了高級介紹。 有關如何為組織設定此功能的詳細資訊，請參閱 [入門指南](./getting-started.md)。
