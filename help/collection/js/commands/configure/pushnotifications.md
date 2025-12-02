---
title: pushNotifications
description: 設定Web SDK的推播通知，以啟用瀏覽器式的推播訊息。
source-git-commit: 60447ef6f881bf2a34f5502f2259328bf73d08c0
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 3%

---

# `pushNotifications` {#push-notifications}

>[!AVAILABILITY]
>
>Web SDK的推播通知目前在&#x200B;**測試版**&#x200B;中。 功能和檔案可能會有所變更。

`pushNotifications`屬性可讓您設定Web應用程式的推播通知。 此功能可讓您的網頁應用程式接收從伺服器推送的訊息，即使網站目前未載入瀏覽器亦然。

## 先決條件 {#prerequisites}

在設定推播通知之前，請確定您擁有：

1. **使用者許可權**：使用者必須明確授與通知許可權
2. **Service worker**：必須有Registered Service Worker才能執行推播通知
3. **VAPID金鑰**：產生VAPID （自願應用程式伺服器識別）金鑰以進行安全通訊
4. **應用程式ID**：將VAPID金鑰儲存在Adobe Journey Optimizer ->管道 — >推送設定 — >推送認證時所使用的應用程式ID
5. **追蹤資料集ID**：名稱為「AJO推播追蹤體驗事件資料集」的系統資料集ID。 從Adobe Journey Optimizer ->資料集取得此專案

## 產生VAPID金鑰 {#generate-vapid-keys}

若要產生VAPID金鑰，請安裝`web-push` NPM套件並執行：

```bash
npm install web-push -g
web-push generate-vapid-keys
```

此動作會產生公開和私密金鑰組。 在您的Web SDK設定中使用公開金鑰，並將私密金鑰儲存在Adobe Journey Optimizer推播通知頻道中。

## 安裝Service Worker

服務程式碼必須從與網站相同的網域提供。 從Adobe的CDN下載Service Worker程式碼，並從您自己的伺服器託管JavaScript檔案。 可使用以下URL結構取得Web SDK服務背景工作程式碼：

- **已縮制**： `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.min.js`
- **完整**： `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.js`

以下是如何安裝Service Worker的範例：

```html
<script>
  navigator.serviceWorker.register("/alloyServiceWorker.js", { scope: "/" });
</script>
```

## 實作

執行`pushNotifications`命令時設定`configure`物件：

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  pushNotifications: {
    vapidPublicKey: "BEl62iUYgU[...]KGP4jAQlJz",
    applicationId: "my-app-id",
    trackingDatasetId: "4dc19305cdd27e03dd9a6bbe",
  },
});
```

## 屬性 {#properties}

| 屬性 | 類型 | 必要 | 說明 |
|---|---|---|---|
| **`vapidPublicKey`** | 字串 | 是 | 用於推送訂閱的VAPID公開金鑰。 必須是Base64編碼的字串。 |
| **`applicationId`** | 字串 | 是 | 與VAPID公開金鑰相關聯的應用程式ID。 |
| **`trackingDatasetId`** | 字串 | 是 | 用於推播通知追蹤的系統資料集ID。 |

## 重要考量 {#important-considerations}

- **安全性**：推送訂閱繫結至訂閱期間使用的特定VAPID公開金鑰。 如果您變更VAPID金鑰，現有訂閱會自動取消訂閱，並使用新金鑰重新建立。
- **快取**： Web SDK會將目前的ECID和訂閱詳細資料與快取的值比較，以自動管理訂閱更新。 只有在偵測到變更時，才會傳送訂閱資料。
- **Service Worker需求**：推播通知需要註冊的Service Worker。 確保您的Service Worker已正確設定為處理推送事件。

## 使用Web SDK標籤擴充功能設定推播通知 {#configure-push-notifications-tag-extension}

設定擴充功能時，等同於此屬性的Web SDK標籤擴充功能為[[!UICONTROL Push notifications]](/help/tags/extensions/client/web-sdk/configure/push-notifications.md)區段。

## 後續步驟 {#next-steps}

設定推送通知後，請使用[sendPushSubscription](../sendpushsubscription.md)命令向Adobe Experience Platform註冊推送訂閱。
