---
title: 事件轉送概觀
description: 了解 Adobe Experience Platform 中的事件轉送功能，它可讓您使用 Platform Edge Network 執行工作，而不變更標記實施。
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: 16f9ee9d14326f857b444c2361b894aca06b04d6
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 4%

---

# 事件轉送概觀

>[!NOTE]
>
>事件轉送是一項付費功能，屬於Adobe Real-time Customer Data Platform Connections、Prime或Ultimate方案的一部分。

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品檔案中出現了幾項術語變更。 請參閱下列[檔案](../../term-updates.md)，以取得術語變更的彙總參考資料。

Adobe Experience Platform中的事件轉送可讓您將收集的事件資料傳送至目的地以進行伺服器端處理。 事件轉送使用Adobe Experience PlatformEdge Network執行通常在使用者端上完成的工作，以降低網頁和應用程式負載。 透過與標籤類似的方式實作，事件轉送規則可以轉換資料並將資料傳送到新目的地，但此資料不會從網頁瀏覽器之類的使用者端應用程式傳送，而是從Adobe的伺服器傳送。

本檔案提供Platform中事件轉送的整體概觀。

![資料收集生態系統中的事件轉送。](../../../collection/images/home/event-forwarding.png)

>[!NOTE]
>
>若要瞭解事件轉送如何在Platform的資料收集生態系統中運作，請參閱[資料收集概觀](../../../collection/home.md)。

