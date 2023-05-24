---
title: Customer.io源概述
description: 瞭解如何使用API或用戶介面通過利用Webhook將Customer.io連接到Adobe Experience Platform
badge: β
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 0f4ee106-c22b-465c-9c5e-83709e8424f5
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# [!DNL Customer.io]

>[!NOTE]
>
>的 [!DNL Customer.io] 源為beta。 請閱讀 [源概述](../../home.md#terms-and-conditions) 的子菜單。

Adobe Experience Platform允許從外部源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。 您可以從多種源(如Adobe應用程式、基於雲的儲存、資料庫和許多其他源)接收資料。

Experience Platform支援從流應用程式中接收資料。 對流提供商的支援包括 [!DNL Customer.io]。

[[!DNL Customer.io]](https://customer.io/) 是一個自動消息傳遞平台，面向希望擁有更大控制和靈活性的營銷人員，他們可以編寫和發送資料驅動的電子郵件、推送通知、應用內消息和簡訊。

的 [!DNL Customer.io] 源允許您從中獲取支援的webhook事件架構及其關聯事件資料 [!DNL Customer.io] 使用 [[!DNL Customer.io] 報告Webhooks](https://customer.io/docs/api/webhooks/)。

支援的webhook事件架構包括：

* 客戶事件
* 電子郵件事件
* SMS事件
* 推送通知事件
* 應用內消息事件
* Slack事件
* Webhook事件

有關通過Webhooks可用的事件清單，請參閱 [[!DNL Customer.io] 報告Webhook事件](https://customer.io/docs/webhooks/#events) 文檔。

## 先決條件 {#prerequisites}

在建立 [!DNL Customer.io] 源連接，必須首先確保您具有以下功能：

* A [!DNL Customer.io] 帳戶。 如果你沒看過 [[!DNL Customer.io] 註冊頁](https://fly.customer.io/signup) 註冊並建立帳戶。
* 建立帳戶後，您還需要驗證帳戶。 按照 [[!DNL Customer.io] 帳戶驗證](https://customer.io/docs/account-verification/) 的子菜單。

### 設定 [!DNL Customer.io] 網鈎 {#set-up-webhook}

成功建立資料流後，必須設定報告網頁掛接以通知平台 [!DNL Customer.io] 事件。 Webhooks可以在客戶屬性發生更改或人員開啟您的郵件時立即通知您，並將此資訊發送給您 [!DNL Customer.io] 源。 有關詳細資訊，請閱讀上的教程 [獲取流終結點URL](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) 和 [設定 [!DNL Customer.io] 網鈎](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook)。

## 連接 [!DNL Customer.io] 到平台 {#connect-to-platform}

以下文檔提供了有關如何建立 [!DNL Customer.io] 流連接與 [!DNL Platform] 使用API或用戶介面：

### 連接 [!DNL Customer.io] 到使用API的平台 {#connect-to-platform-using-api}

* [建立源連接和資料流以 [!DNL Customer.io] 使用API向平台發送資料。](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### 連接 [!DNL Customer.io] 到使用UI的平台 {#connect-to-platform-using-ui}

* [建立源連接和資料流以 [!DNL Customer.io] 使用用戶介面向平台發送資料](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)
