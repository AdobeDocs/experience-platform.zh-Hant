---
title: 在Adobe Experience Platform Web SDK中除錯
description: 瞭解如何在Experience Platform Web SDK中切換除錯功能。
keywords: 除錯網頁sdk；除錯；configure;configure命令；debug命令；edgeConfigId;setDebug;debugEnabled;debug;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---


# 為  除錯

啟用除錯時，SDK會將訊息輸出至瀏覽器主控台，以協助除錯您的實作並瞭解SDK的運作方式。 除錯也會針對您所設定的架構，產生伺服器端同步驗證所收集的資料。

預設會停用除錯功能，但可以以三種不同的方式開啟：

* `configure` 命令
* `setDebug` 命令
* 查詢字串參數

## 使用Configure命令切換調試

使用`configure`命令設定SDK時，請將`debugEnabled`選項設為`true`以啟用除錯。

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

使用個別的`debug`命令切換除錯，如下所示：

```javascript
alloy("setDebug", {
  "enabled": true
});
```

如果您不想變更網頁上的程式碼，或不想為網站的所有使用者產生記錄訊息，這特別有用，因為您可以隨時在瀏覽器的JavaScript主控台中執行`debug`命令。

## 使用查詢字串參數切換除錯

將`alloy_debug`查詢字串參數設為`true`或`false`，切換除錯，如下所示：

```HTTP
http://example.com/?alloy_debug=true
```

與`debug`命令類似，如果您不想變更網頁上的程式碼，或不想為網站的所有使用者產生記錄訊息，這特別有用，因為您可以在瀏覽器中載入網頁時設定查詢字串參數。

## 優先順序和持續時間

通過`debug`命令或查詢字串參數設定調試時，它將覆蓋在`configure`命令中設定的任何`debug`選項。 在這兩種情況下，除錯功能在工作階段期間仍會繼續開啟。 換言之，如果您使用debug命令或查詢字串參數啟用除錯，則會一直啟用除錯功能，直到下列其中一項為止：

* 課程結束
* 運行`debug`命令
* 您再次設定查詢字串參數

## 檢索庫資訊

存取您載入網站之資料庫後的部分詳細資訊通常很實用。 要執行此操作，請按如下方式執行`getLibraryInfo`命令：

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
});
```

目前，提供的`libraryInfo`物件包含下列屬性：

* `version` 這是載入的程式庫版本。例如，如果要載入的程式庫版本為1.0.0，則值會是`1.0.0`。
