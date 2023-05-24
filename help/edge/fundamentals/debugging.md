---
title: 在Adobe Experience PlatformWeb SDK中調試
description: 瞭解如何在Experience PlatformWeb SDK中切換調試功能。
keywords: 調試web sdk；調試；配置；配置命令；debug命令；edgeConfigId;setDebug;debugEnabled;debug;
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: f5270d1d1b9697173bc60d16c94c54d001ae175a
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 2%

---

# 為  除錯

啟用調試後，SDK會將消息輸出到瀏覽器控制台，這些消息有助於調試您的實現並瞭解SDK的行為。

預設情況下，調試處於禁用狀態，但可以通過以下四種不同方式切換：

* `configure` 命令
* `setDebug` 命令
* 查詢字串參數
* 切換在Adobe Experience Platform調試器中啟用調試。 Adobe Experience Platform是一種功能強大的工具，它可檢查您的網頁並幫助您調試Experience Cloud產品的實施問題。 Adobe Experience Platform調試器作為 [鉻](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) 和 [火狐](https://addons.mozilla.org/zh-TW/firefox/addon/adobe-experience-platform-dbg/) 擴展。 可以從AEP Web SDK部分的配置頁籤啟用調試。

![](../assets/enable-debugging.png)

## 使用Configure命令切換調試

使用 `configure` 命令，通過設定 `debugEnabled` 選項 `true`。

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!TIP]
>
>這允許對網頁的所有用戶進行調試，而不是僅針對個人瀏覽器。

## 使用Debug命令切換調試

使用單獨的 `debug` 命令，如下所示：

```javascript
alloy("setDebug", {
  "enabled": true
});
```

如果您不希望更改網頁上的代碼或不希望為網站的所有用戶生成日誌記錄消息，則此功能特別有用，因為您可以運行 `debug` 命令。

## 使用查詢字串參數切換調試

通過設定 `alloy_debug` 查詢字串參數 `true` 或 `false` 如下：

```HTTP
http://example.com/?alloy_debug=true
```

與 `debug` 命令，如果您不希望更改網頁上的代碼或不希望為網站的所有用戶生成日誌記錄消息，則此功能特別有用，因為您可以在瀏覽器中載入網頁時設定查詢字串參數。

## 優先順序和持續時間

通過 `debug` 命令或查詢字串參數，它將覆蓋任何 `debug` 中 `configure` 的子菜單。 在這兩種情況下，調試在會話期間仍處於切換狀態。 換句話說，如果使用debug命令或查詢字串參數啟用調試，則在以下某項之前，它將保持啟用狀態：

* 會話結束
* 您運行 `debug` 命令
* 再次設定查詢字串參數

## 檢索庫資訊

訪問您已載入到網站上的庫後的一些詳細資訊通常會有所幫助。 為此，請執行 `getLibraryInfo` 命令，如下所示：

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

目前， `libraryInfo` 對象包含以下屬性：

* `version`:這是已載入庫的版本。 例如，如果要載入的庫版本為1.0.0，則值將 `1.0.0`。 當庫在標籤擴展（名為「AEP Web SDK」）內運行時，版本是庫版本，而標籤擴展版本與「+」符號聯接。 例如，如果庫的版本為1.0.0，而標籤擴展的版本為1.2.0，則值為 `1.0.0+1.2.0`。
* `commands`:這些是載入的庫支援的所有可用命令。
* `configs`:這些是載入庫中的所有當前配置。
