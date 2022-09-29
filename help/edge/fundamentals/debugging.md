---
title: 在Adobe Experience Platform Web SDK中除錯
description: 了解如何切換Experience PlatformWeb SDK中的除錯功能。
keywords: 偵錯web sdk；除錯；設定；設定命令；除錯命令；edgeConfigId;setDebug;debugEnabled；除錯；
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: f5270d1d1b9697173bc60d16c94c54d001ae175a
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 2%

---

# 為  除錯

啟用除錯後，SDK會將訊息輸出至瀏覽器主控台，有助於除錯實作及了解SDK的行為方式。

預設會停用除錯，但可透過四種不同方式開啟：

* `configure` 命令
* `setDebug` 命令
* 查詢字串參數
* 在Adobe Experience Platform Debugger中開啟啟用除錯。 Adobe Experience Platform是一項功能強大的工具，可檢查您的網頁，並協助您偵錯Experience Cloud產品的實作問題。 Adobe Experience Platform Debugger可用於 [鉻黃](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) 和 [Firefox](https://addons.mozilla.org/zh-TW/firefox/addon/adobe-experience-platform-dbg/) 擴充功能。 您可以從AEP Web SDK區段的「設定」標籤啟用除錯功能。

![](../assets/enable-debugging.png)

## 使用Configure命令切換調試

使用設定SDK時 `configure` 命令，通過設定 `debugEnabled` 選項 `true`.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!TIP]
>
>這可為網頁的所有使用者（而非僅針對您的個人瀏覽器）進行除錯。

## 使用Debug命令切換除錯

使用個別的 `debug` 命令，如下所示：

```javascript
alloy("setDebug", {
  "enabled": true
});
```

如果您不想變更網頁上的程式碼，或不想為網站的所有使用者產生記錄訊息，這特別有用，因為您可以執行 `debug` 命令。

## 使用查詢字串參數切換除錯

透過設定 `alloy_debug` 查詢字串參數 `true` 或 `false` 如下所示：

```HTTP
http://example.com/?alloy_debug=true
```

類似於 `debug` 命令，如果您不希望更改網頁上的代碼或不希望為網站的所有用戶生成日誌消息，則此選項特別有用，因為您可以在瀏覽器中載入網頁時設定查詢字串參數。

## 優先順序和持續時間

透過設定除錯時 `debug` 命令或查詢字串參數，它會覆寫 `debug` 選項 `configure` 命令。 在這兩種情況下，在工作階段期間，除錯功能也會維持開啟狀態。 換句話說，如果您使用debug命令或查詢字串參數啟用除錯功能，則除非執行下列其中一項操作，否則會保持啟用狀態：

* 作業結束
* 您執行 `debug` 命令
* 您可以再次設定查詢字串參數

## 檢索庫資訊

存取您載入至網站的程式庫後面的部分詳細資訊通常會很有幫助。 要執行此操作，請執行 `getLibraryInfo` 命令，如下所示：

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

目前，已提供 `libraryInfo` 物件包含下列屬性：

* `version`:這是載入的程式庫的版本。 例如，如果要載入的程式庫版本為1.0.0，則值會是 `1.0.0`. 當程式庫在標籤擴充功能（名為「AEP Web SDK」）內執行時，版本為程式庫版本，而標籤擴充功能版本以「+」符號連結。 例如，如果程式庫版本為1.0.0，而標籤擴充功能的版本為1.2.0，則值會是 `1.0.0+1.2.0`.
* `commands`:這些是載入的程式庫支援的所有可用命令。
* `configs`:這些是載入程式庫中的所有目前設定。