結合Adobe Experience Platform [Web SDK](/help/web-sdk/home.md)和[Mobile SDK](https://experienceleague.adobe.com/docs/platform-learn/data-collection/mobile-sdk/overview.html)的事件轉送提供下列優點：

**效能**：

* 從包含資料裝載的頁面發出單一呼叫，接著在伺服器端組成聯盟，以減少使用者端網路流量，並為客戶提供更快速的體驗。
* 減少載入網頁所需的時間，以提升網站效能。
* 減少所需的使用者端技術數量，以提供您的體驗並將資料傳送至許多目的地。

**資料控管**：

* 增加透明度和控制跨所有屬性傳送哪些資料。

## 事件轉送與標籤之間的差異 {#differences-from-tags}

在設定方面，事件轉送使用許多與標籤相同的概念，例如[規則](../managing-resources/rules.md)、[資料元素](../managing-resources/data-elements.md)和[延伸模組](../managing-resources/extensions/overview.md)。 兩者之間的主要差異可概括如下：

* 標籤&#x200B;**會從網站或原生行動應用程式收集**&#x200B;事件資料，並將其傳送至平台Edge Network。
* 事件轉送&#x200B;**將**&#x200B;傳入的事件資料從PlatformEdge Network傳送至端點，該端點代表最終目的地或端點，提供您想要擴充原始裝載的資料。

雖然標籤會使用Platform Web和Mobile SDK直接從您的網站或原生行動應用程式收集事件資料，但事件轉送需先透過PlatformEdge Network傳送事件資料，才能將其轉送至目的地。 換言之，您必須在數位屬性上實作Platform Web或Mobile SDK （透過標籤或使用原始程式碼），才能使用事件轉送。

### 屬性 {#properties}

事件轉送會維護其專屬的屬性存放區，這些屬性與標籤不同，您可以在左側導覽中選取&#x200B;**[!UICONTROL 事件轉送]**，以在Experience PlatformUI或資料收集UI中檢視這些屬性。

>[!TIP]
>
>使用右側面板產品說明中的，深入瞭解事件轉送，並檢視其他可用的資源。

![資料收集UI中的事件轉送屬性。](../../images/ui/event-forwarding/overview/properties.png)

所有事件轉送屬性都會將&#x200B;**[!UICONTROL Edge]**&#x200B;列為平台。 它們不會區分Web或行動裝置，因為它們只會處理從PlatformEdge Network收到的資料，而該容器本身可同時從Web和行動平台接收事件資料。

### 擴充功能 {#extensions}

事件轉送有自己的相容擴充功能目錄，例如[核心](../../extensions/server/core/overview.md)擴充功能和[Adobe雲端聯結器](../../extensions/server/cloud-connector/overview.md)擴充功能。 您可以在左側導覽中選取&#x200B;**[!UICONTROL 擴充功能]**，然後選取&#x200B;**[!UICONTROL 目錄]**，以檢視UI中事件轉送屬性的可用擴充功能。

您可以從右側面板中選取![about](../../images/ui/event-forwarding/overview/about.png)，檢視其他可用的資源，以進一步瞭解此功能。

![資料收集UI中的事件轉送擴充功能。](../../images/ui/event-forwarding/overview/extensions.png)

### 資料元素 {#data-elements}

事件轉送中可用的資料元素型別僅限於提供它們的相容[擴充功能](#extensions)的目錄。

雖然資料元素本身在事件轉送中的建立與設定方式與標籤相同，但在如何參照來自平台Edge Network的資料方面，有一些重要的語法差異。

#### 從平台Edge Network參考資料 {#data-element-path}

若要參照來自PlatformEdge Network的資料，您必須建立提供該資料的有效路徑的資料元素。 在UI中建立資料元素時，請為擴充功能選取&#x200B;**[!UICONTROL 核心]**，為型別選取&#x200B;**[!UICONTROL 路徑]**。

資料元素的&#x200B;**[!UICONTROL 路徑]**&#x200B;值必須遵循模式`arc.event.{ELEMENT}` （例如： `arc.event.xdm.web.webPageDetails.URL`）。 必須正確指定此路徑才能傳送資料。

您可以從右側面板中選取![about](../../images/ui/event-forwarding/overview/about.png)，檢視其他可用的資源，以進一步瞭解此功能。

![用於事件轉送的路徑型別資料元素範例。](../../images/ui/event-forwarding/overview/data-reference.png)

### 規則 {#rules}

在事件轉送屬性中建立規則的運作方式與標籤類似，主要差異在於您無法選取事件做為規則元件。 反之，事件轉送規則會處理從[資料串流](../../../datastreams/overview.md)接收的所有事件，並在滿足某些條件時將那些事件轉送至目的地。

此外，有一個30秒的逾時適用於單一事件，因為單一事件會在事件轉送屬性內的所有規則（以及因此產生的所有動作）中處理。 這表示單一事件的所有規則和所有動作都必須在此時間範圍內完成。

您可以從右側面板中選取![about](../../images/ui/event-forwarding/overview/about.png)，檢視其他可用的資源，以進一步瞭解此功能。

![資料收集UI中的事件轉送規則。](../../images/ui/event-forwarding/overview/rules.png)

#### 資料元素代碼化 {#tokenization}

在標籤規則中，資料元素會在名稱的頭尾分別加上`%` （例如： `%viewportHeight%`），加以代碼化， 在事件轉送規則中，資料元素會改以資料元素名稱開頭的`{{`和`}}`結尾的`{{viewportHeight}}`加以代碼化。

您可以從右側面板中選取![about](../../images/ui/event-forwarding/overview/about.png)，檢視其他可用的資源，以進一步瞭解此功能。

![用於事件轉送的路徑型別資料元素範例。](../../images/ui/event-forwarding/overview/tokenization.png)

#### 規則動作順序 {#action-sequencing}

事件轉送規則的[!UICONTROL 動作]區段一律依序執行。 例如，如果規則有兩個動作，則第二個動作要等到前一個動作完成時才會開始執行（如果預期端點會回應，則表示該端點已回應）。 儲存規則時，請確認動作順序正確。此執行序列無法像使用標籤規則時一樣以非同步方式執行。

## 秘密 {#secrets}

事件轉送可讓您建立、管理和儲存秘密，這些秘密可用於向您傳送資料的目的地伺服器進行驗證。 請參閱[密碼](./secrets.md)指南，瞭解不同種類的可用密碼型別以及這些型別在UI中的實作方式。

## 影片概觀 {#video}

以下影片旨在協助您更清楚瞭解事件轉送和Real-Time CDP連線。

>[!VIDEO](https://video.tv.adobe.com/v/3429308)

## 後續步驟

本檔案簡要介紹事件轉送。 如需有關如何為您的組織設定此功能的詳細資訊，請參閱[快速入門手冊](./getting-started.md)。
