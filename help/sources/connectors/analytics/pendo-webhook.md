---
title: Pendo源概述
description: 瞭解如何使用API或通過利用Webhooks將Pendo連接到Adobe Experience Platform
badge: β
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# [!DNL Pendo]

>[!NOTE]
>
>的 [!DNL Pendo] 源為beta。 請閱讀 [源概述](../../home.md#terms-and-conditions) 的子菜單。

Adobe Experience Platform允許從外部源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。 您可以從多種源(如Adobe應用程式、基於雲的儲存、資料庫和許多其他源)接收資料。

Experience Platform支援從第三方分析應用程式接收資料。 對分析提供方的支援包括 [!DNL Pendo]。

[[!DNL Pendo]](https://pendo.io/) 是一款產品分析應用，旨在幫助軟體公司開發能夠引起客戶共鳴的產品。 這款應用使軟體製造商能夠用多種工具嵌入產品，這些工具既能為用戶帶來更好的產品體驗，也能為產品團隊帶來新的見解。

的 [!DNL Pendo] 源允許您從中獲取支援的webhook事件架構及其關聯事件資料 [!DNL Pendo.io] 使用 [[!DNL Pendo] 網鈎](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks)。 的 [!DNL Pendo] 源工作 [!DNL Pendo] URL網頁掛接。

支援的Webhook包括：

* [指南](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) 顯示
* [投票](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) 已顯示/已提交
* [網路啟動程式分數](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) 已顯示/已提交

## 先決條件 {#prerequisites}

在建立 [!DNL Pendo] 源連接，必須首先確保您具有以下功能：

A [!DNL Pendo] 帳戶。 如果你還沒看到 [[!DNL Pendo] 註冊](https://app.pendo.io/register) 頁，以註冊和建立帳戶。

### 設定 [!DNL Pendo] 網鈎 {#set-up-webhook}

成功建立資料流後，必須設定Webhook以通知平台 [!DNL Pendo] 事件。 [!DNL Pendo] Webhooks可以在某些事件發生時向其他服務推送即時通知，並將此資訊發送給您 [!DNL Pendo] 源。 有關詳細資訊，請閱讀上的教程 [獲取流終結點URL](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) 和 [設定 [!DNL Pendo] 網鈎](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook)。

## 連接 [!DNL Pendo] 到平台 {#connect-to-platform}

以下文檔提供了有關如何建立 [!DNL Pendo] 流式連接器連接到 [!DNL Platform] 使用API或用戶介面：

### 連接 [!DNL Pendo] 到使用API的平台 {#connect-to-platform-using-api}

* [建立源連接以 [!DNL Pendo] 使用API向平台發送資料。](../../tutorials/api/create/analytics/pendo-webhook.md)

### 連接 [!DNL Pendo] 到使用UI的平台 {#connect-to-platform-using-ui}

* [建立源連接以 [!DNL Pendo] 使用用戶介面向平台發送資料](../../tutorials/ui/create/analytics/pendo-webhook.md)
