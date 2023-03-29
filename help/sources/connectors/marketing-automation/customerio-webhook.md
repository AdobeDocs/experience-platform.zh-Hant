---
title: Customer.io源概述
description: 了解如何運用WebHook，使用API或使用者介面將Customer.io連線至Adobe Experience Platform
badge: "Beta"
source-git-commit: 9d6a4b5f60f7895e2c1833493926db147064f3f1
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# [!DNL Customer.io]

>[!NOTE]
>
>此 [!DNL Customer.io] 來源為測試版。 請閱讀 [來源概觀](../../home.md#terms-and-conditions) 以取得使用測試版標籤來源的詳細資訊。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。

Experience Platform支援從串流應用程式擷取資料。 支援串流提供者包括 [!DNL Customer.io].

[[!DNL Customer.io]](https://customer.io/) 是自動化傳訊平台，適合行銷人員，他們想要擁有更多控制力和彈性，以製作和傳送資料導向的電子郵件、推播通知、應用程式內訊息和簡訊。

此 [!DNL Customer.io] 來源可讓您從擷取支援的網頁連結事件結構及其相關事件資料 [!DNL Customer.io] 使用 [[!DNL Customer.io] 報告Webhook](https://customer.io/docs/api/webhooks/).

支援的Webhook事件結構包括：

* 客戶事件
* 電子郵件事件
* SMS事件
* 推播通知事件
* 應用程式內訊息事件
* Slack事件
* Webhook事件

如需可透過Webhook使用的事件清單，請參閱 [[!DNL Customer.io] 報告Webhook事件](https://customer.io/docs/webhooks/#events) 檔案。

## 先決條件 {#prerequisites}

建立 [!DNL Customer.io] 源連接時，必須首先確保您具有以下內容：

* A [!DNL Customer.io] 帳戶。 如果沒有人讀 [[!DNL Customer.io] 註冊頁面](https://fly.customer.io/signup) 註冊並建立帳戶。
* 建立帳戶後，您還需要驗證您的帳戶。 請依照 [[!DNL Customer.io] 帳戶驗證](https://customer.io/docs/account-verification/) 頁面來完成程式。

### 設定 [!DNL Customer.io] Webhook {#set-up-webhook}

成功建立資料流後，必須設定Reporting Webhook以通知Platform [!DNL Customer.io] 事件。 Webhook可在客戶屬性變更或人員開啟您的訊息時立即通知您，並將此資訊傳送至您的 [!DNL Customer.io] 來源。 如需詳細資訊，請參閱 [取得串流端點URL](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) 和 [設定 [!DNL Customer.io] Webhook](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook).

## 連接 [!DNL Customer.io] 到平台 {#connect-to-platform}

以下檔案提供如何建立 [!DNL Customer.io] 串流連線以連線至 [!DNL Platform] 使用API或使用者介面：

### Connect [!DNL Customer.io] 使用API到平台 {#connect-to-platform-using-api}

* [建立源連接和資料流以帶來 [!DNL Customer.io] 使用API將資料傳送至Platform。](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### Connect [!DNL Customer.io] 使用UI設為Platform {#connect-to-platform-using-ui}

* [建立源連接和資料流以帶來 [!DNL Customer.io] 使用者介面將資料傳送至Platform](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)

