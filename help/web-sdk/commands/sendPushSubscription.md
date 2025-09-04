---
title: sendPushSubscription
description: 向Adobe Experience Platform註冊推播通知訂閱。
source-git-commit: 9c3f19cc2b32ab70869584b620f5a55d5b808751
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 2%

---


# `sendPushSubscription` {#send-push-subscription}

>[!AVAILABILITY]
>
> Web SDK的推播通知目前在&#x200B;**測試版**&#x200B;中。 功能和檔案可能會變更。

`sendPushSubscription`命令會向Adobe Experience Platform註冊推播通知訂閱。 此命令會處理從瀏覽器擷取推播訂閱詳細資料，並將其傳送至您設定的資料流。

## 先決條件 {#prerequisites}

使用`sendPushSubscription`之前，請確定您擁有：

1. **已設定推播通知**：使用您的VAPID公開金鑰設定[`pushNotifications`](configure/pushnotifications.md)設定屬性
2. **使用者許可權**：使用者必須已授予通知許可權(`Notification.permission === "granted"`)
3. **服務背景工作**：您的網站上必須有已登入的服務背景工作
4. **推播管理員支援**：瀏覽器必須支援推播通知，並且有可用的PushManager API

## 使用網頁SDK標籤擴充功能註冊推播訂閱 {#register-push-subscription-tag-extension}

在Adobe Experience Platform資料收集標籤介面的規則中，以動作執行傳送推播訂閱資料。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 規則]**，然後選取所要的規則。
1. 在[!UICONTROL 動作]下，選取現有動作或建立動作。
1. 將[!UICONTROL 擴充功能]下拉式欄位設定為&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，並將[!UICONTROL 動作型別]設定為&#x200B;**[!UICONTROL 傳送推播訂閱]**。
1. 按一下&#x200B;**[!UICONTROL 保留變更]**，然後執行您的發佈工作流程。

## 使用網頁SDK JavaScript資料庫註冊推播訂閱 {#register-push-subscription-javascript}

呼叫您設定的Web SDK執行個體時執行`sendPushSubscription`命令。 在呼叫[`configure`](configure/overview.md)命令之前，請確定您已設定推播通知來呼叫`sendPushSubscription`命令。

```js
alloy("sendPushSubscription")
  .then(() => {
    console.log("Push subscription recorded successfully");
  })
  .catch((error) => {
    console.error("Failed to send push subscription:", error);
  });
```

## 建議的執行頻率 {#recommended-execution-frequency}

為獲得最佳的推播通知功能，Adobe建議每天執行`sendPushSubscription`命令&#x200B;**一次**。 這可確保：

- Adobe Experience Platform中的訂閱詳細資料保持最新狀態
- 會擷取對推送代號或訂閱狀態所做的任何變更
- 使用者的設定檔會與最新的推播通知偏好設定一起更新

您可以使用類似下列的方法來實施此方法：

```js
// Check if we've sent subscription data today
const lastSent = localStorage.getItem("alloy_push_last_sent");
const today = new Date().toDateString();

if (lastSent !== today) {
  alloy("sendPushSubscription").then(() => {
    localStorage.setItem("alloy_push_last_sent", today);
  });
}
```

## 運作方式 {#how-it-works}

`sendPushSubscription`命令會執行下列動作：

1. **驗證先決條件**：驗證是否已設定推播通知並授予使用者許可權
2. **等待身分識別**：等待使用者的ECID可用
3. **擷取訂閱**：使用設定的VAPID金鑰從Service Worker取得作用中推播訂閱
4. **檢查變更**：比較目前的訂閱詳細資料與快取的值（ECID +訂閱詳細資料）。 如果訂閱詳細資料未變更，該命令會記錄一則資訊訊息，並且不會提出網路要求即會傳回
5. **傳送至資料流**：如果偵測到變更，會將訂閱資料傳輸至您設定的Adobe Experience Platform資料流
6. **更新快取**：儲存新的訂閱詳細資料，以供日後比較

## 錯誤處理 {#error-handling}

常見錯誤條件及其訊息：

| 錯誤 | 原因 |
| ------- | ---- |
| `"Push notifications module is not configured. No VAPID public key was provided."` | pushNotifications設定遺失或無效 |
| `"Service workers are not supported in this browser."` | 瀏覽器不支援服務背景工作 |
| `"Push notifications are not supported in this browser."` | 瀏覽器不支援推播通知或通知API |
| `"The user has not given permission to send push notifications."` | 使用者尚未授予通知許可權 |
| `"No service worker registration was found."` | 目前來源未登入服務背景工作 |
| `"No VAPID public key was provided."` | 設定中缺少VAPID公開金鑰 |

## 資料裝載 {#data-payload}

該命令會以下列格式傳送推播通知資料：

```js
{
  pushNotificationDetails: [
    {
      appID: "example.com", // Current domain
      token: "...", // Serialized subscription details + ECID
      platform: "web", // Always "web" for Web SDK
      denylisted: false, // Always false
      identity: {
        namespace: {
          code: "ECID",
        },
        id: "12345678901234567890", // User's ECID
      },
    },
  ],
}
```

## 相關檔案

- [設定推播通知](configure/pushnotifications.md)
- [網頁推播API規格](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
- [Service Worker API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
