---
title: 除錯
seo-title: Adobe Experience Platform Web SDK除錯
description: 瞭解如何切換Experience Platform Web SDK除錯
seo-description: 瞭解如何切換Experience Platform Web SDK除錯
keywords: debugging web sdk;debugging;configure;configure command;debug command;edgeConfigId;setDebug;debugEnabled;debug;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---


# 除錯

啟用除錯時，SDK會將訊息輸出至瀏覽器主控台，以協助除錯您的實作並瞭解SDK的運作方式。 除錯也會針對您所設定的架構，產生伺服器端同步驗證所收集的資料。

預設會停用除錯功能，但可以以三種不同的方式開啟：

* `configure` 命令
* `setDebug` 命令
* 查詢字串參數

## 使用Configure命令切換調試

使用命令設定SDK時， `configure` 請將選項設為，以啟 `debugEnabled` 用除錯 `true`。

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!TIP]
>
>如此可讓網頁的所有使用者除錯，而不只是您的個人瀏覽器。

## 使用Debug命令切換除錯

使用個別命令切換除 `debug` 錯，如下所示：

```javascript
alloy("setDebug", {
  "enabled": true
});
```

如果您不想變更網頁上的程式碼，或不想為網站的所有使用者產生記錄訊息，這特別有用，因為您隨時都可在瀏覽器的JavaScript主控台中執行 `debug` 該命令。

## 使用查詢字串參數切換除錯

將查詢字串參數設 `alloy_debug` 定為或如下，以 `true` 切換除 `false` 錯：

```HTTP
http://example.com/?alloy_debug=true
```

與命 `debug` 令類似，如果您不想變更網頁上的程式碼，或不想為網站的所有使用者產生記錄訊息，這特別有用，因為您可以在瀏覽器內載入網頁時設定查詢字串參數。

## 優先順序和持續時間

通過命令或查詢字串參 `debug` 數設定調試時，它會覆蓋命 `debug` 令中設定的任何 `configure` 選項。 在這兩種情況下，除錯功能在工作階段期間仍會繼續開啟。 換言之，如果您使用debug命令或查詢字串參數啟用除錯，則會一直啟用除錯功能，直到下列其中一項為止：

* 課程結束
* 運行命 `debug` 令
* 您再次設定查詢字串參數
