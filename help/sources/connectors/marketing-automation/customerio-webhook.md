---
title: Customer.io Source概觀
description: 瞭解如何使用API或使用者介面利用Webhook將Customer.io連線至Adobe Experience Platform
badge: Beta
exl-id: 0f4ee106-c22b-465c-9c5e-83709e8424f5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# [!DNL Customer.io]

>[!NOTE]
>
>[!DNL Customer.io]來源是測試版。 如需使用Beta版標籤來源的相關資訊，請參閱[來源概觀](../../home.md#terms-and-conditions)。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Experience Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從串流應用程式擷取資料。 對串流提供者的支援包括[!DNL Customer.io]。

[[!DNL Customer.io]](https://customer.io/)是自動化訊息平台，行銷人員可藉此擁有更多控制權和彈性，以製作及傳送資料導向電子郵件、推播通知、應用程式內訊息及簡訊。

[!DNL Customer.io]來源可讓您使用[[!DNL Customer.io] 報告Webhook](https://customer.io/docs/api/webhooks/)，從[!DNL Customer.io]擷取支援的Webhook事件結構描述及其相關事件資料。

支援的webhook事件結構描述包括：

* 客戶事件
* 電子郵件事件
* 簡訊事件
* 推播通知事件
* 應用程式內訊息事件
* Slack事件
* Webhook活動

如需可透過Webhook取得的活動清單，請參閱[[!DNL Customer.io] 報告Webhook活動](https://customer.io/docs/webhooks/#events)檔案。

## 先決條件 {#prerequisites}

在建立[!DNL Customer.io]來源連線之前，您必須先確定您有下列專案：

* [!DNL Customer.io]帳戶。 如果您沒有可以閱讀[[!DNL Customer.io] 註冊頁面](https://fly.customer.io/signup)來註冊並建立您的帳戶。
* 建立帳戶後，您還需要驗證帳戶。 請依照[[!DNL Customer.io] 帳戶驗證](https://customer.io/docs/account-verification/)頁面上記錄的步驟完成程式。

### 設定[!DNL Customer.io] Webhook {#set-up-webhook}

成功建立資料流後，您必須設定報告Webhook，以通知Experience Platform有關[!DNL Customer.io]個事件的資訊。 Webhook可在客戶屬性變更或某人開啟您的訊息時立即通知您，並將此資訊傳送至您的[!DNL Customer.io]來源。 如需詳細資訊，請閱讀[取得串流端點URL](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint)和[設定 [!DNL Customer.io] Webhook](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook)的教學課程。

## 正在將[!DNL Customer.io]連線到Experience Platform {#connect-to-platform}

以下檔案提供有關如何使用API或使用者介面建立[!DNL Customer.io]串流連線以與[!DNL Experience Platform]連線的資訊：

### 使用API連線[!DNL Customer.io]至Experience Platform {#connect-to-platform-using-api}

* [建立來源連線和資料流，以使用API將 [!DNL Customer.io] 資料帶入Experience Platform。](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### 使用UI連線[!DNL Customer.io]至Experience Platform {#connect-to-platform-using-ui}

* [使用使用者介面建立來源連線和資料流，將 [!DNL Customer.io] 資料帶入Experience Platform](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)
