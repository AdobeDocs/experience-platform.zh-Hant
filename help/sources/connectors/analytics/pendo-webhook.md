---
title: Pendo來源概觀
description: 瞭解如何使用API或使用者介面利用Webhook將Pendo連線至Adobe Experience Platform
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
source-git-commit: 68c14d7b187075b4af6b019a8bd1ca2625beabde
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# [!DNL Pendo]

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從協力廠商分析應用程式擷取資料。 對分析提供者的支援包括 [!DNL Pendo].

[[!DNL Pendo]](https://pendo.io/) 是產品分析應用程式，專為協助軟體公司開發可與客戶引起共鳴的產品而打造。 此應用程式可讓軟體製造商將產品與各種工具內嵌，讓使用者獲得更好的產品體驗，產品團隊獲得新的見解。

此 [!DNL Pendo] 來源可讓您從擷取支援的webhook事件結構描述及其關聯的事件資料 [!DNL Pendo.io] 使用 [[!DNL Pendo] Webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks). 此 [!DNL Pendo] 來源適用於 [!DNL Pendo] URL webhook。

支援的Webhook包括：

* [指南](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) 已顯示
* [輪詢](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) 已顯示/已提交
* [網路推廣者分數](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) 已顯示/已提交

## 先決條件 {#prerequisites}

建立之前 [!DNL Pendo] 來源連線，您必須先確定您有以下專案：

A [!DNL Pendo] 帳戶。 如果您還沒有這類使用者，請參閱 [[!DNL Pendo] 註冊](https://app.pendo.io/register) 頁面以註冊及建立您的帳戶。

### 設定 [!DNL Pendo] Webhook {#set-up-webhook}

在成功建立資料流後，您必須設定webhook以通知Platform以下事項 [!DNL Pendo] 事件。 [!DNL Pendo] Webhook可以在特定事件發生時將即時通知推送至其他服務，並將此資訊傳送至您的 [!DNL Pendo] 來源。 如需詳細資訊，請參閱以下教學課程： [取得您的串流端點URL](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) 和 [設定 [!DNL Pendo] Webhook](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook).

## 正在連線 [!DNL Pendo] 至平台 {#connect-to-platform}

以下檔案提供如何建立 [!DNL Pendo] 要連線的串流聯結器 [!DNL Platform] 使用API或使用者介面：

### 連線 [!DNL Pendo] 使用API移至Platform {#connect-to-platform-using-api}

* [建立來源連線以帶來 [!DNL Pendo] 資料使用API移轉至Platform。](../../tutorials/api/create/analytics/pendo-webhook.md)

### 連線 [!DNL Pendo] 使用UI移至Platform {#connect-to-platform-using-ui}

* [建立來源連線以帶來 [!DNL Pendo] 使用使用者介面將資料傳遞至Platform](../../tutorials/ui/create/analytics/pendo-webhook.md)
