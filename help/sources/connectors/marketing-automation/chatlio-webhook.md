---
title: 查圖文源概述
description: 瞭解如何使用API或通過利用Webhooks將Chatlio連接到Adobe Experience Platform
badge: β
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
>的 [!DNL Chatlio] 源為beta。 請閱讀 [源概述](../../home.md#terms-and-conditions) 的子菜單。

Adobe Experience Platform允許從外部源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。 您可以從多種源(如Adobe應用程式、基於雲的儲存、資料庫和許多其他源)接收資料。

Experience Platform支援從流應用程式接收資料。 對流提供商的支援包括 [!DNL Chatlio]。

[[!DNL Chatlio]](https://chatlio.com/) 是一個與 [!DNL Slack] 並為多個支援代理提供方便，同時幫助單個站點訪問者。 [!DNL Chatlio] 使用 [!DNL Chatio Zapier App] 連接 [!DNL Chatlio] 有2000多個不同的應用和服務。

的 [!DNL Chatlio] 源允許您從中獲取支援的webhook事件架構及其關聯事件資料 [!DNL Chatlio.com] 使用 [[!DNL Chatlio] 網鈎](https://chatlio.com/docs/webhooks/)。

支援的Webhook包括：

* 導出聊天記錄
* 導出離線郵件
* 新對話已開始
* 訪問者沒有及時得到答案
* 訪問者在聊天后留下反饋

## 先決條件 {#prerequisites}

在建立 [!DNL Chatlio] 源連接，必須首先確保您具有以下功能：

* A [!DNL Chatlio] 帳戶。 如果您還沒有訪問 [[!DNL Chatlio] 註冊頁](https://chatlio.com/app/#/signup) 註冊並建立帳戶。
* 成功註冊帳戶後，請 [[!DNL Chatlio] 設定文檔](https://chatlio.com/docs/setup/) 完成帳戶設定。

### 設定 [!DNL Chatlio] 網鈎 {#set-up-webhook}

成功建立資料流後，必須設定Webhook以通知平台 [!DNL Chatlio] 事件。 Webhooks可在客戶屬性發生更改或人員開啟您的郵件並將此資訊發送給您時立即通知您 [!DNL Chatlio] 源。

有關詳細資訊，請閱讀上的教程 [獲取流終結點URL](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) 和 [設定 [!DNL Chatlio] 網鈎](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook)。

## 連接 [!DNL Chatlio] 到平台 {#connect-to-platform}

以下文檔提供了有關如何建立 [!DNL Chatlio] 流式連接器連接到 [!DNL Platform] 使用API或用戶介面：

### 連接 [!DNL Chatlio] 到使用API的平台 {#connect-to-platform-using-api}

* [建立源連接以 [!DNL Chatlio] 使用API向平台發送資料。](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### 連接 [!DNL Chatlio] 到使用UI的平台 {#connect-to-platform-using-ui}

* [建立源連接以 [!DNL Chatlio] 使用用戶介面向平台發送資料](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)
