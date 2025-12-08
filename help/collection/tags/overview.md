---
title: 標籤使用者端JavaScript概述(_satellite)
description: 瞭解使用者端_satellite物件，以及您可在標籤中執行的各種功能。
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: 7f932e9868e84cf8abdaa6cf0b2da5bac837234d
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# 標籤使用者端JavaScript概觀(`_satellite`)

_這些頁面概述如何使用`_satellite`物件，讓您能夠使用JavaScript管理和自訂標籤邏輯。 如需如何在資料收集UI中設定實作的詳細資訊，請參閱[Adobe Experience Platform Web SDK標籤擴充功能](/help/tags/extensions/client/web-sdk/overview.md)。_

`_satellite`物件公開數個支援的進入點，可協助您與網站上發佈的標籤程式庫互動。 如果正確實作載入器標籤，所有標籤部署都會公開`_satellite`。 此物件有幾個主要使用案例：

* 在自訂程式碼區塊中使用標籤程式庫，可讓您完整存取標籤程式庫本身。
* 對任何環境（開發、預備或生產）中部署的實作進行除錯
* 直接在您的網站上實作，讓您能夠完全控制事件或標籤規則觸發的時間。 若為新實作，Adobe建議使用更靈活的策略，例如[Adobe使用者端資料層](/help/tags/extensions/client/client-data-layer/overview.md)。

>[!IMPORTANT]
>
>如果您從網站程式碼（例如`_satellite`）呼叫`_satellite.track()`，請&#x200B;**保護每次呼叫**，讓網站不會與標籤程式庫緊密結合。
>
>在標籤屬性的自訂程式碼內或在您的瀏覽器主控台本機中使用`_satellite`不需要防範。

## 常見使用範例

```js
// Read and write a temporary data element value (guarded)
if(window._satellite?.getVar && window._satellite?.setVar) {
  const region = _satellite.getVar('user_region');
  _satellite.setVar('promo_code', code);
}

// Manually trigger a rule configured in your tag property (guarded)
if (window._satellite?.track) {
  _satellite.track('cart_add', { sku: '123', qty: 2 });
}

// Local console debugging (guarding not needed)
_satellite.setDebug(true);
_satellite.logger.log('Rule evaluated');
```
