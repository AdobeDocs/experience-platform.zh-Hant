---
title: 在Adobe Experience Platform Web SDK中除錯
description: 了解如何切換Experience PlatformWeb SDK中的除錯功能。
keywords: 偵錯web sdk；除錯；設定；設定命令；除錯命令；edgeConfigId;setDebug;debugEnabled；除錯；
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: c0e2d01bd21405f07f4857e1ccf45dd0e4d0f414
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# 為  除錯

啟用除錯時，SDK會將訊息輸出至瀏覽器主控台，有助於除錯實作及了解SDK的行為方式。

預設會停用除錯，但可透過三種不同方式開啟：

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
>這可為網頁的所有使用者（而非僅針對您的個人瀏覽器）進行除錯。

## 使用Debug命令切換除錯

使用單獨的`debug`命令切換調試，如下所示：

```javascript
alloy("setDebug", {
  "enabled": true
});
```

如果您不想變更網頁上的程式碼，或不想為網站的所有使用者產生記錄訊息，這特別有用，因為您可以隨時在瀏覽器的JavaScript主控台中執行`debug`命令。

## 使用查詢字串參數切換除錯

將`alloy_debug`查詢字串參數設定為`true`或`false`，切換偵錯，如下所示：

```HTTP
http://example.com/?alloy_debug=true
```

與`debug`命令類似，如果您不希望更改網頁上的代碼或不希望為網站的所有用戶生成日誌消息，這特別有用，因為您可以在瀏覽器內載入網頁時設定查詢字串參數。

## 優先順序和持續時間

透過`debug`命令或查詢字串參數設定偵錯時，會覆寫`configure`命令中設定的任何`debug`選項。 在這兩種情況下，在工作階段期間，除錯功能也會維持開啟狀態。 換句話說，如果您使用debug命令或查詢字串參數啟用除錯功能，則除非執行下列其中一項操作，否則會保持啟用狀態：

* 作業結束
* 運行`debug`命令
* 您可以再次設定查詢字串參數

## 檢索庫資訊

存取您載入至網站的程式庫後面的部分詳細資訊通常會很有幫助。 要執行此操作，請執行`getLibraryInfo`命令，如下所示：

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
});
```

目前，提供的`libraryInfo`物件包含下列屬性：

* `version` 這是載入的程式庫的版本。例如，如果要載入的程式庫版本為1.0.0，則值會是`1.0.0`。 當程式庫在標籤擴充功能（名為「AEP Web SDK」）內執行時，版本為程式庫版本，而標籤擴充功能版本以「+」符號連結。 例如，如果程式庫版本為1.0.0，而標籤擴充功能的版本為1.2.0，則值會是`1.0.0+1.2.0`。
