---
title: 查圖源概述
description: 了解如何使用API或使用者介面，運用Webhook將Chatlio連線至Adobe Experience Platform
badge: Beta
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 4a71d1dc-e0eb-443e-a956-8caa0e82fa18
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# [!DNL Chatlio]

>[!NOTE]
>
>此 [!DNL Chatlio] 來源為測試版。 請閱讀 [來源概觀](../../home.md#terms-and-conditions) 以取得使用測試版標籤來源的詳細資訊。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。

Experience Platform支援從串流應用程式擷取資料。 支援串流提供者包括 [!DNL Chatlio].

[[!DNL Chatlio]](https://chatlio.com/) 是與 [!DNL Slack] 並協助多個支援代理同時協助個別網站訪客。 [!DNL Chatlio] 使用 [!DNL Chatio Zapier App] 連接 [!DNL Chatlio] 提供超過2000種不同的應用和服務。

此 [!DNL Chatlio] 來源可讓您從擷取支援的網頁連結事件結構及其相關事件資料 [!DNL Chatlio.com] 使用 [[!DNL Chatlio] Webhook](https://chatlio.com/docs/webhooks/).

支援的Webhook包括：

* 導出聊天記錄
* 匯出離線訊息
* 新對話已開始
* 訪客未及時獲得答案
* 訪客在聊天后留下意見

## 先決條件 {#prerequisites}

建立 [!DNL Chatlio] 源連接時，必須首先確保您具有以下內容：

* A [!DNL Chatlio] 帳戶。 如果尚未有任何人造訪 [[!DNL Chatlio] 註冊頁面](https://chatlio.com/app/#/signup) 註冊並建立帳戶。
* 成功註冊帳戶後，請遵循 [[!DNL Chatlio] 設定檔案](https://chatlio.com/docs/setup/) 完成帳戶設定。

### 設定 [!DNL Chatlio] webhook {#set-up-webhook}

成功建立資料流後，必須設定Webhook以通知Platform [!DNL Chatlio] 事件。 Webhook可在客戶屬性變更時或人員開啟您的訊息並將此資訊傳送至您的 [!DNL Chatlio] 來源。

如需詳細資訊，請參閱 [取得串流端點URL](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) 和 [設定 [!DNL Chatlio] Webhook](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## Connect [!DNL Chatlio] 到平台 {#connect-to-platform}

以下檔案提供如何建立 [!DNL Chatlio] 串流連接器與 [!DNL Platform] 使用API或使用者介面：

### Connect [!DNL Chatlio] 使用API到平台 {#connect-to-platform-using-api}

* [建立源連接以 [!DNL Chatlio] 使用API將資料傳送至Platform。](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Connect [!DNL Chatlio] 使用UI設為Platform {#connect-to-platform-using-ui}

* [建立源連接以 [!DNL Chatlio] 使用者介面將資料傳送至Platform](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)
