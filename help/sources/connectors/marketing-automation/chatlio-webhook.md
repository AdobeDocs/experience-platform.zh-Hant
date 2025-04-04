---
title: Chatlio Source概觀
description: 瞭解如何使用API或使用者介面利用Webhook將Chatlio連線至Adobe Experience Platform
badge: Beta
exl-id: 4a71d1dc-e0eb-443e-a956-8caa0e82fa18
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# [!DNL Chatlio]

>[!NOTE]
>
>[!DNL Chatlio]來源是測試版。 如需使用Beta版標籤來源的相關資訊，請參閱[來源概觀](../../home.md#terms-and-conditions)。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Experience Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從串流應用程式擷取資料。 對串流提供者的支援包括[!DNL Chatlio]。

[[!DNL Chatlio]](https://chatlio.com/)是與[!DNL Slack]完全整合的即時聊天應用程式，可協助多個支援代理程式同時協助個別網站訪客。 [!DNL Chatlio]使用[!DNL Chatio Zapier App]將[!DNL Chatlio]與2000多個不同的應用程式和服務連線。

[!DNL Chatlio]來源可讓您使用[[!DNL Chatlio] Webhooks](https://chatlio.com/docs/webhooks/)，從[!DNL Chatlio.com]擷取支援的Webhook事件結構描述及其相關的事件資料。

支援的Webhook包括：

* 匯出聊天記錄
* 匯出離線訊息
* 新交談已開始
* 訪客未及時收到答案
* 訪客在聊天後留下意見回饋

## 先決條件 {#prerequisites}

在建立[!DNL Chatlio]來源連線之前，您必須先確定您有下列專案：

* [!DNL Chatlio]帳戶。 如果您還沒有帳號，請造訪[[!DNL Chatlio] 註冊頁面](https://chatlio.com/app/#/signup)來註冊並建立您的帳號。
* 成功註冊帳戶後，請依照[[!DNL Chatlio] 設定檔案](https://chatlio.com/docs/setup/)完成帳戶設定。

### 設定[!DNL Chatlio] webhook {#set-up-webhook}

成功建立資料流後，您必須設定webhook以通知Experience Platform有關[!DNL Chatlio]個事件的資訊。 Webhook可在客戶屬性變更或有人開啟您的訊息並將此資訊傳送至您的[!DNL Chatlio]來源時，立即通知您。

如需詳細資訊，請閱讀[取得串流端點URL](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint)和[設定 [!DNL Chatlio] Webhook](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook)的教學課程。

## 將[!DNL Chatlio]連線至Experience Platform {#connect-to-platform}

以下檔案提供有關如何使用API或使用者介面建立[!DNL Chatlio]串流聯結器以與[!DNL Experience Platform]連線的資訊：

### 使用API連線[!DNL Chatlio]至Experience Platform {#connect-to-platform-using-api}

* [使用API建立來源連線，將 [!DNL Chatlio] 資料帶入Experience Platform。](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### 使用UI連線[!DNL Chatlio]至Experience Platform {#connect-to-platform-using-ui}

* [使用使用者介面建立來源連線，將 [!DNL Chatlio] 資料帶入Experience Platform](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)
